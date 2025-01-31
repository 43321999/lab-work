# 🇷🇺
## 01.fd.conf
```ini
# fd00
[Interface]
Address = 10.0.0.1/24
PostUp = iptables -A FORWARD -i %i -j ACCEPT; iptables -t nat -A POSTROUTING -o %i -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -t nat -D POSTROUTING -o %i -j MASQUERADE
ListenPort = 1026
PrivateKey = XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX=

# fd01
[Peer]
PublicKey = YYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY=
AllowedIPs = 10.0.0.2/32
```
## 00.fd.conf
```ini
# fd01
[Interface]
Address = 10.0.0.2/32
PrivateKey = <ЗДЕСЬ_ВАШ_ЗАГЛУШКА_КЛЮЧА>
ListenPort = 1026
# DNS = 1.1.1.1

# fd1c
[Peer]
PublicKey = <ЗДЕСЬ_ПУБЛИЧНЫЙ_ЗАГЛУШКА_КЛЮЧА>
AllowedIPs = 0.0.0.0/0
Endpoint = <ЗАГЛУШКА_ENDPOINT_IP>:1026
PersistentKeepAlive = 25
```
## 00.fd.conf
```ini

# fd01
[Interface]
Address = 10.0.0.2/32
PrivateKey = <ЗДЕСЬ_ВАШ_ЗАГЛУШКА_КЛЮЧА>
ListenPort = 1026
# DNS = 1.1.1.1

# fd1c
[Peer]
PublicKey = <ЗДЕСЬ_ПУБЛИЧНЫЙ_ЗАГЛУШКА_КЛЮЧА>
AllowedIPs = 192.0.2.1, 203.0.113.0/24#192.0.2.1, 198.51.100.0/24
Endpoint = <ЗАГЛУШКА_ENDPOINT_IP>:1026
PersistentKeepAlive = 26
```
# 🇺🇸
## 01.fd.conf
```ini
[Interface]
Address = 10.0.1.1/24
# SaveConfig = true
PostUp = iptables -A FORWARD -i fd01 -j ACCEPT; iptables -t nat -A POSTROUTING -o ens4 -j MASQUERADE
PostDown = iptables -D FORWARD -i fd01 -j ACCEPT; iptables -t nat -D POSTROUTING -o ens4 -j MASQUERADE
ListenPort = 1026
PrivateKey = <PRIVATE_KEY_PLACEHOLDER>

[Peer]
PublicKey = <PUBLIC_KEY_PLACEHOLDER>
AllowedIPs = 10.0.1.2/32
```
## 1c.fd.conf
```ini
# fd01
[Interface]
Address = 10.0.1.2/32
PrivateKey = <ВАШ_ЗАГЛУШКА_ДЛЯ_ПРИВАТНОГО_КЛЮЧА>
ListenPort = 1027
#DNS = 1.1.1.1

# fd1c
[Peer]
PublicKey = <ВАША_ЗАГЛУШКА_ДЛЯ_ПУБЛИЧНОГО_КЛЮЧА>
AllowedIPs = 192.0.2.1/32
Endpoint = <ЗАГЛУШКА_ENDPOINT_IP>:1026
PersistentKeepAlive = 26
```
# 🇫🇷
## server
```ini

```
## client
```ini

```
# 🇯🇵
## server
```ini

```
## client
```ini

```
# 🇰🇿
## server
```ini

```
## client
```ini

```
# 🇭🇰
## server
```ini

```
## client
```ini

```
# 🇪🇺
## server
```ini

```
## client
```ini

```

