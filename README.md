# eNSP-install-win
华为 eNSP 网络模拟器 Windows 所需的安装包及简单安装指南，


## 📦 包含文件

| 文件 | 版本 | 大小 | 说明 |
|------|------|------|------|
| `WinPcap_4_1_3.exe` | 4.1.3 | 894 KB | 网络抓包驱动 |
| `Wireshark-4.4.6-x64.exe` | 4.4.6 | 84 MB | 网络协议分析器 |
| `VirtualBox-5.2.44-139111-Win.exe` | 5.2.44 | 106 MB | 虚拟机（**必须是此版本**） |
| `eNSP-Setup.exe` | - | 543 MB | eNSP 主程序 |

> 所有文件请从 [Releases 页面](../../releases) 下载。

## ⚠️ 安装顺序（必须严格遵守）

```
① WinPcap 4.1.3
     ↓
② Wireshark 4.4.6
     ↓
③ VirtualBox 5.2.44
     ↓
④ eNSP
```

### 各步骤注意事项

#### ① WinPcap 4.1.3
- 直接安装，无特殊注意事项。

#### ② Wireshark 4.4.6
- 安装过程中会弹出界面询问是否安装 **Npcap**
- **🚫 千万不要勾选 Npcap！一定要取消勾选！**
- Npcap 与 WinPcap 冲突，会导致 eNSP 抓包功能异常

#### ③ VirtualBox 5.2.44
- **必须是 5.2.44 版本**，更高版本与 eNSP 不兼容
- 安装后不要升级

#### ④ eNSP
- 最后安装，会自动检测已安装的依赖

## 🖥️ 虚拟机嵌套运行

如果在虚拟机中运行 eNSP（eNSP 内会再启动 VirtualBox 虚拟机），需要开启：

- **嵌套虚拟化**（Nested VT-x/AMD-V）
- **允许 MAC 地址欺骗**（Promiscuous Mode: 全部允许）

### VMware 设置

```
虚拟机设置 → 处理器 → ✅ 虚拟化 Intel VT-x/EPT 或 AMD-V/RVI
虚拟机设置 → 网络适配器 → 高级 → MAC 地址欺骗 → 允许
```

### VirtualBox 设置

```bash
# 宿主机执行
VBoxManage modifyvm "VM名称" --nested-hw-virt on
```

## ❓ 常见问题

### 设备启动失败（AR 路由器 / 交换机）

1. 检查 VirtualBox 版本是否为 5.2.44
2. 以管理员身份运行 eNSP
3. 检查是否开启了 Windows Hyper-V（与 VirtualBox 冲突）

### 抓包无数据

1. 确认安装了 WinPcap 而非 Npcap
2. Wireshark 安装时是否取消勾选了 Npcap
3. 尝试重装 WinPcap → Wireshark（按顺序）

### VirtualBox 无法启动虚拟机

```bash
# 关闭 Hyper-V（管理员 PowerShell）
bcdedit /set hypervisorlaunchtype off
# 重启电脑
```

## 📄 许可

本仓库仅提供安装包合集和安装指南。各软件版权归各自原作者所有：

- WinPcap: [WinPcap 许可](https://www.winpcap.org/)
- Wireshark: [GPL-2.0](https://www.wireshark.org/)
- VirtualBox: [GPL-2.0](https://www.virtualbox.org/)
- eNSP: 华为技术有限公司
