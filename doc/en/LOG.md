---
name: project-log-en
description: Project bugs, limitations, decisions, and handoff
metadata:
  version: "1.0.0"
  lang: "en"
---

# Log

## Multi-language

[简体中文](../LOG.md) | **English** | [Español](../es/LOG.md)

## Documentation

- Project overview: [README](README.md)

- Design rationale: [DESIGN](DESIGN.md)

- Project status: [LOG](LOG.md)
- Historical records: [HISTORY](HISTORY.md)
- Version changelog: [CHANGELOG](CHANGELOG.md)

- Third-party notices: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## Records

- [History](HISTORY.md)
- [Changelog](CHANGELOG.md)

## Bugs

No confirmed bugs.

## Limitations

- The system image ships with a backup keybox seed. It stops working once it expires or is revoked, after which key attestation requires the user to import a valid keybox. The validity of the seed in this release has not been verified.
- Keep-data flashing only applies to a device already running this project's BP1A system.
- LE Audio is disabled; dual-mode headphones use classic Bluetooth.
- Face unlock is a WEAK biometric: it can unlock and do weak verification, but it cannot authorize payments or open StrongBox credentials.
- Trimming removed the preinstalled Google apps and the accessibility apps (TalkBack, etc.); reinstall what you need from Play.
- The Bluetooth call fix targets the ZUI 17.0.12.044 vendor bundled in this package. If the device's vendor is replaced with another version, the fix may not apply (not verified).
- About 3 pixels of space remain at the bottom after hiding the navigation bar. The official BP1A launcher also uses the taskbar's stashed height as the end-of-gesture region for the recents swipe, and setting it to 0 leaves apps unresponsive after a swipe-up that is reversed halfway, so it is set to 1dp.

## Decisions

| Date | Decision | Status | Reason |
| --- | --- | --- | --- |
| 2026-11-05 | One repository per base-image version | Accepted | PixelOS 15 tangorpro has several base-image versions |
| 2026-11-05 | Releases contain only the complete 9008 flashing package, not root variants or incremental patches | Accepted | Specified by the user |
| 2026-11-05 | 7z volumes are 2000 MiB each | Accepted | Below GitHub's 2 GiB per-asset limit |
| 2026-11-05 | Release numbers are per base-image line; the first release of this repository is user-v1.0 | Accepted | Avoids clashing with the 1.4 of the AP3A line |
| 2026-11-05 | Third-party licenses not yet verified when the repository is made public | Accepted | Follows what the AP3A repository did; verification is listed as a remaining step |

## Handoff

The current handoff is maintained in the [Simplified Chinese LOG.md](../LOG.md#交接).
