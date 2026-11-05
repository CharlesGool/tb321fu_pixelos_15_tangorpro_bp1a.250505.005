---
name: project-design
description: 项目架构与设计约束
metadata:
  version: "1.0.0"
  lang: "zh-CN"
---

# tb321fu_pixelos_15_tangorpro_bp1a.250505.005 — 设计

## 多语言

**简体中文** | [English](en/DESIGN.md) | [Español](es/DESIGN.md)

## 文档

- 项目概览: [README](../README.md)

- 设计思路: [DESIGN](DESIGN.md)

- 项目状态: [LOG](LOG.md)
- 历史记录: [HISTORY](HISTORY.md)
- 变更日志: [CHANGELOG](CHANGELOG.md)

- 第三方声明: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## 设计目标

- [x] 提供联想拯救者 Y700 三代(TB321FU)刷 Pixel Tablet A15 GSI `BP1A.250505.005` 的完整 9008 刷机包.
- [x] 刷机包拆成不超过 GitHub 单个资产上限的 7z 分卷.
- [x] 每个 Release 附模块列表, 写明该版本打了哪些补丁模块.

## 架构

本仓库只负责分发成品, 不含构建系统. 补丁和构建系统在 [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods):

```text
GSI 底包 ──依次 apply 选中的 system 补丁──→ system 镜像 + vbmeta_system ─┐
原厂 boot ─apply 固件补丁────────────────→ boot 集                    ─┼─→ 完整 9008 包 ──7z 分卷──→ GitHub Release
原厂 9008 包 ────────────────────────────────────────────────────────┘
```

| 位置 | 职责 |
| --- | --- |
| `doc/` | 项目文档, 以及每个正式版的模块列表 `modules-<版本>.md` |
| GitHub Releases | 刷机包分卷, `SHA256SUMS.txt` 和模块列表 |

## 设计约束

- Release 只放完整 9008 刷机包, 不放 root 变体和增量补丁.
- 7z 分卷每卷 2000 MiB, 两卷按顺序拼接后与原 `.7z` 逐字节一致.
- 一个底包版本一个仓库: PixelOS 15 tangorpro 有多个底包版本, 本仓库只对应 `BP1A.250505.005`.
