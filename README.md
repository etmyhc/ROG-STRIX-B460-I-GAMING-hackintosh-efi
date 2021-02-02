# ROG STRIX B460-I GAMING-hackintosh efi

* 此efi基于ROG STRIX B460-I GAMING制作，使用OpenCore (0.6.5 release)，已安装macOS Catalina 10.15.7。 制作流程参考 [Dortania Guide](https://dortania.github.io/OpenCore-Install-Guide/) 中 [Comet Lake](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#starting-point) 部分。

* 此efi为仅可启动版本，请勿作为正式用途，使用此efi发生的损失及后果自行承担。

* 运行情况：暂未配置GUI，AX200基本可用（有概率断连或重启后不可用），所有后面板USB可使用, 启动后自动向BIOS添加opencore启动项，防止windows篡改。

* This efi do not have a series number / ROM and ralated info, please DIY !!!

* 此efi文件不包含序列号/网卡等相关信息，请自行补足！！！

## 硬件

* 主板: ROG STRIX B460-I GAMING (BIOS 1003)
* WiFi 模组: 板载AX200 (可驱动)
* CPU: Intel Core i5-10900 es (QTB1)
* 散热: 利民axp-90i-纯铜版
* 显卡1: Intel UHD630 
* 显卡2: Radeon™ Pro WX 8200 (由Radeon RX Vega⁵⁶修改BIOS)
* 内存: 科赋 Bolt X DDR4 3600MHz 16G*2
* 存储: 三星 SM961 512G
* 机箱: ZS-A4S V3

## 安装

### 0. BIOS设置

#### 关闭
* Secure Boot
* CFG Lock
* VT-d (can be enabled if you set DisableIoMapper to YES)
* Intel SGX
* Fast Boot
* CSM

#### 启用
* VT-x
* DVMT Pre-Allocated(iGPU Memory): 64MB
* OS type: Windows 8.1/10 UEFI Mode
* EHCI/XHCI Hand-off
* Hyper-Threading
* SATA Mode: AHCI
* Above 4G decoding

### 1. SSDTs
已按照 ROG STRIX B460-I GAMING 定制SSDT-USBX，其他都是现成下载的。

* SSDT-AWAC
* SSDT-EC-USBX-DESKTOP
* SSDT-PLUG-DRTNIA
* SSDT-RHUB
* SSDT-USBX

### 2. Kexts

* AirportItlwm.kext
* AppleALC.kext
* CpuTscSync.kext
* IntelBluetoothFirmware.kext
* IntelBluetoothInjector.kext
* IntelMausi.kext
* Lilu.kext
* NVMeFix.kext
* SMCProcessor.kext
* SMCSuperIO.kext
* USBMap.kext
* VirtualSMC.kext
* WhateverGreen.kext


### 3. USB
此主板有两个USB控制器，我选购的机箱没有前置USB面板，因此只使用了后置USB面板，是intel的控制器。

### 4. config.plist中需要手动修改的地方


参考 [Dortania guide](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html) 进行设置

 
#### PlatformInfo
* 我使用的SMBIOS为iMac20,2，具体情况参考：

| SMBIOS | CPU型号 |
|---|---|
| iMac20,1 | i7-10700K或更低(ie. 8核心及以下) |
| iMac20,2 | i9-10850K或更高(ie. 10核心及以上) |

* 用户需要使用 [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) 生成Type, Serial, Board Serial, SmUUID, 填入config.plist

| GenSMBIOS提供 | config.plist中对应 |
|---|---|
| Type | SystemProductName |
| Serial | SystemSerialNumber |
| Board Serial | MLB |
| SmUUID | SystemUUID |

* ROM 中需要填写 电脑网卡的MAC地址,不需要：(冒号)，格式为连续的12位数字字母组合



### 参考
* [Dortania Configuration](https://dortania.github.io/docs/latest/Configuration.html)
* [asus-rog-strix-b460I-hackintosh](https://github.com/roederja/asus-rog-strix-b460I-hackintosh)
* [ROG_B460i_Hackintosh](https://github.com/polarisink/ROG_B460i_Hackintosh#i5-10600--rog-b460i-%E6%A0%B8%E6%98%BE-hackintosh-efi)
* [ASUS ROG STRIX B460-I GAMING 评测](https://www.chiphell.com/article-24505-1.html)
