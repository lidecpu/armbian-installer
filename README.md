<div align="center">

# Armbian Installer Debian 13.5

基于 Debian Live 的 x86-64 img 镜像安装器，用于快速安装 Debian 13.5。

[![Debian](https://img.shields.io/badge/Debian-13.5-A81D33?logo=debian&logoColor=white)](https://www.debian.org/)
[![Platform](https://img.shields.io/badge/Platform-x86--64-2F6FED)](#适用场景)
[![Release](https://img.shields.io/badge/Download-GitHub%20Releases-238636?logo=github)](https://github.com/lidecpu/armbian-installer/releases)
[![License](https://img.shields.io/badge/License-MIT-informational)](LICENSE)

</div>

## 简介

这是一个面向 x86-64 设备的 Debian 13.5 img 镜像安装器。

主要改动是把安装器底层 Debian Live 环境更新为 Debian 13.5，并保留原安装器的使用方式：启动 ISO 后，通过安装菜单把系统写入目标磁盘。

## 背景

嵌入式设备的系统镜像通常采用 img 格式，常见安装方式包括线刷、烧录 SD 卡或使用 `dd` 写盘。

随着软路由、迷你主机、NAS 和虚拟机逐渐普及，越来越多 x86-64 设备也开始使用这类 img 系统。但传统烧录方式在 x86-64 场景下不够直观，通常还需要额外准备 PE、手动传递系统镜像文件或执行写盘命令，流程容易变得低效和复杂。

本项目的目标是把这类安装流程做得更接近普通系统安装：从 ISO 启动，进入 Debian Live 环境，然后通过安装菜单把 Debian 13.5 写入目标磁盘。

## 与直接导入 img 的区别

许多 NAS 或虚拟机平台支持直接导入 img 镜像，但这类导入通常只是把 raw img 自动转换成 qcow2 等虚拟磁盘格式。转换完成后，虚拟磁盘容量会被锁定为原 img 的固定大小，后续扩容和升级都容易受限制。

这种模式在后续替换或升级系统镜像时尤其明显：如果新版镜像体积大于原始 img，即使不保留原配置，也可能因为虚拟磁盘空间不足而写入失败，甚至出现启动异常。

ISO 安装器的逻辑不同。安装前可以自行设置目标虚拟磁盘容量，安装过程只把系统写入目标磁盘的一部分空间，不会把磁盘上限锁死在原 img 大小内。只要预留空间足够，后续替换、升级或扩展都会更灵活。

整体体验更接近安装传统 Windows 或 Linux 原版系统，解决了直接导入 img 后容量固化的问题。

## 实现方式

本项目基于开源项目 [debian-live](https://github.com/dpowers86/debian-live) 制作。

构建流程先生成一个支持 EFI 引导的 Debian Live 系统，然后把需要安装的 img 镜像和自定义写盘脚本集成到 Live 系统中，并一起打包进 `filesystem.squashfs` 文件系统。

`filesystem.squashfs` 会在打包过程中压缩内容，因此可以在保留完整安装环境和目标镜像的同时，尽量控制最终 ISO 体积。

最后将新的 `filesystem.squashfs` 及相关启动文件重新打包为 ISO，用于虚拟机、软路由、迷你主机和 NAS 等 x86-64 设备启动安装。

## 开源说明

本项目延续上游项目的开源方式，代码保持 MIT 协议。

## 适用场景

| 场景 | 用法 |
| --- | --- |
| 虚拟机 | 直接选择 ISO 启动 |
| 物理机 | 建议通过 Ventoy U 盘启动 |
| 软路由 / 迷你主机 / NAS | 从 ISO 启动后写入目标磁盘 |

## 快速使用

1. 下载 Release 中的 ISO 文件。
2. 虚拟机直接挂载 ISO，物理机建议放入 Ventoy U 盘。
3. 从 ISO 启动进入 Debian Live 安装器。
4. 在安装器所在系统里输入 `ddd` 命令，即可调出安装菜单：

```bash
ddd
```

## 默认信息

安装器 Debian Live 系统：

```text
用户: root
密码: 1234
```

安装后的 Debian 13.5 系统：

```text
用户: root
密码: 1234
Web 地址: 接好网线后查看屏幕提示
```

## 注意事项

- 写盘或安装会覆盖目标磁盘数据，操作前请确认磁盘。
- ISO 镜像请放在 GitHub Releases，不要直接提交到 Git 仓库。
- 仓库只保存说明、许可证和忽略规则。
- 如果重新制作 ISO，请同步更新 Release 附件。
