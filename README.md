# DP Talker

**NMEA 0183 serial reader · sensor & PRS simulator — for Android.**

A field and bench tool for marine ETOs and DP technicians. Plug a USB-serial
adapter into a phone and read what a sensor is actually putting on the wire, or
transmit a simulated one into a bench setup.

> **Not for use as a position reference input on a vessel in DP operations.**

---

## ⚠ Before you transmit

DP Talker writes NMEA sentences onto a real serial line. To the equipment
listening, simulated and replayed data are **indistinguishable from a live
sensor** — nothing in the sentence says it was made up.

Transmit only into equipment isolated from the vessel's DP, or into an input
whose operators know the data is simulated and have accepted it.

**Never** feed simulated or recorded data to a position reference, gyro, wind or
MRU input on a vessel in DP operations or preparing for them. A recording
carries a past position and a past time; a DP that accepts it will hold station
on somewhere the vessel is not.

The app cannot see what is on the other end of the cable. That check is yours,
every time.

---

## What it does

**Read.** Frames and decodes what arrives, and says how much it understood.
Decoded value cards for heading, wind, position, VRU motion, depth, log speed
and laser/radar range & bearing, each with its measured rate and a stale state
when the source goes quiet. Tap any raw line for a full field breakdown with
DP-specific guidance.

**Simulate.** Gyro, wind, DGNSS, VRU/MRU and position-reference sources, driven
live from the transmit screen — slew a heading, dial a sea state, swing a
bearing — with the exact frames previewed before a byte goes out.

**Record and replay.** Capture a session to a raw `.nmea` file, replay it to the
screen, or re-transmit it out the port at original timing. Checksum failures are
marked on the scrubber so a fault can be jumped to rather than hunted for.

**Sentences it knows.** GGA, GST, VTG, ZDA, RMC, GLL, HDT, THS, ROT, MWV, VBW,
DPT, Kongsberg PSXN,23, TSS1, and the position-reference telegram family —
Fanbeam/MDL, CyScan, ASCII17, Artemis, Nautronix.

---

## Requirements

- Android 8.0 (API 26) or newer
- **USB OTG support** — the app is useless without it
- A USB-to-serial adapter: FTDI, Prolific, CP210x, CH340 and CDC-ACM are all
  supported

---

## Install

Builds are published under [**Releases**](../../releases).

**Check the signature before you install.** A sideloaded APK is only as
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

The same fingerprint is shown inside the app under **Settings → About & safety →
Signing key**, read from the installed package itself. If the two do not match,
the APK is not this app, whatever it calls itself.

---

## Privacy

DP Talker has **no INTERNET permission**, so it cannot send anything anywhere.
No telemetry, no analytics, no crash reporting, no account.

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

A field and bench tool, written and maintained by one person. It is **not**
calibrated test equipment, **not** type-approved, **not** a position reference
system, and **not** endorsed by any manufacturer, operator or class society.
What you read is only as good as the adapter and the cable — treat it as an
indication, and confirm anything that goes into a report with an instrument that
carries a certificate.

Provided as-is, without warranty of any kind. Using it is your professional
judgement and your responsibility.

---

## Sentence definitions

DP Talker's sentence layouts were compiled from publicly available references —
gpsd's *NMEA Revealed*, manufacturers' published interface descriptions for
their own equipment, and output observed from real sensors.

The NMEA 0183 Interface Standard is a paid, copyrighted document published by
the National Marine Electronics Association. It was **not** used in building this
app, and DP Talker does not claim conformance to it or to any version of it.

Where DP Talker disagrees with your equipment's interface manual, **the manual is
right**. Tell me and I will fix it.

---

## Licence

DP Talker is **free to use** and **closed source**. Copyright © 2026 Choiril
Luthfi, all rights reserved — the source is not public and is not licensed for
reuse. Receiving a build permits installing and running it, and nothing more.

Third-party components keep their own licences and their notices ship inside the
app under **About → Licences**. See [NOTICES.md](NOTICES.md).

---

## Feedback

Bug reports and sentence corrections are welcome, and corrections especially:
the version, build and adapter model make them actionable.

- Issues: [this repository](../../issues)
- Email: c.luthfi07@gmail.com

Independent project. No affiliation with, or endorsement by, any equipment
manufacturer, operator or vessel.
