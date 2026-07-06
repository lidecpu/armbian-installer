# Armbian Installer Debian 13.5

这是基于 wukongdaily 的 Armbian Installer x86_64 ISO 修改的 Debian 13.5 版本。

主要改动是把安装器底层 Debian Live 环境更新为 Debian 13.5，使用方式保持原 Armbian 安装器逻辑。

## 下载

ISO 文件不放在 Git 仓库里，请从 GitHub Releases 下载：

https://github.com/lidecpu/armbian-installer/releases

当前 ISO 文件：

```text
armbian-debian13.5.iso
```

文件大小：

```text
611,983,360 bytes
```

SHA256：

```text
61237004FE777DADA62779BE801D1942C599F39453DC7AB91F3C08A3EE8D02F1
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

## 使用方式

虚拟机：

```text
直接选择 armbian-debian13.5.iso 启动
```

物理机：

```text
建议使用 Ventoy U 盘启动 ISO
```

启动进入安装器系统后，根据屏幕提示操作。

如需进入安装菜单，在安装器系统内执行：

```bash
ddd
```

## 默认信息

安装器 Debian Live 系统：

```text
用户: root
密码: 1234
```

安装后的 Armbian 系统：

```text
用户: root
密码: 1234
Web 地址: 接好网线后查看屏幕提示
```

## 说明

- 仓库只保存脚本、说明和构建配置。
- ISO 镜像请放在 GitHub Releases，不要直接提交到 Git。
- 如果重新制作 ISO，请同步更新文件名、大小和 SHA256。
- 写盘或安装会覆盖目标磁盘数据，操作前请确认目标磁盘。

## 项目来源

本仓库基于以下 ISO 修改，当前版本主要更新为 Debian 13.5：

```text
https://github.com/wukongdaily/img-installer/releases/tag/Armbian-Installer-x86_64-ISO
```
