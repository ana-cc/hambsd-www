---
title: "HamPKI"
date: 2021-06-03T11:43:03+01:00
draft: false
slug: hampki
---


To build robust and resilient amateur packet networks, they need to be able to resist attack. As with other systems with poor or non-existent authentication, over time the probability that they will be attacked approaches certainty.

We have seen this happen again and again, and in some cases it has removed applications from existence. Example range from guestbooks on personal websites [filled with spam](https://en.wikipedia.org/wiki/Spamdexing#Link_spam) to attacks on communications signalling systems (e.g. [BGP](https://en.wikipedia.org/wiki/BGP_hijacking), [SS7](https://www.theguardian.com/technology/2016/apr/19/ss7-hack-explained-mobile-phone-vulnerability-snooping-texts-calls)). Another recent example is the [certificate flooding attacks](https://dkg.fifthhorseman.net/blog/openpgp-certificate-flooding.html) on OpenPGP key servers. Personal guestbooks and the OpenPGP key servers have drifted into the past, replaced by comments sections authenticated by Facebook accounts and new [key distribution systems](https://wiki.gnupg.org/WKD). Even where applications have survived, they are no longer as easy to use.

HamPKI aims to prevent amateur radio services from falling to the same fate by providing a framework for authenticating radio amateurs using packet radio systems.

### Root Certificate Bundle

HamBSD includes an additional CA bundle found at `/etc/hamcert.pem`. This bundle can be used to authenticate servers and clients as licensed radio amateurs. Callsigns are found in issued certificates as `OID.1.3.6.1.4.1.12348.1.1`.

*   [Download the latest bundle](https://raw.githubusercontent.com/HamBSD/src/master/lib/libcrypto/hamcert.pem)

### Future Goals

*   Produce a policy for inclusion of new root certificates
*   Produce a toolkit for operating a CA