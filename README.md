# ThinkPad T450s X250 T450 X1C3 Big Sur OpenCore 0.6.6
<img align="right" src="/picture/Thismachine.png" alt="Lenovo Thinkpad T450s macOS Hackintosh OpenCore" width="400">

[![macOS](https://img.shields.io/badge/macOS-11.2.1-blue)](https://developer.apple.com/documentation/macos-release-notes)
[![OpenCore](https://img.shields.io/badge/OpenCore-0.6.6-green)](https://github.com/acidanthera/OpenCorePkg)
[![ThinkPad](https://img.shields.io/badge/ThinkPad-T450s.X250.T450.X1C3-orange)](https://think.lenovo.com.cn/index.html)

**免责声明:**

作者：[@CLAY-BIOS](https://github.com/CLAY-BIOS)  
在开始之前，请阅读整个自述文件。
我对可能造成的任何损失不承担任何责任。
此仓库部分ACPI补丁由本人独立完成，使用和引用请注明出处。
如果您发现错误或有任何改进（无论是在配置中还是在文档中），请考虑打开问题或请求请求。
如果您发现我的工作有用，可以考虑点击右上角的⭐️Star。
这对我来说意义重大。 


## 简介
- 这是一个完整的ThinkPad T450s macOS + DW1820a Hackintosh 配置。
- 声卡默认 layout-id = 32，耳机杂音请使用声卡修复脚本(ALCPlugFix)。 
- 如果你想使用扩展坞上的音频接口，请将声卡 layout-id 设置为 55 ，选择线路输出。
- 支持触摸屏（带有多点触控和触屏手势）。
- 支持 Catalina。
- 支持 Mojave。
- 此仓库可适用于所有第五代ThinkPad，已经确认支持的型号如下：
- 支持 ThinkPad X250 ThinkPad T450 ThinkPad T450s ThinkPad X1 Carbon 3rd。

## 硬件信息
```  
- CPU：Intel Core i7-5600U i7-5500u i5-5300U i5-5200U

- 核心显卡：Intel HD 5500 Graphics 

- 声卡：ALC292

- 无线网卡：DW1820A   Intel 7265AC   Intel AX200
```
## 安装和BIOS设置

<details>  
<summary><strong>如何安装macOS </strong></summary>
</br>

1. [创建安装媒体](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/#making-the-installer)
1. 下载[最新的EFI文件](https://github.com/CLAY-BIOS/Lenovo-ThinkPad-T450s-Hackintosh-Big-Sur-OpenCore/releases) 并将其复制到ESP分区中
1. 从USB启动安装程序（按“ F12”选择启动盘），然后[开始安装过程](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html#booting-the-opencore-usb)

</details>

<details>  
<summary><strong>BIOS设置 </strong></summary>
</br>

**BIOS (1.37):**
-  Security -> Security Chip`: **Disabled**;
-  Memory Protection -> Execution Prevention`: **Enabled**;
-  Virtualization -> Intel Virtualization Technology`: **Enabled**;
-  Internal Device Access -> Bottom Cover Tamper Detection`: must be **Disabled**;
-  Anti-Theft -> Current Setting`: **Disabled**;
-  Anti-Theft -> Computrace -> Current Setting`: **Disabled**;
-  Secure Boot -> Secure Boot`: **Disabled**;
-  UEFI/Legacy Boot`: **UEFI Only**;
-  CSM Support`: **Yes**.

</details>

## 状态
<details>  
<summary><strong>什么有效 ✅</strong></summary>
</br>
 
- [x] CPU电源管理
- [x] Intel HD 5500 Graphics 
- [x] 完整的USB
- [x] 摄像头
- [x] 休眠/唤醒/关机/重启
- [x] 英特尔千兆以太网  （连接扩展坞后无法使用笔记本上的以太网接口）
- [x] Wi-Fi，蓝牙，空投投送，切换，连续性  （使用intel- Wi-Fi将导致某些功能不可用）
- [x] iMessage, FaceTime, App Store, iTunes Store
- [x] 扬声器和耳机插孔
- [x] 电池和完整的电池信息  
- [x] 键盘地图和热键 [ThinkpadAssistant](https://github.com/MSzturc/ThinkpadAssistant) 
- [x] 触控板、小红点和物理按钮
- [x] 触摸屏 （带有多点触控和触屏手势）
- [x] mini DisplayPort
- [x] SD卡读卡器 
- [x] 扩展坞 USB
- [x] 扩展坞 以太网
- [x] 扩展坞 耳机插孔 （需要将声卡 layout-id 设置为 55 ）
- [x] 扩展坞 VGA
- [x] 扩展坞 DisplayPort
- [x] 扩展坞 DVI
- [x] 扩展坞 HDMI

</details>

<details>  
<summary><strong>什么不起作用 ⚠️</strong></summary>
</br>

- [ ] VGA
- [ ] Sidecar
- [ ] 指纹

</details>

<details>  
<summary><strong>Intel Wi-Fi</strong></summary>
</br>

### 驱动一：
- AirportItlwm.kext。
- 以将AirportItlwm.kext添加到项目中，根据自己的系统版本勾选，默认为Big Sur。
- 隔空投送不可用。使用AirportItlwm.kext可能导致触控板和蓝牙出现问题。
- 不讨论Intel Wi-Fi的问题，因为驱动程序不稳定。
- 参考:  https://github.com/OpenIntelWireless/itlwm
![AirportItlwm](./picture/AirportItlwm.png)

 ### 驱动二：
- AirPortOpenBSD.kext
- 隔空投送、接力、连续性不可用，使用AirPortOpenBSD.kext不会出现触控板和蓝牙问题。
- 感兴趣的朋友可以自己下载尝试。
- 参考:  https://github.com/a565109863/AirPortOpenBSD

</details>

<details>  
<summary><strong>关于扩展坞</strong></summary>
</br>

- 使用扩展坞会导致睡眠出现问题，解决方法是在 config.plist->ACPI 中勾选 SSDT-IGBE 补丁。
- 使用 SSDT-IGBE 补丁无法使用翻盖模式。
- 扩展坞已完美适配，但还需要一些测试。
![Docking](./picture/Docking.png)

</details>

<details>  
<summary><strong>ThinkPad助手(ThinkpadAssistant)</strong></summary>
</br>

- 可让你在Thinkpad T450s X250 T450笔记本电脑上使用所有功能键。
- 复制ThinkpadAssistant到应用程序文件夹。
- 启动ThinkpadAssistant，并在菜单栏中勾选“登录时启动”。
- F4：麦克风静音/取消静音（带有状态LED指示）。
- F7：屏幕镜像/屏幕扩展。
- F8：启用/停用Wi-Fi。
- 左Shift + F8键：启用/停用蓝牙。
- F9：打开系统偏好设置。
- F12：打开启动板。
- FN + Space：切换键盘背光。
- FN + 4：睡眠快捷键。
（睡眠过程中再次按下睡眠快捷键即可终止睡眠。）
（连接外部显示器时，按睡眠按钮后，工作屏幕变为外部显示器（内部屏幕关闭）；再按一次睡眠按钮，内部和外部显示器恢复正常。）
- PrtSc 映射到 F13：可在系统偏好设置-->键盘-->快捷键将它设置为截图。

</details>

<details>  
<summary><strong>启用风扇和LED控制</strong></summary>
</br>

1. 下载并安装 [YogaSMC-App-Release.dmg](https://github.com/zhen-zen/YogaSMC/releases) 
1. 打开应用程序
1. 勾选“登录后启动”选项

</details>

<details>  
<summary><strong>一键开启Hi-DPI</strong></summary>
</br>

1. 参考:   https://github.com/xzhih/one-key-hidpi

</details>



> # 学分

- [@benbender](https://github.com/benbender/x1c6-hackintosh/blob/experimental/EFI/OC/dsl/SSDT-BATX.dsl) 新一代电池补丁。
- [@zhen-zen](https://github.com/zhen-zen) for YogaSMC。
- [daliansky/OC-little](https://github.com/daliansky/OC-little) 各种ACPI热补丁样本。 
- [@xzhih](https://github.com/xzhih) 一键开启Hi-DPI。 
- [@cholonam](https://github.com/cholonam/Sinetek-rtsx) 读卡器修复。 https://github.com/cholonam/Sinetek-rtsx/pull/18
- [@MSzturc](https://github.com/MSzturc/ThinkpadAssistant) ThinkPad助手。
- [@zxystd](https://github.com/OpenIntelWireless/itlwm) Intel Wi-Fi Drivers for macOS。

非常感谢 [Acidanthera](https://github.com/acidanthera) 团队，如果没有他们的工作，这将是不可能的。

欢迎提问，但请不要问太低级的问题。
