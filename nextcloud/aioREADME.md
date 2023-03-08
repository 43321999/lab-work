# [manual install](https://github.com/nextcloud/all-in-one/tree/main/manual-install)
```sh
cd ~/apps/nextcloud/
wget https://github.com/nextcloud/all-in-one/archive/refs/heads/main.zip
unzip ./*.zip
rm ./*.zip
cd all-in-one/manual-install
cp sample.conf .env
```
```vi .env``` & edit ```# TODO!``` values:
- secrets: wU7&jo9ik\XVo1Gh/W55!YLzry",bx7
- domain: localhost
- timezone: Europe/London


```docker stack deploy -c stack.yml AIO``` 🟥🟥 deadlock 🟥🟥
