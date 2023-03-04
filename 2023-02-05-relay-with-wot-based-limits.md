---
layout: post
title: Make Nostr Relay that applies limits based on proximity to a group of accounts
date:   2023-02-05
categories: code
author: giszmo
value: 0.02172215
currency: btc
contact: https://brb.io/u/npub1gm7tuvr9atc6u7q3gevjfeyfyvmrlul4y67k7u7hcxztz67ceexs078rf6
status: New
---

Create or modify an existing relay such that limits can be applied by proximity in a
graph of followers.

I want to run a relay financed by a tiny percentage of its users and strongly believe
in the following being a way to align incentives for all clients and relay operators:

For this bounty, the minimum requirement is:

- [ ] Implement authentication. The relay does only process REQests and EVENTs from clients linked to pubkeys once this module is activated
- [ ] Measure resource use per pubkey: milliseconds spent on queries, query count, events sent, event kBs sent, etc.
- [ ] Define group of primary users (how this works is independent of this issue but in my case it might be people I follow or people that pay $x/month).
- [ ] Secondary users are follows of primary users etc.
- [ ] Define limits depending on follows distance to primary users, using five tiers: 0 = primary users, 1 = follows, 2 = follows of follows, 3 = follows of follows of follows, inf = all the other pubkeys

With this in place, the relay can set rules depending on tiers:

```yaml
limits:
  0:
  1:
  2:
    eventsPerHour: 8
  3:
    eventsPerHour: 8
    maxEventSize: 1000
  inf:
    eventsPerHour: 8
    eventsPerDay: 12
    maxEventSize: 300
    embedUrls: false
```

This bounty was offered in other places before, including in https://github.com/hoytech/strfry/issues/17
