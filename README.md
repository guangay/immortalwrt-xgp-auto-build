# NLnet XiGuaPi V3 (西瓜皮V3) Immortalwrt 自动构建

[![Build and Release](https://github.com/zzzz0317/immortalwrt-xgp-auto-build/actions/workflows/build.yml/badge.svg)](https://github.com/zzzz0317/immortalwrt-xgp-auto-build/actions/workflows/build.yml)

# 正在开发与调试中，小白误用
[https://github.com/guangay/immortalwrt-xgp-auto-build/blob/main/QQ20260430-172451.png]
## 已知问题

1. 通过转接板连接的 PCIe 5G 模块在刷机后需要断电（直接拔DC插头，拔市电那头要多等几秒电容放电）一次，否则大概率找不到模块，转接板硬件原因导致模块在重启时不能正常下电。
2. 第一次使用本固件时，请使用 RKDevTool 刷入。请勿从其他固件的系统内直接升级到此固件，大概率会不兼容，包括同作者提供的 [LEDE 固件](https://github.com/zzzz0317/lede-xgp-auto-build/)。
3. 没有使用 RKDevTool 的条件的话，从其它固件升级，请不要在页面中直接升级，可以尝试 `dd` 命令，先进入网页管理->系统->启动项，禁用 docker、qmodem、openclash、passwall 等不影响系统启动、联网的服务，然后重启，使用 SSH 连接设备，将刷机包传输至 `/tmp` 目录，然后使用 `gzip -d immortalWrt-nlnet_xiguapi-v3-xxxx-squashfs-sysupgrade.img.gz` 命令解压 `.img.gz` 格式的固件为 `.img`，然后执行 `dd if=/tmp/immortalWrt-nlnet_xiguapi-v3-xxxx-squashfs-sysupgrade.img of=/dev/mmcblk0 bs=4M oflag=direct`（注意替换文件名），显示 `XXX+0 records in XXX+0 records out` 并可以执行新命令后，不要执行任何操作，直接拔电源重启，大概率能成功，不成功就只能用 RKDevTool 救了，**非常不建议使用本方案**。

## 说明

1. 第一次使用建议通过 RKDevTool 刷入，若通过 Web 刷入时提示不兼容请做好 USB 救砖准备再尝试
2. [Actions](https://github.com/zzzz0317/immortalwrt-xgp-auto-build/blob/main/.github/workflows/build.yml) 在北京时间每周五凌晨2点自动拉取 [Immortalwrt](https://github.com/immortalwrt/immortalwrt) 代码编译并发布，平时可能会不定期手动触发更新
3. 默认 Wi-Fi SSID: `XGP`，密码: `88888889`
4. 默认 LAN 接口地址: `10.10.10.1`
5. 默认 root 密码:password 
6. 使用 PCIe 模块在刷机后建议断一次电
7. 移除了对istore的首页和网络向导，以及其他的对istore首页的依赖
8. 添加了对第三发屏幕驱动的支持，支持更多的屏幕自定义[https://github.com/junhong-l/xgp-v3-screen]
9. 添加对imm稳定版的支持
10. 已知bug，通过转接板连接的 PCIe 5G 模块在刷机后需要断电（直接拔DC插头，拔市电那头要多等几秒电容放电）一次，否则大概率找不到模块，转接板硬件原因导致模块在重启时不能正常下电。
    MBIM 模式若无法正常拨号请在 QWRT模组管理 -> 拨号总览 -> 模组配置 -> 高级设置 中指定 APN，。第一次启动检测到 T99W373 模块时会自动禁用 QModem 拨号以防止产生巨量日志（MBIM 模式自动拨号找不到 APN），请您在适当调整 设置后手动启用。
    7916国产版本无法开启160hz，否则无线模块会无限重启
## ⚠️ 免责声明

1. **项目性质说明**  
   本项目在 GitHub Actions 自动编译过程中：
   - 实时拉取 [Immortalwrt](https://github.com/immortalwrt/immortalwrt) 源码，和其它组件源码
   - 仅添加本仓库中的**公开可审查内容**

2. **设备风险自担**  
   - 任何因使用本项目固件导致的设备故障/变砖/安全问题
   - 任何因配置不当产生的网络风险或数据损失
   - 任何因第三方源码更新引发的兼容性问题
   **均与项目作者无关**，使用者需自行承担全部风险。


