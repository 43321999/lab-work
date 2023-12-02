# setup

> Why [nfs](https://sungup.github.io/2020/01/15/How-to-Setup-the-NFS-on-Ubuntu.html):
>
> \+ Data is transmitted in the transparent form.

## server
### ~/apps/overlay-storage/Dockerfile
```dockerfile
FROM node:lts-bookworm
RUN apt update && apt install -y nfs-kernel-server
COPY exports /etc/exports
COPY main.js /
EXPOSE 111/udp 111/tcp 2049/udp 2049/tcp
CMD ["node", "--experimental-default-type=module", "/main.js"]
```

### ~/apps/overlay-storage/main.js
```javascript
import { spawn } from 'child_process';

// Паттерн «Цепочка обязанностей» (Chain of Responsibility)
class NFSStorage {
  constructor() {
    this.nfsPackageName = 'nfs-kernel-server';
    this.nfsServiceName = 'nfs-kernel-server';
  }

  async install() {
    try {
      await this.executeCommand('apt', ['install', this.nfsPackageName, '-y']);
      console.log(`Установка ${this.nfsPackageName} выполнена успешно`);
    } catch (error) {
      console.error(`Возникла ошибка при установке ${this.nfsPackageName}`);
    }
  }

  async start() {
    try {
      await this.executeCommand('systemctl', ['start', this.nfsServiceName]);
      console.log(`${this.nfsServiceName} успешно запущен`);
    } catch (error) {
      console.error(`Возникла ошибка при запуске ${this.nfsServiceName}`);
    }
  }

  executeCommand(command, args) {
    return new Promise((resolve, reject) => {
      const process = spawn(command, args);
      process.on('exit', (code) => {
        if (code === 0) {
          resolve();
        } else {
          reject(new Error(`Exit code: ${code}`));
        }
      });
    });
  }
}
const nfsStorage = new NFSStorage();
//nfsStorage.install().then(() => {
//  nfsStorage.start();
//});
nfsStorage.start();
```
### ~/apps/overlay-storage/exports
```
/public *(rw,sync,no_subtree_check)
```
### run
```shell
docker build -t localhost:5000/nfs .
docker run -d --privileged -p 111:111/tcp -p 111:111/udp -p 2049:2049/tcp -p 2049:2049/udp -v /public:/public localhost:5000/nfs
# флаг --privileged предоставляет контейнеру все привилегии root-пользователя хостовой операционной системы, а также полный доступ к устройствам.
```
>
> ```shell
> # server shell
> # checking 
> service nfs-kernel-server status
> # starting
> service nfs-kernel-server start
> # client shell
> # checking
> showmount -e 192.168.0.4
> ```
> 

## client
### lvm
