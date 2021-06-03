---
title: "FAQ: Terminal Node Controllers"
date: 2021-06-03T14:50:40+01:00
draft: false
faq: true
---

-   [Supported TNCs][]
-   [Configuring a TNC as a network interface][]
-   [Automatically initialising a TNC][]
-   [Using KISS-over-TCP][]

------------------------------------------------------------------------

## [Supported TNCs][1]

A list of TNCs that are known to work with HamBSD's kiss(4) driver are
maintained in the [manual page][]. Most, if not all, TNCs that implement
the KISS protocol over a serial interface should be supported. This
includes those with RS-232 interfaces, USB-to-serial interfaces, or
using a pseudo-terminal ([pty(4)][]).

## [Configuring a TNC as a network interface][2]

To configure a TNC to be used as an [AX.25][] network interface on boot,
create a [hostname.if(5)][] file. For the first interface on the system
this should be named `/etc/hostname.axkiss0`.

    lladdr MYCALL up
    !ldattach -s 1200 kiss cua00

Replace *MYCALL* with your callsign. This also assumes the TNC's serial
port (not on-air baud rate) operates at 1200 baud and is connected to
the first serial port. For USB-to-serial interfaces, the first interface
will be *cuaU0*.

## [Automatically initialising a TNC][3]

A [chat(8)][] script may be used to initialise a TNC that requires
configuration before it enters KISS mode. The following example works
for the Kenwood TM-D700E:

    cmd:--cmd: 'kiss on'
    cmd: 'mon off'
    cmd: restart

This script can be stored as `/etc/kiss.chat` and run automatically by
adding the following to the relevant [hostname.if(5)][] file before
calling ldattach:

    !stty -f /dev/cuaXX 9600
    !chat -t 5 -f /etc/kiss.chat <>/dev/cuaXX >&0

## [Using KISS-over-TCP][4]

To use KISS-over-TCP, for example with Dire Wolf, the [rkissd(8)][]
daemon can be used.

To start an interface automatically at boot, create a new
[hostname.if(5)][] file for a `kiss` interface (e.g.
`/etc/hostname.kiss0`):

    !rkissd 192.168.0.10 8001

To start an interface manually:

    ifconfig create kiss0
    rkissd 192.168.0.10 8001

[Supported TNCs]: #supported
[Configuring a TNC as a network interface]: #config
[Automatically initialising a TNC]: #init
[Using KISS-over-TCP]: #kisstcp
[1]: #supported
[manual page]: https://man.hambsd.org/kiss.4
[pty(4)]: https://man.hambsd.org/pty.4
[2]: #config
[AX.25]: https://man.hambsd.org/ax25.4
[hostname.if(5)]: https://man.hambsd.org/hostname.if.5
[3]: #init
[chat(8)]: https://man.hambsd.org/chat.8
[4]: #kisstcp
[rkissd(8)]: https://man.hambsd.org/rkissd.8