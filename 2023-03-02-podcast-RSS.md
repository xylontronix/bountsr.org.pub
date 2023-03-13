---
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

