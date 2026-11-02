# 构建 LinuxRunner

大多数用户安装 IPA。以下说明在 `iSH.xcodeproj` 中构建 **LinuxRunner** scheme，保留版本 **1.1.0**，构建 **900** 和包标识符 `dev.linuxrunner.app`。

## 工具要求

使用 macOS 和完整的 Xcode 及 iPhoneOS SDK，PATH 上有 Git、Python 3、Meson、Ninja、CMake、pkg-config、`ld.lld` 以及系统归档/签名工具。保留的构建 900 归档记录了 iPhoneOS SDK **27.2**、ARM64 和最低 OS **15.0**。部署目标不是广泛的设备/旧 OS 认证。GPU 依赖构建还使用 GN/depot_tools、rsync 和 ANGLE 下载的工具链输入。

```sh
git clone https://github.com/mxhm11cr/LinuxRunner.git
cd LinuxRunner
git submodule update --init --recursive --checkout -- deps/libapps deps/libarchive deps/glslang deps/spirv-cross
scripts/bootstrap-macos.sh
```

发布后，在重现此版本时选择批准的 `v1.1.0` 版本。在此之前，公共仓库可能仍包含之前的版本；不要用旧版本替换较新的本地检出。继承的 `deps/linux` gitlink 是可选的，不用于在应用中启动内核。

## 解释器/软件变体

源代码默认 `LINUXRUNNER_JIT=NO` 和 `LINUXRUNNER_VIRGL=NO`：

```sh
scripts/build-ipa.sh --unsigned
python3 scripts/verify-ipa.py build/releases
```

这构建功能性的解释器/软件变体。它不重现支持 Metal/JIT 的构建 900 发布二进制文件。

## Metal/可选 JIT 变体

选定的发布 IPA 包括两个编译时功能。运行时 JIT 权限仍然是可选的，单独检查。

在仓库的源文件之外创建图形依赖目录，并将 `GPU_DEPS` 设置为其绝对路径。该目录必须包含以下记录版本的仓库：

| 目录 | 上游 | 版本 |
| --- | --- | --- |
| `virglrenderer` | `https://gitlab.freedesktop.org/virgl/virglrenderer.git` | `e0a1caf3b147bb26dfe524dbb85ded1177e7e49e` |
| `libepoxy` | `https://github.com/anholt/libepoxy.git` | `d1f952c4565c389d82fd1657153e84e050f35b27` |
| `angle` | `https://chromium.googlesource.com/angle/angle` | `feebf60fe088ccec3a26a7419d6ac68edf542c7a` |
| `depot_tools` | `https://chromium.googlesource.com/chromium/tools/depot_tools.git` | `a20039648c0de69d8156906b18052bd47e9bf230` |

对于新的检出，使用记录的版本准备依赖。这些命令下载大量额外的构建输入：

```sh
mkdir -p ../linuxrunner-gpu-deps
export GPU_DEPS="$(cd ../linuxrunner-gpu-deps && pwd)"
git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git "$GPU_DEPS/depot_tools"
git -C "$GPU_DEPS/depot_tools" checkout --detach a20039648c0de69d8156906b18052bd47e9bf230
export PATH="$GPU_DEPS/depot_tools:$PATH"
git clone https://gitlab.freedesktop.org/virgl/virglrenderer.git "$GPU_DEPS/virglrenderer"
git -C "$GPU_DEPS/virglrenderer" checkout --detach e0a1caf3b147bb26dfe524dbb85ded1177e7e49e
git clone https://github.com/anholt/libepoxy.git "$GPU_DEPS/libepoxy"
git -C "$GPU_DEPS/libepoxy" checkout --detach d1f952c4565c389d82fd1657153e84e050f35b27
git clone https://chromium.googlesource.com/angle/angle "$GPU_DEPS/angle"
git -C "$GPU_DEPS/angle" checkout --detach feebf60fe088ccec3a26a7419d6ac68edf542c7a
(cd "$GPU_DEPS/angle" && python3 scripts/bootstrap.py && gclient sync)
```

引导创建 ANGLE 的 gclient 配置；sync 解析固定检出的 DEPS 和工具。遵循保留的 ANGLE `doc/DevSetup.md` 了解平台先决条件。不要替换当前的依赖版本。

准备这些源检出后，从 LinuxRunner 仓库根目录：

```sh
scripts/build-gpu-deps.sh iphoneos
LINUXRUNNER_JIT=YES LINUXRUNNER_VIRGL=YES scripts/build-ipa.sh --unsigned
LINUXRUNNER_JIT=YES python3 scripts/verify-ipa.py build/releases
```

`GPU_DEPS` 必须已导出。脚本检查记录的 virglrenderer/ANGLE 版本，但记录而非强制执行 libepoxy 的当前 HEAD；显式检出表的 libepoxy 版本。它对副本应用保留的 iOS 进程图像补丁。输出包括 `build/gpu/iphoneos/REVISIONS` 和静态库/头文件。

此准备重新审计了保留的归档；它没有对所有图形依赖进行干净的重建。额外依赖/源包的干净检出认证仍然是版本审查项目。应用的链接器必须保持动态解析的 EGL 导出：经验证的 IPA 保留 44 个 EGL 导出，包括 `eglGetProcAddress` 和 `eglGetCurrentDisplay`。

## 打包和签名

默认输出是 `build/releases/LinuxRunner.ipa`，带有保留的归档、符号、校验和和验证报告。`RELEASE_DIR` 和 `ARTIFACT_NAME` 选择其他目标/名称；验证时使用相同的工件名称。对于保留的发布文件名使用 `ARTIFACT_NAME=LinuxRunner-1.1.0-build900`。

无签名模式添加临时签名，没有 Apple 配置。兼容的安装方法必须提供设备授权。对于你自己的签名，在 Xcode 中配置 Apple 团队并使用 `TEAM_ID=YOUR_TEAM_ID scripts/build-ipa.sh`，如果需要，添加上面的变体变量。永远不要提交证书、密钥或配置描述文件。可选的 App Group 访问使用 `group.dev.linuxrunner.app`；存在私有容器后备。

Alpine 3.24.2 是校验和固定的。`ROOTFS_CACHE` 可以提供缓存的归档；仍然适用验证。`verify-ipa.py` 检查包身份、rootfs 哈希、90 个 GUI 资源、源指纹、设备 Mach-O 依赖、IPA/归档身份和匹配的符号。在检查保留工件与其源时设置 `LINUXRUNNER_VERIFY_SOURCE_TREE` 和 `LINUXRUNNER_EXPECTED_SOURCE_COMMIT`。
