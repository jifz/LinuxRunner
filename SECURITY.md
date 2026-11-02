# 安全策略

## 报告漏洞

如果你发现 LinuxRunner 中的安全漏洞，请通过 [GitHub Security Advisories](https://github.com/mxhm11cr/LinuxRunner/security/advisories/new) 私下报告。

请不要在公共问题上发布安全漏洞。

## 支持版本

| 版本 | 支持安全更新 |
| ------- | ------------------ |
| 1.1.x | ✅ |
| 1.0.x | ✅ |
| < 1.0 | ❌ |

## 安全模型

LinuxRunner 在 iOS 沙箱内运行，具有以下安全特性：

- **无内核访问：** LinuxRunner 不启动 Linux 内核或加载内核模块。它运行用户空间程序。
- **iOS 沙箱：** 应用程序受标准 iOS 沙箱限制。Linux 程序不能绕过 iOS 安全边界。
- **网络限制：** Linux 套接字使用 iOS 的网络堆栈。应用程序受 iOS 网络权限约束。
- **文件隔离：** Linux 环境存储在应用程序的私有容器中。其他应用程序无法直接访问。
- **无 root 提升：** Linux "root" 账户是 Linux 环境内的兼容性功能，不提供 iOS 上的额外权限。

## 已知限制

- Linux 账户和权限是兼容性功能，不是安全边界。
- 在 Linux 环境中运行的程序可以访问该环境内的所有文件。
- 网络访问受 iOS 权限控制，但 Linux 程序可以使用主机可用的任何网络。
- JIT 执行需要平台权限；解释器模式始终可用。

## 最佳实践

1. **保持更新：** 使用最新版本的 LinuxRunner 以获得最新的安全修复。
2. **审查网络活动：** 使用网络诊断工具监控 Linux 程序的网络活动。
3. **最小权限：** 仅在需要时启用管理员（sudo）访问。
4. **备份数据：** 定期导出重要文件，因为 iOS 可以终止应用程序及其 Linux 进程。

## 联系

如有安全问题，请使用 [GitHub Security Advisories](https://github.com/mxhm11cr/LinuxRunner/security/advisories/new)。

对于一般支持，请使用 [GitHub Issues](https://github.com/mxhm11cr/LinuxRunner/issues)。
