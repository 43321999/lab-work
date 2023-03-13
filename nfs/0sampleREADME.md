# [nfs](https://sungup.github.io/2020/01/15/How-to-Setup-the-NFS-on-Ubuntu.html)
```docker run -v overlay:/mnt/overlay --name volume_overlay -it ubuntu bash```
```sh
apt update
apt install -y nfs-kernel-server
systemctl enable nfs-kernel-server
# systemctl start nfs-kernel-server
service nfs-kernel-server
```

