# shotcut: [dockerhub](https://computingforgeeks.com/run-ubuntu-linux-in-docker-with-desktop-environment-and-vnc/)
- ```ssh superadmin@hyper-v```
- ```lxc config set master limits.memory 3GB```
- ```sudo iptables -t nat -A PREROUTING -p tcp --dport 6080 -j DNAT --to-destination 10.202.91.171:6080```
- ```lxc config device add master home disk source=/home/${USER}/share path=/home/ubuntu/mnt```
- ```lxc shell master```
- ```su - ubuntu```
- ```docker run -d --name ubuntu_desktop -e USER=mo0osx -e PASSWORD=xso0om -v /home/ubuntu:/root/mnt -v /dev/shm:/dev/shm -p 6080:80 dorowu/ubuntu-desktop-lxde-vnc```
- 
