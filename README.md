# tb321fu_pixelos_15_tangorpro_bp1a.250505.005

**简体中文** | [English](doc/en/README.md) | [Español](doc/es/README.md)

联想拯救者 Y700 三代(TB321FU)刷 Pixel Tablet Android 15 GSI(`BP1A.250505.005`)的 9008 刷机包.

[![Release](https://img.shields.io/github/v/release/CharlesGool/tb321fu_pixelos_15_tangorpro_bp1a.250505.005?logo=github)](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_bp1a.250505.005/releases/latest)

## 文档

- 项目概览: [README](README.md)

- 设计思路: [DESIGN](doc/DESIGN.md)

- 项目状态: [LOG](doc/LOG.md)
- 历史记录: [HISTORY](doc/HISTORY.md)
- 变更日志: [CHANGELOG](doc/CHANGELOG.md)

- 第三方声明: [THIRD_PARTY_NOTICES](doc/THIRD_PARTY_NOTICES.md)

## 简介

联想拯救者 Y700 三代(TB321FU)的 Pixel Tablet Android 15 GSI(`BP1A.250505.005`)9008 刷机包. 当前正式版 user-v1.0(内部版本 V3). 已知问题见 [LOG](doc/LOG.md#限制).

### 重点, 写在前面

1. 本刷机包是 9008 刷机包, 可在不解锁 BL 的情况下刷入. 已签名, 不需要关 vbmeta 验证. 包里带完整的联想原厂 ZUI 17.0.12.044 9008 固件, 不需要事先刷官方底包.
2. 下列所有功能都是 rootless 实现.
3. 除蓝牙硬件卸载(A2DP offload)外, 本机上遇到的硬件 Bug 都已修复. 蓝牙功能可以正常使用, 只是修得不够完美.
4. 本刷机包可自动化构建. 有 Linux PC 的话, 可以自己更换 GSI 和底包版本并构建(底包和原厂固件需自备), 见 [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods).

每个模块的作用见 [modules-user-v1.0](doc/modules-user-v1.0.md). 本版共 32 个模块, 补丁集与 AP3A.241005.015 线的 user-v1.4 对齐: 全部必选模块加 6 个可选模块.

### 身份和认证

- 还原真实 TB321FU 身份(`ro.product.*`, 指纹, build 描述符取自原厂固件).
- rootless 密钥认证引擎: 可导入 keybox, 可本地下发 RKP 密钥(参考 Oh My Keymint 模块的功能).
- 全局机型伪装(可选模块 `global-pif`): 一键伪装成 Pixel Tablet 等机型, 伪装成 Pixel 机型后可通过 Play 完整性检查. 这是目前找到的 rootless 方案里影响最小的通过 Play 认证的办法, 但开启后会被检测到系统异常挂载. 不想要就不开启.
- `herald-core`: 免 root 的命令和插件入口(`heraldctl`), 前端 App 通过它控制系统功能.

### 相机

- 内置 Pixel 相机(Google 相机 4.4).
- 微距相机修复, 2 号微距相机对第三方相机可用.

### 人脸解锁

- 新增人脸解锁, 移植自 PixelOS 的 ParanoidSense(旷视 Megvii SDK), 走前置摄像头, 可用于锁屏解锁和 App 等非支付场景. 它是 WEAK(Class 2)生物识别, 不能授权支付或打开 StrongBox 凭据. 框架钩子已按官方 BP1A 的 `services.jar` 重新适配.

### 屏幕和显示

- 自动亮度修复: 补回设置里的自适应亮度开关, 换上联想原厂的亮度曲线和反应速度, 手动最低档还原原厂.
- 屏幕方向修复: Pixel Tablet 系统和本机默认方向不同, 只能横屏的应用(如 B 站全屏)不再倒过来.
- 自适应刷新率修复: 补回原厂的空闲/触摸定时器和内容检测, 静止降档, 触摸升档, 视频按帧率.
- 流畅显示档位: 设置里"流畅显示"开 = 不设上限(面板最高 165Hz), 关 = 120Hz(Pixel 原系统是 60/165Hz 切换, 改成 120/165Hz 更实用).
- 自由旋转: 90/180/270 度都能自动旋转, 包括竖屏倒过来.

### 网络和蓝牙

- 6GHz Wi-Fi 频段和国家码修复, Wi-Fi APEX 重新打包.
- 热点界面修复: Pixel Tablet 默认隐藏 WLAN 热点入口, 已补回设置入口和快捷设置磁贴.
- 蓝牙音频修复: 关 A2DP 硬件 offload 和 LE Audio, 改走 vendor 软件编码, 修耳机没声音和通话听不到.

### 应用兼容

- 移植 Tango, 支持 32 位 APK, 可以玩 32 位应用(参考一加 12 Android 15 ColorOS).

### 系统精简

- 删 Pixel 专属应用和数据, 精简旧版 VNDK, 精简本机没有的 Pixel 硬件组件.
- Google 应用精简: 删 Google 预装应用(计算器, 日历, 通讯录, 拨号, 短信, 相册, Gmail, 地图, YouTube, 时钟, 天气, 录音机等), Google 助理和 GoogleTTS 语音数据, 并删除无障碍应用(TalkBack 等), 需要的自己从 Play 装回来.
- 清理 GSI(phh/Mystic)残留痕迹.

### 去痕迹和收尾

- 关闭调试(原版 adb root/调试默认开着).
- 隐藏 GSI 身份痕迹(防 GSI 检测).
- 反编译去掉开机"设备内部出现了问题"弹窗.
- 统一内核编译者字符串, 清理过期预编译, boot 重新打包并针对本机 AVB 重签.

### 界面

- 可隐藏导航栏(平板/手机模式均支持). 隐藏后底部会留约 3 像素占位: 官方 BP1A 启动器把任务栏的收起高度也用作多任务手势的收尾判定区, 清成 0 会让"上滑多任务中途掉头"后 App 点不动, 所以取 1dp.

### 稳定性修复

- SELinux 规则修复: 开机即 Enforcing(原版缺规则会报错).
- 设备连接服务(DeviceConnectionService)域修复, 不再每 10 秒崩一次.

补丁和构建系统在 [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods). PixelOS 15 tangorpro 有多个底包版本, 每个底包版本一个仓库, 本仓库只对应 `BP1A.250505.005`; `AP3A.241005.015` 的见 [tb321fu_pixelos_15_tangorpro_ap3a.241005.015](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_ap3a.241005.015).

## 要求

- 联想拯救者 Y700 三代 TB321FU, 能进 9008(EDL)模式.
- Windows 电脑, USB 数据线, 7-Zip.
- 保数据刷只适用于手机上原来就是本项目的系统; 其他情况用清数据刷.

## 安装

### 快速安装

从 [Releases](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_bp1a.250505.005/releases/latest) 下载全部分卷(`.7z.001`, `.7z.002`)放在同一目录, 用 7-Zip 解压 `.7z.001`, 设备进 9008 后在解压目录运行 `flash.bat`(清数据). 刷机包带完整的联想原厂 9008 固件, 不需要事先刷官方底包.

### 常规安装

```bash
sha256sum -c SHA256SUMS.txt
7z x pixelos_tangorpro_bp1a.250505.005_user-v1.0_optional.7z.001
```

保数据刷运行 `flash_keep_data.bat`. 两个脚本都在解压目录根部.

## 指南

| 文件 | 内容 |
| --- | --- |
| `…user-v1.0_optional.7z.001`, `.002` | 完整 9008 刷机包的 7z 分卷, 每卷 2000 MiB |
| `SHA256SUMS.txt` | 分卷的校验值; 拼接后整包的 sha256 写在对应 Release 的说明里 |
| `module-list.md` | 本版模块列表, 同 [modules-user-v1.0](doc/modules-user-v1.0.md) |

### 使用人脸解锁

设置 → 安全与隐私 → 设备解锁 → 人脸解锁 → 输入 PIN → 走完录入, 之后锁屏对准前置摄像头即可. 删除: 设置里的人脸模型 → 删除. 它是 WEAK 生物识别, **禁止**用来保护支付, 银行这类应用. 菜单路径沿用旧版本的写法, 未在 user-v1.0 上逐步复核.

### 版本标识

对外版本 `user-vMAJOR.MINOR`, 内部版本号 `V<数字>` 写在镜像里, user-v1.0 = V3. 每条底包线从自己的 v1.0 起编号, 本仓库的首个正式版就是 user-v1.0.

## 升级

本版是本仓库的第一个正式版, 没有旧版本可以升级. 从原厂系统, AP3A.241005.015 线或其他版本换过来, 请用完整包运行 `flash.bat`(清数据). 保数据刷(`flash_keep_data.bat`)只适用于手机上原来就是本项目 BP1A 系统的情况. 验证: 开机后设置里的版本号应含 `user-v1.0`.

## 卸载

快速卸载没有单独的办法. 完全卸载: 用联想原厂 ZUI 17.0.12 的 9008 包整套重刷, 数据会被清除.

## 致谢

- Google 的 Pixel Tablet 官方 `BP1A.250505.005` 镜像, 经 MysticGSI 工具转成 GSI 作为底包.
- 人脸解锁移植自 PixelOS 的 ParanoidSense(旷视 Megvii SDK).
- 认证引擎 fork 自 [ITxiao6666/OhMyKeymint](https://github.com/ITxiao6666/OhMyKeymint)(原作者 James Clef / qwq233).
- 联想 ZUI 原厂固件和刷机工具.

署名和合规信息见 [THIRD_PARTY_NOTICES](doc/THIRD_PARTY_NOTICES.md).

## 许可证

本仓库尚未选定许可证, 未授予任何许可. 第三方组件各自的许可证状态见 [THIRD_PARTY_NOTICES](doc/THIRD_PARTY_NOTICES.md).
