<p align="center">
  <img src="assets/branding/linuxrunner-icon.svg" alt="LinuxRunner" width="144">
</p>
<h1 align="center">LinuxRunner</h1>
<h2 align="center">你的 iPhone。一台真正的 Linux 电脑。</h2>
<p align="center">ARM64 Linux 应用程序。完整的桌面环境。外接显示器上的工作区。</p>
<p align="center">
  <img src="assets/branding/version-badge.svg" alt="版本 1.1.0 · 构建 900">
  <img src="assets/branding/platform-badge.svg" alt="iOS 和 iPadOS">
  <a href="LICENSE.md"><img src="assets/branding/license-badge.svg" alt="GPL-3.0 授权的应用程序"></a>
</p>
<p align="center">
  <a href="https://github.com/mxhm11cr/LinuxRunner/releases">下载</a> ·
  <a href="#getting-started">快速开始</a> ·
  <a href="docs/releases/v1.1.0.md">1.1.0 更新内容</a> ·
  <a href="docs/TROUBLESHOOTING.md">帮助</a>
</p>

LinuxRunner 通过自定义指令解释器、可选的 JIT 引擎和 Linux 兼容层，将 ARM64 Linux 用户空间带到 iPhone 和 iPad。运行 Linux 应用程序、探索桌面环境，并将你的工作区扩展到外接显示器。

**无需越狱。JIT 可选。** LinuxRunner 执行 Linux 用户空间程序；它不启动 Linux 内核或使用全系统虚拟机。

[![Hyprland 桌面在 LinuxRunner 中运行，带 Metal GPU 加速](assets/screenshots/desktop/hyprland-metal.jpg)](assets/screenshots/desktop/hyprland-metal.jpg)

**Hyprland · 实验性** — Metal GPU 加速。需要至少 8 GB 内存和 Arch Linux ARM。

[![KDE Plasma 桌面与 Dolphin](assets/screenshots/linuxrunner-dolphin.png)](assets/screenshots/linuxrunner-dolphin.png)

**KDE Plasma** — Debian 上的实验性桌面选项。

## 你的 iPhone。你的桌面。

[![LinuxRunner 在外接显示器上显示 ONLYOFFICE，通过 iPhone 触控板控制](assets/screenshots/desktop/dex-external-display.jpg)](assets/screenshots/desktop/dex-external-display.jpg)

**DeX 模式** 将 Linux 桌面带到兼容的外接显示器。使用键盘和鼠标，或将 iPhone 变成触控板。这是 LinuxRunner 自己的桌面集成和 ARM64 运行时；不涉及 Android 和三星 DeX。

1. 使用设备支持的适配器/线缆连接兼容的显示器。对于 AirPlay，通过 **iOS 控制中心 → 屏幕镜像** 连接到兼容的接收器。
2. 启用 **设置 → 设备 → 外部桌面输出**。
3. 选择 **主页 → 打开桌面**（或 **恢复桌面**）。
4. 在查看器中，打开 **桌面 → 使用 iPhone 作为触控板**。当单独的外部场景和桌面框架就绪时，控件可用。
5. 滑动移动，点击单击，按住并滑动拖动。使用两根手指滚动或点击右键单击。键盘按钮打开打字控件；兼容的硬件输入通过 iOS 转发。

使用 **桌面 → 桌面设置… → 显示** 进行缩放和 **分辨率与查看器偏好**。客户机分辨率更改在下次桌面启动时应用；查看器缩放立即更改。默认桌面大小为 960 × 540。

AirPlay 接收器行为各异。纯屏幕镜像显示相同图像，无法提供独立的手机控制界面。这是一个 Linux 桌面输出，不是多个扩展的客户机显示器。不支持仅 Miracast 的接收器。[显示和输入指南](docs/NETWORKING_AND_DISPLAYS.md)

## 1.1.0 内部功能

