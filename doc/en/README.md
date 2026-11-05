# tb321fu_pixelos_15_tangorpro_bp1a.250505.005

[简体中文](../../README.md) | **English** | [Español](../es/README.md)

9008 flashing package for the Pixel Tablet Android 15 GSI (`BP1A.250505.005`) on the Lenovo Legion Y700 Gen 3 (TB321FU).

[![Release](https://img.shields.io/github/v/release/CharlesGool/tb321fu_pixelos_15_tangorpro_bp1a.250505.005?logo=github)](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_bp1a.250505.005/releases/latest)

## Documentation

- Project overview: [README](README.md)

- Design rationale: [DESIGN](DESIGN.md)

- Project status: [LOG](LOG.md)
- Historical records: [HISTORY](HISTORY.md)
- Version changelog: [CHANGELOG](CHANGELOG.md)

- Third-party notices: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## Introduction

The Pixel Tablet Android 15 GSI (`BP1A.250505.005`) 9008 flashing package for the Lenovo Legion Y700 Gen 3 (TB321FU). The current release is user-v1.0 (internal build V3). Known issues are in [LOG](LOG.md#limitations).

### Key Points Up Front

1. This is a 9008 flashing package that can be flashed without unlocking the bootloader (BL). It is signed, and disabling vbmeta verification is not required. The package includes the complete Lenovo stock ZUI 17.0.12.044 9008 firmware, so you do not need to flash an official base image beforehand.
2. All features below are implemented rootless.
3. Apart from Bluetooth hardware offload (A2DP offload), all hardware bugs encountered on this device have been fixed. Bluetooth works normally, though the fix is not perfect.
4. This package can be built automatically. With a Linux PC, you can replace the GSI and base-image versions and build it yourself (the base image and stock firmware must be supplied by you); see [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods).

The function of each module is described in [modules-user-v1.0](../modules-user-v1.0.md). This release includes 32 modules, with a patch set aligned with user-v1.4 of the AP3A.241005.015 line: all required modules plus 6 optional modules.

### Identity and Attestation

- Restores the real TB321FU identity (`ro.product.*`, fingerprint, and build descriptors taken from the stock firmware).
- Rootless key attestation engine: keybox import is supported, and RKP keys can be issued locally (refer to the functionality of the Oh My Keymint module).
- Global device spoofing (optional module `global-pif`): one-tap spoofing as a Pixel Tablet and other models. Spoofing as a Pixel model passes Play Integrity checks. It is currently the rootless approach with the least impact for passing Play attestation that has been found, but enabling it will be detected as an abnormal system mount. Leave it off if you do not want this.
- `herald-core`: root-free command and plugin entry point (`heraldctl`); the front-end app uses it to control system features.

### Camera

- Built-in Pixel Camera (Google Camera 4.4).
- Macro camera fix: the macro camera (camera 2) is available to third-party camera apps.

### Face Unlock

- New face unlock, ported from PixelOS's ParanoidSense (Megvii SDK). It uses the front camera and can be used for lock screen unlock and for apps and other non-payment scenarios. It is a WEAK (Class 2) biometric and cannot authorize payments or open StrongBox credentials. The framework hooks were re-adapted to the official BP1A `services.jar`.

### Display

- Auto brightness fix: restores the adaptive brightness toggle in Settings and uses Lenovo's stock brightness curve and response speed. The lowest manual level is restored to stock.
- Screen orientation fix: the Pixel Tablet system and this device have different default orientations, so apps that only support landscape (such as Bilibili fullscreen) no longer rotate upside down.
- Adaptive refresh rate fix: restores stock idle and touch timers and content detection. It downshifts when the screen is static, upshifts on touch, and follows the frame rate for video.
- Smooth display mode: in Settings, "Smooth display" on = no cap (panel up to 165Hz), off = 120Hz. The original Pixel system switches between 60Hz and 165Hz; 120Hz and 165Hz is more practical.
- Free rotation: auto-rotates at 90, 180 and 270 degrees, including portrait upside down.

### Network and Bluetooth

- 6GHz Wi-Fi band and country code fix; Wi-Fi APEX repackaged.
- Hotspot UI fix: the Pixel Tablet hides the WLAN hotspot entry by default. The Settings entry and Quick Settings tile are restored.
- Bluetooth audio fix: disables A2DP hardware offload and LE Audio, and uses vendor software encoding instead. Fixes headphones with no sound and callers not being heard.

### App Compatibility

- Ported Tango, which supports 32-bit APKs so that 32-bit apps can run (refer to OnePlus 12 Android 15 ColorOS).

### System Trimming

- Removes Pixel-exclusive apps and data, trims old VNDK, and removes Pixel hardware components this device does not have.
- Google app trimming: removes the preinstalled Google apps (Calculator, Calendar, Contacts, Dialer, Messages, Photos, Gmail, Maps, YouTube, Clock, Weather, Recorder, etc.), Google Assistant and the GoogleTTS voice data, and the accessibility apps (TalkBack, etc.). Reinstall what you need from Play.
- Cleans up GSI (phh/Mystic) leftovers.

### Trace Removal and Cleanup

- Disables debugging (stock adb root and debugging are on by default).
- Hides GSI identity traces (against GSI detection).
- Decompiled and removed the "Internal problem with the device" popup at boot.
- Unified the kernel build-user string, cleaned up expired prebuilts, and repackaged boot, re-signing it for this device's AVB.

### Interface

- The navigation bar can be hidden (supported in both tablet and phone modes). About 3 pixels of space remain at the bottom after hiding: the official BP1A launcher also uses the taskbar's stashed height as the end-of-gesture region for the recents swipe, and setting it to 0 leaves apps unresponsive after a swipe-up that is reversed halfway, so it is set to 1dp.

### Stability Fixes

- SELinux rule fix: Enforcing on boot (stock was missing rules and reported errors).
- DeviceConnectionService domain fix: no longer crashes every 10 seconds.

Patches and the build system are in [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods). PixelOS 15 tangorpro has several base-image versions, each with its own repository; this repository only covers `BP1A.250505.005`; for `AP3A.241005.015` see [tb321fu_pixelos_15_tangorpro_ap3a.241005.015](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_ap3a.241005.015).

## Requirements

- Lenovo Legion Y700 Gen 3 TB321FU, able to enter 9008 (EDL) mode.
- A Windows PC, a USB data cable, and 7-Zip.
- Keep-data flashing only applies to a device already running this project's system; in all other cases, use the wipe-data flash.

## Install

### Quick Install

Download all volumes (`.7z.001`, `.7z.002`) from [Releases](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_bp1a.250505.005/releases/latest) into the same directory. Extract `.7z.001` with 7-Zip. Once the device is in 9008 mode, run `flash.bat` (wipe data) in the extracted directory. The flashing package includes the complete Lenovo stock 9008 firmware, so there is no need to flash an official base image beforehand.

### Normal Install

```bash
sha256sum -c SHA256SUMS.txt
7z x pixelos_tangorpro_bp1a.250505.005_user-v1.0_optional.7z.001
```

For a keep-data flash, run `flash_keep_data.bat`. Both scripts are in the root of the extracted directory.

## Usage

| File | Contents |
| --- | --- |
| `…user-v1.0_optional.7z.001`, `.002` | The 7z volumes of the complete 9008 flashing package, 2000 MiB each |
| `SHA256SUMS.txt` | Checksums for the volumes; the sha256 of the concatenated complete package is in the notes of the corresponding Release |
| `module-list.md` | Module list for this release, same as [modules-user-v1.0](../modules-user-v1.0.md) |

### Using Face Unlock

Settings → Security & privacy → Device unlock → Face unlock → enter PIN → complete enrollment; afterward, point the front camera at your face on the lock screen to unlock. To delete: in Settings, face model → Delete. It is a WEAK biometric, and **do not** use it to protect payment or banking apps. The menu path follows the wording used in earlier versions and has not been step-by-step verified on user-v1.0.

### Version Naming

The public version is `user-vMAJOR.MINOR`, and the internal build number `V<数字>` is written into the image; user-v1.0 = V3. Each base-image line is numbered from its own v1.0; the first release of this repository is user-v1.0.

## Upgrade

This is the first release of this repository, so there is no earlier version to upgrade from. When coming from the stock system, the AP3A.241005.015 line or any other version, run `flash.bat` (wipe data) from the full package. Keep-data flashing (`flash_keep_data.bat`) only applies to a device already running this project's BP1A system. Verification: after boot, the version number in Settings should contain `user-v1.0`.

## Uninstall

There is no separate quick uninstall. For a full uninstall, re-flash the complete Lenovo stock ZUI 17.0.12 9008 package. All data will be erased.

## Acknowledgements

- Google's official Pixel Tablet `BP1A.250505.005` image, converted to a GSI with the MysticGSI tool, used as the base image.
- Face unlock is ported from PixelOS's ParanoidSense (Megvii SDK).
- The attestation engine is forked from [ITxiao6666/OhMyKeymint](https://github.com/ITxiao6666/OhMyKeymint) (original author James Clef / qwq233).
- Lenovo's stock ZUI firmware and flashing tools.

For attribution and compliance information, see [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md).

## License

No license has been chosen for this repository, and no license is granted. For the license status of each third-party component, see [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md).
