# docker
<details>
    <summary>short</summary>
    <p>
        ```sh
        curl -fsSL get.docker.com | sudo sh
        ```
    </p>
</details>
<details><summary>long</summary>
```sh
# docker https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository
#
sudo apt-get remove docker docker-engine docker.io containerd runc
#
sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
#
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
#
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
#
sudo apt-get update
#
#
#
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
# * You can change the configuration of this build by modifying the files $
# * Additional certificates used by the Docker daemon to authenticate with$
# **Running Docker as normal user** 
#
# By default, Docker is only accessible with root privileges (`sudo`). If $
sudo addgroup --system docker
sudo adduser $USER docker
sudo newgrp docker
sudo snap disable docker
sudo snap enable docker
```
</details>
