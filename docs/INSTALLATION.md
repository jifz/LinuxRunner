# 安装 LinuxRunner

安装 IPA 安装 LinuxRunner。然后你在 **应用内部** 安装 Linux 发行版。不需要越狱或 JIT 激活。

## 要求

构建 900 设备 IPA 是 ARM64，为 iPhone 和 iPad 配置，部署目标 15.0。iOS/iPadOS 15 是预期的最低版本，不是广泛验证的兼容性；开发和测试主要使用更新的版本。参见 [硬件、内存和存储指导](../README.md#supported-devices-and-requirements)。早期的 iPhone 11/iOS 17 启动黑屏报告仍未解决。

## 下载、签名和打开

1. 从 [GitHub Releases](https://github.com/mxhm11cr/LinuxRunner/releases) 下载 IPA。
2. 将原始文件的 SHA-256 与该版本提供的校验和进行比较。
3. 使用你首选的兼容 IPA 侧载工具安装，如 [Sideloadly](https://sideloadly.io/) 或 [AltStore Classic](https://altstore.io/)。
4. 打开应用，然后 **发行版 → 设置 Linux…**。按照 [Linux 安装演练](GETTING_STARTED.md)。

提议的 1.1.0 资源是 **LinuxRunner-1.1.0-build900.ipa**。它有临时签名，没有 Apple 配置描述文件。兼容的工具必须提供普通设备安装所需的签名/配置。签名要求、续期间隔和兼容性取决于工具和账户；不保证任何服务都能工作。

包标识符是 `dev.linuxrunner.app`。可选的 App Group 访问在配置时使用 `group.dev.linuxrunner.app`；否则使用私有应用存储。**普通解释器执行不需要调试器/JIT 权限。** 可选的 JIT 激活有单独的签名/OS 限制；参见 [JIT](engine/IOS_JIT.md)。

## 验证原始下载

在 macOS/Linux 上，使用实际下载的文件名：

```sh
shasum -a 256 LinuxRunner-1.1.0-build900.ipa
```

在 Windows PowerShell 上：

```powershell
Get-FileHash -Algorithm SHA256 .\LinuxRunner-1.1.0-build900.ipa
```

构建 900 的经验证原始哈希是：

```text
b2d73496307b6d2f535d80f09c00ef06aaf2b324a3ab9a52798999d4155634ae
```

签名更改文件；在签名之前比较。有效的校验和确认下载的字节，不确认与每个安装程序或设备的兼容性。

## 更新而不丢失环境

备份重要文件并保留你之前的 IPA。保留现有的包标识符和 App Group/容器配置。更改签名身份或存储授权可以更改对现有数据的访问。不要卸载 LinuxRunner 或删除根文件系统来诊断问题。参见 [故障排除](TROUBLESHOOTING.md)。
