# LinuxRunner 如何工作

LinuxRunner 在 iOS/iPadOS 应用程序内托管 ARM64 Linux 用户空间。它结合了指令解释、可选的块翻译和 Linux ABI 兼容层。它不启动 Linux 内核或使用硬件虚拟化。

```text
Debian / Arch Linux ARM / Alpine 程序和库
       │ ELF 加载，客户机地址空间
       ▼
ARM64 解释器 ─── 可选 JIT，当 iOS 允许可执行内存时
       │
Linux 系统调用兼容性：进程、线程、信号、内存、文件、套接字
       │                                      │
主机平台 API                           Linux 图形/显示服务
       │                               X11 / 受支持的 Wayland 合成器
       │                                      │
iOS/iPadOS 存储和网络                  Mesa virgl → virglrenderer
                                              → ANGLE → Metal
                                       或软件渲染
                                              │
                                原生查看器 / 外部场景 / 输入
```

## 加载和执行 ARM64 程序

ELF 加载器将 ARM64 Linux 可执行文件和共享库映射到客户机地址空间，准备进程状态并将控制权转移到运行时。Asbestos 解释器将受支持的指令解码为预编译主机例程（gadget）的缓存序列。共享 ARM64 架构不使这成为任意 Linux 程序的原生执行。

可选的 JIT 将受支持的客户机块翻译成主机机器代码。其区域必须通过 iOS 可执行内存权限检查；没有权限时解释器仍然可用。默认源代码配置禁用 JIT 编译，而选定的构建 900 IPA 包含它。运行时状态区分编译能力、调试器附加和实际执行。[JIT 实现](engine/IOS_JIT.md)

## 提供 Linux 语义

兼容层处理文件、内存映射、伪终端、套接字、进程/线程状态、信号、同步和客户机 `fork`/`clone`/`execve` 行为。这些是用户空间实现和到平台操作的翻译，不是到客户机 Linux 内核的系统调用。覆盖不完整。

每个环境有自己的根文件系统和软件包数据库。`fakefs` 将真实后备文件与 SQLite 持有的 Linux 所有权/模式元数据结合。导入/导出和每环境共享文件夹提供选定的文件访问。存储使用配置时的可选 App Group，否则使用私有后备。

客户机进程保留在 LinuxRunner 的应用程序生命周期内。它们不会成为独立的 iOS 应用程序或安全容器。主机沙箱仍然是安全边界。

## 集成 Linux 桌面

X11 会话使用 Xvfb 和 x11vnc 馈送原生 RFB 查看器。管理的启动器提供所选用户的显示授权和会话变量。默认轻量级会话使用 Openbox、面板和文件管理器；LXQt、Enlightenment 和 Debian KDE 在受支持时使用自己的组件。

实验性 Wayfire/Hyprland 会话使用 LinuxRunner 的虚拟 DRM/KMS 显示路径。兼容的客户机 Mesa/virgl 工作负载将渲染命令发送到应用的 virglrenderer 集成，它使用 ANGLE 的 Metal 后端。软件渲染仍然可用。这不同于早期的选择性图形拦截器和已渲染帧缓冲的 Metal 呈现。

Metal 不是通用图形 API 支持。应用程序、客户机 Mesa 驱动程序、合成器、内存限制和显示路径都很重要。[性能和激活](PERFORMANCE.md)

## 转发显示和输入

UIKit/Metal 呈现在应用中或外部场景中显示帧。触摸、键盘和受支持的指针事件转发到 Linux。当有单独的外部场景可用时，DeX 模式添加相对手机触控板。显示一个客户机桌面；这不实现多个独立扩展的 Linux 显示器。[显示控件](NETWORKING_AND_DISPLAYS.md)

## 通过主机的网络

Linux 套接字使用平台网络。接口/地址/路由查询将可用的主机信息翻译成面向 Linux 的形式，包括 netlink 和 proc 视图。没有独立的 Linux 网络命名空间或不受限制的无线电/原始设备访问。不支持蓝牙网络。

## 实现映射

- `asbestos/guest-arm64/`：解释器 gadget、解码和可选 JIT。
- `emu/`、`kernel/`、`fs/`：执行状态、系统调用兼容性和文件系统。
- `graphics/`：客户机图形桥接和辅助工具。
- `app/LinuxRunner/`：环境/设置 UI、原生运行时桥接、桌面/查看器集成。
- `scripts/gpu/`、`scripts/build-gpu-deps.sh`：图形依赖集成/构建。
- `tests/linuxrunner/`：运行时、图形和兼容性契约。

全系统仿真器建模机器及其内核；传统 VM 通过虚拟化运行客户机内核。LinuxRunner 相反提供 Linux 用户空间兼容性与指令解释/翻译。[限制](KNOWN_LIMITATIONS.md) · [安全](../SECURITY.md)
