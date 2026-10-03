# DP Talker

NMEA 0183 serial reader · sensor & PRS simulator for Android.

A field and bench tool for marine ETOs and DP technicians. Plug a USB-serial
adapter into a phone and read what a sensor is actually putting on the wire, or
transmit a simulated one into a bench setup.

> **Not for use as a position reference input on a vessel in DP operations.**

---

## ⚠ Before you transmit

DP Talker writes NMEA sentences onto a real serial line. To the equipment
listening, simulated and replayed data are indistinguishable from a live
sensor. Nothing in the sentence says it was made up.

Transmit only into equipment isolated from the vessel's DP, or into an input
whose operators know the data is simulated and have accepted it.

Never feed simulated or recorded data to a position reference, gyro, wind or
MRU input on a vessel in DP operations or preparing for them. A recording
carries a past position and a past time; a DP that accepts it will hold station
on somewhere the vessel is not.

The app cannot see what is on the other end of the cable. That check is yours,
every time.

---

## What it does

### Read

Frames and decodes what arrives, and shows line by line what it decoded.
Decoded value cards for heading, wind, position, VRU motion, depth, log speed
and laser/radar range & bearing, each with its measured rate and a stale state
when the source goes quiet. Tap any raw line for a full field breakdown with
DP-specific guidance.

### Simulate

Gyro, wind, DGNSS, VRU/MRU and position-reference sources. Drive them live from
the transmit screen: slew a heading, dial a sea state, swing a bearing. The
exact frames are previewed before a byte goes out.

### Record and replay

Capture a session to a raw `.nmea` file, replay it to the screen, or re-transmit
it out the port at original timing. Checksum failures are marked on the
scrubber so you can jump straight to a fault.

### Sentences it knows

GGA, GST, VTG, ZDA, RMC, GLL, HDT, THS, ROT, MWV, VBW, DPT, Kongsberg PSXN,23,
TSS1, and the position-reference telegram family: Fanbeam/MDL, CyScan, ASCII17,
Artemis, Nautronix, and the RadaScan, RADius and SpotTrack formats ($PSXST,
$PGNKM, $PSXRAD, $PGNMT, $PGNRR, ABBDP).

---

## Requirements

- Android 8.0 (API 26) or newer
- USB OTG support: the app is useless without it
- A USB-to-serial adapter: FTDI, Prolific, CP210x, CH340 and CDC-ACM are all
  supported

---

## Install

Install it from [Google Play](https://play.google.com/store/apps/details?id=io.github.cluthfi.dptalker),
or download the APK from [Releases](../../releases). The two copies are signed
by different keys, so neither installs over the other: uninstall one before you
switch, which deletes its recordings.

**Check the signature before you install an APK.** A sideloaded APK is only as
trustworthy as the key that signed it:

```
apksigner verify --print-certs DPTalker-x.y.z.apk
```

The SHA-256 must match:

```
DF:11:E0:4A:03:BE:6F:E8:7B:4B:1F:B4:79:0E:97:F9:4A:62:E6:01:F6:92:4C:3A:F8:42:F9:53:BF:0E:8E:C0
```

apksigner prints it in lower case without the colons; the app shows it in the
form above. They are the same 32 bytes.

Inside the app, **Settings → About & safety → Signing key** shows the fingerprint
of the installed copy, read from the package itself. A copy from Releases shows
the one above. A copy from Google Play is signed by Google's app signing key and
shows this one:

```
98:5A:5C:13:2B:FF:90:7A:5E:15:C7:60:50:A7:26:46:39:51:82:6D:9B:60:F1:C4:8A:6A:2C:B3:A3:BA:01:68
```

Any other value means it is not this app, whatever it calls itself.

---

## Privacy

DP Talker has no INTERNET permission, so it cannot reach the internet. No
telemetry, no analytics, no crash reporting, no account.

Serial data you record, the session metadata and your settings are written to
the app's private storage on this device. They leave only when you share or
export a file yourself, and then only to the app you pick.

Uninstalling the app deletes its private storage, including recordings.

The permissions it does declare, and why:

| Permission | Why |
|---|---|
| `USB_HOST` (feature) | reading and writing the serial adapter |
| `FOREGROUND_SERVICE` + `CONNECTED_DEVICE` | keeping a transmit alive with the screen off |
| `WAKE_LOCK` | a foreground service alone does not stop the SoC suspending, which would stall the transmit timer |
| `POST_NOTIFICATIONS` | the notification that says a transmit is still running |

---

## Scope

A field and bench tool, written and maintained by one person. It is not
calibrated test equipment, not type-approved, not a position reference system,
and not endorsed by any manufacturer, operator or class society. What you read
is only as good as the adapter and the cable. Treat it as an indication, and
confirm anything that goes into a report with an instrument that carries a
certificate.

Provided as-is, without warranty of any kind. Using it is your professional
judgement and your responsibility.

---

## Sentence definitions

I compiled DP Talker's sentence layouts from publicly available references:
gpsd's *NMEA Revealed*, manufacturers' published interface descriptions for
their own equipment, and output observed from real sensors.

The NMEA 0183 Interface Standard is a paid, copyrighted document published by
the National Marine Electronics Association. It was not used in building this
app, and DP Talker does not claim conformance to it or to any version of it.

Where DP Talker disagrees with your equipment's interface manual, the manual is
right. Tell me and I will fix it.

---

## Licence

DP Talker is free to use and closed source. Copyright © 2026 Choiril Luthfi,
all rights reserved. The source is not public and is not licensed for reuse.
Receiving a build permits installing and running it, and nothing more.

Third-party components keep their own licences and their notices ship inside the
app under **Settings → About & safety → Licences**. See [NOTICES.md](NOTICES.md).

---

## Feedback

Bug reports and sentence corrections are welcome, and corrections especially:
the version, build and adapter model make them actionable.

- Issues: [this repository](../../issues)
- Email: dptalkersupport@gmail.com

Independent project. No affiliation with, or endorsement by, any equipment
manufacturer, operator or vessel.
