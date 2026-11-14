# Ninebot Pro

通过 Wi-Fi Direct 将相册图片、视频、摄像头或手机屏幕投到兼容的九号仪表。本仓库用于分发 Android APK。

## 最新版本

- 版本：`0.6.1`（`versionCode 9`）
- [版本记录](https://github.com/xmz28/ninebot_pro/releases/tag/v0.6.1)
- [下载正式版 APK](https://github.com/xmz28/ninebot_pro/releases/download/v0.6.1/ninebot-pro-release-v0.6.1.apk)
- 包名：`com.example.ninebotpro`
- 系统要求：Android 8.0 或更新版本

## 投屏预设

| 仪表 | 分辨率 | 编码与传输 | 默认帧率 | 默认码率或画质 |
| --- | --- | --- | --- | --- |
| 5 寸（默认） | 848×480 | H.264 / RTP | 20 FPS | 2000 kbps |
| 7 寸（待实测） | 1024×600 | H.264 / KCP | 25 FPS | 2000 kbps |
| 4.3 寸（测试） | 480×272 | JPEG / RTP | 10 FPS | JPEG 质量 80 |

五寸 848×480 曾在 KZ110 仪表上验证。七寸适配依据 iOS 投屏抓包，Android 实机显示仍待验证；4.3 寸也待仪表验收。

## 安装与使用

1. 从 GitHub Release 下载 APK。曾安装同包名调试版的用户需要先卸载调试版，卸载会清除该版的本地配置。
2. 开启仪表投屏和手机 Wi-Fi，按系统提示授予附近 Wi-Fi 或定位权限。
3. 点击「扫描 P2P」，选择自己的仪表并按系统提示确认。再次打开应用时会尝试重连上次成功连接的仪表。
4. 在「投屏配置」选择仪表预设，可手动调整宽高。曾保存旧七寸配置的用户请重新选择七寸预设并保存，以启用 KCP。保存后选择相册媒体、摄像头或手机屏幕。
5. 在「关于 → 使用说明」可重新查看操作步骤。

本项目为独立开发的投屏工具，与九号公司无官方关联。[抖音主页](https://v.douyin.com/x64M2NbYj0A/)

七寸传输使用 [KCP](https://github.com/skywind3000/kcp)，许可证随 APK 提供。
