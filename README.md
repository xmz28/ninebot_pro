<div align="center">

# Ninebot Pro

**把手机里的画面，带到九号仪表上。**

[![Android 0.6.2](https://img.shields.io/badge/Android-0.6.2-2E7D32?style=flat-square)](https://github.com/xmz28/ninebot_pro/releases/tag/v0.6.2)
[![iOS 1.0.1](https://img.shields.io/badge/iOS-1.0.1-1565C0?style=flat-square)](https://github.com/xmz28/ninebot_pro/releases/tag/ios-v1.0.1)
[![仪表 Wi-Fi 投屏](https://img.shields.io/badge/连接-仪表_Wi--Fi-546E7A?style=flat-square)](#平台差异)

提供 Android APK 与 iOS IPA，支持图片、视频和摄像头投屏。手机屏幕与 CarPlay 视频流的接入方式因平台而异。

[下载安装](#下载安装) · [界面预览](#界面预览) · [平台差异](#平台差异) · [开始使用](#开始使用) · [常见问题](#常见问题)

</div>

## 下载安装

| 平台与版本 | 系统要求 | 下载入口 | 安装方式 |
| --- | --- | --- | --- |
| **Android 0.6.2** | Android 8.0+ | [下载 APK](https://github.com/xmz28/ninebot_pro/releases/download/v0.6.2/ninebot-pro-release-v0.6.2.apk) · [说明](https://github.com/xmz28/ninebot_pro/releases/tag/v0.6.2) | 同签名版本可覆盖升级 |
| **iOS 1.0.1** | iOS / iPadOS 17.0+，ARM64 | [下载 IPA](https://github.com/xmz28/ninebot_pro/releases/download/ios-v1.0.1/ninebot-pro-ios-v1.0.1-unsigned.ipa) · [说明](https://github.com/xmz28/ninebot_pro/releases/tag/ios-v1.0.1) | 需自行签名安装 |

**iOS IPA 未签名，不能直接安装。** 请使用自己的有效证书和描述文件签名后安装；有效期和续签方式取决于所用签名渠道。这不是 App Store 或 TestFlight 版本。

<details>
<summary>安装包标识与验证范围</summary>

- Android：`com.example.ninebotpro`，`versionCode 10`。曾安装同包名但不同签名的调试版，需要先卸载再安装；卸载会清除该版配置。
- iOS：`com.hanlin.ninebotpro`，构建号 `2`。IPA 约 2.78 MiB，文件大小与 SHA-256 见对应发布说明。
- iOS 包已完成 Release 构建、包体元数据及 ZIP 完整性核验。同源开发签名版本已在 iPhone 17 Pro Max 安装并获用户确认；最终未签名 IPA 未对所有第三方自签工具完成端到端安装验证。
- 自签时建议保留 Bundle ID。如签名工具修改 Bundle ID，App 内更新可能无法匹配元数据，可从本页手动下载新版后重新签名。

</details>

## 界面预览

iOS 1.0.1 模拟器截图。CarPlay 服务地址仅为示例。

| 首页与内容选择 | CarPlay 服务配置 | 关于与更新入口 |
| --- | --- | --- |
| <img src="docs/screenshots/ios-home.png" alt="iOS 首页：连接仪表与选择投屏内容" width="260"> | <img src="docs/screenshots/ios-carplay.png" alt="CarPlay 配置：服务地址与兼容接口说明" width="260"> | <img src="docs/screenshots/ios-about.png" alt="关于页：版本、使用说明与检查更新" width="260"> |

本版 iOS 优化了首页、连接状态、关于页和设置入口，新增更新提醒与下载入口，并改进配置取消和视频进度操作。完整变更见 [iOS 发布说明](https://github.com/xmz28/ninebot_pro/releases/tag/ios-v1.0.1)。

## 平台差异

| 功能 | Android | iOS / iPadOS |
| --- | --- | --- |
| 连接仪表 | App 内扫描 Wi-Fi Direct，可重连上次仪表 | 在系统设置中手动连接仪表 Wi-Fi |
| 相册图片、视频、摄像头 | 支持 | 支持 |
| 手机屏幕投屏 | 支持 | 当前不支持跨 App 屏幕录制 |
| CarPlay 视频流 | 手机屏幕投屏，无 OXP 直连入口 | 直接接入兼容 OXP 接口的视频流 |
| 仪表预设 | 五寸；七寸待实测；4.3 寸为测试功能 | 五寸；4.3 寸为实验功能；不支持七寸 KCP |
| App 更新 | 下载并校验 APK，由系统确认安装 | 打开新版下载页，下载后需重新自行签名 |

两端摄像头均需在前台使用：Android 离开前台后停止摄像头投屏；iOS 进入后台后暂停采集、保留最后画面。图片、视频等来源的后台运行取决于平台设置及系统状态。视频声音在手机播放。

CarPlay 接收应用需要提供兼容接口。当前 iOS 使用 OXP `/oxp/v0` 与 H.264 视频流，仅投画面，不传声音和触控；通用文案不代表所有同类软件均已兼容，CarWithin、CarCast 尚未列为已验证支持。

## 开始使用

### Android

1. 在仪表或官方 App 开启投屏，打开手机 Wi-Fi，并按提示授权。Android 13+ 需要附近 Wi-Fi 权限；Android 12 及以下需要精确定位权限，并在扫描时开启系统定位。
2. 点击“扫描 P2P”，选择仪表并按系统提示确认。连接后核对“投屏配置”；App 会记住仪表配置，并尝试重连上次成功核对的仪表。
3. 选择“相册媒体”“摄像头”或“手机屏幕”。相机和屏幕采集需按系统提示授权。
4. 点击“停止”结束投屏，点击“断开”结束 P2P 连接。

### iOS / iPadOS

1. 完成 IPA 自签安装，在仪表开启投屏，再到“设置 → Wi-Fi”手动连接仪表网络。
2. 返回 App，允许本地网络访问，刷新并核对仪表地址与预设。可在“诊断与日志”中先投送测试图。
3. 选择相册图片、视频或摄像头。使用 CarPlay 时，先在兼容接收应用中启动服务，再填写其服务地址和端口。
4. 在“画面设置”中调整画面参数，在“后台继续投屏”中选择后台行为；点击“停止投屏”结束。

更多操作步骤可在 App 的“关于 → 使用说明”中查看。

## 检查更新

两端均可在“关于 → 检查更新”中手动检查，也会在前台空闲时按 24 小时间隔自动检查。连接、投屏或准备任务期间会延后；访问 GitHub 需要可用的互联网连接。

- **稍后提醒**：推迟 24 小时；“此版本不再提醒”只跳过当前版本，手动检查仍可看到它。
- **Android**：下载后校验 APK 的 SHA-256、包名、版本和签名，再打开系统安装器。首次使用可能需要允许安装应用。同签名版本覆盖升级可保留配置；0.6.1 用户需先手动安装一次较新版本。
- **iOS**：点击“前往下载”打开对应发布页，下载 IPA 后仍需自行签名安装。Release 包没有调试预览入口。

## 仪表与传输

五寸 848×480 曾在 KZ110 仪表上验证。七寸 Android 预设依据 iOS 抓包调整，实际显示仍待验证；4.3 寸模式仍需按实际仪表确认兼容性。

### Android 仪表预设与传输原理

以下为 Android 当前发布版的预设，不能直接套用于 iOS。

| 仪表 | 分辨率 | 编码与传输 | 默认帧率 | 默认码率或画质 |
| --- | --- | --- | --- | --- |
| 五寸（默认） | 848×480 | H.264 / RTP | 20 FPS | 2000 kbps |
| 七寸（待实测） | 1024×600 | H.264 / KCP | 25 FPS | 2000 kbps |
| 4.3 寸（测试） | 480×272 | JPEG / RTP | 10 FPS | JPEG 质量 80 |

**连接。** Android 通过 Wi-Fi Direct 加入仪表 P2P 组，以完整设备名称和 MAC 匹配目标，组网后核对组主身份，核对通过才开放投屏。手机已有其他 P2P 连接时，会保留连接并提示手动选择。

**画面处理。** 手机将来源画面缩放、旋转，再编码分包。视频走 UDP 5012，RTCP 控制与保活走 UDP 5013。

- 五寸使用 H.264，按仪表使用的 RTP 格式直接发送。
- 七寸在 H.264 / RTP 外增加 KCP，由接收端确认驱动重传。抓包中的视频可解码为 1024×600、标称 25 FPS；2000 kbps 为 App 默认设置。
- 4.3 寸逐帧压缩 JPEG，再切片发送。每帧可独立解码，可调整 JPEG 质量。

配置按仪表保存。“完整”保留整幅画面，“裁满”裁掉超出部分，“拉伸”改变画面比例。保存过旧七寸配置时，需要重新选择七寸预设并保存，单改分辨率不会启用 KCP。


## 常见问题

**扫不到仪表？** Android 可打开设备列表中的“全部”，并检查投屏模式和扫描权限。如果仪表被其他手机占用，先在原手机断开。iOS 需要先在系统 Wi-Fi 设置中手动连接。

**连接成功但没有画面？** 核对仪表尺寸和配置，先尝试测试图。网络回应不保证仪表已经显示画面；Android 七寸需要选择带 KCP 的预设。

**七寸日志显示“尚无回应”？** 当前 Android 版尚未识别七寸样本中的 24 字节控制回复。请结合实际画面判断，可导出日志排查。

**iOS 下载后无法安装？** IPA 未签名，需先完成自签。请检查证书、描述文件、设备及签名工具的安装要求。[Apple 注册设备分发说明](https://developer.apple.com/documentation/xcode/distributing-your-app-to-registered-devices/)

**CarPlay 服务连不上？** 确认设备位于同一局域网，地址、端口和兼容接口正确。能在某个应用中显示 CarPlay，不代表该应用提供本工具需要的视频流接口。

---

本项目为独立开发的投屏工具，与九号公司无官方关联。[抖音主页](https://v.douyin.com/x64M2NbYj0A/) · [全部发布记录](https://github.com/xmz28/ninebot_pro/releases)

Android 七寸传输使用 [KCP](https://github.com/skywind3000/kcp)，许可证随 APK 提供。
