# vvlliicc_microservices

##Создание docker host
##Создание своего образа
##Работа с Docker Hub


##Соберем образы с нашими сервисами
```bash
docker build -t <your-dockerhub-login>/post:1.0 ./post-py
docker build -t <your-dockerhub-login>/comment:1.0 ./comment
docker build -t <your-dockerhub-login>/ui:1.0 ./ui
```
##Создадим специальную сеть для приложения:
Запустим наши контейнеры
```bash
docker network create reddit
docker run -d --network=reddit \
--network-alias=post_db --network-alias=comment_db mongo:latest
docker run -d --network=reddit \
--network-alias=post <your-dockerhub-login>/post:1.0
docker run -d --network=reddit \
--network-alias=comment <your-dockerhub-login>/comment:1.0
docker run -d --network=reddit \
-p 9292:9292 <your-dockerhub-login>/ui:1.0
```
##Выключим старые копии контейнеров:
```bash
 docker kill $(docker ps -q)
 ```
