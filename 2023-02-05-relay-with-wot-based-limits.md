---
layout: post
title: Make Nostr Relay that applies limits based on proximity to a group of accounts
date:   2023-02-05
categories: code
author: giszmo
pledges:
  - [0.02172215, giszmo]
currency: btc
contact: https://brb.io/u/npub1gm7tuvr9atc6u7q3gevjfeyfyvmrlul4y67k7u7hcxztz67ceexs078rf6
status: New
---

I want to **run a relay** financed by a tiny percentage of its users and strongly believe
in the following being a way to align incentives for all clients and relay operators:

For this bounty, the minimum requirement for the resulting relay is:

* relay is as efficient or better than [strfry](https://github.com/hoytech/strfry) at supported nips, synchronization between instances and handling concurrent connections
* nip42 support
* all read and write operations are metered per connected pubkey: milliseconds spent on queries, query count, events sent, event kBs sent, etc. (If Alice pushes Bob's events, it gets tallied to her pubkey - the one authenticated via nip42)
* allow managing group of primary (TIER 0 or T0) users via API
* secondary users are those followed by T0 users etc.
* define limits depending on follows distance to primary users, using five tiers: 0 = primary users, 1 = follows, 2 = follows of follows, 3 = follows of follows of follows, inf = all the other pubkeys
* allow configuring hourly, daily and monthly limits per tier

**This bounty was created with the goal of actually running a relay with this feature and will not be awarded for a proof of concept that is not a fully functional and performant relay. Strfry is "good enough". If you want to implement the proposed feature in a different relay, please reach out to discuss first.**

This bounty was offered in other places before:

* https://github.com/hoytech/strfry/issues/17
* https://bountsr.org/relay-with-wot-based-limits/
* https://nostrbounties.com/b/naddr1qpqxgdpcxu6rqcej8pjnxdekxpjkzefnvfjk2wtrvcervdm9xc6ryenpvycn2d3sv4snxvpnvy6rwc34xsmxxwr9v5cnyetyxf3njwtyvvpzq3huhccxt6h34eupz3jeynjgjgek8lel2f4adaea0svyk94a3njdqvzqqqr4guugzfhl
