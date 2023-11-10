# [debian](https://www.debian.org/releases/stable/amd64/index.ru.html)

>>>
>>> При помощи каких утилит NextCloud, производит объединение дисков в одно логическое хранилище?
>>>
>>> youtu.be/afD2_H215JM?si=S8dAdn65ujWDE2Pl
>>> 

## hardware debian setup on «American Mega Trends… » bios
Graphic installation:
  - Installation language: English
  - Location, Locale, Timezone, live country: United Kingdom
  - Keyboard layout: American English
  - hostname: 00
  - domain name: 164
  - no root passwd
  - superadmin passwd: < zte superadmin >
  - use entire sda disk
  - package manager mirror (Russian Federation): deb.debian.org
  - blank proxy or test proxy=socks5://ip:port
  - usage statistics: no
  - predefined soft:
    - [x] Debian desktop env
    - [x] GNOME
    - [x] SSH
    - [x] standard system utilities
  - GRUB boot loader: sda
```shell
sudo su
apt update
mkdir /etc/systemd/sleep.conf.d
vi /etc/systemd/sleep.conf.d/nosuspend.conf
```
To prevent unexpected message: - «:The system will suspend now!»
Copy this:
```config
[Sleep]
AllowSuspend=no
AllowHibernation=no
AllowSuspendThenHibernate=no
AllowHybridSleep=no
```
and paste to: ```/etc/systemd/sleep.conf.d/nosuspend.conf```
```# reboot```
