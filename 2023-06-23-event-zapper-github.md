---
layout: post
title:  "Event Zapper - A way to Zap speakers at in-person events, in realtime"
date:   2023-06-20 22:37:00 -0400
categories: code
author: Owen
pledges:
  - [0.005, Owen]
currency: BTC
contact: npub1am50jqjytzdtepftqfzf8grh2gs4wpt7d4t90zxc6z288wqazj5skdks29
status: New
---

While attending the first ever Canadian Bitcoin Conference in Toronto, and listening to Derek Ross’s intro to Nostr talk - two things struck me:

* There are still a ton of Bitcoiners who are not using Nostr 
* I missed having the ability to ZAP when I liked what speakers were saying (even in person). 

This made me think - During Bitcoin 2023 in Miami, pablof7z created the wonderful Zaplife.lol screen. This screen displayed a realtime feed of Zaps to attendees of the conference (see: https://twitter.com/WalkerAmerica/status/1659211191770832901). During the live stream, many of us remote nostriches attempted to capture screenshots of our zaps on the big screen behind the live stream hosts. 

So, why not take this one step further and make it part of the main event? It helps solve both of the issues mentioned above, and opens the door to a bunch of other benefits and opportunities.   

—

There are two main components of this project:

* Presentation view

* Dashboard view

—

**Presentation view is what the audience can see, and interact with.** 
Speakers with nostr profiles are displayed on the screen, along with a QR code. Audience members can scan those QR code to find the speaker on nostr. From there, they can Zap the speaker’s profile when they like what they hear. A realtime feed of Zaps is displayed below the speaker image, and a total number of zaps it recorded.

Speakers without nostr profiles are not left out either. Audience can Zap non-nostriches too, but those Zaps are routed (donated) to a different npub (maybe one of the speaker’s choosing).  

**Dashboard view is what the event organizer uses to configure Presentation view**
Event organizers can select the number of speakers to be displayed on the screen. They can enter npubs for each speaker. Images, names, and QR codes are generated based on what is entered here.

*In conclusion, the aim is to bring Zapping to the masses at live events and demonstrate the power of value for value*

-

![Event Zapper](https://github.com/coinkite/bountsr.org.pub/assets/123519473/d689666a-d377-4dfe-8dbe-0a909209d6b7)

