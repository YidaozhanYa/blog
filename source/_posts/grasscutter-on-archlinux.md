---
title: ð å¨ Arch Linux ä¸æ­å»ºå¹¶è¿å¥å²èæºæå¡å¨
date: 2022-05-01 14:36:19
tags:
- Grasscutter
- åç¥
- ArchLinux
category: æ¸¸æ
cover: 'https://imgsrc.baidu.com/super/pic/item/c8ea15ce36d3d53967867e027f87e950342ab0bc.jpg'
---

è¿ç¯æç« æå¤§å®¶å¨ Arch Linux ä¸æ­å»ºãå²èæºãï¼å³ ~~æäºæ¬¡åæ¸¸æ~~ çç§æï¼å¹¶å¨æ¸¸æä¸­è¿å¥å²èæºã

æ¬æç¨å¯è½ä¸éç¨äº Arch Linux ARMãå¦ææ³å¨ Arch Linux ARM ä¸æ­å»ºï¼è¯·åè [è¿ç¯æç¨](https://www.chitang.tech/posts/grasscutter-android/)ã

ä»ä¾å­¦ä¹ äº¤æµï¼è¯·å¨ 24 å°æ¶åå é¤è¿äºæä»¶ã

## æ­å»ºæå¡å¨

### è·åå²èæº jar æä»¶åæäºæ¬¡åæ¸¸æç BinOutput

è¿éä¸ååè¿°ï¼è¯¦è§ [å²èæº Wiki](https://github.com/Grasscutters/Grasscutter/wiki)

### å®è£å¹¶å¯å¨ MongoDB

```bash
sudo pacman -S mongodb --needed
sudo systemctl enable --now mongodb
```

### å®è£å¶å®æéæä»¶

```bash
sudo pacman -S mitmproxy python --needed # mitmproxy
sudo pacman -S jdk17-openjdk --needed # Java 17
```

### å¯å¨æå¡å¨

```bash
cd /path/to/grasscutter
mitmdump -s proxy.py -k --set block_global=false & \
sudo /usr/lib/jvm/java-17-openjdk/bin/java -jar grasscutter.jar
```

## è¿å¥æå¡å¨

### å®è£è¯ä¹¦

è¿äºè¯ä¹¦éè¦åæå¡å¨çç¸åã

```bash
certutil -A -n "mitmproxy" -t "TCu,Cu,Tuw" -i "$HOME/.mitmproxy/mitmproxy-ca-cert.cer" -d sql:$HOME/.pki/nssdb # å®è£ç¨æ·è¯ä¹¦ï¼å¯é
openssl x509 -inform PEM -in "$HOME/.mitmproxy/mitmproxy-ca-cert.pem" -out "$HOME/.mitmproxy/mitmproxy-ca-cert.crt" # æ pem è¯ä¹¦è½¬ä¸º crt
sudo trust anchor "$HOME/.mitmproxy/mitmproxy-ca-cert.crt" --store
sudo cp "$HOME/.mitmproxy/mitmproxy-ca-cert.crt" /etc/ca-certificates/trust-source/anchors/
sudo update-ca-trust
```

### å¯å¨æ¸¸æ

å¦æä½¿ç¨å¯å¨èæ¬ï¼

```bash
env http_proxy=http://localhost:8080 https_proxy=http://localhost:8080 /path/to/certain_anime_game_startup.sh
```

å¦æä½¿ç¨ Lutrisï¼
æ·»å ä¸¤è¡ç¯å¢åéï¼åå«ä¸ºï¼

| key | value |
| --- | --- |
| http_proxy | http://localhost:8080 |
| https_proxy | http://localhost:8080 |

å¶ä¸­ localhost å¯ä»¥æ¢ä¸ºæå¡å¨ç IP æç»å®ååã

