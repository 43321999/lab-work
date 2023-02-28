## alpinelinux setup
[VK article](vk.com/@-130358072-hyper-v)

## ssh
remote shell
```sh
cp /etc/ssh/sshd_config /etc/ssh/sshd_config.ORIGINAL
## - [default]: PermitRootLogin yes
# sed -i 's:#PermitRootLogin prohibit-password:PermitRootLogin yes:' /etc/ssh/sshd_config
# rc-service sshd restart
exit
```
local shell ```ssh-copy-id username@remote_host```

remote shell
```sh
sed -i 's:#PasswordAuthentication yes:PasswordAuthentication no\nChallengeResponseAuthentication no:' /etc/ssh/sshd_config
sed -i 's:#PubkeyAuthentication yes:PubkeyAuthentication yes:' /etc/ssh/sshd_config
# sed -i 's:#PermitRootLogin yes:PermitRootLogin yes:' /etc/ssh/sshd_config
rc-service sshd restart
exit
```

