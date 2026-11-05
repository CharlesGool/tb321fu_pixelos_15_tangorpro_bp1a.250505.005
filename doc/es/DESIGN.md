---
name: project-design-es
description: Arquitectura y restricciones de diseño del proyecto
metadata:
  version: "1.0.0"
  lang: "es"
---

# tb321fu_pixelos_15_tangorpro_bp1a.250505.005 — Diseño

## Multilingüe

[简体中文](../DESIGN.md) | [English](../en/DESIGN.md) | **Español**

## Documentación

- Descripción general del proyecto: [README](README.md)

- Justificación del diseño: [DESIGN](DESIGN.md)

- Estado del proyecto: [LOG](LOG.md)
- Registros históricos: [HISTORY](HISTORY.md)
- Historial de cambios: [CHANGELOG](CHANGELOG.md)

- Avisos de terceros: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## Objetivos de diseño

- [x] Proporcionar el paquete de flasheo 9008 completo de la Lenovo Legion Y700 de tercera generación (TB321FU) con el GSI A15 de Pixel Tablet `BP1A.250505.005`.
- [x] Dividir el paquete de flasheo en volúmenes 7z que no superen el límite por archivo de GitHub.
- [x] Cada Release incluye la lista de módulos, que indica qué módulos de parches tiene esa versión.

## Arquitectura

Este repositorio solo distribuye los productos terminados y no contiene el sistema de compilación. Los parches y el sistema de compilación están en [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods):

```text
Base GSI ──aplicar parches system seleccionados──→ imagen system + vbmeta_system ─┐
boot original ─aplicar parches de firmware────────→ conjunto boot                ─┼─→ paquete 9008 completo ──volúmenes 7z──→ GitHub Release
paquete 9008 original ────────────────────────────────────────────────────────────┘
```

| Ubicación | Responsabilidad |
| --- | --- |
| `doc/` | Documentación del proyecto y la lista de módulos de cada versión oficial, `modules-<versión>.md` |
| GitHub Releases | Volúmenes del paquete de flasheo, `SHA256SUMS.txt` y la lista de módulos |

## Restricciones de diseño

- Los Release solo incluyen el paquete 9008 completo, no variantes con root ni parches incrementales.
- Cada volumen 7z mide 2000 MiB; la concatenación en orden de los dos volúmenes es idéntica byte a byte al `.7z` original.
- Un repositorio por versión base: PixelOS 15 tangorpro tiene varias versiones base; este repositorio corresponde solo a `BP1A.250505.005`.
