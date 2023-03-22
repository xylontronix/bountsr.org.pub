---
layout: post
title: Bounties Manager
date: 2023-02-04 21:19:00 -0300
categories: code
author: FNF
pledges:
  - [0.05, FNF]
currency: BTC
contact: https://t.me/fiatjaf
status: Claimed
---

A very simple and lean web Nostr client dedicated to managing quick and easy bounties like https://stacker.news/items/127070.

## Browsing view

It should show a list of available and closed bounties along with their amounts and who is offering the bounty (name and picture fetched from `kind:0` events + `npub`, otherwise just `npub`).

When clicking a bounty the visitor should see the details of the bounty and the history of bounties offered from that same user and if they were paid or not. They are "paid" when there is an event replying to the bounty that states that (see below).

## Bounty creation view

It should work with a soft-standard text format text on top of `kind:1` posts. The flow should be something like:

1. user connects with a NIP-07 extension
2. writes title, amount and terms of the bounty
3. the app publishes the event with the `"t"` tag set to `"bounty"` and content set to something like

```
bounty: Build a wheel
description: A wheel must be built so it spins.
reward: 10000 sats
```

## Additional bounty pledges

Other people should be able to add to the bounty. When showing that in the UI the additional pledges should be clearly separated from the original bounty, for example, `"reward: 10000 sats + 542 sats"`, the 542 sats being the addition, in a different color.

There should be a button somewhere to add to the pledge. Any user should be able to click that, select the amount and press "ok" and then an event is sent as a reply to the original bounty offer, with `"t"` tag set to something like `"bounty-added-reward"` or something like that. These tags should be standardized.

The content should be something like:

```
added reward: 542 sats
```

## Bounty award and bounty cancelation

A similar flow, with yet another special hashtag (`"t"`) and again a standard format, should be published, again as a reply to the original bounty event. I'll not be very specific here because that is not necessary.

---

The specs above are just ideas to serve as inspiration. Let me know how they could be improved.

The bounty size can be increased depending on how this is going.

Please reach out to me before starting to work on this.

---

## Claimed!

- https://nostrbounties.com/
- https://github.com/diamsa/nostrbounties