| 功能 | 带来的改进 |
| --- | --- |
| **Linux 桌面** | LinuxRunner 桌面、LXQt、Enlightenment 和实验性 Wayland/Plasma 选项。 |
| **Metal 图形** | 虚拟 Linux GPU 将兼容的 Mesa 工作负载连接到 Apple GPU。 |
| **可选 ARM64 JIT** | 当设备允许时的额外执行路径；解释器仍然可用。 |
| **更快的解释器** | NEON、内存和原子操作改进，加上指令正确性修复。 |
| **Linux 应用程序** | 软件包管理器、开发者工具、办公软件、通讯应用等。兼容性各异。 |
| **文件和网络** | 导入/导出、每环境共享文件夹、套接字、接口和路由报告。 |
| **三个发行版** | Debian ARM64、Arch Linux ARM 和 Alpine ARM64，具有独立的环境和 Linux 账户。 |

## 支持的设备和要求

LinuxRunner 支持 ARM64 iPhone 和 iPad 布局、触摸输入、硬件键盘和兼容的指针。**iPad 支持已由维护者进行物理测试。** 其更大的窗口为终端和 Linux 应用程序提供更多空间；支持查看器大小调整、旋转和键盘快捷键。

| | 最低指导 | 推荐 |
| --- | --- | --- |
| 设备 | iPhone 11 或更新，或同等兼容的 iPad/设备 | iPhone 12 Pro 或更新，或具有更多内存的兼容设备 |
| 内存 | 至少 4 GB | 至少 6 GB |
| 系统 | iOS/iPadOS 15.0 部署目标；见下方注意事项 | iOS/iPadOS 26 或更新，最好是最近测试的版本 |
| 可用存储 | 基本使用约 3–4 GB | 桌面和大型应用程序至少 10 GB |

**iOS 15 是预期的兼容性目标，不是广泛验证的支持。** 开发和设备测试主要使用更新的版本。旧版本可能有局限性或启动问题；早期的 iPhone 11/iOS 17 黑屏报告仍未解决。这些是工作负载指导，不是每个型号的认证。大型安装可能需要远超 10 GB 的空间。

**Hyprland 需要至少 8 GB 内存。** 它仍然是实验性的，仍在优化中；推荐 Metal。[兼容性详情](docs/COMPATIBILITY.md)

## 支持的 Linux 发行版

| 发行版 | 软件包 | 桌面体验 |
| --- | --- | --- |
| **Debian GNU/Linux 13 ARM64** | `apt`、`dpkg` | 推荐。LinuxRunner 桌面、LXQt；实验性 KDE Plasma 和 Wayfire。 |
| **Arch Linux ARM** | `pacman` | 推荐用于更新的桌面/应用程序软件包。LinuxRunner 桌面、LXQt、Enlightenment、Wayfire 和实验性 Hyprland。 |
| **Alpine Linux 3.24 ARM64** | `apk` | 小型终端环境；桌面和应用程序覆盖更有限。 |

桌面使用推荐 Debian 或 Arch。Alpine 仍然受支持，计划进一步进行兼容性和桌面集成工作。计划支持更多发行版。多个环境可以共存；每次应用启动一个运行时处于活动状态。

## 安装

