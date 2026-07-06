<div align="center">

# Armbian Installer Debian 13.5

基于 Debian Live 的 x86-64 img 镜像安装器，用于快速安装 Debian 13.5。

[![Debian](https://img.shields.io/badge/Debian-13.5-A81D33?logo=debian&logoColor=white)](https://www.debian.org/)
[![Platform](https://img.shields.io/badge/Platform-x86--64-2F6FED)](#适用场景)
[![Release](https://img.shields.io/badge/Download-GitHub%20Releases-238636?logo=github)](https://github.com/lidecpu/armbian-installer/releases)
[![License](https://img.shields.io/badge/License-MIT-informational)](LICENSE)

</div>

## 简介

这是一个基于 wukongdaily 的 Armbian Installer x86_64 ISO 修改的 Debian 13.5 版本。

主要改动是把安装器底层 Debian Live 环境更新为 Debian 13.5，并保留原安装器的使用方式：启动 ISO 后，通过安装菜单把系统写入目标磁盘。

## 下载

ISO 文件不放在 Git 仓库里，请从 GitHub Releases 下载：

```text
https://github.com/lidecpu/armbian-installer/releases
```

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

## 项目来源

本仓库基于以下 ISO 修改，当前版本主要更新为 Debian 13.5：

```text
https://github.com/wukongdaily/img-installer/releases/tag/Armbian-Installer-x86_64-ISO
```
