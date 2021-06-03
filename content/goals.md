---
title: "Goals"
date: 2021-06-03T13:38:12+01:00
draft: false
---

### Project guidelines

-   Follow [OpenBSD][]'s security practices and coding style
    -   Consistently use [style(9)][] for all kernel code
    -   Avoid complex parsing in the kernel, which may lead to not
        implementing some protocol features
    -   Consistently use [style(9)][], [pledge(2)][] and [unveil(2)][]
        across all userspace code
    -   Use privilege-separation when parsing data from network, modem
        or disk
-   Keep the entire code base as unrestricted as possible (at least
    unrestricted enough to upstream to OpenBSD)

### Long-term goals

-   Provide a complete amateur radio network stack for OpenBSD
-   KISS TNC support:
    -   a new [kiss(4)][] line discipline
    -   able to use any [tty(4)][] including [pty(4)][]s
    -   attached via [ldattach(8)][] (can be done during
        [netstart(8)][])
-   ax25(4) link layer support
    -   TCP/IP in AX.25 encapsulation, simply give the interface an IP
        address
        -   Compatibility with Linux hosts
    -   AF_AX25 socket support, as a layer 2 (non-routed) protocol only,
        including:
        -   SOCK_DGRAM — AX.25 UI frames
-   AX.25 dissection for [tcpdump(8)][]
-   a new [kiss(4)][] network interface for AX.25 over KISS
-   a new [axtap(4)][] network interface for tunnels (e.g. APRS-IS and
    maybe soundmodems)
-   a new axeth(4) network pseudo-interface for AX.25 encapsulation in
    Ethernet
-   a new axip(4) network pseudo-interface for AX.25 encapsulation in
    IPv4/IPv6
-   [aprsd(8)][] — a new privilege-separated APRS tracker/digipeater
    -   using location data available via the sensors framework, e.g.
        from [nmea(4)][]
    -   *using data available via some mechanism from a weather station*
-   [aprsisd(8)][] — APRS-IS client daemon
    -   using (perhaps exclusively) TLS connection to the APRS-IS server
-   [rkissd(8)][] — Remote KISS daemon
-   *softmodem(8) — software modem supporting Bell 103 AFSK, Bell 202
    AFSK and PACTOR modes*
-   Consider the needs of both leisure and emergency operators

### Side goals

These goals may be corollaries from other activities, but are not
explicitly goals of this project:

- A generic network interface driver for different serial line protocols
(e.g. both KISS and SLIP)

### Non-goals

- In-kernel digipeating

  -   AX.25 headers are variable length which gets a bit messy. We want to
    parse as little as possible in the kernel.

- SOCK_SEQPACKET for AF_AX25

  -   This is a complicated lump of code. There are state machines and
    timers and all sorts. If you want this, you can do it in userspace
    using the SOCK_RAW support.

- IPIP (protocol 4 or 94) tunnels

  -   Perhaps it is possible to be convinced that these are worthwhile,
    but the idea of a worldwide amateur Internet which joins the public
    Internet in places just isn't that appealing. Aside from the
    operating license headaches and potential abuse, it's not clear what
    services operate in 44net that are really useful for the average
    operator. It is already possible to establish tunnels using other
    technologies between sites.
    
[OpenBSD]: https://www.openbsd.org
[style(9)]: https://man.hambsd.org/style.9
[pledge(2)]: https://man.hambsd.org/pledge
[unveil(2)]: https://man.hambsd.org/unveil
[kiss(4)]: https://man.hambsd.org/kiss.4
[tty(4)]: https://man.hambsd.org/tty.4
[pty(4)]: https://man.hambsd.org/pty.4
[ldattach(8)]: https://man.hambsd.org/ldattach.8
[netstart(8)]: https://man.hambsd.org/netstart.8
[tcpdump(8)]: https://man.hambsd.org/tcpdump.8
[axtap(4)]: https://man.hambsd.org/axtap.4
[aprsd(8)]: https://man.hambsd.org/aprsd.8
[nmea(4)]: https://man.hambsd.org/nmea.4
[aprsisd(8)]: https://man.hambsd.org/aprsisd.8
[rkissd(8)]: https://man.hambsd.org/rkissd.8