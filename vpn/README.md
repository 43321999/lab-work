#  vpn | ~~tochka~~ | ~~dot~~ | ~~vintranet~~ | ~~router~~ 

> - > |
> - > |
> - > может быть:
> - > настроить dns в контейнерах wg для хостов?! 00, 0a, 0b, etc...
> - > |

The VPN “connection” term is technically false, as WireGuard uses UDP and there is no persistent connection. For proof click [here…](https://ubuntu.com/server/docs/wireguard-vpn-introduction#main-content)

>>> Run wg container Sample
>>> ```sh
>>>   --sysctl="net.ipv4.conf.all.src_valid_mark=1" \
>>>   --sysctl="net.ipv6.conf.all.forwarding=1" \
>>>   --cap-add=NET_ADMIN # предоставляет контейнеру администрирование сетевых интерфейсов..
>>> ```

