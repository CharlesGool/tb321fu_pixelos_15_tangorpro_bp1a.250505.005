---
name: project-design-en
description: Project architecture and design constraints
metadata:
  version: "1.0.0"
  lang: "en"
---

# tb321fu_pixelos_15_tangorpro_bp1a.250505.005 — Design

## Multi-language

[简体中文](../DESIGN.md) | **English** | [Español](../es/DESIGN.md)

## Documentation

- Project overview: [README](README.md)

- Design rationale: [DESIGN](DESIGN.md)

- Project status: [LOG](LOG.md)
- Historical records: [HISTORY](HISTORY.md)
- Version changelog: [CHANGELOG](CHANGELOG.md)

- Third-party notices: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## Design Goals

- [x] Provide a complete 9008 flashing package that installs the Pixel Tablet A15 GSI `BP1A.250505.005` on the Lenovo Legion Y700 Gen 3 (TB321FU).
- [x] Split the flashing package into 7z volumes that do not exceed GitHub's per-asset size limit.
- [x] Each release includes a module list that states which patch modules that version includes.

## Architecture

This repository only distributes finished products and does not contain the build system. Patches and the build system are in [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods):

```text
GSI 底包 ──依次 apply 选中的 system 补丁──→ system 镜像 + vbmeta_system ─┐
原厂 boot ─apply 固件补丁────────────────→ boot 集                    ─┼─→ 完整 9008 包 ──7z 分卷──→ GitHub Release
原厂 9008 包 ────────────────────────────────────────────────────────┘
```

| Location | Responsibility |
| --- | --- |
| `doc/` | Project documentation, plus the module list `modules-<版本>.md` for each release |
| GitHub Releases | Flashing package volumes, `SHA256SUMS.txt`, and the module list |

## Design Constraints

- Releases contain only the complete 9008 flashing package, not root variants or incremental patches.
- Each 7z volume is 2000 MiB. The two volumes concatenated in order are byte-for-byte identical to the original `.7z`.
- One repository per base-image version: PixelOS 15 tangorpro has several base-image versions, and this repository only covers `BP1A.250505.005`.
