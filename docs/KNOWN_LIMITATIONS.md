# 已知限制

- 仅 ARM64 用户空间。不支持 x86 应用程序、Linux 内核启动、内核模块或通用 systemd-as-init/容器。
- 系统调用、图形和应用程序覆盖不完整。
- Hyprland、Wayfire、KDE Plasma 和 Metal 后端是实验性的。
- JIT 取决于平台权限；解释器始终可用。
- iOS/iPadOS 可以暂停或终止 LinuxRunner，结束 Linux 进程。
- 大型桌面可能超出设备内存或热限制。
- 不支持蓝牙网络。
- Linux 账户和权限是兼容性功能，不是安全边界。
- 接收器特定的外部输出行为各异。
- 旧操作系统兼容性可能有限。
