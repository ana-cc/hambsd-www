---
title: "MB7UAR APRS IGate"
date: 2021-06-03T12:14:29+01:00
draft: false
slug: mb7uar
---

{{< figure src="/mb7uar/mb7uar.jpg" width="750px">}}

### Overview

|               |                          |
|---------------|--------------------------|
| Callsign      | MB7UAR                   |
| Frequency     | 144.800 MHz              |
| Location      | Northfield, Aberdeen     |
| Locator       | IO87wd                   |
| Mode          | AFSK 1200 APRS           |
| Gateway       | Bi-directional (APRS-IS) |
| Digipeating   | WIDEn-N                  |
| Looking Glass | in development...        |
| NoV Issued    | 5 Nov 2019               |
| Nov Expiry    | 4 Nov 2020               |
| Keeper        | MM0ROR                   |


### Usage Instructions

When in range of MB7UAR, send APRS packets on 144.800MHz. All packets will be relayed to APRS-IS.

If a position report is sent, it will be possible to establish two-way messaging between your RF station and either an Internet station or another RF station linked via another IGate.

To enable RF-to-RF communication locally, MB7UAR may be used as a digipeater. It will digipeat packets according to the "new n-N Paradigm". In practice, this means that you should set your path to include at least "WIDE2-1" or at most "WIDE1-1,WIDE2-1".

### Coverage

The following map was calculated with some perhaps over-optimistic assumptions. It is probably more representative for fixed stations than mobiles, and for handhelds you may struggle. YMMV.

At the time the antenna was installed, the local noise floor was recorded at around S6.
{{< figure src="/mb7uar/mb7uar-cov.png" width="250px">}}{{< figure src="/mb7uar/noise.jpg" width="250px">}}

Reports are encouraged and should be sent to [irl@hambsd.org](mailto:irl@hambsd.org) with the subject line "MB7UAR Report".

### Station Details

#### Controller

While HamBSD matures, this station is currently controlled by a Raspberry Pi running Dire Wolf on Raspbian. The following configuration is used:

ADEVICE plughw:1,0
PTT /dev/ttyUSB0 RTS
TXDELAY 50

MYCALL MB7UAR

# MB7UAR Position Beacon
PBEACON delay=05 every=30 overlay=I symbol="digi" lat=57^09.89N long=002^09.67W comment="Northfield IGate" via=WIDE1-1,WIDE2-1
PBEACON delay=05 every=10 overlay=I symbol="digi" lat=57^09.89N long=002^09.67W comment="Northfield IGate" sendto=IG

# GB3GN Object Beacon
OBEACON objname=GB3GN delay=15 every=30 symbol=/r lat=57^1.0629N long=002^21.5402W comment="145.775MHz T067 -600 Banchory www.grampianrepeatergroup.co.uk" via=WIDE1-1,WIDE2-1
OBEACON objname=GB3GN delay=05 every=10 symbol=/r lat=57^1.0629N long=002^21.5402W comment="145.775MHz T067 -600 Banchory www.grampianrepeatergroup.co.uk" sendto=IG

# GB3NG Object Beacon
OBEACON objname=GB3NG delay=25 every=30 symbol=/r lat=57^36.1319N long=002^1.9699W comment="145.625MHz T067 -600 Fraserburgh www.grampianrepeatergroup.co.uk" via=WIDE1-1,WIDE2-1
OBEACON objname=GB3NG delay=05 every=10 symbol=/r lat=57^36.1319N long=002^1.9699W comment="145.625MHz T067 -600 Fraserburgh www.grampianrepeatergroup.co.uk" sendto=IG

IGSERVER euro.aprs2.net
IGLOGIN MB7UAR \*\*\*\*\*

DIGIPEAT 0 0 ^WIDE\[3-7\]-\[1-7\]$ ^WIDE\[12\]-\[12\]$
IGTXVIA 0
IGTXLIMIT 6 10

#### Transceiver

MB7UAR uses a Yaesu FT-1900 as its transciever. The radio is connected via a soundcard interface cable connected to its microphone and external speaker ports. This radio does not have the 5-pin mini-DIN data port that is common on Yaesu radios.

The transmitter power output is set to 5 watts and uses a "narrow" channel. The mic gain setting (menu item 27) has been used to set the peak deviation to 2.5kHz.

#### Antenna and Feeder

A simple dipole is installed in the attic. The bracket, support and elements are made from aluminium.

10 meters of RG58 coax is used to connect the antenna and the radio with PL259 connecters at both ends.

The reading of SWR from the Yaesu FT-817 is not an accurate reading, but suggests that the SWR is probably somewhere between 1:1 and 1.5:1. The FT-817 does not actually measure SWR but instead only measures reflected power. This reading was taken using 5W output.

{{< figure src="/mb7uar/antenna.jpg" width="450px" >}}
{{< figure src="/mb7uar/swr.jpg" width="250px">}}

#### Internet Gateway

This IGate has a redundant connection to the Internet, using fixed VDSL and failover to an LTE connection. It uses the APRS2 European round-robin to select the server to connect to.