---
layout: post
title:  Output nevent and nprofile codes with relay hints, add relay hints to tags
date:   2023-04-07 21:19:00 -0300
categories: code
author: FNF
pledges:
  - [0.01, FNF]
currency: BTC
contact: https://t.me/fiatjaf
status: New
---

The idea is that the client should add a relay hint on the tag when mentioning other notes, as the `e` tag, and when mentioning people using the `p` tag. If using NIP-27, they should embed `nostr:nevent1...` and `nostr:nprofile1...` URLs that contain at least one relay hint to each. And finally, when showing copiable/shareable identifiers to notes and to profiles, the client should display `nprofile` and `nevent` codes.

I may have forgotten some, but this bounty applies to all major open-source clients in operation:

 - Nozzle
 - Nostros
 - Iris
 - Coracle
 - Snort
 - Gossip
 - Nuestr
 - Astral
 - Amethyst
 - Plasma
 - Satellite (when open-source)
 - Camelus
 - Primal
 - Nostrmo

For other clients please ask first, or suggest adding here with a PR.

---

The bounty can be increased depending on the implementation.

The bounty doesn't have to be claimed by the app maintainer, it can be claimed by whoever implemented the feature.

Multiple payouts of this same bounty can be made if it is implemented in multiple apps.

---
