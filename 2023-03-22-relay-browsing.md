---
layout: post
title:  Implement seamless relay browsing somehow
date:   2023-03-22 21:19:00 -0300
categories: code
author: FNF
pledges:
  - [0.05, FNF]
currency: BTC
contact: https://t.me/fiatjaf
status: New
---

The basic idea is that, for global feeds, replies feeds or mention feeds -- or whatever else I am forgetting here --, users should be able to easily switch between multiple relays to get a nice view of their content differences.

Imagine someone writes a comment saying that The Beatles was a terrible band. Then that person may see disagreeing replies from a relay full of Beatles fans, and agreeing replies from a relay full of Beatles haters, replies that are pure spam from a third relay and replies that vary in tone and quality from other relays, or maybe they just want to see what their friends are replying, and there is a relay with only their friends. The app should make it seamless to browse these various scenarios, I have no idea how.

The same line of thought can be applied, for example, to a "global feed" (more like a local feed). For example, a user may not be interested in whatever the entire world is saying, or what the relays full of bitcoiners are saying, but may be interested in a local relay made only of their town people, a local relay accessible only through WiFi (for example, in a conference), a relay of their friends, or maybe they just want to see what the bitcoiners are saying in the bitcoiners group of relays (it would be interesting to also be able to group relays and browse between groups). This would enable some relays to act as silos of manually curated content, for example, or communities that are read-only for the world and can only be written to by a group of selected high-signal people, among a million of other use cases.

I may have forgotten some, but this bounty applies to all major open-source clients in operation:

 - Nozzle
 - Nostros
 - Iris
 - Coracle
 - Snort
 - Gossip
 - Nuestr
 - Damus
 - Astral
 - Amethyst
 - Plasma
 - Satellite (when open-source)
 - Camelus

For other clients please ask first, or suggest adding here with a PR. It can also apply to new clients, if they are good and usable and have some users and are well-received by the public.

---

**Important:** the user must never have to go to a "Settings" menu to be able to use this feature. Typing relay URLs manually can be supported (I'd say it probably _must_ be), but should not be the only way a user can use this feature, although this will depend.

---

The bounty can be increased depending on the implementation.

The bounty doesn't have to be claimed by the app maintainer, it can be claimed by whoever implemented the feature.

Multiple payouts of this same bounty can be made if it is implemented in multiple apps.
