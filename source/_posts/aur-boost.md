---
title: ð¨ å é AUR çè½¯ä»¶ä¸è½½åå®è£
date: 2021-12-26 18:37:51
tags:
- ArchLinux
- AUR
---

### ä¸ãç½ç»å é

AUR çè½¯ä»¶ç»å¸¸éè¦ç¨å° GitHub çä»åºãRaw æ Releasesï¼æä»¥éè¦æ¿æ¢é¨å ``makepkg`` èæ¬è§£å³ã

- ##### ä¸è½½å é
  
  ``makepkg`` å¯ä»¥èªå®ä¹ä¸è½½å¨ï¼æä»¥å¯ä»¥åä¸ä¸ªä¸è½½èæ¬ï¼æ¿æ¢åæ¬ç ``curl``ã
  
  é¦åä»è¿éä¸è½½æå¶ä½å¥½çèæ¬ï¼ä½¿ç¨ aria2 å éä¸è¬æä»¶çä¸è½½ï¼å¹¶ä¸æ GitHub ååæ¿æ¢ä¸º FastGitï¼ï¼æ¾å¨ä¸ä¸ªèªå®ä¹ä½ç½®ï¼æè¿éä½¿ç¨ ``/usr/local/bin/aurdl``ï¼å¹¶ä¸èµäºå¯æ§è¡æéã
  
  ```bash
  sudo pacman -S --needed aria2 # å®è£ aria2
  sudo curl -L "https://file.yidaozhan.top/d/OneDrive/Linux/aurdl.sh" -o /usr/local/bin/aurdl
  sudo chmod +x /usr/local/bin/aurdl
  ```
  
  ä¹åå° ``makepkg`` HTTP / HTTPS ä¸è½½åè®®çä¸è½½å¨æ¹ä¸ºååçä¸è½½èæ¬ã
  
  ååå»ºä¸ä»½æ¬å° makepkg éç½®æä»¶ (``install -D /etc/makepkg.conf ~/.config/pacman/makepkg.conf``)ï¼ç¶åç¨ä»»æææ¬ç¼è¾å¨æå¼ ``~/.config/pacman/makepkg.conf``ï¼ä¹åå° DLAGENTS æ°ç»ä¸­åæç ``'https::/usr/bin/curl -gqb "" -fLC - --retry 3 --retry-delay 3 -o %o %u'``ä¸è¡æ¿æ¢ä¸º``'https::/usr/local/bin/aurdl %o %u'``ã
- ##### Git å é
  
  ``makepkg`` ä¸è½èªå®ä¹ Git å®¢æ·ç«¯ï¼æä»¥éè¦ä¿®æ¹ ``makepkg`` æ¬ä½ã
  
  {% border  color:red %}
  
  æ­¤æä½éè¦ä¿®æ¹ ``makepkg`` æ¬ä½ï¼å·æä¸å®å±é©æ§ï¼è¯·è°¨ææä½ï¼
  
  å¦å¤æ­¤æä½ä¼éç ``pacman`` åçæ´æ°èå¤åï¼æä»¥å½ ``pacman`` æ´æ°çæ¶åï¼éè¦éæ°æä½ã
  
  {% endborder %}
  
  é¦åä¸è½½æå¶ä½ç Git èæ¬ï¼æ¿æ¢ GitHub ååä¸º FastGitï¼ï¼æ¾å¨èªå®ä¹ä½ç½®ï¼æè¿éä½¿ç¨ ``/usr/local/bin/fakegit``ï¼å¹¶ä¸èµäºå¯æ§è¡æéã
  
  ```bash
  sudo curl -L "https://file.yidaozhan.top/d/OneDrive/Linux/fakegit.sh" -o /usr/local/bin/fakegit
  sudo chmod +x /usr/local/bin/fakegit
  ```
  
  ä¹åä¿®æ¹ ``makepkg`` ï¼å°ææ Git å½ä»¤è¡æ¿æ¢ä¸ºä¿®æ¹çèæ¬ï¼å¹¶ä¸å»é¤ä¸æ¸¸å°åæ ¡éªã
  
  ```bash
  sudo sed -i 's/git clone/\/usr\/local\/bin\/fakegit clone/' /usr/share/makepkg/source/git.sh
  sudo sed -i 's/(git config --get remote.origin.url)/url/' /usr/share/makepkg/source/git.sh
  ```

---

### äºãç¼è¯å é

#### â  å¤çº¿ç¨ç¼è¯

ç¨ææ¬ç¼è¾å¨ä¿®æ¹ ``~/.config/pacman/makepkg.conf``ï¼ä¿®æ¹ ``MAKEFLAGS`` åéä¸º``-j``ã

ä¿®æ¹åè¯¥è¡ä¸º ``MAKEFLAGS="-j"``ã

#### â¡ å¤çº¿ç¨åç¼©

{% border %}

åèï¼https://www.limstash.com/articles/202004/1597

{% endborder %}

åå®è£ `pigz` å `pbzip2`ï¼è¿ä¸¤ä¸ªåæ¯æå¤çº¿ç¨åç¼©ã

```bash
sudo pacman -S pigz pbzip2
```

ä¹åç¨ææ¬ç¼è¾å¨ä¿®æ¹ ``~/.config/pacman/makepkg.conf``ï¼ä¿®æ¹ä»¥ä¸å ä¸ªåéã

```bash
COMPRESSXZ=(xz -c -z - --threads=0)
COMPRESSGZ=(pigz -c -f -n)
COMPRESSBZ2=(pbzip2 -c -f)
COMPRESSZST=(zstd -c -z -q - --threads=0)
```

