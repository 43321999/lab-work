#  vpn | ~~tochka~~ | ~~dot~~ | ~~vintranet~~ | ~~router~~ 

> - > |
> - > |
> - > может быть:
> - > настроить dns в контейнерах wg для хостов?! 00, 0a, 0b, etc...
> - > |

The VPN “connection” term is technically false, as WireGuard uses UDP and there is no persistent connection. For proof click [here…](https://ubuntu.com/server/docs/wireguard-vpn-introduction#main-content)

>>> Run wg container Sample
>>> ```sh
>>> docker run -d \
>>>   --cap-add=NET_ADMIN \
>>>   --cap-add=SYS_MODULE \
>>>   --name=wireguard \
>>>   -e PUID=1000 -e PGID=1000 \
>>>   -e TZ=Europe/London \
>>>   -e SERVERURL=wireguard.example.com \
>>>   -e SERVERPORT=51820 \
>>>   -e PEERS=5 \
>>>   -e INTERNAL_SUBNET=10.13.13.0 \
>>>   -e INTERNAL_SUBNET_MASK=24 \
>>>   -e PEERDNS=auto \
>>>   -e KEEPALIVE=25 \
>>>   -e DNS=1.1.1.1 \
>>>   -p 51820:51820/udp \
>>>   -v /path/to/appdata/config:/config \
>>>   -v /lib/modules:/lib/modules \
>>>   --sysctl="net.ipv4.conf.all.src_valid_mark=1" \
>>>   --sysctl="net.ipv6.conf.all.forwarding=1" \
>>>   wireguard-container
>>> ```
>>> --cap-add=NET_ADMIN предоставляет контейнеру права администратора сети, что позволяет управлять сетевыми интерфейсами..
