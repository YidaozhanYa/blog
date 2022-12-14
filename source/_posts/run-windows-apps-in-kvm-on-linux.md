---
title: ð  ä½¿ç¨ KVM å¨ Linux ä¸æ ç¼è¿è¡ Windows åºç¨
date: 2022-04-20 21:40:40
tags:
- KVM
- Linux
category: Archæè¾è®°
cover: 'http://imgsrc.baidu.com/super/pic/item/d009b3de9c82d15863d0d864c50a19d8bd3e4291.jpg'
---

**çåé¡»ç¥ï¼ä¸æ¯æå¾å½¢å é**

å¨æ¥ç¨ Linux çè¿ç¨ä¸­ï¼æ»æå¿é¡»ä½¿ç¨æäº Windows ç¬å è½¯ä»¶ï¼æ¯å¦ Microsoft 365ãAdobe å¨å®¶æ¡¶ãFL Studio ç­ï¼çåºæ¯ï¼è¿æ¶åå¤§é¨åäººä¼éæ©åç³»ç»ï¼å¶å®èææºä¹å¯ä»¥è§£å³ï¼å¹¶ä¸å¯è½ä½éªæ´å¥½ã

ææé¢è§ï¼![p](http://imgsrc.baidu.com/super/pic/item/d009b3de9c82d15863d0d864c50a19d8bd3e4291.jpg)
![p](http://imgsrc.baidu.com/super/pic/item/241f95cad1c8a786086ecbdb2209c93d71cf509b.jpg)

[KVM](https://baike.baidu.com/item/KVM%E8%99%9A%E6%8B%9F%E6%9C%BA/11016451?fr=aladdin) æ¯ Linux åæ ¸èªå¸¦çèæåæ¨¡åï¼æçå¾é«ï¼å¯ä»¥ä½¿ç¨ libvirt è¿è¡ç®¡çï¼éå RDP å¯ä»¥å®ç°æ ç¼è¿è¡ Windows åºç¨ã
æ¬æå°ä½¿ç¨ WinApps èæ¬éç½® RDPã

#### 0ãéç½®ç¡¬ä»¶èæåå¹¶ä¸è½½å¥½æéæä»¶

å³äºå¦ä½å¼å¯ç¡¬ä»¶èæåï¼è¯·èªè¡ç¾åº¦ã

é¦åéè¦ä¸ä¸ª Win10 çéåï¼æ°çå¯è½æ æ³ä½¿ç¨ VirtIO Windows é©±å¨ç¨åºï¼æä»¥è¿éææ¨è LTSC2019 çï¼ï¼è¿éè¦ [VirtIO Windows é©±å¨ç¨åº](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/archive-virtio/virtio-win-0.1.217-1/virtio-win.iso) éåã

ä¹ååé WinApps èæ¬ç Git ä»åºã

```bash
git clone https://github.com/Fmstrat/winapps
```

#### 1ãå®è£æéè½¯ä»¶å¹¶éç½® libvirt æé

```bash
sudo pacman -S libvirt qemu edk2-ovmf freerdp
sudo systemctl enable --now libvirtd virtstoraged virtnetworkd
```

```bash
sudo sed -i "s/#user = "root"/user = "$(id -un)"/g" /etc/libvirt/qemu.conf
sudo sed -i "s/#group = "root"/group = "$(id -gn)"/g" /etc/libvirt/qemu.conf
sudo usermod -a -G kvm $(id -un)
sudo usermod -a -G libvirt $(id -un)
sudo systemctl restart libvirtd
sudo ln -s /etc/apparmor.d/usr.sbin.libvirtd /etc/apparmor.d/disable/ # å¦ææ AppArmor çè¯
sudo echo 'unix_sock_group = "libvirt"' >> /etc/libvirt/libvirtd.conf
sudo echo 'unix_sock_rw_perms = "0770"' >> /etc/libvirt/libvirtd.conf
echo "export LIBVIRT_DEFAULT_URI=qemu:///system" >> ~/.xprofile
export LIBVIRT_DEFAULT_URI=qemu:///system
sudo systemctl restart libvirtd
```

```bash
virsh net-list --all # å¦æçè§è¡¨ä¸­æ default åç»§ç»­ï¼å¦åéå¯
virsh net-autostart default
virsh net-start default
```

#### 2ãå®è£ Win10 èææºå¹¶éç½®å¥½è¿ç¨æ¡é¢

æ­¤å¤çç¥ï¼å¯ä»¥æç§ [WinApps å®æ¹è¯´æ](https://github.com/Fmstrat/winapps/blob/main/docs/KVM.md) è¿è¡æä½ã

æ³¨æï¼ä¸»æºåéè¦ä¸º RDPWindowsï¼å¹¶ä¸æå¥½è¦æå¯ç ã

#### 3ãéç½® WinApps

æç§ç¬¬äºæ­¥éç½®å¥½èææºä¹åï¼å¨èææºä¸­å®è£ [SPICE Guest Tools](https://www.spice-space.org/download/windows/spice-guest-tools/spice-guest-tools-latest.exe)ï¼å¯ä»¥ä½¿é¼ æ æ´å æµçã

ç¨ææ¬ç¼è¾å¨æå¼ ``~/.config/winapps/winapps.conf``ï¼è¥æä»¶å¤¹ä¸å­å¨å°±èªè¡åå»ºï¼ï¼å å¥å¦ä¸åå®¹ï¼

```bash
RDP_USER="ç¨æ·å"
RDP_PASS="å¯ç "
#RDP_SCALE=100 #å¯éï¼å¯ä»¥æ¹ä¸ºæéç¼©æ¾æ¯ï¼å¦ 125
#MULTIMON="true" #å¦æä¸ºå¤æ¾ç¤ºå¨å°±å¼å¯æ­¤è¡
```

å¦æä½ è¿å¼çèæç³»ç»ç®¡çå¨ï¼å°±ä»èææºä¸­æ³¨éï¼å³æç®¡çå¨ï¼ä½¿èææºå¨åå°è¿è¡ãç¶å cd å° WinApps ä»åºæä»¶å¤¹ï¼æ§è¡å¦ä¸å½ä»¤ï¼

```bash
./bin/winapps check
```

å¦æå¼¹åºä¸ä¸ª RDP è¿ç¨æ¡é¢ï¼åè¯´ææ²¡é®é¢äºï¼å¯ä»¥è¿è¡ä¸ä¸æ­¥ã

#### 4ãå¨èææºä¸­å®è£éè¦è¿è¡çè½¯ä»¶

#### 5ãéç½®å¿«æ·æ¹å¼ï¼desktopï¼

cd å° WinApps ä»åºæä»¶å¤¹ï¼æ§è¡ `./installer.sh` ï¼è¿ä¼èªå¨å¨å®¿ä¸» Linux ç³»ç»ä¸­åå»ºèææºåè½¯ä»¶çå¿«æ·æ¹å¼ã

#### 6ãåç»­ç»´æ¤

å¦æä½ åç»­åå®è£äºè½¯ä»¶ï¼å¹¶ä¸è¯¥è½¯ä»¶ [å¨æ¯æåè¡¨ä¸­](https://github.com/Fmstrat/winapps) ææå¼å§èåå¿«æ·æ¹å¼ï¼åè¿å¯ä»¥è¿è¡ `installer.sh` ï¼ä¼éæ°éç½®ææå¿«æ·æ¹å¼ï¼åæ¬ä»¥åçåæ°çï¼ãå¦æåç»­å®è£çè½¯ä»¶æ²¡æå¿«æ·æ¹å¼ï¼åå¯ä»¥å»ºç«ä¸ä¸ª shell èæ¬ï¼åå®¹ä¸º

```bash
#!/bin/sh
$HOME/.local/bin/winapps manual "exeå¨èææºä¸­çè·¯å¾"
```

ä¹åæ§è¡è¿ä¸ªèæ¬å³å¯ã

#### éå½ï¼å¾å½¢ä¼å

å¦æé¨åè½¯ä»¶ä¸è½å¨ Microsoft åºæ¬æ¾ç¤ºééå¨ä¸­è¿è¡ï¼å¯ä»¥ä½¿ç¨ Mesa 3D ç llvmpipe æ¸²æå¨è¿è¡æ¸²æã

å¯ä»¥å¨ [è¿é](https://fdossena.com/?p=mesa/index.frag) ä¸è½½ Mesa 3D For Windowsã

å¦æåªéè¦é¡¶æ¿ OpenGL æ¸²æå¨ï¼å¨ exe ä½ç½®æ¾å¥ opengl32.dll å³å¯ã

å¦æè¿éè¦é¡¶æ¿ Direct3D æ¸²æå¨ï¼åè¿éè¦ä¸è½½ [WineD3D For Windows](https://fdossena.com/?p=wined3d/index.frag)ï¼å¹¶æç§åç¼©å README åçè¯´æ³æ¾ç½® dllï¼opengl32.dll ä¹è¦æ¾è¿å»ï¼ã

#### éå½ï¼ä¸äºå¸¸ç¨å½ä»¤

```bash
virsh start RDPWindows #å¯å¨èææº
virsh shutdown RDPWindows #å³é­èææº
virsh net-dhcp-leases default |grep RDPWindows |awk '{print $5}' #æ¥çèææºç IP å°å
```

æäºèææºç IP å°åï¼å°±å¯ä»¥éç½® SMB å±äº«ï¼å¶å®èæ¬å·²ç»å±äº«äºä½ çå®¶ç®å½ï¼ç­æå¡ã

