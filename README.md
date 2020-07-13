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

## hw DOCKER-4
- Изучили типы сетей поддерживаемых docker: none, bridge и host.
-  Запустили  приложения в двух изолированных сетях.
- Создали docker-compose.yml, для запуска и конфигурации  контейнеров.
- Доработана конфигурация сети - front_net и back_net
- Для формирования имени проекта можно использовать переменную окружения COMPOSE_PROJECT_NAME


## Gitlab-CI
Развернули тестового инстанса Gitlab, на базе docker-образа.
Сконфигурирован Gitlab-runner;
Изучены основные возможности функцианала непрерывной интеграции;
Выполнено знакомство с динамическими окружениями.


## Monitoring-1

- Настроили Prometheus: запуск, конфигурация, знакомство с
Web UI
- Запустили дополнительные контейнеры для мониторинга состояния микросервисов
- Настроили сбор метрик хоста с использованием экспортера
https://hub.docker.com/u/vvlliicc
