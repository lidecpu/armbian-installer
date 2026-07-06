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

它把 Debian Live、目标 img 镜像和写盘脚本打包成 ISO。启动 ISO 后，在安装器系统里输入 `ddd` 调出菜单，即可把 Debian 13.5 写入目标磁盘。

相比 NAS 或虚拟机直接导入 img，本安装器不会把磁盘容量锁死在原 img 大小内。安装前可以自行设置目标磁盘容量，后续升级、替换或扩展更灵活。

本项目基于 [debian-live](https://github.com/dpowers86/debian-live) 制作，代码保持 MIT 协议。

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
直接进入 root 环境，无需输入密码
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
