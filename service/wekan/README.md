# wekan
```yml
version: '3.8'

services:
  wekan:
    image: wekan/wekan:latest
    deploy:
      replicas: 3
      placement:
        constraints:
          - node.role == worker
      restart_policy:
        condition: on-failure
    volumes:
      - type: volume
        source: wekan_data
        target: /data
    environment:
      - ROOT_URL=http://wekan.example.com
      - MONGO_URL=mongodb://mongo:27017/wekan
    networks:
      - wekan_network

networks:
  wekan_network:

volumes:
  wekan_data:
    driver: local
    driver_opts:
      type: nfs
      o: addr=[fc00::],rw
      device: ":/mnt/00/wekan/"
```
