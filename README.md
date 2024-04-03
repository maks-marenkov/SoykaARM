Установка MediaWiki на Docker

```
git clone https://github.com/maks-marenkov/SoykaARM
docker-compouse -f wiki.yml -d up
```

Запрос адресса базы данных

```
docker ps

CONTAINER ID   IMAGE       COMMAND                  CREATED          STATUS          PORTS                                   NAMES
cf996875fd07   mariadb     "docker-entrypoint.s…"   28 minutes ago   Up 28 minutes   3306/tcp                                root_database_1

docker exec -it cf996875fd07 /bin/bash
hostname -i
```

Зайти на сайт MediaWiki 192.168.1.1:8080. Начнется установка. Указать все данные доступа. В строку сервер базы данных записать IP результат команды hostname -i. После чего скачается файл LocalSettings.php. Необходимо загрузить файл на сервер. 

```
nano wiki.yml
```
Убрать комментарий на строчке 
```
 - ./LocalSettings.php:/var/www/html/LocalSettings.php
```
