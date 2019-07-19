# Пример приложения c микросервисной архитектурой.

* comment — микросервис комментариев.
* ui — микросервис веб-интерфейса
* post-py — микросервис постов
---
0. Склонировать репозиторий и перейти в директорию:
```bash
git clone https://github.com/alexwirehead/microservices.git && cd microservices
```

1. Для работы микросервисов на Docker-хосте необходимо сначала создать сеть:
```bash
docker network create reddit
```
2. В качестве БД используется MongoDB. Для того чтобы развернуть MongoDB выполнить команду:
    ```bash
       docker pull mongo:latest && \
       docker run -d --name=db --network=reddit \
              --network-alias=post_db_host \
              --network-alias=comment_db_host \
       mongo:latest

    ```
    * --network-alias=post_db_host — для взаимодействия с микросервисом post
    * -network-alias=comment_db_host — для взаимодействия с микросервисом comment
3. Для билда и запуска контейнеров выполнить команду:
    ```bash
        docker build -t comment:2.0 ./comment \
        &&  docker build -t ui:2.0 ./ui \
        &&  docker build -t post:1.0 ./post-py \
        &&  docker run -d --name=reddit_post  --network=reddit \
                          --network-alias=post_host \
            post:1.0 \
        &&  docker run -d --name=reddit_comments --network=reddit \
                          --network-alias=comment_host \
            comment:2.0 \
        &&  docker run -d --name=reddit_ui --network=reddit \
                       -p 9292:9292 \
            ui:2.0 \
        && docker ps -a
    ```
    * микросервис ui общается с comment и post используя:
      * --network-alias=post_host
      * --network-alias=comment_host

