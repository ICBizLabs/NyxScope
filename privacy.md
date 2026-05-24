# Privacy Policy — Nyx Scope

**Last updated:** 2026-05-11

This document describes what data the Nyx Scope desktop app sends to
ICBizLabs servers (i-c.biz), why, and how to opt out. It is plain-language
and intentionally short.

If you have questions, email [support@i-c.biz](mailto:support@i-c.biz).


## At a glance

| Data | When | Optional? | Where it goes |
|---|---|---|---|
| Crash reports | Only after you click "Send" on the prompt | Yes | `https://i-c.biz/api/v1/crash-report` |
| License heartbeat | Every few hours while the app runs (Trial/Licensed only) | No (only by deactivating the license) | `https://i-c.biz/api/v1/license/heartbeat` |
| FCC database queries | Each time you click Lookup or Auto-enrich a frequency | Yes (don't click Lookup) | `https://i-c.biz/db/api/v2/...` |

We do **not** transmit audio, IQ samples, recordings, transcripts, or your
spectrum waterfall. Those stay on your machine.


## Crash reports

When the app panics, the next launch shows a `CrashReportPromptDialog` with
the full report inline. Nothing is sent unless you click **Send**.

Before transmission, the report is **double-redacted**:

- **In the JS preview** you see what will be sent. License keys, API tokens,
  IP addresses, and home-directory paths are replaced with
  `<redacted-license-key>`, `<redacted-token>`, `<redacted-ip>`,
  `<redacted-home>`.
- **In Rust before HTTP send**, the same redaction runs again as a
  belt-and-suspenders check.

The transmitted report includes: panic message, file:line of the panic,
backtrace, the last ~100 breadcrumbs (UI events + decoder lifecycle
markers), app version, OS, and a SHA-256 hash of your hardware fingerprint
(used purely for de-duplication so we can tell "this is the same crash on
the same machine" without storing the raw fingerprint).

**Opt out**: tick "Don't ask again" in the prompt. Re-enable later in
Settings → Diagnostics (planned for a future minor release; for now,
deleting the per-app config file resets the choice).

Retention: crash reports are kept until they're triaged or 365 days,
whichever comes first.


## License heartbeat

Trial and Licensed installs ping `/api/v1/license/heartbeat` every few hours
to confirm the license isn't on the server-side revocation list. The ping
contains:

- Your license key id (numeric, not the full key)
- Your hardware fingerprint (a 16-character hex hash of stable hardware IDs)
- App version
- The current unix timestamp

No telemetry beyond this. No keystrokes, no usage statistics.

The heartbeat exists so revoked / fraud-flagged keys stop working without
requiring an app update. If your machine has no internet access, the app
continues to work offline indefinitely — the heartbeat is best-effort,
not a license-validity gate.

**Opt out**: deactivate the license in Settings → License.


## FCC database lookups (i-c.biz/db)

When you use Frequency Lookup, RadioReference Import (when configured to
also probe i-c.biz), or Auto-enrich, the app queries `/db/api/v2/search/...`
with the frequency, state, and your search filters. Authenticated via your
NyxScope license key (Trial/Licensed get FCC access bundled, no separate
key needed).

The search query is logged on the server for rate-limiting and abuse
detection. We do not log spectrum content or VFO state — only the explicit
search parameters you submit.

**Opt out**: don't click Lookup. The offline band-allocation database always
works without any network call.


## Local data

Recordings (audio + IQ), transcripts, your scan ranges, channel banks,
trunked-system configs, and all your settings live on your local disk in
the standard per-platform config directory. None of this is uploaded.

The app does not analytics-instrument the UI. There is no "first-run"
ping, no usage telemetry, no A/B testing framework.


## Storefront and customer portal (i-c.biz)

If you buy a license at <https://i-c.biz/buy/>, that's a standard Stripe
checkout — Stripe sees your card details (we don't), and we store the
order id, your email, the claim code we issued, and the IP you bought from
(captured for fraud-rate-limiting; we use Cloudflare's `CF-Connecting-IP`
header so your real IP is logged, not Cloudflare's edge). Standard
e-commerce data; nothing about your radio activity ties back to that
purchase record.

The customer portal (`i-c.biz/portal`) is a magic-link login keyed off
your purchase email. It logs your last login IP and timestamp for account
security; there's no other tracking.


## Third parties

- **Stripe** — payment processor. See <https://stripe.com/privacy>.
- **Cloudflare** — DNS + CDN + DDoS protection in front of i-c.biz. See
  <https://www.cloudflare.com/privacypolicy/>.
- The desktop app does **not** call any third-party API directly other
  than the user-configured Whisper / OpenAI transcription endpoint (only
  if you opted into transcription with the OpenAI engine — see Settings
  → Transcription).


## Changes to this policy

If we materially change what data is collected, we'll bump the "Last
updated" date and surface a one-time notice in the app. The current
version is also embedded as `privacy.md` in every release artifact.

For questions or data-deletion requests, email
[support@i-c.biz](mailto:support@i-c.biz).
