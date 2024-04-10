---
layout: post
title:  "【vmware】绕过虚拟机检测——为VMware虚拟机Bypass Virtual Machine detection for a windows 10 VMware"
date:  2022-07-27 00:16:54
categories: vmware 
tags: 
excerpt: .
mathjax: true
---

Tools:

(1)[winhex.zip](https://github.com/CheungPro/CheungPro.github.io/files/9194328/winhex.zip) 

(2)[PhoenixBIOS.zip](https://github.com/CheungPro/CheungPro.github.io/files/9194329/PhoenixBIOS.zip)

不同的软件可能使用了不同的方法以躲避检测，本文以VMware15软件为例，不同版本之间，软件或许会有所差异。**特别提示：请务必先将修改的文件进行备份，以防因意外导致的虚拟机无法启动。

# 对VMware软件作出修改

首先，找到vmware路径下的`C:\Program Files (x86)\VMware\VMware Workstation\x64`目录下的文件`BIOS.440.ROM`和`vmware-vmx.exe`。

使用winhex软件打开`vmware-vmx.exe`，搜索字符串`NVMe Disk`（视实际虚拟机设备管理器中的硬盘设备决定，可能具有差异）

![image](https://user-images.githubusercontent.com/63193298/181669198-875b388d-2294-43ce-aa61-a8fa56a12117.png)

该文件保存后，复制到原路径。

# 对虚拟机进行修改

使用PhoenixBIOS软件（可能需要在兼容模式下运行，Windows98操作系统），打开并编辑文件`BIOS.440.ROM`。请将下图黄色区域的文字进行修改。修改后不要保留VMware字样。

![image](https://user-images.githubusercontent.com/63193298/181669516-6ed89443-3d43-4541-a76b-2c4ee38f23b3.png)

该文件保存后，另存到虚拟机路径。可以重命名为`1.ROM`。
![image](https://user-images.githubusercontent.com/63193298/181669717-d2ba8bb8-c826-4626-9f50-9a835c7eb2ae.png)

找到该路径的后缀为`.vmx`的文件，添加以下代码

```

SMBIOS.noOEMStrings = "TRUE"
isolation.tools.getPtrLocation.disable = "TRUE"
isolation.tools.setPtrLocation.disable = "TRUE"
isolation.tools.setVersion.disable = "TRUE"
isolation.tools.getVersion.disable = "TRUE"
monitor_control.disable_directexec = "TRUE"
monitor_control.disable_chksimd = "TRUE"
monitor_control.disable_ntreloc = "TRUE"
monitor_control.disable_selfmod = "TRUE"
monitor_control.disable_reloc = "TRUE"
monitor_control.disable_btinout = "TRUE"
monitor_control.disable_btmemspace = "TRUE"
monitor_control.disable_btpriv = "TRUE"
monitor_control.disable_btseg = "TRUE"
monitor_control.restrict_backdoor = "TRUE"
scsi0:0.productID = "Xiaomi 12S Ultra"
scsi0:0.vendorID = "Xiaomi 12S Ultra"
bios440.filename ="1.ROM"

cpuid.1.ecx = 01111110110110000011001000001011
cpuid.1.edx = 00010111100010111111101111111111
cpuid.80000000.0.ebx="0111:0101:0110:1110:0110:0101:0100:0111"
cpuid.80000000.0.ecx="0110:1100:0110:0101:0111:0100:0110:1110"
cpuid.80000000.0.edx="0100:1001:0110:0101:0110:1110:0110:1001"
cpuid.80000001.0.eax="0000:0000:0000:0000:0000:0000:0000:0000"
cpuid.80000002.0.eax="0110:0101:0111:0100:0110:1110:0100:1001"
cpuid.80000002.0.ebx="0010:1001:0101:0010:0010:1000:0110:1100"
cpuid.80000002.0.ecx="0110:1100:0110:0101:0100:0011:0010:0000"
cpuid.80000002.0.edx="0110:1110:0110:1111:0111:0010:0110:0101"
cpuid.80000003.0.eax="0010:0000:0010:1001:0101:0010:0010:1000"
cpuid.80000003.0.ebx="0010:0000:0101:0101:0101:0000:0100:0011"
cpuid.80000003.0.ecx="0011:0010:0011:1000:0011:0001:0100:0111"
cpuid.80000003.0.edx="0010:0000:0100:0000:0010:0000:0011:0000"
cpuid.80000004.0.eax="0011:0000:0011:0111:0010:1110:0011:0010"
cpuid.80000004.0.ebx="0000:0000:0111:1010:0100:1000:0100:0111"
cpuid.80000004.0.ecx="0000:0000:0000:0000:0000:0000:0000:0000"
cpuid.80000004.0.edx="0000:0000:0000:0000:0000:0000:0000:0000"

monitor.virtual_mmu = "automatic"
monitor.virtual_exec = "automatic"


```

