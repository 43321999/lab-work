# docker
## uninstall
### uninstall docker engine
>
>To delete all images, containers, and volumes:
>
```sh
sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
```
```sh
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```
### uninstall old version
>
>To uninstall older versions to install a new version:
>
```sh
# docker https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository
#
sudo apt-get remove docker docker-engine docker.io containerd runc
# or
sudo apt-get remove docker docker.io containerd runc
#
sudo apt autoremove
#
```
## install
```sh
sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg
#
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

#
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

#
sudo apt-get update

#
#
#
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

#
sudo docker run hello-world
```
## [optional post-installation](https://docs.docker.com/engine/install/linux-postinstall)
### [rootless mode](https://docs.docker.com/engine/security/rootless/)
```sh
# * You can change the configuration of this build by modifying the files $
# * Additional certificates used by the Docker daemon to authenticate with$
# **Running Docker as normal user** 
#
# By default, Docker is only accessible with root privileges (`sudo`). If $
sudo addgroup --system docker
sudo adduser $USER docker
sudo newgrp docker
```
```sh
```
