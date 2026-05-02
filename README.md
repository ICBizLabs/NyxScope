# NyxScope

**Professional wideband SDR scanner for Windows, macOS, and Linux.**

Turn an inexpensive software-defined radio into a serious multi-protocol monitoring station. Watch the spectrum live, lock onto signals, follow trunked radio systems, decode digital voice, transcribe conversations, track aircraft and vessels, capture pager messages, log smart meters and weather sensors — all from one polished desktop application.

[**Download for your platform**](https://github.com/ICBizLabs/NyxScope/releases/latest) · [**Landing page**](https://icbizlabs.github.io/NyxScope/) · [**Report a bug**](https://github.com/ICBizLabs/NyxScope/issues)

---

## Why NyxScope

- **One app, fifty-plus protocols.** Aviation, marine, public safety, amateur, paging, weather, broadcast — NyxScope decodes them all out of the box, no plugins, no glue scripts.
- **Sixteen simultaneous receivers from one radio.** Each with its own waterfall, audio, recording, transcription, and tone detection. Listen to a whole band at once.
- **Built for serious listening.** Adaptive squelch tracks the noise floor in real time. Per-band tuning learns the right settings for each frequency range. Auto-identify tells you what protocol is on a strange frequency.
- **Smart trunking.** P25 Phase 1 and 2, EDACS, and NXDN with control-channel auto-discovery and seamless voice following. Phase 2 TDMA voice decode included.
- **Live transcription.** Speech-to-text on every active channel, powered by Whisper. Search every conversation you've ever heard.
- **Live tracking maps.** ADS-B aircraft, AIS vessels, APRS stations, and weather balloons plotted on an interactive map next to the data table — never a blocking modal.
- **Zero-config decoders.** All major decoders ship inside the app. No separate downloads. No `PATH` fiddling.
- **Self-updating.** Future releases install with one click.

## Highlights

- **Live spectrum and waterfall** with peak picking, frequency-hover tooltips, right-click tune-to-frequency, and one-click skip from peaks
- **Up to 16 concurrent VFOs** with mini-waterfalls and audio per channel
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

## Protocol Coverage

### Trunked Radio

- **P25 Phase 1** — native IMBE voice with best-effort FEC, 94–96 % frame recovery on signals where other tools get nothing
- **P25 Phase 2 TDMA** — native AMBE+2 voice with automatic Phase-1/Phase-2 routing from the control channel
- **EDACS** — Standard, EA, and Networked sites with optional ProVoice digital voice
- **NXDN** — NXDN48 and NXDN96 systems with channel-map editing
- **Control-channel auto-discovery** scans 851–869 MHz and identifies systems by NAC, WACN, RFSS, and Site
- **Active call tracking** with talkgroup, source ID, encryption flag, and call history
- **Encrypted-call indicator** so you know at a glance whether you'll hear voice

### Digital Voice

P25 (Phase 1 & 2), DMR, NXDN48, NXDN96, D-STAR, Yaesu System Fusion, M17, ProVoice — manual mode selection on a locked frequency, or hit the **Identify** button and let the app pick.

### Aviation & Marine

- **ADS-B 1090** — live aircraft positions, ICAO codes, altitude, callsigns, on a map
- **UAT 978** — general aviation ADS-B
- **AIS 162** — vessel MMSI, position, speed, heading, on a map
- **ACARS 130** — flight messages, registrations, labels, on the messages tab
- **VDL2 137** — VHF Data Link Mode 2 frames

### Paging & Sensors

- **POCSAG 512 / 1200 / 2400** with capcode filtering and force-alpha override for medical and commercial pagers
- **FLEX and FLEX NEXT** with capcode tracking
- **rtl_433** — 200+ ISM device types: smart meters (ERT, IDM, NETIDM), weather stations (Bresser, Acurite, LaCrosse, Ambient), tire pressure monitors, garage doors, doorbells, soil moisture sensors, and many more
- **Radiosondes** — RS41, RS92, DFM, M10/M20 weather balloon telemetry on 400–406 MHz
- **LoRa** packet decode (with optional external decoder)

### Tones, Signaling, Emergency

- DTMF, ZVEI 1/2/3, DZVEI, PZVEI, EEA, EIA, CCIR selective calling
- CTCSS — 50 standard tones detected per VFO
- DCS — 83 standard codes detected per VFO
- EAS / SAME emergency alerts
- CallerID (CLIP) and German FMS (fire/ambulance)
- Native Morse / CW decoder with on-card readout

### Broadcast

- **HD Radio (NRSC-5)** — locks onto FM broadcast, switches between HD1–HD4 programs, displays station name, slogan, title, artist, album, genre, and quality stats
- **RDS** — station name, RadioText, program type, traffic alerts on any WFM lock

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
| 433 Sensors | 433 MHz ISM | European wireless sensors |
| 915 Sensors | 902–928 MHz | US smart meters, weather, security |
| Radiosonde 400–406 | 400–406 MHz | Weather balloon telemetry |

## Hardware Support

Bring your own SDR — the popular ones work natively:

| Hardware | Frequency Range |
| --- | --- |
| RTL-SDR (and clones) | 24 MHz – 1.766 GHz |
| HackRF One | 1 MHz – 6 GHz |
| Airspy R2 / Mini | 24 MHz – 1.8 GHz |
| SDRplay (RSP series) | 1 kHz – 2 GHz |
| LimeSDR / LimeSDR Mini | 100 kHz – 3.8 GHz |
| PlutoSDR / Pluto+ | 70 MHz – 6 GHz (USB or Ethernet) |
| Network SDRs | `rtl_tcp` servers, auto-discovered on the LAN |

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

### Trial — 7 days, no card required

Every Pro feature unlocked:

- Up to 16 concurrent VFOs
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

1. Install and run NyxScope — your 7-day trial starts automatically.
2. Open **Settings → License**.
3. Copy the hardware fingerprint shown in the dialog.
4. Purchase a key (link in the dialog at launch).
5. Paste the key back into the License dialog and activate.

Licenses are bound to your computer's hardware fingerprint and can be transferred between machines on request.

## Privacy

- **Local Whisper** transcription is fully offline — your audio never leaves your machine.
- **Cloud transcription** (OpenAI, AssemblyAI) is opt-in per channel; the app never sends audio without an explicit Enable click.
- **Your listening data stays on your machine.** Recordings, transcripts, sensor logs, and call history never leave the app unless you export them.
- **No telemetry.** NyxScope doesn't phone home.

## System Requirements

- 64-bit Windows 10 or 11, macOS 11+, or modern Linux (glibc 2.31+)
- 4 GB RAM minimum, 8 GB recommended for heavy multi-VFO use with transcription
- Compatible SDR hardware (see table above)
- ~500 MB disk for the app, plus your own room for recordings

## Download

| Platform | File | Get it |
| --- | --- | --- |
| Windows | `.exe` installer or `.msi` | [Releases](https://github.com/ICBizLabs/NyxScope/releases/latest) |
| macOS | `.dmg` (Apple Silicon and Intel) | [Releases](https://github.com/ICBizLabs/NyxScope/releases/latest) |
| Linux | `.deb` and `.AppImage` | [Releases](https://github.com/ICBizLabs/NyxScope/releases/latest) |

All releases are signed and self-update once installed — install once, future releases land with a single click.

## Support

- **Bug reports & feature requests** — [open an issue](https://github.com/ICBizLabs/NyxScope/issues)
- **Documentation & guides** — [icbizlabs.github.io/NyxScope](https://icbizlabs.github.io/NyxScope/)
 

## Notices

NyxScope is commercial software distributed by ICBizLabs. The bundled third-party decoders (multimon-ng, rtl_433, dsd-neo, nrsc5, direwolf, acarsdec, dump978, AIS-catcher, rs41mod, mbelib-neo) are open source and ship under their original licenses. See `THIRD_PARTY_NOTICES.md` in each release for the full list.

---

*Built by ICBizLabs · [icbizlabs.github.io/NyxScope](https://icbizlabs.github.io/NyxScope/)*
