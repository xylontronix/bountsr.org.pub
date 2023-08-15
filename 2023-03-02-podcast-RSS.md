Custom RSS feed using fiatjaf's noscl. There are three files. 'create.sh' 'news.sh' and 'fetch_rss.py'. Put 'create.sh' in the '/home/' folder and the other two in the users '/go/bin' directoy. Navigate to the user's 'go/bin' directory and run 'su news' (with news being the username), and the run 'nohup ./news.sh &> /dev/null &' to run after being logged off. This could probably all be performed by one python script, but I don't know how to do that yet. You can replace the links in the python script with an .xml or rss feed of your choice. Put a different feed on each line.

---
#create.sh

#!/bin/bash

# Define the username and home directory
username="news"
home_dir="/home/$username"

# Create the user with the home directory
if ! useradd -m $username; then
  echo "Failed to create user $username. Aborting."
  exit 1
fi
chown -R $username:$username /home/$username
chmod -R 755 /home/$username

home_dir="/home/$username"

# Update and upgrade the system
sudo apt-get update && sudo apt-get upgrade -y

# Install pip, Go, and the faker library for random name and sentence
sudo apt-get install -y python3-pip
sudo snap install go --classic
sudo -u $username pip3 install --user faker

# Create a new user with home directory and set password
sudo useradd -d $home_dir -m $username
echo "$username:script123!@#" | sudo chpasswd
sudo usermod -aG sudo $username

# Append Go path configuration
echo -e "# Set go path to user's home directly\nexport GOPATH=\$HOME/go\nexport PATH=\$PATH:\$GOROOT/bin:\$GOPATH/bin" | sudo -u $username tee -a $home_dir/.bashrc

# Install noscl package and create necessary directory
sudo -u $username bash -c "go install github.com/fiatjaf/noscl@latest"
sudo -u $username mkdir -p $home_dir/.config/nostr

# Change to user's 'bin' directory and execute noscl
cd $home_dir/go/bin
sudo -u $username ./noscl

# Add relay endpoints
for relay in wss://relay.damus.io wss://nostr.mutinywallet.com wss://nostr-pub.wellorder.net wss://offchain.pub wss://nos.lol wss://relay.nostr.band wss://nostr.wine wss://relay.primal.net; do
  sudo -u $username ./noscl relay add $relay
done

# Generate a key and pause the script
private_key=$(sudo -u $username ./noscl key-gen | grep -oE '[0-9a-f]{64}$')
echo "Captured String: $private_key"
read -p "Press Enter to continue once you have manually set the private key..."
sudo -u $username ./noscl setprivate $private_key
public_result=$(sudo -u $username ./noscl public)
echo "Public Result: $public_result"

# Create crontab entry for news.sh
(crontab -u $username -l; echo "* * * * * /home/\$username/go/bin/news.sh") | crontab -u $username -
echo "Crontab entry for news.sh has been created for the user $username."

# Generate a random name and sentence
random_name=$(sudo -u $username python3 -c "from faker import Faker; fake = Faker(); print(fake.name())")
random_about=$(sudo -u $username python3 -c "from faker import Faker; fake = Faker(); print(fake.sentence())")

# Set metadata with random name and about sentence
sudo -u $username ./noscl metadata --name="$random_name" --about="$random_about"

# Copy news.sh and fetch_rss.py to /home/$username/go/bin
cp /home/news.sh /home/$username/go/bin
cp /home/fetch_rss.py /home/$username/go/bin


---
#news.sh

#!/bin/bash

# Get the directory of the currently executing script
DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )"

# Fetch the RSS feed using the Python script (in the same directory)
NEWS_ITEMS_JSON=$(python3 $DIR/fetch_rss.py)

# In-memory storage for published links
declare -A PUBLISHED_LINKS

