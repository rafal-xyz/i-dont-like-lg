# i-dont-like-lg

A single-file LG Smart TV (webOS) anti-telemetry, anti-ACR, and ad blocklist for
Pi-hole, AdGuard Home, or a plain hosts file.

Every domain was **verified by DNS-logging two real LG webOS TVs** (a 2020 and a
2023 model), then merged with the known public LG lists. Unlike most lists it is
**region-proof** (enumerates `pl.*`, `eu.*`, `de.*`, not just `us.*`) and it is
**tuned to keep the TV usable**: Netflix voice search, streaming, the LG app
store, and LG ThinQ smart-home control are deliberately left working.

## Use it

Add the raw URL as an adlist in Pi-hole (Lists) or AdGuard Home (Filters ->
DNS blocklists):

```
https://raw.githubusercontent.com/rafal-xyz/i-dont-like-lg/main/hosts.txt
```

Then update gravity (`pihole -g`) or let AdGuard refresh. Or append `hosts.txt`
to `/etc/hosts` directly.

## What it blocks

LG Smart Ad, Smart Delivery Platform + `rdx2` ad-exchange, IoT/telemetry
(`lgtviot`), Alphonso ACR (fingerprints what is on screen), WISE content
recognition, platform/account telemetry (`lgsmartplatform`, `lgeapi`), Content
Store ad/billing hosts, the Customer Data Platform / ads / home-screen promos on
`lgtvcommon.com`, LG video-ad partners (`yumenetworks`, `smartclip`,
`cjpowercast`), and LG firmware/OTA update hosts. Sections are commented inside
the file.

## Deliberately left working

`netflixvoice.lgtvcommon.com` (Netflix voice search), all streaming
(Netflix/Prime/YouTube), and the base `lgappstv.com` / `lgthinq.com` (app store +
smart-home). Only their ad/telemetry subdomains are blocked.

## Notes

- The firmware/OTA section **freezes webOS updates**. Remove those lines if you
  want updates.
- Blocking `lgeapi.com` may affect LG account sign-in on some setups; allow it if
  needed.
- **DoH warning:** some webOS firmware uses hardcoded DNS-over-HTTPS and can bypass
  DNS blocking. Also block outbound DoH on your router and do not set a manual
  public DNS on the TV.

## License

MIT. See `LICENSE`. Provided as-is; blocking telemetry can change TV behavior.
