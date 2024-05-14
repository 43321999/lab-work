#  vpn
## 00
```
cat /etc/network/interfaces
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

auto ens128
iface ens128 inet dhcp

iface ens128 inet6 static
    address fd00::
    netmask 8
```
```sh
cd /etc/wireguard/
umask 077
wg genkey | tee privatekey | wg pubkey > publickey
```
```sh
root@00:/etc/wireguard# cat fd0c.conf
[Interface]
PrivateKey = aaasasdfajskdfja;sldajskfl=
listenPort = 1025
Address = fd00::/16

[Peer]
PublicKey = aaasssdfdfdsa';lksdfasdfasd=
AllowedIPs = fd0c::/16
Endpoint = 192.0.2.1:1025
PersistentKeepAlive = 25
```
```
# wg-quick up fd0c
systemctl enable wg-quick@fd0c

systemctl status wg-quick@fd0c
stemctl start wg-quick@fd0c

# systemctl stop wg-quick@fd0c
# systemctl disable wg-quick@fd0c
```
## 0a
1.
```sh
cat /etc/network/interfaces
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

auto enp1s0
iface enp1s0 inet dhcp

iface enp1s0 inet6 static
    address fd0a::
    netmask 8
    # Добавьте маршрут на интерфейс
    up ip -6 route add fd0c::/16 via fd00:: dev enp1s0
    # Убедитесь, что маршрут удаляется при отключении интерфейса
    down ip -6 route del fd0c::/16 via fd00:: dev enp1s0
```
2.
```sudo ifdown enp1s0 && sudo ifup enp1s0```
or
```sh
sudo systemctl restart networking
ip -6 route show
```
3. test
## 0b

## 0c

## 1b

## 1c

## 01
1. System Preferences > network > advanced > TCP/IP:
-  IPv6 address: fd01::
-  Prefix length: 8
3. ```sudo route -n add -inet6 fd0c::/16 -gateway fd00::```
   or
   ```sudo vi /usr/local/bin/add_route.sh```
   ```sh
   #!/bin/sh
   # Ждем 30 секунд для убеждения, что сетевой интерфейс инициализирован
   sleep 30

   # Добавление маршрута при запуске
   route -n add -inet6 fd0c::/16 -gateway fd00::   
   ```
   ```sh
   sudo chmod +x /usr/local/bin/add_route.sh
   sudo vi /Library/LaunchDaemons/com.user.delayedroute.plist
   ```
   ```sh
   <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
    <plist version="1.0">
    <dict>
      <key>Label</key>
      <string>com.user.delayedroute</string>
      <key>ProgramArguments</key>
      <array>
        <string>/usr/local/bin/add_route.sh</string>
      </array>
      <key>RunAtLoad</key>
      <true/>
      <key>StandardErrorPath</key>
      <string>/tmp/com.user.delayedroute.err</string>
      <key>StandardOutPath</key>
      <string>/tmp/com.user.delayedroute.out</string>
    </dict>
    </plist>
   ```
  5. test
  ```sh
  sudo launchctl load /Library/LaunchDaemons/com.user.delayedroute.plist
  ping6 -c 1 fd0c::
  ```
  ```sh
   sudo reboot
   ping6 -c 1 fd0c::
  ```
