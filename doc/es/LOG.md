---
name: project-log-es
description: Errores, limitaciones, decisiones y traspaso del proyecto
metadata:
  version: "1.0.0"
  lang: "es"
---

# Registro

## Multilingüe

[简体中文](../LOG.md) | [English](../en/LOG.md) | **Español**

## Documentación

- Descripción general del proyecto: [README](README.md)

- Justificación del diseño: [DESIGN](DESIGN.md)

- Estado del proyecto: [LOG](LOG.md)
- Registros históricos: [HISTORY](HISTORY.md)
- Historial de cambios: [CHANGELOG](CHANGELOG.md)

- Avisos de terceros: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## Registros

- [Registros históricos](HISTORY.md)
- [Historial de cambios](CHANGELOG.md)

## Errores

No hay errores confirmados.

## Limitaciones

- La imagen del sistema incluye una semilla de keybox de respaldo; caduca o queda invalidada si se revoca, y a partir de ese momento la autenticación de claves requiere que el usuario importe un keybox válido. La validez de la semilla de esta versión no se ha revisado.
- El flasheo conservando datos solo se aplica si el dispositivo ya tenía el sistema BP1A de este proyecto.
- LE Audio está desactivado; los auriculares de modo dual usan Bluetooth clásico.
- El desbloqueo facial es biometría WEAK: sirve para desbloquear y para verificaciones débiles, pero no autoriza pagos ni abre credenciales de StrongBox.
- La reducción eliminó las aplicaciones de Google preinstaladas y las de accesibilidad (TalkBack, etc.); instale de nuevo desde Play las que necesite.
- La corrección de llamadas Bluetooth está hecha para el vendor ZUI 17.0.12.044 incluido en este paquete; si el vendor del dispositivo se cambia por otra versión, la corrección puede no aplicarse (no verificado).
- Al ocultar la barra de navegación quedan unos 3 píxeles de espacio en la parte inferior. El launcher oficial de BP1A también usa la altura recogida de la barra de tareas como zona de finalización del gesto de apps recientes, y ponerla a 0 deja las aplicaciones sin respuesta tras un gesto de deslizar hacia arriba que se revierte a medias; por eso se usa 1dp.

## Decisiones

| Fecha | Decisión | Estado | Motivo |
| --- | --- | --- | --- |
| 2026-11-05 | Un repositorio por versión base | Aceptada | PixelOS 15 tangorpro tiene varias versiones base |
| 2026-11-05 | Los Release solo incluyen el paquete 9008 completo, no variantes con root ni parches incrementales | Aceptada | Indicación del usuario |
| 2026-11-05 | Volúmenes 7z de 2000 MiB cada uno | Aceptada | Por debajo del límite de 2 GiB por archivo de GitHub |
| 2026-11-05 | La numeración de versiones es por línea de versión base; la primera versión de este repositorio es user-v1.0 | Aceptada | Evita coincidir con el 1.4 de la línea AP3A |
| 2026-11-05 | Licencias de terceros sin verificar al hacer público el repositorio | Aceptada | Sigue lo hecho en el repositorio de AP3A; la verificación queda como paso pendiente |

## Traspaso

Consulte el traspaso vigente en el [LOG.md en chino simplificado](../LOG.md#交接).
