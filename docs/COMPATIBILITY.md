# 兼容性 — LinuxRunner 1.1.0 (900)

兼容性取决于发行版、软件包版本、设备内存、操作系统和执行/图形路径。安装软件包不能确定每个功能都工作。

## 设备和发行版

保留的 IPA 是 ARM64，设备系列 iPhone/iPad，最低 OS 元数据 15.0。维护者确认了实体 iPhone 和 iPad 使用；不暗示通用型号/OS 认证。旧操作系统测试有限，有未解决的早期 iPhone 11/iOS 17 启动黑屏报告。[要求](../README.md#supported-devices-and-requirements)

Debian 13 ARM64 和 Arch Linux ARM 推荐用于桌面应用程序。Alpine 3.24 ARM64 提供小型 `apk` 终端环境，桌面集成覆盖较少。每次应用启动只有一个已安装环境处于活动状态。切换使用 **下次启动时使用** 和完全应用重启。

## 桌面组合

| 桌面 | Debian | Arch | Alpine |
| --- | --- | --- | --- |
| LinuxRunner 桌面 | 主要轻量级路径 | Openbox / LXQt 组件 | 实验性桌面路径 |
| LXQt | 可用 | 可用 | 覆盖较低；首选 Debian/Arch |
| Enlightenment | 已禁用：启动画面/黑屏启动问题 | 可用 | 未认证 |
| Wayfire | 实验性 | 实验性；GPU 路径已实现 | 不提供 |
| Hyprland | 不提供 | 实验性，最低 8 GB 内存；推荐 Metal | 不提供 |
| KDE Plasma | 实验性 X11 会话 | 当前 Plasma 未验证 | 不提供 |

Hyprland 首次启动可能需要 **重试**。LinuxRunner 桌面保持为后备。实验性 Wayland 支持不确立完整的 Wayland/KWin 兼容性。

## 应用程序结果

| 应用程序 | 当前证据和范围 |
| --- | --- |
| Vesktop / Discord | 维护者报告在新版本中测试了完整功能。提供的捕获显示其界面；登录二维码已编辑。未提供确切的发行版/软件包版本。 |
| Telegram 桌面 | 维护者在 Arch 上使用构建 897 测试了登录、消息和通话。新版本不意味着每个软件包版本都已重新测试。 |
| Firefox | 新提供的捕获显示浏览 LinuxRunner GitHub 仓库。完整的浏览器/媒体/站点兼容性尚未确立。 |
| Visual Studio Code | 新提供的捕获显示其编辑器打开 C 项目。扩展/调试器不因此被认证。 |
| FreeCAD | 新提供的捕获显示其选择 Metal 的建模界面。此图片不确立完整的 CAD 工作流。 |
| ONLYOFFICE | 新的外部显示器照片显示其文档编辑器，由手机控制。完整的办公套件功能覆盖尚未确立。 |
| Blender | 早期提供的捕获显示 3D 视口。渲染、插件和所有工具不因此被认证。 |
| Dolphin / Konsole | 包含在实验性 Debian Plasma 路径中；Dolphin 出现在保留的桌面捕获中。 |
| 终端工具 | Shell/软件包管理器功能受支持；个别程序仍受系统调用/指令覆盖限制。 |

维护者将所有提供的应用捕获标识为实体设备使用。Hyprland 和 FreeCAD 捕获使用了 GPU 加速。这些事实不会将单独的开发主机基准测试变成手机性能测量。

## 图形和执行

Metal 需要 **设置 → 图形 → Linux GPU 设备 → GPU → Metal GPU · 实验性** 和完全应用重启。检查 **活动渲染器**。软件和加速路径支持不同的工作负载；Vulkan 和任意主机图形 API 不是普遍可用的。

解释器仍然是默认的。选定的构建 900 IPA 包含可选的 JIT 代码，但 iOS 必须在翻译的块可以运行之前授予可执行内存。仅调试器附加不能证明活动的 JIT；检查应用的实际后端/状态。实体设备 JIT 认证不由可用的工程测试记录确立。

Linux 网络公开 iOS 提供的接口和路由的有界兼容性视图。它不授予无线电控制、不受限制的原始网络或蓝牙网络。外部输出取决于接收器/平台场景支持；屏幕镜像不能提供独立的手机控件。

[限制](KNOWN_LIMITATIONS.md) · [故障排除](TROUBLESHOOTING.md) · [测量性能](PERFORMANCE.md)
