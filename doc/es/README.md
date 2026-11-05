# tb321fu_pixelos_15_tangorpro_bp1a.250505.005

[简体中文](../../README.md) | [English](../en/README.md) | **Español**

Paquete de flasheo 9008 para la Lenovo Legion Y700 de tercera generación (TB321FU) con el GSI de Android 15 de Pixel Tablet (`BP1A.250505.005`).

[![Release](https://img.shields.io/github/v/release/CharlesGool/tb321fu_pixelos_15_tangorpro_bp1a.250505.005?logo=github)](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_bp1a.250505.005/releases/latest)

## Documentación

- Descripción general del proyecto: [README](README.md)

- Justificación del diseño: [DESIGN](DESIGN.md)

- Estado del proyecto: [LOG](LOG.md)
- Registros históricos: [HISTORY](HISTORY.md)
- Historial de cambios: [CHANGELOG](CHANGELOG.md)

- Avisos de terceros: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## Introducción

Paquete 9008 del GSI de Android 15 de Pixel Tablet (`BP1A.250505.005`) para la Lenovo Legion Y700 de tercera generación (TB321FU). Versión oficial actual: user-v1.0 (versión interna V3). Los problemas conocidos están en [LOG](LOG.md#limitaciones).

### Lo principal, antes de empezar

1. Este paquete 9008 se puede flashear sin desbloquear el BL. Está firmado y no requiere desactivar la verificación de vbmeta. Incluye el firmware 9008 completo de la ZUI 17.0.12.044 original de Lenovo, por lo que no hace falta flashear antes un firmware oficial.
2. Todas las funciones siguientes están implementadas sin root.
3. Salvo el offload de hardware de Bluetooth (A2DP offload), los errores de hardware encontrados en este equipo están corregidos. La función Bluetooth funciona con normalidad, aunque la corrección no es perfecta.
4. Este paquete se puede compilar automáticamente. Con un PC Linux, puede cambiar el GSI y la versión de la base y compilarlo usted mismo (la base y el firmware original deben aportarse); véase [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods).

Cada módulo está descrito en [modules-user-v1.0](../modules-user-v1.0.md). Esta versión tiene 32 módulos, con un conjunto de parches alineado con user-v1.4 de la línea AP3A.241005.015: todos los obligatorios más 6 opcionales.

### Identidad y autenticación

- Restaura la identidad real del TB321FU (`ro.product.*`, huella digital y descriptores de build, tomados del firmware original).
- Motor de autenticación de claves sin root: permite importar keybox y emitir claves RKP localmente (inspirado en las funciones del módulo Oh My Keymint).
- Suplantación global de modelo (módulo opcional `global-pif`): con un clic se hace pasar por un modelo como Pixel Tablet, y así se puede superar la verificación de integridad de Play. Es la opción de menor impacto que he encontrado para superar la autenticación de Play sin root, pero al activarla se detecta un montaje anómalo del sistema. Si no la quiere, no la active.
- `herald-core`: punto de entrada de comandos y complementos sin root (`heraldctl`); las aplicaciones de frontend lo usan para controlar funciones del sistema.

### Cámara

- Incluye la cámara de Pixel (Cámara de Google 4.4).
- Corrección de la cámara macro: la cámara macro n.º 2 está disponible para cámaras de terceros.

### Desbloqueo facial

- Nuevo desbloqueo facial, portado de ParanoidSense de PixelOS (SDK de Megvii), con la cámara frontal; sirve para el bloqueo de pantalla y para aplicaciones en escenarios que no son de pago. Es biometría WEAK (Class 2) y no autoriza pagos ni abre credenciales de StrongBox. Los hooks del framework se han readaptado al `services.jar` oficial de BP1A.

### Pantalla y visualización

- Corrección del brillo automático: restaura el interruptor de brillo adaptativo en Ajustes, usa la curva y la velocidad de respuesta del brillo original de Lenovo, y el nivel mínimo manual vuelve al original.
- Corrección de la orientación: el sistema de Pixel Tablet y este equipo tienen orientaciones por defecto distintas; las aplicaciones que solo funcionan en horizontal (como la pantalla completa de B 站) ya no aparecen invertidas.
- Corrección de la tasa de refresco adaptativa: restaura los temporizadores de inactividad y de tacto originales y la detección de contenido; baja con la pantalla estática, sube al tocar, y en vídeo sigue la tasa de fotogramas.
- Niveles de fluidez de pantalla: en Ajustes, con "Fluidez de pantalla" activada no hay límite (el panel llega a 165Hz); desactivada, 120Hz (el sistema Pixel original alterna entre 60 y 165Hz; pasar a 120/165Hz resulta más útil).
- Rotación libre: 90, 180 y 270 grados rotan automáticamente, incluida la vertical invertida.

### Red y Bluetooth

- Banda Wi-Fi de 6GHz y corrección del código de país; Wi-Fi APEX reempaquetado.
- Corrección de la interfaz del punto de acceso: Pixel Tablet oculta por defecto la entrada del punto de acceso WLAN; se ha restaurado la entrada en Ajustes y el mosaico de ajustes rápidos.
- Corrección del audio Bluetooth: se desactivan el offload A2DP por hardware y LE Audio, y se usa la codificación por software del vendor; se corrigen los auriculares sin sonido y las llamadas que no se oyen.

### Compatibilidad de aplicaciones

- Portado de Tango, con soporte para APK de 32 bits; se pueden usar aplicaciones de 32 bits, tomando como referencia el OnePlus 12 con Android 15 ColorOS.

### Reducción del sistema

- Elimina las aplicaciones y datos exclusivos de Pixel, reduce el VNDK antiguo y elimina los componentes de hardware de Pixel que este equipo no tiene.
- Reducción de aplicaciones de Google: elimina las aplicaciones de Google preinstaladas (Calculadora, Calendario, Contactos, Teléfono, Mensajes, Fotos, Gmail, Maps, YouTube, Reloj, Tiempo, Grabadora, etc.), el Asistente de Google y los datos de voz de GoogleTTS, y las aplicaciones de accesibilidad (TalkBack, etc.); instale de nuevo desde Play las que necesite.
- Limpia los restos de GSI (phh/Mystic).

### Limpieza y cierre

- Desactiva la depuración (adb root y la depuración vienen activados por defecto en la versión original).
- Oculta las huellas de GSI, para evitar la detección de GSI.
- Mediante descompilación, elimina la ventana emergente "Se ha producido un problema interno en el dispositivo" al arrancar.
- Unifica la cadena de autoría del kernel, limpia los precompilados caducados, reempaqueta boot y lo refirma para la AVB de este equipo.

### Interfaz

- Permite ocultar la barra de navegación (en modo tablet y en modo teléfono). Al ocultarla quedan unos 3 píxeles de espacio en la parte inferior: el launcher oficial de BP1A también usa la altura recogida de la barra de tareas como zona de finalización del gesto de apps recientes, y ponerla a 0 deja las aplicaciones sin respuesta tras un gesto de deslizar hacia arriba que se revierte a medias; por eso se usa 1dp.

### Correcciones de estabilidad

- Corrección de reglas de SELinux: arranca en modo Enforcing (la versión original daba error cuando faltaban reglas).
- Corrección del dominio del servicio de conexión de dispositivos (DeviceConnectionService), que ya no falla cada 10 segundos.

Los parches y el sistema de compilación están en [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods). PixelOS 15 tangorpro tiene varias versiones de base; cada una tiene su propio repositorio, y este solo corresponde a `BP1A.250505.005`; para `AP3A.241005.015` véase [tb321fu_pixelos_15_tangorpro_ap3a.241005.015](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_ap3a.241005.015).

## Requisitos

- Lenovo Legion Y700 de tercera generación TB321FU, capaz de entrar en el modo 9008 (EDL).
- PC con Windows, cable USB y 7-Zip.
- El flasheo conservando datos solo se aplica si el dispositivo ya tenía este sistema del proyecto; en los demás casos, use el flasheo con borrado de datos.

## Instalación

### Instalación rápida

Descargue todos los volúmenes (`.7z.001`, `.7z.002`) desde [Releases](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_bp1a.250505.005/releases/latest) y colóquelos en el mismo directorio. Descomprima `.7z.001` con 7-Zip. Con el dispositivo en modo 9008, ejecute `flash.bat` en el directorio descomprimido (borra los datos). El paquete incluye el firmware 9008 completo de Lenovo; no hace falta flashear antes un firmware oficial.

### Instalación normal

```bash
sha256sum -c SHA256SUMS.txt
7z x pixelos_tangorpro_bp1a.250505.005_user-v1.0_optional.7z.001
```

Para flashear conservando datos, ejecute `flash_keep_data.bat`. Ambos scripts están en la raíz del directorio descomprimido.

## Guía

| Archivo | Contenido |
| --- | --- |
| `…user-v1.0_optional.7z.001`, `.002` | Volúmenes 7z del paquete completo de flasheo 9008, de 2000 MiB cada uno |
| `SHA256SUMS.txt` | Sumas de verificación de los volúmenes; el sha256 del paquete completo tras concatenar los volúmenes figura en las notas del Release correspondiente |
| `module-list.md` | Lista de módulos de esta versión, igual que [modules-user-v1.0](../modules-user-v1.0.md) |

### Uso del desbloqueo facial

Ajustes → Seguridad y privacidad → Desbloqueo del dispositivo → Desbloqueo facial → introduzca el PIN → complete el registro; después, basta con mirar a la cámara frontal en la pantalla de bloqueo. Para eliminarlo: en Ajustes, modelo facial → Eliminar. Es biometría WEAK, **prohibido** usarla para proteger aplicaciones de pagos o bancarias. La ruta del menú se mantiene como en versiones anteriores y no se ha revisado paso a paso en user-v1.0.

### Identificación de versión

La versión pública es `user-vMAJOR.MINOR`; el número interno `V<数字>` está escrito en la imagen. user-v1.0 = V3. Cada línea de versión base se numera desde su propio v1.0; la primera versión de este repositorio es user-v1.0.

## Actualización

Esta es la primera versión de este repositorio, por lo que no hay una versión anterior desde la que actualizar. Si viene del sistema original, de la línea AP3A.241005.015 o de cualquier otra versión, ejecute `flash.bat` (borra los datos) con el paquete completo. El flasheo conservando datos (`flash_keep_data.bat`) solo se aplica si el dispositivo ya tenía el sistema BP1A de este proyecto. Verificación: tras arrancar, el número de versión en Ajustes debe contener `user-v1.0`.

## Desinstalación

No hay un método separado para la desinstalación rápida. Desinstalación completa: vuelva a flashear el paquete 9008 del ZUI 17.0.12 original de Lenovo; los datos se borrarán.

## Agradecimientos

- La imagen oficial de Google para Pixel Tablet `BP1A.250505.005`, convertida a GSI con la herramienta MysticGSI, como base del sistema.
- El desbloqueo facial está portado de ParanoidSense de PixelOS (SDK de Megvii).
- El motor de certificación es una bifurcación de [ITxiao6666/OhMyKeymint](https://github.com/ITxiao6666/OhMyKeymint) (autor original: James Clef / qwq233).
- El firmware original de ZUI y las herramientas de flasheo de Lenovo.

Los datos de autoría y de cumplimiento están en [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md).

## Licencia

Este repositorio todavía no ha elegido una licencia y no concede ninguna. El estado de licencia de cada componente de terceros está en [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md).
