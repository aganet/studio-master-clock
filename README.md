# LED Studio Master Clock

A fullscreen LED-style master clock in a single HTML file, for TV and radio studios,
ham radio shacks and anywhere else a big, accurate clock is wanted.

## About this clock

I have always been fascinated by studio-style LED clocks, with their sleek and professional appearance often seen in television studios and production environments. Unfortunately, I never had the opportunity to own one myself. After searching extensively for a similar project online and not finding anything that matched my vision, I decided to create one from scratch. This clock is my way of combining my appreciation for studio aesthetics with my passion for programming.

This project is highly versatile and can be used in various ways:

- As a studio-style LED clock with Raspberry Pi and screens.
- By ham radio enthusiasts to display custom call signs alongside the clock.

I am sharing this project to help others who might also be interested in having a similar clock. Feel free to use, customize, or contribute to its development!

![master-clock](https://github.com/user-attachments/assets/877a2fba-d43a-4280-a8dc-6d10175b1404)

## Demo

[DEMO](https://clock.aganet.gr)

## Features

- Seven-segment LED digits (DSEG7 font, embedded, so the page works offline) with a 60-dot
  second ring and hour markers.
- Date line with the time zone abbreviation (CET, UTC, ...), any IANA time zone, 12 or 24 hour.
- Second clock in another zone, e.g. UTC next to local time. `?utc` puts UTC in the main
  display and local time in the second clock, the usual ham radio setup.
- Custom label under the time: studio name or call sign.
- ON AIR sign, count-up timer and countdown with overrun, hourly time pips.
- Remote control over Server-Sent Events or WebSocket: ON AIR, label, dim, timer.
- Optional time server sync: NTP-style four-timestamp exchange, drift estimation, slewed
  corrections and a holdover state with an error bound when the server goes away.
- Wide screens get the ON AIR sign and timer beside the dial, square and portrait screens
  use the corners. Screen wake lock, hidden cursor, dim mode and anti-burn-in drift.
- No dependencies, no build step, one file.

## Quick start

Open `master-clock.html` in a browser and press `F` for fullscreen. Everything is configured
through URL parameters, so a kiosk setup is just a bookmark:

```
master-clock.html?text=STUDIO%201&tz2=UTC
master-clock.html?utc&text=M0JPK%20JN47
master-clock.html?color=amber&h12&lang=de-CH
```

Press `H` on the clock for the full list.

### Keys

| Key | Action |
| --- | --- |
| `F` or double-click | Fullscreen |
| `D` | Dim the display |
| `O` | Toggle the ON AIR sign |
| `T` / `R` | Start or stop the timer / reset it |
| `1`-`9` / `0` | Load a 1-9 minute countdown / back to count-up |
| `P` | Toggle the hourly time pips |
| `S` | Sync now |
| `H` or `Esc` | Help |

### URL parameters

| Parameter | Meaning |
| --- | --- |
| `text=STUDIO%201` | Label under the time, empty hides it |
| `color=red` | `red`, `green`, `amber`, `blue`, `white` or a hex value |
| `utc` | Main clock in UTC, local time in the second clock |
| `tz=Europe/Zurich` | Time zone of the main clock |
| `tz2=UTC`, `tz2label=` | Second clock and its label |
| `h12` | 12-hour display |
| `lang=de-CH` | Language of the date |
| `date=0`, `zone=0` | Hide the date or the zone abbreviation |
| `pips` | Hourly time pips (browsers need one click or key press before playing sound) |
| `sync=timeapi` | Time server, see below. `timeapi` and `worldtimeapi` are public shortcuts, any URL returning an ISO time or epoch works |
| `interval=60`, `samples=4` | Seconds between syncs, samples per burst |
| `warn=500` | Warn when this computer's clock is off by more than this many ms |
| `countdown=300` | Preload the timer as a countdown (seconds) |
| `onair` | Always show the ON AIR sign |
| `events=...`, `ws=...` | Remote control endpoint |
| `dim`, `shift=0` | Start dimmed, turn off the anti-burn-in drift |

## Time

Without `sync` the clock shows the operating system time, so keep the computer on NTP.
The top-left status says so.

With `sync=<url>` the page disciplines its own clock against a time server: it takes a burst
of samples, keeps the one with the lowest round trip, fits offset and drift over the last 30
minutes, slews small corrections (time never runs backwards) and steps large ones. The status
shows the lock state, the error bound, how far the computer's own clock is off, and the drift
in ppm. If the server disappears the clock goes to holdover and the error bound grows.

## Remote control

The clock listens for commands over Server-Sent Events (`?events=<url>`) or a WebSocket
(`?ws=ws://host:port`). A message is JSON or plain `ON` / `OFF`:

```
ON
{"onair": false, "text": "STUDIO 2"}
{"timer": {"countdown": 300, "start": true}}
{"timer": "stop"}
{"dim": true}
```

Any small server that pushes these to the displays will do.

## Kiosk setup

On a Raspberry Pi or any Linux box, a fullscreen Chromium kiosk is enough:

```
chromium --kiosk --noerrdialogs --disable-infobars "file:///path/to/master-clock.html?text=STUDIO%201&tz2=UTC"
```

The page requests a screen wake lock, hides the cursor after three seconds and nudges the
dial by a fraction of a millimetre every five minutes to avoid burn-in.

## Requirements

- A current browser (Chrome, Edge, Firefox, Safari).

## Credits

- [DSEG](https://github.com/keshikan/DSEG) seven-segment font by keshikan, SIL Open Font License 1.1.

## License

This project is licensed under the MIT License.
