---
name: project-changelog-es
description: Historial de cambios
metadata:
  version: "1.0.0"
  lang: "es"
---

# Historial de cambios

## Multilingüe

[简体中文](../CHANGELOG.md) | [English](../en/CHANGELOG.md) | **Español**

## Documentación

- Descripción general del proyecto: [README](README.md)

- Justificación del diseño: [DESIGN](DESIGN.md)

- Estado del proyecto: [LOG](LOG.md)
- Registros históricos: [HISTORY](HISTORY.md)
- Historial de cambios: [CHANGELOG](CHANGELOG.md)

- Avisos de terceros: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## Historial de cambios

### user-v1.0(V3)- 2026-11-05

- Añadido: primera Release de este repositorio, con las partes completas del paquete de flasheo 9008, `SHA256SUMS.txt` y la lista de módulos.
- Nota: la línea de versión base BP1A se numera de forma independiente desde v1.0, y su conjunto de parches está alineado con user-v1.4 de la línea AP3A.
- Cambiado: el desbloqueo facial se ha readaptado al `services.jar` oficial de BP1A.
- Cambiado: ocultar la barra de navegación usa un nuevo enfoque: la altura recogida del launcher es 1dp y, cuando la barra inferior es la Taskbar, ya no se alterna el modo de navegación. Corrige que las aplicaciones no respondan y que el gesto de atrás no funcione tras un deslizamiento hacia arriba a apps recientes revertido a medias.
