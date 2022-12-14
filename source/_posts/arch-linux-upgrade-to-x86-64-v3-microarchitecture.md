---
title: "ð ç» Arch Linux ãå¤§èåçº§ãå° x86-64-v3 æ¶æï¼è·å¾æ§è½æå"
date: 2022-08-11 22:19:00
tags:
- Arch Linux
category: Archæè¾è®°
cover: 'https://imgsrc.baidu.com/super/pic/item/7a899e510fb30f241d999ac28d95d143ac4b03eb.jpg'
---

[x86-64-v3](https://en.wikipedia.org/wiki/X86-64#Microarchitecture_levels) æ¯ x86-64 å¤çå¨æ¶æçä¸ä¸ªãå¾®æ¶æãï¼æ­è½½äº Haswell åå¶ä¹åçå¤çå¨ï¼å¶æ¯æ AVX2 ç­æ°æä»¤éãæ®ä¼ å°ç¨åºç¼è¯ä¸º x86-64-v3 æ¶æå¯ä»¥è·å¾å¤§çº¦ 10% çæ§è½æå {% sup (ä¸ç¡®å®) %}ã

Arch Linux [æ¯æ](https://gitlab.archlinux.org/archlinux/rfcs/-/blob/master/rfcs/0002-march.rst) x86-64-v3 æ¶æï¼å æ­¤å°åæ ¸ãç¼è¯å¨ç­è½¯ä»¶åæ´æ¢ä¸º x86-64-v3 æ¶æå¯ä»¥æåæ§è½ï¼è½ç¶~~è¿æ¯ Gentoo åæ§çæä¼å¹²çäº~~ï¼ä½æä»¬ Arch ä¹å¯ä»¥å°è¯ä¸ä¸ã

<!--more-->

### â ï¸ æä½åé¡»ç¥

<font color="red">ç¨ç¬¬ä¸æ¹è½¯ä»¶ä»åºæ¿ä»£å®æ¹è½¯ä»¶ä»åºæé£é©ï¼è¯·è°¨ææ§è¡ï¼</font>

æ¬ææå°çç¬¬ä¸æ¹è½¯ä»¶ä»åºæ²¡æå½åéåæºï¼æä»¥éåº¦å¾æ¢ï¼è¯·ä½¿ç¨éæä»£çææé« `pacman.conf` ä¸­ç `ParallelDownloads` å¼ã

### ð æ£æ¥æ¯å¦æ¯æ x86-64-v3 æ¶æ

å¨ç»ç«¯ä¸­æ§è¡ `/lib/ld-linux-x86-64.so.2 --help | grep "x86-64-v"`ï¼å¦æè¾åºä¸­æ `x86-64-v3 (supported, searched)` å­æ ·ï¼å³ä»£è¡¨æ¯æ x86-64-v3 æ¶æã

### ðï¸ æ´æ¢ x86-64-v3 æ¶æè½¯ä»¶ä»åº

#### CachyOS

CachyOS æ¯ä¸ä¸ªåºäº Arch Linux çåè¡çï¼å¶ä½¿ç¨ x86-64-v3 æ¶æï¼å¹¶ä¸æä¾å¼å¯äº `-O3`ã`thinlto` ä¼åçè½¯ä»¶åã

- æ§è¡å¦ä¸å½ä»¤ï¼

  ```bash
  sudo pacman-key --recv-keys F3B607488DB35A47 --keyserver keyserver.ubuntu.com
  sudo pacman-key --lsign-key F3B607488DB35A47
  sudo pacman -U 'https://mirror.cachyos.org/repo/x86_64/cachyos/cachyos-keyring-2-1-any.pkg.tar.zst' 'https://mirror.cachyos.org/repo/x86_64/cachyos/cachyos-v3-mirrorlist-13-1-any.pkg.tar.zst'
  ```

- ç¼è¾ `/etc/pacman.conf`ï¼ç¨ `Architecture = x86_64 x86_64_v3` æ¿æ¢æåæç `#Architecture = auto`ï¼å¹¶å¨åçè½¯ä»¶ä»åº (coreãextraãcommunity) ä¸æ¹å å¥ `cachyos-v3` ä»åºï¼

  ```ini
  [cachyos-v3]
  Include = /etc/pacman.d/cachyos-v3-mirrorlist
  ```

#### ALHP

ALHP æ¯ç¤¾åºåèµ·ç x86-64-v3 è½¯ä»¶ä»åºï¼å¶æä¾ä½¿ç¨ x86-64-v3 æ¶æç¼è¯ï¼å¹¶å¼å¯äº `-O3` å `lto` ä¼åçè½¯ä»¶åãä½ä»æä¸äºè½¯ä»¶åæªè¢«å å¥æ­¤ä»åºï¼æ¯å¦ `vim`ï¼ï¼æä»¥ä¸è½å æåççä»åºï¼èæ¯å°æ­¤ä»åºæ¾å¨åçä»åºä¸æ¹ã

- ä» AUR å®è£ `alhp-keyring alhp-mirrorlist` è¿ä¸¤ä¸ªè½¯ä»¶åã

- ç¼è¾ `/etc/pacman.conf`ï¼å¨åçè½¯ä»¶ä»åº (coreãextraãcommunity) ä¸æ¹å å¥å¦ä¸åå®¹ï¼

  ```ini
  [core-x86-64-v3]
  Include = /etc/pacman.d/alhp-mirrorlist
  
  [extra-x86-64-v3]
  Include = /etc/pacman.d/alhp-mirrorlist
  
  [community-x86-64-v3]
  Include = /etc/pacman.d/alhp-mirrorlist
  ```

{% note color:red æ³¨æï¼ALHP ä»åºçæäºéè¦è½¯ä»¶åï¼æ¯å¦ `icu` `openssl`ï¼å¯è½ä¼æ´æ°ä¸åæ¶ï¼è¯·æ CachyOS æ¾å¨ ALHP ä¸æ¹ã %}

å¨æ·»å å®æä¹åï¼`sudo pacman -Syyu` å¼ºå¶å·æ°æ°æ®åºå¹¶æ´æ°ç³»ç»ãæ­¤æ¶ä½ çåæ ¸ä¹ä¼è¢«æ¿æ¢ä¸º x86-64-v3 æ¶æï¼æä»¥å¦æä½ ä½¿ç¨ `nvidia`ï¼å°±æ¢ä¸º `nvidia-dkms` (`virtualbox-host-modules-arch` ä¹éè¦æ¢ä¸º `virtualbox-host-dkms`)ï¼å¹¶ä¸è¿éè¦ [éå»ºå¼å¯¼éç½®](#â»ï¸-éå»ºå¼å¯¼éç½®æ³¨æäºé¡¹)ã

### ð¥ (å¯é) ä½¿ç¨ CachyOS çä¼ååæ ¸

- `linux-cachyos` åæ ¸ææ­è½½äºä¸åè°åº¦å¨çä¸åçæ¬ï¼å¯ä»¥å `sudo pacman -Ss linux-cachyos` æ¥çææçæ¬ï¼ä¹åéæ©å®è£ãå¦æä½ éæ©å°é¾çï¼ç´æ¥å®è£ `linux-cachyos linux-cachyos-headers` å°±å¥½ã

### ð¥ (å¯é) ä½¿ç¨ CachyOS çä¼å 32 ä½åº

CachyOS è½¯ä»¶ä»åºä¸­ï¼32 ä½åºä¹å¯ç¨äº `thinlto` ä¼åãç¡®ä¿ `cachyos-v3` å¨ `multilib` ä¸æ¹å³å¯ã

---

### ð¦ å¦ä½ç¼è¯åº x86-64-v3 è½¯ä»¶å

å¦æä½¿ç¨æ­£å¸¸ç make ç¼è¯ï¼åéè¦å å¥ `-march=x86-64-v3 -mtune=native` CFLAGSã

å¦æä½¿ç¨ Arch æå»ºç³»ç» makepkg ç¼è¯ (å¦ä» AUR å®è£è½¯ä»¶å)ï¼åéè¦æ´æ¹ makepkg éç½®æä»¶ã

é¦åæåç makepkg éç½®æä»¶å¤å¶å°ç¨æ·ç®å½ä¸ï¼

```bash
install -D /etc/makepkg.conf ~/.config/pacman/makepkg.conf
```

ä¹åç¼è¾ä¹ï¼

é¦åå° CFLAGS ä¸­ç `-march=x86-64 -mtune=generic` æ¹ä¸º `-march=x86-64-v3 -mtune=native`ã

å¦æææ´é«çæ§è½éæ±ï¼å¯ä»¥æ `-O2` æ¹ä¸º `-O3`ï¼ä¸è¿è¿ä¼å¯¼è´å°é¨åè½¯ä»¶åæ æ³æ­£å¸¸ç¼è¯ï¼å¹¶ä¸ä¼å¯¼è´æ´é«åå­å ç¨ã

ç¶åå¨ CFLAGS æ«å°¾å å¥ ` -mpclmul` åæ°ä»¥å¯ç¨ PCLMUL æä»¤éã

æ ¹æ® CPU ä¸åï¼è¿å¯ä»¥éæ©ä»¥ä¸æ©å±æä»¤éï¼

```
-mcx16 -msahf -mpopcnt -msse3 -msse4.1 -msse4.2 -mssse3 -mavx -mavx2 -mbmi -mbmi2 -mf16c -mfma -mlzcnt -mmovbe -mxsave
```

åæ OPTIONS ä¸­ç `!lto` æ¹ä¸º `lto`ï¼å å¥ `LTOFLAGS="-flto=thin -falign-functions=32"` ä»¥å¯ç¨ `thinlto` ä¼åã

å¦æéè¦ç¼è¯ Rust è½¯ä»¶åï¼åå å¥ `RUSTFLAGS="-Copt-level=3 -Ctarget-cpu=x86-64-v3"`ï¼å¦æéè¦ç¼è¯ Go è½¯ä»¶åï¼åå å¥ `GOAMD64="v3"`ã