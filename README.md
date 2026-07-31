# OpenWrt2026 — 自动编译带 OpenClash + Nikki/Mihomo + Momo/Sing-box 的固件

一键编译 OpenWrt x86-64 固件，预装 **OpenClash**、**Nikki/Mihomo**、**Momo/Sing-box** 和 **OpenAppFilter**，通过 GitHub Actions 自动构建。

## 特性

- ✅ **OpenClash** — 图形化代理管理面板
- ✅ **Nikki/Mihomo** — Mihomo 透明代理管理组件
- ✅ **Momo/Sing-box** — Sing-box 透明代理管理组件
- ✅ **OpenAppFilter** — 应用识别和家长控制
- ✅ **简体中文界面**
- ✅ 常用工具：`curl`, `htop`, `iperf3`, `nano`, `tcpdump`
- ✅ USB 3 支持
- ✅ 固定 OpenWrt 24.10 和第三方 feed 提交，保证构建可复现
- ✅ 每 7 天自动重建（可手动触发）
- ✅ 固件产物自动上传为 Artifacts

## 使用方法

### 方式一：手动触发

1. Fork 或 Push 到这个仓库
2. 打开 GitHub → **Actions** → **Build OpenWrt with OpenClash + Nikki/Mihomo + Momo/Sing-box + OAF**
3. 点击 **Run workflow**
4. 等约 1.5-2 小时编译完成
5. 在 workflow run 页面下载 **Artifacts**

### 方式二：Push 自动触发

每次 push 到 `master` 分支自动触发编译。

## 输出固件

编译完成后在 Artifacts 里下载 `openwrt-x86-64`，包含：

- `openwrt-x86-64-generic-ext4-combined.img.gz` — 写盘用（推荐）
- `openwrt-x86-64-generic-rootfs.tar.gz` — 容器用
- `openwrt-x86-64-generic-squashfs-combined.img.gz` — 升级用
- 所有 IPK 包（可单独安装）

## 写盘方法

```bash
# 解压
gunzip openwrt-x86-64-*-ext4-combined.img.gz

# 写入 U 盘或硬盘（替换 /dev/sdX 为你的设备）
sudo dd if=openwrt-x86-64-*-ext4-combined.img of=/dev/sdX bs=4M status=progress
```

首次启动后：
- LAN 地址：`10.0.0.2`
- 用户名：`root`，无密码

## 自定义

修改 `.github/workflows/build.yml` 中的 `CONFIG_PACKAGE_*` 配置可以增删软件包，推送后会自动编译新固件。OpenWrt 源码和第三方 feed 均使用 workflow 中固定的提交；升级依赖时应同步更新并验证包名。
