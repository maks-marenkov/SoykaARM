Установка MediaWiki на Docker

```
git clone https://github.com/maks-marenkov/SoykaARM
docker-compouse -f wiki.yml -d up
```

Запрос адресса базы данных

```
docker ps
cf996875fd07   mariadb     "docker-entrypoint.s…"   28 minutes ago   Up 28 minutes   3306/tcp                                root_database_1

docker exec -it cf996875fd07 /bin/bash
hostname -i
```
