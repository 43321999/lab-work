[nextcloud+postgres](https://github.com/docker/awesome-compose/tree/master/nextcloud-postgres)

nextcloud-stack.yml
```yaml
services:
  nc:
    image: nextcloud:apache
    environment:
      - POSTGRES_HOST=db
      - POSTGRES_PASSWORD=nextcloud
      - POSTGRES_DB=nextcloud
      - POSTGRES_USER=nextcloud
    ports:
      - 1025:80
    restart: always
    volumes:
      - nc_data:/var/www/html
    deploy:
      mode: global
  db:
    image: postgres:alpine
    environment:
      - POSTGRES_PASSWORD=nextcloud
      - POSTGRES_DB=nextcloud
      - POSTGRES_USER=nextcloud
    restart: always
    volumes:
      - db_data:/var/lib/postgresql/data
    expose:
      - 5432
    deploy:
      mode: global
volumes:
  db_data:
  nc_data:
```
```docker stack deploy -c ~/apps/nextcloud/stack.yml```
