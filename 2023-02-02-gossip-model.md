---
layout: post
title:  Implement the Gossip Model in one of the established clients
date:   2023-02-02 21:19:00 -0300
categories: code
author: FNF
pledges:
  - [0.05, FNF]
currency: BTC
contact: https://t.me/fiatjaf
status: New
---

Video explanation of the Gossip model: https://mikedilger.com/gossip-relay-model.mp4
Gossip codebase: https://github.com/mikedilger/gossip

The idea is to implement this model (or a variant of it) for keeping track of relays people post in and following them and making Nostr more decentralized in one of the already established clients:

 - Amethyst
 - Nozzle
 - Nostros
 - Astral
 - Snort
 - Iris
 - Coracle
 - Plasma
 - Satellite
 - Camelus
 - Primal

For other clients please ask first, or suggest adding here with a PR.

---

Basic description of the essence of the Gossip model:

  - Keep track of relays in which people post on, according to:
    - events from that person seen on that relay
    - relay hints from other events
    - `nprofile` relays
    - NIP-05 relays
    - kind 2
    - kind 3
    - etc
  - Discover new relays organically through route hints while browsing global feeds, loading replies (from whatever relays) and following relay hints in events
  - When loading the home feed, try to not connect to all relays on the earth, and only ask the relevant relays for the relevant pubkeys instead of flooding queries.
  - Make relays manually editable for each person followed

Slightly related (but ignorable): https://fiatjaf.com/3f106d31.html

---

The bounty can be increased depending on the implementation.

Multiple payouts of this same bounty can be made if it is implemented in multiple apps.

---

**Claimed**, so far, by

- Coracle
- Nozzle
- Camelus
