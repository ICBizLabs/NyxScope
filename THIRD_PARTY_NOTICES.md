# Third-Party Notices

Nyx Scope incorporates the following third-party components. Each is
listed with its upstream project and license. This document is provided
for attribution and license-compliance purposes.

The authoritative per-component upstream commit reference for the
**exact** source matching every bundled binary is recorded in
[`THIRD_PARTY_SOURCES.json`](./THIRD_PARTY_SOURCES.json). Full license
texts (GPL-2.0, GPL-3.0, LGPL-2.0, LGPL-2.1) are bundled in
[`LICENSES/`](./LICENSES/).

## Bundled Decoders

These decoder binaries are distributed with Nyx Scope and invoked as
separate sidecar processes at runtime (Tauri `externalBin`). Each
remains under its own upstream license; the Nyx Scope application code
is governed by the EULA in [`eula.md`](./eula.md).

| Component   | Purpose                                            | Upstream                                            | License              |
| ----------- | -------------------------------------------------- | --------------------------------------------------- | -------------------- |
| multimon-ng | Paging, tones, EAS, AFSK, classic digital decodes  | https://github.com/EliasOenal/multimon-ng           | GPL-2.0-or-later     |
| rtl_433     | ISM-band sensors and utility meters                | https://github.com/merbanan/rtl_433                 | GPL-2.0-or-later     |
| acarsdec    | ACARS decode                                       | https://github.com/TLeconte/acarsdec                | LGPL-2.0             |
| direwolf    | APRS / AX.25 decode                                | https://github.com/wb2osz/direwolf                  | GPL-2.0              |
| nrsc5       | HD Radio / NRSC-5 decode                           | https://github.com/theori-io/nrsc5                  | GPL-3.0              |
| rs41mod     | RS41 radiosonde decode                             | https://github.com/rs1729/RS                        | GPL-3.0              |
| dump978     | UAT 978 MHz ADS-B decode                           | https://github.com/mutability/dump978 (archived)    | GPL-2.0              |
| AIS-catcher | AIS decode                                         | https://github.com/jvde-github/AIS-catcher          | GPL-3.0-or-later     |
| dumpvdl2    | VDL Mode 2 decode                                  | https://github.com/szpajder/dumpvdl2                | GPL-3.0              |
| dsd-neo     | P25 / DMR / NXDN digital voice decode              | https://github.com/arancormonk/dsd-neo              | GPL-3.0-or-later     |

> **Note on dump978.** The `mutability/dump978` repository was archived
> upstream in 2023 and explicitly redirects users to the FlightAware
> fork at `flightaware/dump978`, which is distributed under
> BSD-2-Clause. The dump978 binary bundled here corresponds to the
> archived `mutability/dump978` (GPL-2.0); the matching source remains
> available at the archived repository URL.

## IMBE / AMBE / AMBE+2 Vocoder — GPL Containment Subprocess

The Nyx Scope main binary contains **no statically or dynamically linked
GPL or LGPL object code**. The `mbelib-neo` vocoder needed for P25
Phase 1 (IMBE), P25 Phase 2 (AMBE+2), and EDACS ProVoice (IMBE 7100x4400)
voice decoding lives exclusively in a separate executable, **`sdr-imbe-helper`**,
which the main app spawns as a child process and communicates with over
`stdin` / `stdout`. This subprocess boundary is the project's GPL
containment line: `sdr-imbe-helper` is itself a GPL-2.0-or-later combined
work, but the main Nyx Scope binary that invokes it is not.

| Component         | Purpose                                                                       | Upstream                                            | License              |
| ----------------- | ----------------------------------------------------------------------------- | --------------------------------------------------- | -------------------- |
| mbelib-neo        | IMBE / AMBE / AMBE+2 vocoder (linked into sdr-imbe-helper; also into dsd-neo) | https://github.com/arancormonk/mbelib-neo           | GPL-2.0-or-later     |
| sdr-imbe-helper   | Nyx Scope's GPL containment helper wrapping mbelib-neo over a stdio protocol  | this distribution (`crates/sdr-imbe-helper/`)       | GPL-2.0-or-later     |

