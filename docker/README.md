# [setup](https://docs.docker.com/engine/install/debian/)
install from [apt repo](https://docs.docker.com/engine/install/debian/#install-using-the-repository)
to replase Docker Compose on Docker Swarm:
- Remove ```docker-compose-plugin``` from second command of install guide:
  ```shell
  sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin
  ```
- init swarm:
  ```sh
  sudo docker swarm init --advertise-addr fc00::
  ```
# [post-install](https://docs.docker.com/engine/install/linux-postinstall/)
shortly:
```sh
sudo usermod -aG docker $USER
newgrp docker
```
copy this:
```json
{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3"
  }
}
```
and paste here: ```/etc/docker/daemon.json```

# enable IPv6
1. copy this
```json
{
  "ipv6": true
}
```
append to: ```/etc/docker/daemon.json```

2. copy this ```--fixed-cidr-v6=fc0a::/16```
and edit ```ExecStart``` line of ```/lib/systemd/system/docker.service``` file

3. ``` sudo systemctl restart docker```
