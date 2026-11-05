---
name: project-changelog-en
description: Changelog
metadata:
  version: "1.0.0"
  lang: "en"
---

# Changelog

## Multi-language

[简体中文](../CHANGELOG.md) | **English** | [Español](../es/CHANGELOG.md)

## Documentation

- Project overview: [README](README.md)

- Design rationale: [DESIGN](DESIGN.md)

- Project status: [LOG](LOG.md)
- Historical records: [HISTORY](HISTORY.md)
- Version changelog: [CHANGELOG](CHANGELOG.md)

- Third-party notices: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## Changelog

### user-v1.0(V3)- 2026-11-05

- Added: The first release of this repository, providing the complete 9008 flashing package volumes, `SHA256SUMS.txt`, and the module list.
- Note: The BP1A base-image line is numbered independently from v1.0, and its patch set is aligned with user-v1.4 of the AP3A line.
- Changed: Face unlock was re-adapted to the official BP1A `services.jar`.
- Changed: Hide-navigation-bar uses a new approach: the launcher's stashed height is 1dp, and when the bottom bar is the Taskbar the navigation mode is no longer toggled. This fixes apps being unresponsive and the back swipe being dead after a half-completed, reversed swipe-up to recents.
