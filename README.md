# Ninebot Pro

[![platform: Android 8.0+](https://img.shields.io/badge/platform-Android%208.0%2B-blue)](#安装与使用) [![connection: Wi-Fi Direct](https://img.shields.io/badge/connection-Wi--Fi%20Direct-blue)](#投屏原理) [![Release](https://img.shields.io/github/v/release/xmz28/ninebot_pro?label=release)](https://github.com/xmz28/ninebot_pro/releases/latest)

通过 Wi-Fi Direct 将相册图片、视频、摄像头或手机屏幕投到兼容的九号仪表。本仓库提供 Android APK 和 iOS IPA。

## Android 正式版

- 版本：`0.6.2`（`versionCode 10`）
- [版本记录](https://github.com/xmz28/ninebot_pro/releases/tag/v0.6.2)
- [下载正式版 APK](https://github.com/xmz28/ninebot_pro/releases/download/v0.6.2/ninebot-pro-release-v0.6.2.apk)
- 包名：`com.example.ninebotpro`
- 系统要求：Android 8.0 或更新版本

## iOS 正式版

- 版本：`1.0.1`（构建号 `2`）
- 系统要求：iOS / iPadOS 17.0 或更新版本，ARM64
- Bundle ID：`com.hanlin.ninebotpro`
- 安装包：`ninebot-pro-ios-v1.0.1-unsigned.ipa`（约 2.78 MiB），[下载未签名 IPA](https://github.com/xmz28/ninebot_pro/releases/download/ios-v1.0.1/ninebot-pro-ios-v1.0.1-unsigned.ipa) · [发布说明与校验信息](https://github.com/xmz28/ninebot_pro/releases/tag/ios-v1.0.1)
- 签名状态：未签名，需使用自己的有效证书和描述文件自行签名安装；不能直接安装，也不是 App Store / TestFlight 版本。

### iOS 本版更新

优化首页投屏卡片、连接状态、关于页和设置入口；新增 iOS 更新提醒及下载入口；统一应用图标，改进配置取消和视频进度操作。CarPlay 使用通用服务文案，接收应用需提供兼容 OXP 接口；未新增其他协议支持，也未将 CarWithin、CarCast 列为已验证兼容。

### iOS 安装与使用

1. 下载 IPA，用自己的有效证书与描述文件签名，再通过所用工具安装。签名有效期及续签方式取决于实际签名渠道。[Apple 注册设备分发说明](https://developer.apple.com/documentation/xcode/distributing-your-app-to-registered-devices/)
2. 建议保留 Bundle ID；如签名工具修改 Bundle ID，App 内更新可能无法匹配元数据，请从 GitHub 手动下载新版后重新签名安装。
3. 在仪表开启投屏模式，到 iPhone 或 iPad 的“设置 → Wi-Fi”手动连接仪表网络。返回 App，按提示允许本地网络访问，并核对仪表预设和地址。
4. 选择相册图片、视频、摄像头或 CarPlay。可先在“诊断与日志”投送测试图；CarPlay 地址与端口以接收应用的服务设置为准。
5. 五寸使用 H.264，4.3 寸 JPEG 为实验功能。七寸 KCP 与跨 App 系统屏幕录制不在本版支持范围内。
6. “关于 → 检查更新”可查看 iOS 新版本，提醒后打开下载页面；下载 IPA 后仍需自行签名。Release 包没有调试预览入口。

本包已完成 Release 构建、包体元数据及 ZIP 完整性核验。同源开发签名版本此前已在 iPhone 17 Pro Max 安装并获用户确认；最终未签名 IPA 未对所有第三方自签工具做端到端安装验证。

以下预设、P2P 扫描和 App 内更新说明适用于 Android 版。

## 投屏预设

| 仪表 | 分辨率 | 编码与传输 | 默认帧率 | 默认码率或画质 |
| --- | --- | --- | --- | --- |
| 5 寸（默认） | 848×480 | H.264 / RTP | 20 FPS | 2000 kbps |
| 7 寸（待实测） | 1024×600 | H.264 / KCP | 25 FPS | 2000 kbps |
| 4.3 寸（测试） | 480×272 | JPEG / RTP | 10 FPS | JPEG 质量 80 |

五寸 848×480 曾在 KZ110 仪表上验证。七寸预设依据 iOS 成功投屏的抓包调整，当前 Android 版的实际显示仍待验证。4.3 寸预设已完成手机端 JPEG 编码验证，仪表显示待验收。

## 投屏原理

**连接仪表。** 手机通过 Wi-Fi Direct 加入仪表的 P2P 组。App 扫描时以完整设备名称和 MAC 匹配所选目标，组网后再核对实际组主身份，核对通过才开放投屏。下次打开 App 会尝试重连上次成功核对的仪表。手机已有其他 P2P 连接时，会保留当前连接并提示手动选择。

**生成和发送画面。** App 将图片、视频、摄像头或手机屏幕的画面按所选预设缩放、旋转，再编码和分包。视频数据走 UDP 5012，控制和保活走 UDP 5013。不同预设决定画面尺寸、编码方式和分包传输方式。

- **5 寸**使用 H.264 连续编码，按仪表使用的 RTP 格式直接发送。
- **7 寸**同样使用 H.264，但在 RTP 外加一层 KCP。KCP 根据接收端的确认处理重传。iOS 抓包中的视频可解码为 1024×600，标称帧率为 25 FPS。2000 kbps 是 App 的默认设置。
- **4.3 寸**逐帧压缩成 JPEG，再切片发送。每帧可独立解码，可通过 JPEG 质量设置调整压缩程度。

## 安装与使用

1. 从 GitHub Release 下载 APK。曾安装同包名调试版的用户需要先卸载调试版，卸载会清除该版的本地配置。
2. 在仪表或官方 App 中开启仪表投屏，打开手机 Wi-Fi。Android 13 及以上按提示授予附近 Wi-Fi 权限，Android 12 及以下授予精确定位权限，并在扫描时打开系统定位。
3. 点击「扫描 P2P」，选择自己的仪表并按系统提示确认。首页显示已连接后，即可进入「投屏配置」。
4. 按仪表选择预设。宽高、帧率、旋转和画面缩放可按需调整，配置按仪表保存。「完整」保留整幅画面，「裁满」会裁掉超出屏幕的部分，「拉伸」会改变画面比例。曾保存旧七寸配置的用户请重新选择七寸预设并保存，以启用 KCP。
5. 根据需要选择「相册媒体」「摄像头」或「手机屏幕」。相册支持图片和视频，视频可通过手机上的预览控制播放。相机和屏幕采集需要按系统提示授权。
6. 图片、视频和手机屏幕投屏可以在后台继续，摄像头投屏在 App 离开前台后停止，视频声音在手机播放。点击「停止」结束画面发送，点击「断开」结束 P2P 连接。

更多操作步骤可在「关于 → 使用说明」查看。

## App 内更新

从 v0.6.2 起，可在「关于 → 检查更新」手动检查，也可在 App 前台使用时收到新版本提醒。自动检查每 24 小时进行一次，连接或投屏时会延后。检查和下载需要手机能够访问 GitHub。

发现新版时，可选择「现在更新」「此版本不再提醒」或「下次再说」。「此版本不再提醒」只跳过当前版本，手动检查仍可看到它。「下次再说」会推迟提醒 24 小时。

确认下载后，App 会校验 APK 的完整性、包名、版本和签名，并打开 Android 安装器。首次使用时，系统可能要求允许 Ninebot Pro 安装应用。通过正式签名版覆盖升级可保留已保存的仪表配置。v0.6.1 用户请先从本页下载并手动安装一次。

## 常见问题

- **扫不到仪表**。确认仪表的投屏模式已开启，手机已授予扫描权限。可以打开设备列表里的「全部」查看扫描结果。如果仪表已被另一台手机占用，先在原手机上断开，再重新扫描。
- **已连接但仪表没有画面**。先确认仪表尺寸对应的预设，再尝试「测试图」。七寸要使用带 KCP 的预设，单独把旧配置改成 1024×600 不会切换传输方式。
- **七寸日志显示「尚无回应」**。当前版本的控制心跳统计尚未识别七寸样本中的 24 字节回复。请同时观察仪表画面，排查时可用「导出日志」保存诊断信息。

本项目为独立开发的投屏工具，与九号公司无官方关联。[抖音主页](https://v.douyin.com/x64M2NbYj0A/)

七寸传输使用 [KCP](https://github.com/skywind3000/kcp)，许可证随 APK 提供。
