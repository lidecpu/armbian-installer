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

随着软路由、迷你主机、NAS 和虚拟机逐渐普及，越来越多 x86-64 设备也开始使用这类 img 系统。但传统烧录方式在 x86-64 场景下不够直观，通常还需要额外准备 PE、手动传递固件文件或执行写盘命令，流程容易变得低效和复杂。

本项目的目标是把这类安装流程做得更接近普通系统安装：从 ISO 启动，进入 Debian Live 环境，然后通过安装菜单把 Debian 13.5 写入目标磁盘。

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
4. 根据屏幕提示操作。
5. 如需打开安装菜单，执行：

```bash
ddd
```

## 校验

Windows PowerShell：

```powershell
Get-FileHash .\armbian-debian13.5.iso -Algorithm SHA256
```

Debian / Linux：

```bash
sha256sum armbian-debian13.5.iso
```

校验值一致后再写入 U 盘或安装到磁盘。

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
- 如果重新制作 ISO，请同步更新 Release 附件和校验信息。
