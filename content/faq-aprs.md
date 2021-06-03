---
title: "FAQ: Automatic Packet Reporting System (APRS)"
date: 2021-06-03T15:01:37+01:00
draft: false
faq: true
---
-   [Configuring an NMEA sensor][]
-   [Sending APRS position reports][]
-   [Connecting to APRS-IS][]

------------------------------------------------------------------------

## [Configuring an NMEA sensor][1]

To be supported by [nmea(4)][], your device must either attach to a
serial port, or use a virtual (e.g. USB) serial port and use the NMEA
0183 protocol.

Assuming that your GPS device is attached to cuaU0 and will 4800 baud,
edit /etc/ttys to add:

    cuaU0   "/sbin/ldattach nmea"   unknown on softcar

(If your device uses another baud rate, or other exotic settings, see
the [ldattach(8) manual page][].)

Then send *SIGHUP* to [init(8)][] to cause the file to be reloaded:

    # kill -s HUP 1

You can check the sensor is working correctly by using [sysctl(8)][]:

    # sysctl hw.sensors.nmea0
    hw.sensors.nmea0.indicator0=On (Signal), OK
    hw.sensors.nmea0.timedelta0=-0.001002 secs (GPS autonomous), OK, Sun Oct 28 17:08:04.998
    hw.sensors.nmea0.angle0=57.3748 degrees (Latitude), OK
    hw.sensors.nmea0.angle1=-2.3849 degrees (Longitude), OK

## [Sending APRS position reports][2]

APRS position reports can be sent using [aprsd(8)][] and are configured
with a file described by [aprsd.conf(5)][].

In the simplest case, to beacon your current GPS position, create the
configuration file at /etc/aprsd.conf with the contents:

    beacon position sensor nmea0

Then enable and start the [aprsd(8)][] service:

    # rcctl enable aprsd
    # rcctl start aprsd

## [Connecting to APRS-IS][3]

Create a new file /etc/hostname.axtap0 with the contents:

    !aprsisd -i axtap0 MYCALL

(Replace *MYCALL* with your callsign.)

Start the interface with:

    # sh /etc/netstart axtap0

For more advanced options, see the [aprsisd(8) manual page][].

[Configuring an NMEA sensor]: #gps
[Sending APRS position reports]: #tracker
[Connecting to APRS-IS]: #aprsis
[1]: #gps
[nmea(4)]: https://man.hambsd.org/nmea.4
[ldattach(8) manual page]: https://man.hambsd.org/ldattach.8
[init(8)]: https://man.hambsd.org/init.8
[sysctl(8)]: https://man.hambsd.org/sysctl.8
[2]: #tracker
[aprsd(8)]: https://man.hambsd.org/aprsd.8
[aprsd.conf(5)]: https://man.hambsd.org/aprsd.conf.5
[3]: #aprsis
[aprsisd(8) manual page]: https://man.hambsd.org/aprsisd.8