> **License correction (v1.22.0).** Prior versions of this document and
> the EULA labelled mbelib-neo as "LGPL-2.1". That was incorrect.
> Upstream distributes mbelib-neo under "GPL-2.0 or any later version"
> per its README and `LICENSE` file.
>
> **Architecture correction (v1.23.0).** v1.22.0 statically linked
> mbelib-neo into the Nyx Scope main binary via the `sdr-imbe` Rust
> crate's build script. That made the v1.22.0 main binary a GPL
> combined work. **v1.23.0 and later isolate mbelib-neo behind the
> `sdr-imbe-helper` subprocess** so the main binary contains no GPL
> object code and is governed solely by the proprietary EULA. The
> in-process `sdr-imbe` crate is now a thin client that pipes frames
> to `sdr-imbe-helper` and reads back PCM; it links nothing GPL.

## Bundled Runtime Libraries (DLLs)

The Windows installer additionally bundles the following runtime
libraries needed by the decoder sidecars listed above. Each is loaded
dynamically by its parent sidecar (subprocess boundary); none is
linked into the Nyx Scope main binary.

### Inside `src-tauri/dsd-neo-libs/` (dynamic dependencies of dsd-neo.exe)

| Library         | Purpose                                  | Upstream                                            | License              |
| --------------- | ---------------------------------------- | --------------------------------------------------- | -------------------- |
| mbe-neo.dll     | IMBE / AMBE vocoder (see section above)  | https://github.com/arancormonk/mbelib-neo           | GPL-2.0-or-later     |
| SoapySDR.dll    | SDR device abstraction                   | https://github.com/pothosware/SoapySDR              | Boost Software 1.0   |
| codec2.dll      | Speech codec                             | https://github.com/drowe67/codec2                   | LGPL-2.1             |
| FLAC.dll        | FLAC audio                               | https://xiph.org/flac/                              | BSD-3-Clause / GPL-2 |
| libmp3lame.dll  | MP3 encode                               | https://lame.sourceforge.io/                        | LGPL-2.0             |
| mpg123.dll      | MP3 decode                               | https://www.mpg123.de/                              | LGPL-2.1             |
| ogg.dll         | Ogg bitstream                            | https://xiph.org/ogg/                               | BSD-3-Clause         |
| opus.dll        | Opus audio codec                         | https://opus-codec.org/                             | BSD-3-Clause         |
| pdcurses.dll    | Terminal-emulation library               | https://pdcurses.org/                               | Public Domain        |
| portaudio.dll   | Cross-platform audio I/O                 | http://www.portaudio.com/                           | MIT                  |
| rtlsdr.dll      | RTL-SDR driver                           | https://gitea.osmocom.org/sdr/rtl-sdr               | GPL-2.0              |
| sndfile.dll     | libsndfile (PCM/WAV)                     | https://github.com/libsndfile/libsndfile            | LGPL-2.1             |
| vorbis.dll      | Vorbis decode                            | https://xiph.org/vorbis/                            | BSD-3-Clause         |
| vorbisenc.dll   | Vorbis encode                            | https://xiph.org/vorbis/                            | BSD-3-Clause         |

### Inside `src-tauri/binaries/` (MinGW / MSYS2 runtime DLLs for the other sidecars)

