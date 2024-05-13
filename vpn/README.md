#  vpn
## 00

## 0a

## 0b

## 0c

## 1b

## 1c

## 01
1. Системные настройки: Настроить сетевой интерфейс через GUI в разделе "Системные настройки" > "Сеть" > network > advanced > TCP/IP:
-  IPv6 address: fd01::
-  Prefix length: 8
3. ```sudo route -n add -inet6 fd0c::/16 -gateway fd00::```
4. ```ping6 -c 1 fd0c::```
## 