1. 从 [GitHub Releases](https://github.com/mxhm11cr/LinuxRunner/releases) 下载 LinuxRunner IPA。
2. 使用你选择的兼容 IPA 侧载工具安装它，如 Sideloadly 或 AltStore Classic。
3. 在 iPhone 或 iPad 上打开 LinuxRunner。
4. 按照 **设置 Linux…** 在应用内安装 Linux。

IPA 需要适合你安装方法的签名/配置。工具兼容性、账户要求和签名续期各异。**安装或使用 LinuxRunner 不需要 JIT。** 更新前备份重要文件并保留现有的应用身份和存储配置。[签名和下载验证](docs/INSTALLATION.md)

## 快速开始

安装 IPA 安装应用程序。**安装 Linux 发行版是 LinuxRunner 内的单独步骤。**

1. 打开 **发行版 → 设置 Linux… → 继续**。
2. 在 **选择 Linux** 上，桌面使用选择 Debian 或 Arch，或小型终端环境选择 Alpine。
3. 继续到 **安装 Linux**，查看存储/下载信息并选择发行版的安装按钮。
4. 在设置准备根文件系统时保持应用打开。如果请求，按照 **重启 LinuxRunner**；重新打开后设置恢复。
5. 在 **你的账户** 上，创建或选择普通 Linux 用户。如果要安装软件包，启用 **管理员（可以使用 sudo）**。
6. 提供时安装 **桌面组件**，或仅终端使用选择 **稍后**。桌面是可选的。
7. 在主页上，选择 **终端** 或 **打开桌面**。**恢复桌面** 重新连接到现有会话。
8. 可选地在设置中选择另一个桌面，启用 Metal，或配置外部输出。仅当你想实验时配置 JIT。

在终端中尝试 `cat /etc/os-release` 和 `uname -m`。通过 **应用程序管理器** 或发行版的软件包管理器安装 Linux 应用程序。软件包可用性不保证兼容性。

[完整设置演练、账户选项和软件包命令](docs/GETTING_STARTED.md)

## 选择你的桌面

打开 **设置 → 桌面环境**。选择相关的 **安装…** 按钮，等待完成，然后在 **打开桌面启动** 下的 **桌面** 选择器中选择已安装的环境。保存工作并在切换前停止任何运行的桌面。返回主页并选择 **打开桌面**。

| 桌面 | 可用性和状态 |
| --- | --- |
| **LinuxRunner 桌面** | 轻量级基于 Openbox 的默认和后备；面板和文件管理器。 |
| **LXQt** | X11 桌面，带 LXQt 面板、PCManFM-Qt、QTerminal 和 Openbox；首选 Debian 或 Arch。 |
| **Enlightenment** | 在 Arch 上可用。在 Debian 上禁用，因为启动当前停在启动画面。 |
| **Wayfire** | Debian/Arch 上的实验性 Wayland 合成器；GPU 集成在 Arch 上可用。 |
| **Hyprland** | **实验性，仅 Arch，至少 8 GB 内存。推荐 Metal。** |
| **KDE Plasma** | Debian 上的实验性 X11 会话，带 Dolphin 和 Konsole。Arch Plasma 未验证。 |

Hyprland 仍在优化中。其首次启动偶尔可能报告错误；如果提供，选择 **重试**。此已知启动问题计划改进。如果持续存在，使用 LinuxRunner 桌面或 LXQt。[桌面控件和恢复](docs/DESKTOP_CONTROLS.md)

## 真正的 GPU 加速。由 Metal 驱动。

兼容的 Linux 图形工作负载可以使用此路径：

**Linux 图形 API → 客户机 Mesa/virgl → virglrenderer → ANGLE → Apple Metal**

这让受支持的 Linux 应用程序和合成器使用 Apple GPU。它不同于简单地用 Metal 呈现查看器，也不加速每个应用程序或图形 API。

**显式选择 Metal：** 打开 **设置 → 图形 → Linux GPU 设备 → GPU → Metal GPU · 实验性**。完全关闭并重新打开 LinuxRunner，然后检查同一页面上的 **活动渲染器**。**自动** 在构建 900 中不选择此加速路径。**软件渲染** 仍然可用于兼容性，对于要求高的图形可能慢得多。

<p align="center"><a href="assets/screenshots/applications/freecad-metal-iphone.jpg"><img src="assets/screenshots/applications/freecad-metal-iphone.jpg" alt="在 iPhone 上的 LinuxRunner 中选择 Metal GPU 运行的 FreeCAD" width="280"></a></p>

**FreeCAD** — 选择 Metal GPU 捕获。

**真机 iPhone 结果：** 维护者报告在 **iPhone 16 Pro 运行 iOS 27.2** 上进行 **Hyprland** 测试时，**软件渲染约 10 FPS**，**Metal 约 55–60 FPS**。这是报告的观察，不是受控基准测试；未提供计数器/方法和持续时间。Hyprland 和 FreeCAD 捕获也使用 GPU 加速。维护者报告其他桌面有更高的速率；结果因工作负载和呈现路径而异。[性能详情](docs/PERFORMANCE.md)

## 想要时 JIT。不需要时解释器。

**使用 LinuxRunner 不需要 JIT。** ARM64 解释器是默认执行路径，无需启用 JIT 即可工作。可选的 JIT 在平台授予可执行内存时将受支持的客户机块翻译成主机指令。

要检查它，启用 **设置 → 高级 → 开发者模式**，然后打开 **执行引擎 / StikDebug**。页面显示 **JIT 状态**、运行的后端和翻译块计数。根据需要选择 **解释器**、**自动** 或 **JIT**。**使用 StikDebug 附加** 和 **立即激活 JIT** 是实验性激活控件，不保证 iOS 会允许 JIT。

可用性取决于 OS 限制、签名和激活方法。如果权限不可用，LinuxRunner 通过解释器继续。JIT 可以使较长的计算工作负载受益，而翻译开销可能使短程序变慢。[执行详情](docs/engine/IOS_JIT.md)

## 更好的 ARM64 运行时

版本 1.1.0 改进了 NEON 比较/成对操作、独占存储处理和脏页过滤。它添加了 ARMv8 AES 和 SHA 指令的 JIT 翻译，公布经验证的 PMULL/SHA1/SHA2/CRC32 功能，并修复了向量 RBIT 和 JIT 内存偏移正确性。这些更改减少了覆盖的指令失败并改善了兼容软件的执行。

[记录的解释器和 JIT 比较](docs/PERFORMANCE.md) 包括工作负载详情、范围和 JIT 翻译开销较慢的情况。

## 更多 Linux 应用。更多可能性。

<table>
<tr>
<td align="center"><a href="assets/screenshots/applications/vscode.jpg"><img src="assets/screenshots/applications/vscode.jpg" alt="Visual Studio Code 在 LinuxRunner 中编辑 C 文件" width="420"></a><br><b>Visual Studio Code</b></td>
<td align="center"><a href="assets/screenshots/applications/vesktop-redacted.png"><img src="assets/screenshots/applications/vesditor-redacted.png" alt="Vesktop 显示 Discord 登录；登录二维码已编辑" width="420"></a><br><b>Vesktop / Discord</b></td>
</tr>
<tr>
<td align="center"><a href="assets/screenshots/applications/firefox-github.jpg"><img src="assets/screenshots/applications/firefox-github.jpg" alt="LinuxRunner 中的 Firefox" width="420"></a><br><b>Firefox</b></td>
<td align="center"><a href="assets/screenshots/linuxrunner-blender-viewport.jpg"><img src="assets/screenshots/linuxrunner-blender-viewport.jpg" alt="LinuxRunner 中的 Blender 视口" width="420"></a><br><b>Blender</b></td>
</tr>
</table>

Firefox、VS Code、FreeCAD、ONLYOFFICE、Blender 和 Dolphin 是在 LinuxRunner 中运行的应用程序之一。Vesktop 也可以工作，Arch 上的 Telegram 支持登录、消息和通话。

[应用程序兼容性和测试范围](docs/COMPATIBILITY.md)

## 网络和文件

Linux 套接字使用设备的可用网络连接。构建 900 通过 Linux 兼容查询改进了地址、接口和路由报告：

```sh
ip addr
ip link
ip route
```

这些描述 LinuxRunner 可以通过 iOS API 及其兼容层获取的网络信息。它们不给 Linux 程序对无线电、原始数据包或主机路由控件的不受限制访问。**不支持蓝牙网络。**

使用 **设置 → 文件共享** 导入/导出文件或访问活动环境在 `/mnt/LinuxRunnerShared` 的共享文件夹。当该名称可用时创建 `~/Shared` 链接。[文件](docs/FILE_SHARING.md) · [网络](docs/NETWORKING_AND_DISPLAYS.md)

<details>
<summary><b>LinuxRunner 更多内容：界面、设置和 Arch</b></summary>

<table>
<tr>
<td align="center"><img src="assets/screenshots/linuxrunner-home.png" alt="LinuxRunner 主页" width="210"><br><b>主页</b></td>
<td align="center"><img src="assets/screenshots/linuxrunner-settings.png" alt="LinuxRunner 设置" width="210"><br><b>设置</b></td>
</tr>
<tr>
<td align="center"><img src="assets/screenshots/linuxrunner-install-progress.png" alt="Linux 设置进度" width="210"><br><b>安装 Linux</b></td>
<td align="center"><img src="assets/screenshots/linuxrunner-desktop-viewer.png" alt="LinuxRunner 桌面查看器" width="210"><br><b>桌面查看器</b></td>
</tr>
<tr>
<td align="center" colspan="2"><img src="assets/screenshots/arch-telegram-iphone.jpg" alt="Arch Linux ARM 上的 Telegram 桌面" width="210"><br><b>Telegram 桌面</b></td>
</tr>
</table>

现有的图片集仍然可在 [截图](assets/screenshots/README.md) 中找到。较旧的界面捕获说明工作流程；当前指南中的标签描述构建 900。

</details>

## LinuxRunner 如何工作

1. 加载器映射 ARM64 Linux ELF 可执行文件和共享库。
2. 解释器执行受支持的 ARM64 指令；可选的 JIT 在允许时翻译块。
3. 兼容层实现 Linux 系统调用、进程/线程行为、信号、内存映射和文件系统元数据。
4. 每个环境提供自己的客户机文件系统和 Linux 软件包；套接字使用主机网络 API。
5. X11 会话使用 Xvfb/x11vnc。受支持的 Wayland 合成器针对 LinuxRunner 的虚拟显示/GPU 设备运行，显示和输入转发到应用的查看器和外部场景。

这结合了 **指令解释/翻译和用户空间兼容性**。它不是硬件虚拟化或全系统内核仿真。[架构](docs/ARCHITECTURE.md)

## 兼容性和限制

- 仅 ARM64 用户空间；没有 x86 应用程序、Linux 内核启动、内核模块或通用 systemd-as-init/容器支持。
- 系统调用、图形和应用程序覆盖仍然不完整。大型桌面可能超出设备内存或热限制。
- Hyprland、Wayfire、KDE Plasma 和 Metal 后端有实验性路径；桌面/发行版组合不同。
- JIT 取决于平台权限；软件渲染和解释器执行仍然可用。
- iOS/iPadOS 可以暂停或终止 LinuxRunner。**完成** 在应用中留下运行的会话；应用终止结束运行的 Linux 进程。保存的文件持久存在。
- 客户机账户和权限是兼容性功能，不是不受信任软件的安全边界。

[兼容性](docs/COMPATIBILITY.md) · [已知限制](docs/KNOWN_LIMITATIONS.md) · [安全](SECURITY.md)

## 故障排除和贡献

在重新安装环境之前使用 [故障排除](docs/TROUBLESHOOTING.md)。**应用程序管理器 → 修复中心** 提供诊断和软件包修复。**设置 → 高级 → 导出打开桌面报告** 收集会话信息；分享前检查日志中的个人数据。

[报告问题](https://github.com/mxhm11cr/LinuxRunner/issues/new/choose)，包括你的设备、操作系统、版本/构建、发行版、桌面、图形/后端状态和可重现的步骤。欢迎贡献和有范围的兼容性报告：[贡献](CONTRIBUTING.md)。

## 从源代码构建

大多数用户安装 IPA。开发者应遵循 [构建](docs/BUILDING.md)，包括 Metal 启用变体的额外固定图形依赖。构建保持 **1.1.0 (900)**，包标识符 `dev.linuxrunner.app`。

## 许可证和致谢

由 **Leminos ([mxhm11cr](https://github.com/mxhm11cr))** 维护。LinuxRunner 源自 [iSH](https://github.com/ish-app/ish)，由 Theodore Dubois 和贡献者开发，通过 [ios-linuxkit](https://github.com/rcarmo/ios-linuxkit)，由 Rui Carmo 和贡献者开发。

组合应用程序受 GPL-3.0 保护。保留上游贡献特定条款、归属和 [LICENSE.md](LICENSE.md) 及 [LICENSE.IOS](LICENSE.IOS) 中的 App Store 条款。图形、终端、字体、Linux 发行版、桌面和应用程序保留自己的许可证和作者身份。特别是，Metal 集成使用 Mesa/virgl、virglrenderer、libepoxy 和 ANGLE。[第三方通知](THIRD_PARTY_NOTICES.md)
