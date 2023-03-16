# ssh

- remote shell
```sh
cp /etc/ssh/sshd_config /etc/ssh/sshd_config.ORIGINAL
logout
```
- local shell
```sh
ssh-copy-id i@192.168.0.22
```
- remote shell
```sh
sed -i 's:#PasswordAuthentication yes:PasswordAuthentication no\nChallengeResponseAuthentication no:' /etc/ssh/sshd_config
sed -i 's:#PubkeyAuthentication yes:PubkeyAuthentication yes:' /etc/ssh/sshd_config
service ssh reload
logout
```