| Library                | Upstream / Source                                   | License              |
| ---------------------- | --------------------------------------------------- | -------------------- |
| libFLAC.dll            | https://xiph.org/flac/                              | BSD-3-Clause         |
| libacars-2.dll         | https://github.com/szpajder/libacars                | MIT                  |
| libfftw3-3.dll         | http://www.fftw.org/                                | GPL-2.0-or-later     |
| libgcc_s_seh-1.dll     | https://gcc.gnu.org/ (MinGW-w64 runtime)            | GPL-3.0 + GCC RTE    |
| libglib-2.0-0.dll      | https://gitlab.gnome.org/GNOME/glib                 | LGPL-2.1-or-later    |
| libhackrf.dll          | https://github.com/greatscottgadgets/hackrf         | GPL-2.0              |
| libiconv-2.dll         | https://www.gnu.org/software/libiconv/              | LGPL-2.1-or-later    |
| libintl-8.dll          | https://www.gnu.org/software/gettext/               | LGPL-2.1-or-later    |
| liblzma-5.dll          | https://tukaani.org/xz/                             | Public Domain        |
| libmp3lame-0.dll       | https://lame.sourceforge.io/                        | LGPL-2.0             |
| libmpg123-0.dll        | https://www.mpg123.de/                              | LGPL-2.1             |
| libogg-0.dll           | https://xiph.org/ogg/                               | BSD-3-Clause         |
| libopus-0.dll          | https://opus-codec.org/                             | BSD-3-Clause         |
| libpcre2-8-0.dll       | https://github.com/PCRE2Project/pcre2               | BSD-3-Clause         |
| librtlsdr.dll          | https://gitea.osmocom.org/sdr/rtl-sdr               | GPL-2.0              |
| libsndfile-1.dll       | https://github.com/libsndfile/libsndfile            | LGPL-2.1             |
| libsqlite3-0.dll       | https://www.sqlite.org/                             | Public Domain        |
| libstdc++-6.dll        | https://gcc.gnu.org/ (MinGW-w64 runtime)            | GPL-3.0 + GCC RTE    |
| libusb-1.0.dll         | https://libusb.info/                                | LGPL-2.1-or-later    |
| libvorbis-0.dll        | https://xiph.org/vorbis/                            | BSD-3-Clause         |
| libvorbisenc-2.dll     | https://xiph.org/vorbis/                            | BSD-3-Clause         |
| libwinpthread-1.dll    | https://sourceforge.net/projects/mingw-w64/         | MIT-style (MinGW-w64)|
| libxml2-2.dll          | https://gitlab.gnome.org/GNOME/libxml2              | MIT                  |
| zlib1.dll              | https://zlib.net/                                   | Zlib                 |

> **MinGW-w64 / GCC runtime DLLs.** `libgcc_s_seh-1.dll`,
> `libstdc++-6.dll`, and `libwinpthread-1.dll` are MinGW-w64 runtime
> redistributables. They are licensed under GPL-3.0 (gcc) and
> LGPL-2.1+ (winpthreads) subject to the GCC Runtime Library Exception,
> which permits redistribution of compiled programs that use the
> runtime under any license. See
> https://www.gnu.org/licenses/gcc-exception-3.1.html.

## Bundled Microsoft Redistributable

The Windows installer post-install hook
(`src-tauri/installer/hooks.nsh.in`) invokes the bundled
**Microsoft Visual C++ 2015–2022 Redistributable (x64)** installer,
fetched at build time by `scripts/download-vc-redist.py` from
Microsoft's official download URL. The redistributable is licensed
under the Microsoft Visual Studio Community / Enterprise / Professional
license terms applicable to redistribution; redistribution is permitted
to licensed Visual Studio users per the Microsoft documentation at
https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist.

## Optional Components (Not Bundled)

These components can be enabled by installing them separately and
pointing Nyx Scope at their executables. They are *not* shipped in the
installer.

| Component                                 | Purpose                       | Upstream                                                |
| ----------------------------------------- | ----------------------------- | ------------------------------------------------------- |
| rs92mod, dfm09mod, m10mod                 | Additional radiosonde decoders| https://github.com/rs1729/RS                            |
| gr-lora                                   | LoRa decode (GNU Radio)       | https://github.com/rpp0/gr-lora                         |

## Source Code Availability

Per GPL §3(a), exact corresponding source code for every GPL- and
LGPL-licensed component above is published at:

    https://i-c.biz/sources/v{version}/

indexed by Nyx Scope release version. Each per-version directory
contains:

  - The exact Nyx Scope application source corresponding to the
    installer (`nyxscope-source-v{version}.tar.gz`).
  - Per-component source archives matching the bundled GPL/LGPL
    binaries, identified by upstream commit hash.
  - A copy of [`THIRD_PARTY_SOURCES.json`](./THIRD_PARTY_SOURCES.json)
    as audit manifest.
  - `SHA256SUMS.txt` for integrity verification.

A written request for source on physical media may also be made to
<support@i-c.biz>; see EULA §9.3 for the full written offer.

## Application Frameworks

Nyx Scope is built on the following open-source frameworks:

- **Rust** (https://www.rust-lang.org) — Apache-2.0 / MIT
- **Tauri** (https://tauri.app) — Apache-2.0 / MIT
- **Svelte** (https://svelte.dev) — MIT

A full dependency manifest is available in the application's source
tree (`Cargo.lock`, `ui/package-lock.json`).
