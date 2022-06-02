
# Домашнее задание к занятию "5.3. Введение. Экосистема. Архитектура. Жизненный цикл Docker контейнера"

## Как сдавать задания

Обязательными к выполнению являются задачи без указания звездочки. Их выполнение необходимо для получения зачета и диплома о профессиональной переподготовке.

Задачи со звездочкой (*) являются дополнительными задачами и/или задачами повышенной сложности. Они не являются обязательными к выполнению, но помогут вам глубже понять тему.

Домашнее задание выполните в файле readme.md в github репозитории. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.

Любые вопросы по решению задач задавайте в чате учебной группы.

---

## Задача 1

Сценарий выполения задачи:

- создайте свой репозиторий на https://hub.docker.com;
- выберете любой образ, который содержит веб-сервер Nginx;
- создайте свой fork образа;
- реализуйте функциональность:
запуск веб-сервера в фоне с индекс-страницей, содержащей HTML-код ниже:
```
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I’m DevOps Engineer!</h1>
</body>
</html>
```
Опубликуйте созданный форк в своем репозитории и предоставьте ответ в виде ссылки на https://hub.docker.com/username_repo.

ube@lunux-pr:~$ sudo docker pull nginx:stable-alpine
ube@lunux-pr:~$ sudo docker images
REPOSITORY   TAG             IMAGE ID       CREATED      SIZE
nginx        stable-alpine   4341472ddfe8   8 days ago   23.4MB


## Задача 2

Посмотрите на сценарий ниже и ответьте на вопрос:
"Подходит ли в этом сценарии использование Docker контейнеров или лучше подойдет виртуальная машина, физическая машина? Может быть возможны разные варианты?"

Детально опишите и обоснуйте свой выбор.

--

Сценарий:

- Высоконагруженное монолитное java веб-приложение;

Для монолитного высоконагруженного приложения подойдет физический сервер.

- Nodejs веб-приложение;

Подойдет докер контейризация.

- Мобильное приложение c версиями для Android и iOS;

Подойдет докер контейризация.

- Шина данных на базе Apache Kafka;

Виртуальная машина.

- Elasticsearch кластер для реализации логирования продуктивного веб-приложения - три ноды elasticsearch, два logstash и две ноды kibana;

Виртуальная машина или физические серверы.

- Мониторинг-стек на базе Prometheus и Grafana;

Подойдет докер контейризация.

- MongoDB, как основное хранилище данных для java-приложения;

Физический сервер при большой нагрузке. При не большой нагрузке виртуальная машина.

- Gitlab сервер для реализации CI/CD процессов и приватный (закрытый) Docker Registry.

Виртуальная машина. Для сервисов подойдет докер контейризация.


## Задача 3

- Запустите первый контейнер из образа ***centos*** c любым тэгом в фоновом режиме, подключив папку ```/data``` из текущей рабочей директории на хостовой машине в ```/data``` контейнера;

ube@lunux-pr:~$ sudo docker run -it --rm -d --name centos -v $(pwd)/data:/data centos:latest
Unable to find image 'centos:latest' locally
latest: Pulling from library/centos
a1d0c7532777: Pull complete
Digest: sha256:a27fd8080b517143cbbbab9dfb7c8571c40d67d534bbdee55bd6c473f432b177
Status: Downloaded newer image for centos:latest
6977075239f6f3afc7702dfcad13101c3995faa60e5d363cb9ab42a67b2547fb

- Запустите второй контейнер из образа ***debian*** в фоновом режиме, подключив папку ```/data``` из текущей рабочей директории на хостовой машине в ```/data``` контейнера;

ube@lunux-pr:~$ sudo docker run -it --rm -d --name debian -v $(pwd)/data:/data debian:latest
Unable to find image 'debian:latest' locally
latest: Pulling from library/debian
e756f3fdd6a3: Pull complete
Digest: sha256:3f1d6c17773a45c97bd8f158d665c9709d7b29ed7917ac934086ad96f92e4510
Status: Downloaded newer image for debian:latest
ed2e679bc1fad12355b85e757e65b7533857f1ae9e2338886a1f6a70079265d3

- Подключитесь к первому контейнеру с помощью ```docker exec``` и создайте текстовый файл любого содержания в ```/data```;

ube@lunux-pr:~$ sudo docker exec -it centos bash
[root@6977075239f6 /]# echo "This file is written to docker CentOS" >> /data/centos.txt
[root@6977075239f6 /]# exit

- Добавьте еще один файл в папку ```/data``` на хостовой машине;

ube@lunux-pr:~$ sudo su
root@lunux-pr:/home/ube# echo "This file is written to host" >> data/host.txt

- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в ```/data``` контейнера.

ube@lunux-pr:~$ sudo docker exec -it debian bash
root@ed2e679bc1fa:/# ls data/
centos.txt  host.txt




