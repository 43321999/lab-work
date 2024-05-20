# Runtime setup:
- [distribution](distribution/README.md)
# Cluster setup:
- [vpn](vpn/README.md)
- [mnt](mnt/README.md)
- [virtualization](docker/README.md)
- [orchestrator](swarm/README.md)
- [base image](nodejs/README.md)
  - svelte
# Microservices:
- [IDE](vscode/README.md)
- [registry](https://github.com/43321999/RuntimeSetup#registry-service)
- [post](postfix/README.md)
- [task-tracker](wekan/README.md)
- [gui](gui/README.md)
- [ci/cd](https://github.com/43321999/RuntimeSetup#cicd)
# X11

## [vpn](https://docs.docker.com/samples/wireguard/)
```sh
        # hidemyass services:
	# - ipv6 sharing with wireguard: https://errande.com/2021/01/wireguard-he-tunnel/#wireguard-configuration
	# - «tunnelbroker» free subnet: BSd6pLTGkoGYXjtxFNBcGA7iGwOfeV gmail.com
	# - nodejs proxy:
	# - vpn load balancing
```
## registry service
[43321999/registry-stack](43321999/registry-stack)
[registry](https://github.com/43321999/registry-stack)
[vita kalman comment:](https://vk.com/public130358072?w=wall-130358072_149)
### docker-stack-registry.yml ( from kubuntu apps )
```sh
root@hub:~/apps# cat registry/docker-stack-registry.yml 
version: '3.8'
services:
  registry:
    image: registry:2
    ports:
      - 5000:5000
    volumes:
      - ../certs:/certs
    environment:
      - REGISTRY_HTTP_ADDR=0.0.0.0:5000
      - REGISTRY_HTTP_TLS_CERTIFICATE=/certs/domain.crt
      - REGISTRY_HTTP_TLS_KEY=/certs/domain.key 
    deploy:
      restart_policy:
        condition: on-failure
      placement:
        constraints:
          - node.labels.ip == local
          #- node.labels.role == manager
```
## x11 lxc services
### [gimp](docs.microsoft.com/ru-ru/windows/wsl/tutorials/gui-apps#install-gimp)
```sh
        # gimp

# sudo apt update
# sudo apt upgrade -y
# sudo apt install gimp -y
```
```sh
# krita
```

```sh
# inkscape
```
## X11 swarm services
## [?!?!node](https://nodejs.org/)
```sh
        # swarm service

```
-
## [postgres](https://ubuntu.com/server/docs/databases-postgresql)
```sh
        # swarm service
```
-
##
## asterisk
```sh
        # swarm service
```
install CentOS
n. 
https://www.asterisk.org
```sh
# freePBX ISO
wget # [see info here…](https://downloads.freepbxdistro.org/ISO/SNG7-PBX-64bit-2104-1.iso]
# Install from USB
dd # [see info here…](https://wiki.centos.org/HowTos/InstallFromUSBkey)
# chan_dongle
# [see info here…](https://github.com/pospelov-v/wdoekes-asterisk-chan-dongle-16-6-2?ysclid=llik3yxo1r138315109)
# [and here…](https://web.archive.org/web/20230604170612/http://guwi.ru/?p=394)
```
### dongle.conf
```sh
# see noshimorimoshi private gist…
```
## headless CMS (with Mongo & Koa.js & SvelteKit)
- [0](https://strapi.io)
- [1](https://www.npmjs.com/package/yandex-pdd-dns)
- [2](https://nodecms.guide/)
- [3](https://jamstack.org/headless-cms/)
- [4](https://www.npmjs.com/search?q=cms%20koa%20mongo)
- [5](https://vk.com/away.php?to=https%3A%2F%2Fdocs.google.com%2Fspreadsheets%2Fd%2F1DZC8TQz5oNECskVzh1CDCBD89VamNBdXXuQwyAJeoCQ%2Fedit%23gid%3D1994570499&cc_key=)
## openvpn server
## yukon app
- [Node.js and yandex translate api](https://www.youtube.com/watch?v=DsCcK2s6TwU)

## let's encrypt
```sh
	# certbot.eff.org
	# free .com subdomains: 
	#   - freedns.afraid.org/subdomain/
	#     - 2ua7ogmvjc6d mail.ru
	#
	# search for "ipv6 tunnel broker kz" : vk.com/public130358072?w=wall-130358072_178
	#
	
	# полезные программы для поиска доменов: wwhois.ru/favorite_programs.html
	# массовая проверка доменов на занятость: wwhois.ru/masswhois.php
```

## [samba](https://ubuntu.com/server/docs/samba-introduction)
### file list from kubuntu apps
smb/docker-stack-node.yml
```sh
version: "3.8"
services:
  samba:
    image: 164.gr:5000/noshimorimoshi/smb
    ports:
      - 139:139
      - 445:445
    volumes:
      - hub:mnt/smb
    deploy:
      placement:
        constraints:
          - node.labels.role == node
      replicas: 2
      resources:
        limits:
          cpus: '1'
volumes:
  hub:
    driver: local
```
smb/docker-stack.yml
```sh
root@hub:~/apps# cat smb/docker-stack.yml 
version: "3.8"
services:
  samba:
    image: localhost:5000/noshimorimoshi/smb
    ports:
      - 139:139
      - 445:445
    volumes:
      - /samba/:/mnt/smb
    deploy:
      placement:
        constraints:
          - node.labels.role == manager
```
smb/smb.conf
```sh
[global]
        map to guest = Bad User
        log file = /var/log/samba/%m
        log level = 10

[guest]
        path = mnt/smb/shared/
        read only = no
        guest ok = yes
```
smb/Dockerfile
```sh
root@hub:~/apps# cat smb/Dockerfile 
FROM alpine:3.12.0

RUN apk add --no-cache --update \
    samba-common-tools \
    samba-client \
    samba-server

COPY smb.conf /etc/samba/smb.conf

EXPOSE 139/tcp 445/tcp

CMD ["smbd", "--foreground", "--log-stdout", "--no-process-group"]
```
## ci/cd
[couple words](vk.com/@-130358072-devops)
==============================
## static local ip
- login to http://192.168.0.1 / network / lan
- copy MAC address
- locate to Network / LAN / DHCP binding / IP-address: 192.168.0.22
- paste MAC-address

## ddns
Service availability is both a reputation and search optimization matter. While resource conservation is important, it is also crucial to maintain a balance between efficiency and the stability of service operations. It is unofficially known that intercontinental DNS caches are set up with the longest possible refresh interval, making the service entirely unavailable to other continents if the IP address updates more often than once every two days. Furthermore, in the "road warrior" VPN model, when all nodes have dynamic IP addresses, there is a minimal, yet present risk of simultaneous IP updates, resulting in network downtime and requiring time for manual recovery. Additionally, developing any kind of service requires time, attention, and responsibility, which are better directed towards noble grand desires. Therefore, despite a strong inclination, the decision was taken to abandon the idea of DDNS in favor of acquiring a static IP address.

> 
> __docker reccomends:__
>```sh
># collectd: losst.ru/nastrojka-collectd-dlya-nachinayushhih
># ⭐️⭐️⭐️⭐️⭐️
>```
>```sh
># nagios (alert monitoring): https://ubuntu.com/server/docs/tools-nagios
># GUI 🤨
>```
>
> __ubuntu reccomends:__
>```sh
># nagios and munin: ubuntu.com/server/docs/monitoring-nagios-munin # nagios and munin owerview: https://youtu.be/8yBTADrD4hk
>#
># munín (dashboard monitoring): https://ubuntu.com/server/docs/tools-munin
>```
