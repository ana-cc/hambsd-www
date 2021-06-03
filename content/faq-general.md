---
title: "FAQ: General Questions"
date: 2021-06-03T14:15:32+01:00
draft: false
faq: true
---

-   [Is HamBSD a fork of OpenBSD?][]
-   [Why not provide support for IPIP tunnels or an ampr-ripd port?][]

------------------------------------------------------------------------

[Is HamBSD a fork of OpenBSD?]: #fork
[Why not provide support for IPIP tunnels or an ampr-ripd port?]: #amprnet
## [Is HamBSD a fork of OpenBSD?][]

Hopefully not. It would be great to be able to upstream this work into
OpenBSD at some point in the future. Patches that fix or enhance
existing OpenBSD functionality will be submitted upstream.

During development however, technical preview releases may be produced
for amateur radio operators (and others interested) to try out.

## [Why not provide support for IPIP tunnels or an ampr-ripd port?][]

Centralisation is not a goal of this project. In order to provide robust
and resilient infrastructure, we need decentralised systems where
operators actually talk to each other to set up links. When traffic is
coming in from the Internet, it would be great if that traffic were also
authenticated in some way. (The source IP address is *not* a form of
authentication.)


[Is HamBSD a fork of OpenBSD?]: #fork
[Why not provide support for IPIP tunnels or an ampr-ripd port?]: #amprnet