# Iterate through the news items
IFS=$'\n'
for NEWS_ITEM in $NEWS_ITEMS_JSON; do
  # Extract the title, description, and link from the news item
  TITLE=$(echo "$NEWS_ITEM" | awk -F'***' '{print $1}')
  DESCRIPTION=$(echo "$NEWS_ITEM" | awk -F'***' '{print $2}')
  LINK=$(echo "$NEWS_ITEM" | awk -F'***' '{print $3}')

  # Check if the link has been published in the last 72 hours
  TIMESTAMP=${PUBLISHED_LINKS[$LINK]}
  CURRENT_TIME=$(date +%s)
  if [ -z "$TIMESTAMP" ] || [ $((CURRENT_TIME - TIMESTAMP)) -gt 259200 ]; then
    # Summarize the news (retaining the first 50 words of the description)
    SUMMARY=$(echo "$DESCRIPTION" | awk '{print $1,$2,$3,$4,$5,$6,$7,$8,$9,$10,$11,$12,$13,$14,$15,$16,$17,$18,$19,$20,$21,$22,$23,$24,$25,$26,$27,$28,$29,$30,$31,$32,$33,$34,$35,$36,$37,$38,$39,$40,$41,$42,$43,$44,$45,$46,$47,$48,$49,$50}')
	
	# Fetch the HTML content of the link and extract the main JPG image URL (up to .jpg)
    IMAGE_LINK=$(curl -s "$LINK" | grep -o 'https://static01.nyt.com/images/[^"]*.jpg' | head -n 1)

    # The rest of the code for publishing the link
    # Publish the note with the title, summary, hyperlink, and image hyperlink
    ./noscl publish "NY Times: $TITLE - $SUMMARY - $LINK - $IMAGE_LINK"

    # Record the published link with the current timestamp
    PUBLISHED_LINKS[$LINK]=$CURRENT_TIME
  fi

  # Sleep for 70 seconds to prevent rate-limiting
  sleep 70
done


---
#fetch_rss.py

#!/usr/bin/env python3

import feedparser
import random
import logging

FEED_URLS = [
        "https://rss.nytimes.com/services/xml/rss/nyt/Technology.xml",
        "https://rss.nytimes.com/services/xml/rss/nyt/World.xml",
        "https://rss.nytimes.com/services/xml/rss/nyt/Africa.xml",
        "https://rss.nytimes.com/services/xml/rss/nyt/US.xml",
        "https://rss.nytimes.com/services/xml/rss/nyt/Business.xml",
        "https://rss.nytimes.com/services/xml/rss/nyt/HomePage.xml",
        "https://rss.nytimes.com/services/xml/rss/nyt/Americas.xml",
        
]

# Shuffle the feed URLs to ensure a random order
random.shuffle(FEED_URLS)

for url in FEED_URLS:
    try:
        feed = feedparser.parse(url)
        for entry in feed.entries:
            title = entry.title.replace('"', '\\"')  # Escape quotes
            description = entry.description.replace('"', '\\"')  # Escape quotes
            link = entry.link  # Get the hyperlink
            image_link = entry.media_thumbnail[0]['url'] if 'media_thumbnail' in entry else ''  # Get the image hyperlink
            print(f'{title}***{description}***{link}***{image_link}')
    except Exception as e:
        logging.error(f"Error fetching or parsing URL {url}: {str(e)}")




--------------------------------------------------
layout: post
title:  "A podcast RSS mirror/replacement."
date:   2023-03-02 8:48:00 -0500
categories: code
author: nvk
pledges:
  - [0.01, nvk]
currency: BTC
contact: https://nvk.org/nostr
status: New
---

Build a podcast RSS mirror/replacement

1. The mirror takes an existing podcast RSS feed and republishes the entries with your keys. 
2. This needs more thinking as to how this should work, and which *kind* it should use, since a reference to a previous entry in important. May would need a new *nip/kind* that expresses chain of events.

The main goal is to replace RSS for podcasts, and eventually have podcasts players that understand it. So that users would just follow some pubkey and the authors podcast feed magically appears on the podcast client feed.

