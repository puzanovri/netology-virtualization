# Домашнее задание к занятию "6.5. Elasticsearch"

## Задача 1

В этом задании вы потренируетесь в:
- установке elasticsearch
- первоначальном конфигурировании elastcisearch
- запуске elasticsearch в docker

Используя докер образ [centos:7](https://hub.docker.com/_/centos) как базовый и 
[документацию по установке и запуску Elastcisearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/targz.html):

- составьте Dockerfile-манифест для elasticsearch
- соберите docker-образ и сделайте `push` в ваш docker.io репозиторий
- запустите контейнер из получившегося образа и выполните запрос пути `/` c хост-машины

Требования к `elasticsearch.yml`:
- данные `path` должны сохраняться в `/var/lib`
- имя ноды должно быть `netology_test`

В ответе приведите:
- текст Dockerfile манифеста

![11](https://user-images.githubusercontent.com/57503209/186512050-a54eb212-261d-4e7a-b1c4-f2a71ab166d4.jpg)

- ссылку на образ в репозитории dockerhub

https://hub.docker.com/repository/docker/podkovka/devops-elasticsearch

- ответ `elasticsearch` на запрос пути `/` в json виде

![4](https://user-images.githubusercontent.com/57503209/186512219-26a32ed9-3820-4158-af1e-e335ce05d38a.jpg)

Подсказки:
- возможно вам понадобится установка пакета perl-Digest-SHA для корректной работы пакета shasum
- при сетевых проблемах внимательно изучите кластерные и сетевые настройки в elasticsearch.yml
- при некоторых проблемах вам поможет docker директива ulimit
- elasticsearch в логах обычно описывает проблему и пути ее решения

Далее мы будем работать с данным экземпляром elasticsearch.

## Задача 2

В этом задании вы научитесь:
- создавать и удалять индексы
- изучать состояние кластера
- обосновывать причину деградации доступности данных

Ознакомтесь с [документацией](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-create-index.html) 
и добавьте в `elasticsearch` 3 индекса, в соответствии со таблицей:

| Имя | Количество реплик | Количество шард |
|-----|-------------------|-----------------|
| ind-1| 0 | 1 |
| ind-2 | 1 | 2 |
| ind-3 | 2 | 4 |

![21](https://user-images.githubusercontent.com/57503209/186513674-01a46ffe-b30e-483d-922e-cfffadf11409.jpg)

Получите список индексов и их статусов, используя API и **приведите в ответе** на задание.

![22](https://user-images.githubusercontent.com/57503209/186513691-370865b6-ed03-4899-8723-a8541138b8c9.jpg)

Получите состояние кластера `elasticsearch`, используя API.

![23](https://user-images.githubusercontent.com/57503209/186513709-89feadc6-f49f-4fa5-b297-f9549e4e6a05.jpg)

Как вы думаете, почему часть индексов и кластер находится в состоянии yellow?

Первичный шард и реплика не могут находиться на одном узле, если копия не назначена. Таким образом, один узел не может размещать копии.

Удалите все индексы.

![24](https://user-images.githubusercontent.com/57503209/186513744-f5ff6c81-8ca2-449e-b496-4dc7fd98829e.jpg)

**Важно**

При проектировании кластера elasticsearch нужно корректно рассчитывать количество реплик и шард,
иначе возможна потеря данных индексов, вплоть до полной, при деградации системы.

## Задача 3

В данном задании вы научитесь:
- создавать бэкапы данных
- восстанавливать индексы из бэкапов

Создайте директорию `{путь до корневой директории с elasticsearch в образе}/snapshots`.

![31](https://user-images.githubusercontent.com/57503209/186514446-e815be25-6fc7-473c-a0e0-ade6a113d285.jpg)

Используя API [зарегистрируйте](https://www.elastic.co/guide/en/elasticsearch/reference/current/snapshots-register-repository.html#snapshots-register-repository) 
данную директорию как `snapshot repository` c именем `netology_backup`.

![32](https://user-images.githubusercontent.com/57503209/186514521-39618feb-ac2e-460b-9d68-ba1bb835a29b.jpg)

**Приведите в ответе** запрос API и результат вызова API для создания репозитория.

Создайте индекс `test` с 0 реплик и 1 шардом и **приведите в ответе** список индексов.

![33](https://user-images.githubusercontent.com/57503209/186515267-0887fdab-2167-4602-96db-5f098fc623a4.jpg)

[Создайте `snapshot`](https://www.elastic.co/guide/en/elasticsearch/reference/current/snapshots-take-snapshot.html) 
состояния кластера `elasticsearch`.

**Приведите в ответе** список файлов в директории со `snapshot`ами.

Удалите индекс `test` и создайте индекс `test-2`. **Приведите в ответе** список индексов.

[Восстановите](https://www.elastic.co/guide/en/elasticsearch/reference/current/snapshots-restore-snapshot.html) состояние
кластера `elasticsearch` из `snapshot`, созданного ранее. 

**Приведите в ответе** запрос к API восстановления и итоговый список индексов.

Подсказки:
- возможно вам понадобится доработать `elasticsearch.yml` в части директивы `path.repo` и перезапустить `elasticsearch`

---

### Как cдавать задание

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
