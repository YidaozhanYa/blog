---
title: ð¢ å½»åºå¹²æ systemd 251 å³æºèé¸£å¨åå£°
date: 2022-06-06 22:12:09
tags:
- systemd
category: Archæè¾è®°
cover: 'https://imgsrc.baidu.com/super/pic/item/267f9e2f070828388f45add5fd99a9014d08f1a3.jpg'
---
Arch Linux ä¸ç systemd 251 æ´æ°ä¹åï¼å¨å³æºåéå¯çæ¶åé½ä¼å¨ tty æå° wall message å¹¶ä¼´æéè³çèé¸£å¨åå£°ï¼è²ä¼¼æ¯ä¸ä¸ªè¿å¤ç bug åè¢«è§¦åäºãæ¬æå°±æ¥æå¤§å®¶å¦ä½ç¦ç¨æ­¤ç¹æ§ã

<!--more-->

### å¸è½½èé¸£å¨åæ ¸æ¨¡å

```bash
echo "blacklist pcspkr" | sudo tee /etc/modprobe.d/nobeep.conf
sudo rmmod pcspkr
```

### ç¦ç¨æ¡é¢ç¯å¢ wall message

æ¬æ¹æ³åä¸é¢æ¹æ³æ¥èª https://github.com/systemd/systemd/issues/23520#issuecomment-1141290377

```
# å°å¦ä¸åå®¹åå° /etc/systemd/system/disable-wall.service
[Unit]
Requires=systemd-logind.service
After=systemd-logind.service
Description=Disable logind wall messages
[Service]
Type=oneshot
ExecStart=/usr/bin/busctl set-property org.freedesktop.login1 /org/freedesktop/login1 org.freedesktop.login1.Manager EnableWallMessages b false
[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl enable --now disable-wall.service
```

### ç¦ç¨ç»ç«¯å³æº wall message

```bash
# éè¿åå»º alias çæ¹æ³æ¥ç¦ç¨ç»ç«¯å³æº wall message
# å°å¦ä¸åå®¹åå°ä½  shell ç rc æä»¶
alias poweroff="systemctl poweroff --no-wall"
alias reboot="systemctl reboot --no-wall"
```

### ç¦ç¨å½åç¨æ·ç»ç«¯åå¥æé

```bash
echo "mesg n" > ~/.bash_login
# å¦æä¸ºå«ç shell åä¸ºå¯¹åºæä»¶
```
