# NyxScope

**Professional wideband SDR scanner for Windows.**

Turn an inexpensive software-defined radio into a serious multi-protocol monitoring station. Watch the spectrum live, run multiple SDRs side-by-side, lock onto signals, follow trunked radio systems, decode digital voice, transcribe conversations, track aircraft and vessels, capture pager messages, log smart meters and weather sensors — all from one polished desktop application.

[**Download for your platform**](https://github.com/ICBizLabs/NyxScope/releases/latest) · [**Landing page**](https://i-c.biz/#nyx-scope) · [**Discord**](https://discord.gg/Wf4RRc2VPp) · [**Report a bug**](https://github.com/ICBizLabs/NyxScope/issues)

![NyxScope — trunked voice and paging side-by-side](screenshots/Trunkandpaging.png)

---

## Why NyxScope

- **One app, fifty-plus protocols.** Aviation, marine, public safety, amateur, paging, weather, broadcast — NyxScope decodes them all out of the box, no plugins, no glue scripts.
- **Sixteen simultaneous receivers from one radio.** Each with its own waterfall, audio, recording, transcription, and tone detection. Listen to a whole band at once.
- **Multi-SDR tabbed UI.** Plug in more than one radio and run them independently — each tab gets its own scan ranges, VFOs, decoded messages, classifications, and trunking state. Mix RTL-SDR + HackRF + PlutoSDR in the same session.
- **Built for serious listening.** Adaptive squelch tracks the noise floor in real time. Per-band tuning learns the right settings for each frequency range. Auto-identify tells you what protocol is on a strange frequency.
- **Smart trunking.** P25 Phase 1 and 2, EDACS, and NXDN with control-channel auto-discovery and seamless voice following. Phase 2 TDMA voice decode included.
- **Live transcription.** Speech-to-text on every active channel, powered by Whisper. Search every conversation you've ever heard.
- **Live tracking maps.** ADS-B aircraft, AIS vessels, APRS stations, and weather balloons plotted on an interactive map next to the data table — never a blocking modal.
- **Zero-config decoders.** All major decoders ship inside the app. No separate downloads. No `PATH` fiddling.
- **Self-updating.** Future releases install with one click.

## Highlights

- **Live spectrum and waterfall** with peak picking, frequency-hover tooltips, right-click tune-to-frequency, and one-click skip from peaks
- **Up to 16 concurrent VFOs** with mini-waterfalls and audio per channel
- **Multi-SDR tabbed UI** — one tab per connected radio, per-slot state scoping, mix-and-match hardware in a single session
- **Adaptive auto-squelch** with one-shot calibration and continuous tracking modes
- **Auto-identify digital protocol** — point at a strange signal and the app cycles through every digital voice mode and tells you which one fits
- **Signal classification** that names the modulation (FSK, GFSK, OOK, OFDM, …) before you even decide what to do with it
- **Quick Modes** — one-click presets for ADS-B, AIS, ACARS, VDL2, APRS, pagers, ISM sensors, and radiosondes
- **Compact and full VFO views** — pack the screen with channels or expand for diagnostics, your call
- **Channel-bank scanning** with priority sorting, skip lists, and CHIRP / RadioReference / FCC import
- **Live tracking map** for ADS-B, AIS, APRS, and radiosondes — inline split panel beside the data, click-to-filter both ways
- **HTTP audio streaming** — listen to any channel from another device on your network
- **IQ streaming** in RTL-TCP-compatible format for chaining to external tools
- **Per-VFO recording** — WAV audio and IQ formats, with VAD / VOX triggers, pre/post-record buffers, and notes that travel with the file
- **Per-band scanner overrides** — squelch, hold time, dwell, and digital-detect settings tuned automatically for each preset
- **Right-click frequency actions** on every message tab — Lookup Frequency / Save Frequency from DataLog rows, sensor rows, ADS-B / AIS / APRS / UAT / AIS-C / LoRa cards

![Quick Modes — one-click access to every supported preset](screenshots/QuickModes.png)

## Protocol Coverage

### Trunked Radio

- **P25 Phase 1** — native IMBE voice with best-effort FEC, 94–96 % frame recovery on signals where other tools get nothing
- **P25 Phase 2 TDMA** — native AMBE+2 voice with automatic Phase-1/Phase-2 routing from the control channel
- **EDACS** — Standard, EA, and Networked sites with optional ProVoice digital voice
- **NXDN** — NXDN48 and NXDN96 systems with channel-map editing
- **Control-channel auto-discovery** scans 851–869 MHz and identifies systems by NAC, WACN, RFSS, and Site
- **Active call tracking** with talkgroup, source ID, encryption flag, and call history
- **Encrypted-call indicator** so you know at a glance whether you'll hear voice

![P25 trunking — live talkgroup, source ID, encryption flag, and call history](screenshots/P25Trunking.png)

### Digital Voice

P25 (Phase 1 & 2), DMR, NXDN48, NXDN96, D-STAR, Yaesu System Fusion, M17, ProVoice — manual mode selection on a locked frequency, or hit the **Identify** button and let the app pick.

### Aviation & Marine

- **ADS-B 1090** — live aircraft positions, ICAO codes, altitude, callsigns, on a map
- **UAT 978** — general aviation ADS-B
- **AIS 162** — vessel MMSI, position, speed, heading, on a map
- **ACARS 130** — flight messages, registrations, labels, on the messages tab
- **VDL2 137** — VHF Data Link Mode 2 frames

![ADS-B aircraft tracking — interactive map next to the data table](screenshots/ADSB.png)

### Paging & Sensors

- **POCSAG 512 / 1200 / 2400** with capcode filtering and force-alpha override for medical and commercial pagers
- **FLEX and FLEX NEXT** with capcode tracking
- **rtl_433** — 200+ ISM device types: smart meters (ERT, IDM, NETIDM), weather stations (Bresser, Acurite, LaCrosse, Ambient), tire pressure monitors, garage doors, doorbells, soil moisture sensors, and many more
- **Radiosondes** — RS41, RS92, DFM, M10/M20 weather balloon telemetry on 400–406 MHz
- **LoRa** packet decode (with optional external decoder)

![Pager reception — POCSAG/FLEX traffic in real time](screenshots/PagerReception.png)

![ISM sensor decoding — smart meters, weather stations, TPMS, and more](screenshots/sensors.png)

![433 MHz remote controls and keyfobs decoded via rtl_433](screenshots/433CarRemotes.png)

### Tones, Signaling, Emergency

- DTMF, ZVEI 1/2/3, DZVEI, PZVEI, EEA, EIA, CCIR selective calling
- **CTCSS** — 50 standard tones detected per VFO with Goertzel-bank decoder and ratio-gated noise rejection (closely-spaced tones like 67.0 / 69.3 Hz resolve cleanly)
- **DCS** — 83 standard codes detected per VFO via full Golay (23,12) decode with O(1) rotation-and-polarity matching
- **Tone sighting log** — every CTCSS / DCS transition persists to the Tones tab and survives restart
- **TONE master toggle** in the TopBar disables CTCSS / DCS detection app-wide when you need the CPU
- EAS / SAME emergency alerts
- CallerID (CLIP) and German FMS (fire/ambulance)
- Native Morse / CW decoder with on-card readout

### Broadcast

- **HD Radio (NRSC-5)** — locks onto FM broadcast, switches between HD1–HD4 programs, displays station name, slogan, title, artist, album, genre, and quality stats
- **RDS** — station name, RadioText, program type, traffic alerts on any WFM lock

![HD Radio (NRSC-5) — HD1–HD4 program switching with full metadata](screenshots/HDRadio.png)

### Amateur

- **APRS** packet positions, weather, telemetry, messages
- AFSK1200 / AFSK2400 / FSK9600 packet data
- D-STAR, YSF, and M17 digital voice

## Quick Modes

One-click presets:

| Preset | Frequency | What you get |
| --- | --- | --- |
| ADS-B 1090 | 1090 MHz | Aircraft on a live map |
| AIS 162 | 161.975 / 162.025 MHz | Vessels on a live map |
| ACARS 130 | 129–131 MHz | Aircraft messages and flight data |
| VDL2 137 | 136.975 MHz | Modern VHF Data Link aircraft messaging |
| APRS 144.390 | 144.390 MHz | Amateur packet positions and weather |
| Pagers 929–932 | 929–932 MHz | POCSAG and FLEX pager traffic |
| 433 Sensors | 433 MHz ISM | European wireless sensors, keyfobs, garage remotes |
| 915 Sensors | 902–928 MHz | US smart meters, weather, security |
| Radiosonde 400–406 | 400–406 MHz | Weather balloon telemetry |

## Hardware Support

Bring your own SDR — the popular ones work natively, and you can run more than one at the same time:

| Hardware | Frequency Range | Notes |
| --- | --- | --- |
| RTL-SDR (and clones) | 24 MHz – 1.766 GHz | Native USB driver |
| HackRF One | 1 MHz – 6 GHz | 2–20 MHz sample-rate range enforced |
| Airspy R2 / Mini | 24 MHz – 1.8 GHz | Via SoapySDR |
| SDRplay (RSP series) | 1 kHz – 2 GHz | Via SoapySDR |
| LimeSDR / LimeSDR Mini | 100 kHz – 3.8 GHz | Via SoapySDR |
| PlutoSDR / Pluto+ | 70 MHz – 6 GHz | USB or Ethernet, dual-RX on Pluto+ |
| Network SDRs | — | `rtl_tcp` servers auto-discovered on the LAN |

Open the **Devices** dialog, pick more than one — each gets its own tab in the main UI.

## Editions

### Free

Everything you need to start exploring:

- Live spectrum and waterfall
- Single VFO listening
- Channel banks, scan ranges, quick modes
- POCSAG and FLEX paging
- CTCSS / DCS tone detection
- RDS on FM broadcast
- Signal classification
- Local control surface

### Trial — 30 days, no card required

Every Pro feature unlocked:

- Up to 16 concurrent VFOs
- Multi-SDR tabbed UI
- All trunking systems (P25, EDACS, NXDN)
- Full digital voice suite (P25, DMR, NXDN, D-STAR, YSF, M17, ProVoice)
- ADS-B, AIS, ACARS, VDL2, APRS, radiosonde, LoRa
- HD Radio
- Audio and IQ recording
- HTTP audio + IQ streaming
- Live transcription (Whisper, OpenAI, AssemblyAI)

### Pro — Licensed

Everything in Trial, no expiration. Hardware-bound activation key. Pricing announced on launch.

## Activation

1. Install and run NyxScope — your 30-day trial starts automatically.
2. Open **Settings → License**.
3. Copy the hardware fingerprint shown in the dialog.
4. Purchase a key (link in the dialog at launch).
5. Paste the key back into the License dialog and activate.

Licenses are bound to your computer's hardware fingerprint and can be transferred between machines on request.

## Privacy

- **Audio, IQ, recordings, transcripts, and the spectrum waterfall stay on your machine.** None of that is ever transmitted.
- **Local Whisper** transcription is fully offline — your audio never leaves your machine.
- **Cloud transcription** (OpenAI, AssemblyAI) is opt-in per channel; the app never sends audio without an explicit Enable click.
- **License heartbeat** — Trial and Licensed installs check the server every few hours to confirm the key hasn't been revoked. The ping carries your numeric key id and a hashed hardware fingerprint; no listening data is included.
- **Crash reports** are opt-in — the next launch after a panic shows the full report inline and nothing is sent unless you click **Send**. Reports are double-redacted (license keys, tokens, IPs, and home paths replaced) before transmission.
- **FCC database lookups** only happen when you click **Lookup** or **Auto-enrich** on a frequency.

Full plain-language details and opt-out steps live in `privacy.md`, shipped inside every release artifact.

## System Requirements

- 64-bit Windows 10 or 11
- 4 GB RAM minimum, 8 GB recommended for heavy multi-VFO use with transcription
- Compatible SDR hardware (see table above)
- ~500 MB disk for the app, plus your own room for recordings

## What's New

### v1.23.0 — Subprocess isolation

- **mbelib-neo runs out-of-process** as a small helper binary. Keeps the main NyxScope process clean of mbelib-neo's GPL-incompatible vocoder symbols; the helper communicates over stdin/stdout pipes. No user-visible behavior change — voice decode quality is identical.
- **Helper integrity check** rejects stale or placeholder binaries (any candidate under 50 KB) so a stripped install never silently runs without IMBE/AMBE.

### v1.22.0 — Beta polish

- **Beta trial extended from 7 to 30 days** — more time to evaluate every Pro feature.
- **Multi-SDR tabbed UI** — connect multiple radios and run them independently in the same session, each with its own state.
- **CTCSS / DCS decoder rewrite** — Goertzel-bank CTCSS with median-noise + ratio gating; full Golay (23,12) DCS with O(1) rotation/polarity matching. Closely-spaced tones (67.0 / 69.3 Hz) resolve correctly; D023N verified against a live transmitter.
- **Tone sighting log + TONE master toggle** — every CTCSS / DCS transition is logged to the Tones tab and survives restart. One TopBar button disables all tone detection if you need the CPU back.
- **P25 / DMR / NXDN false-positive fixes** — digital voice no longer mis-classifies as analog `Voice`, no phantom CTCSS / DCS sightings during vocoder frames.
- **HackRF Windows retune hang fix** — drift-probe on first retune detects whether the SoapyHackRF driver re-enumerates the device, then skips the failing post-retune reapply for the rest of the session. Eliminates the `EPIPE / Invalid Board ID` death-spiral on fast scans.
- **Right-click frequency actions** on every message tab — Lookup Frequency and Save Frequency from any DataLog row, sensor row, or protocol card.
- **Tab description tooltips** on every DataLog / ProtocolDecoder tab.
- **TopBar visual unification** — design tokens for radius, accent palette, and decoder colors; License badge restyled.

Full per-release notes ship inside the install at `RELEASE_NOTES_v<X.Y.Z>.md`.

## Download

| Platform | File | Get it |
| --- | --- | --- |
| Windows | `.exe` installer or `.msi` | [Releases](https://github.com/ICBizLabs/NyxScope/releases/latest) |

All releases are signed and self-update once installed — install once, future releases land with a single click.

## Support

- **Bug reports & feature requests** — [open an issue](https://github.com/ICBizLabs/NyxScope/issues)
- **Community chat** — [Discord](https://discord.gg/Wf4RRc2VPp)
- **Documentation & guides** — [i-c.biz/#nyx-scope](https://i-c.biz/#nyx-scope)

## Notices

NyxScope is commercial software distributed by ICBizLabs. The bundled third-party decoders (multimon-ng, rtl_433, dsd-neo, nrsc5, direwolf, acarsdec, dump978, AIS-catcher, rs41mod, mbelib-neo) are open source and ship under their original licenses. The mbelib-neo vocoder runs as an isolated helper process to keep its license boundary clean. See `THIRD_PARTY_NOTICES.md` in each release for the full list.

---

*Built by ICBizLabs · [i-c.biz/#nyx-scope](https://i-c.biz/#nyx-scope)*
