# swarm
todo:
- [ ] google request: wireguard subnet docker swarm; [google response](https://github.com/moby/moby/issues/36689)
- [ ] [```dockerd --default-network-opt=bridge=com.docker.network.driver.mtu=1234```](https://github.com/moby/moby/pull/43197)

## manager
``` docker swarm init --advertise-addr [fc00::]:1026```
## [worker](workerREADME.md)
``` docker swarm join --token <token> [fc00::]```
