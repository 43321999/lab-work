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

## 0a
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
```
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

   # Добавление маршрута при запуске
   route -n add -inet6 fd0c::/16 -gateway fd00::   
   ```
   ```sh
   sudo chmod +x /usr/local/bin/add_route.sh
   sudo vi ~/Library/LaunchAgents/com.user.addroute.plist
   ```
   ```sh
   <?xml version="1.0" encoding="UTF-8"?>
   <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
   <plist version="1.0">
   <dict>
     <key>Label</key>
     <string>com.user.addroute</string>
     <key>ProgramArguments</key>
     <array>
       <string>/usr/local/bin/add_route.sh</string>
     </array>
     <key>RunAtLoad</key>
     <true/>
     <key>LaunchOnlyOnce</key>
     <true/>
   </dict>
   </plist>
   ```
-  Выполнив ```visudo```, прокрутить до раздела, "User specification" и добавить ```fd ALL=(ALL) NOPASSWD: /usr/local/bin/add_route.sh```
  ```sh
  launchctl load ~/Library/LaunchAgents/com.user.addroute.plist
  ping6 -c 1 fd0c::
  ```
  ```sh
   sudo reboot
 5. ```ping6 -c 1 fd0c::```
