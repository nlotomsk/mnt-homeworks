# Домашнее задание к занятию 12 «GitLab»

## Подготовка к выполнению

1. Подготовьте к работе GitLab [по инструкции](https://cloud.yandex.ru/docs/tutorials/infrastructure-management/gitlab-containers).
2. Создайте свой новый проект.
3. Создайте новый репозиторий в GitLab, наполните его [файлами](./repository).
4. Проект должен быть публичным, остальные настройки по желанию.

## Основная часть

### DevOps

В репозитории содержится код проекта на Python. Проект — RESTful API сервис. Ваша задача — автоматизировать сборку образа с выполнением python-скрипта:

1. Образ собирается на основе [centos:7](https://hub.docker.com/_/centos?tab=tags&page=1&ordering=last_updated).
2. Python версии не ниже 3.7.
3. Установлены зависимости: `flask` `flask-jsonpify` `flask-restful`.
4. Создана директория `/python_api`.
5. Скрипт из репозитория размещён в /python_api.
6. Точка вызова: запуск скрипта.
7. При комите в любую ветку должен собираться docker image с форматом имени hello:gitlab-$CI_COMMIT_SHORT_SHA . Образ должен быть выложен в Gitlab registry или yandex registry.

   ![image](https://github.com/nlotomsk/mnt-homeworks/assets/93542374/ea3f56ab-fd72-475a-a580-d00ef12e8539)

   ![image](https://github.com/nlotomsk/mnt-homeworks/assets/93542374/2b4aa62f-b72a-40b0-80db-7448d2349488)

   ![image](https://github.com/nlotomsk/mnt-homeworks/assets/93542374/86ffdb11-0941-4285-be53-107223df0c72)

   ![image](https://github.com/nlotomsk/mnt-homeworks/assets/93542374/b5c136a7-4fe0-4fb5-ae71-c67a185fceba)
 
  
8.* (задание необязательное к выполению) При комите в ветку master после сборки должен подняться pod в kubernetes. Примерный pipeline для push в kubernetes по [ссылке](https://github.com/awertoss/devops-netology/blob/main/09-ci-06-gitlab/gitlab-ci.yml).
Если вы еще не знакомы с k8s - автоматизируйте сборку и деплой приложения в docker на виртуальной машине.

### Product Owner

Вашему проекту нужна бизнесовая доработка: нужно поменять JSON ответа на вызов метода GET `/rest/api/get_info`, необходимо создать Issue в котором указать:

1. Какой метод необходимо исправить.
2. Текст с `{ "message": "Already started" }` на `{ "message": "Running"}`.
3. Issue поставить label: feature.

![image](https://github.com/nlotomsk/mnt-homeworks/assets/93542374/8235dcda-8a48-4a30-a006-3ffcffdb5ebe)


### Developer

Пришёл новый Issue на доработку, вам нужно:

1. Создать отдельную ветку, связанную с этим Issue.
2. Внести изменения по тексту из задания.
3. Подготовить Merge Request, влить необходимые изменения в `master`, проверить, что сборка прошла успешно.

![image](https://github.com/nlotomsk/mnt-homeworks/assets/93542374/ba9c7373-49d5-444b-9854-6e89c8aa60db)

![image](https://github.com/nlotomsk/mnt-homeworks/assets/93542374/56436f87-ad2a-4260-921d-e880e771f4ac)

![image](https://github.com/nlotomsk/mnt-homeworks/assets/93542374/114c640c-eab4-4191-8f4e-88767cd58b31)

![image](https://github.com/nlotomsk/mnt-homeworks/assets/93542374/754d31d5-a0ab-43fb-adee-50cde4986bbb)



### Tester

Разработчики выполнили новый Issue, необходимо проверить валидность изменений:

1. Поднять докер-контейнер с образом `python-api:latest` и проверить возврат метода на корректность.
2. Закрыть Issue с комментарием об успешности прохождения, указав желаемый результат и фактически достигнутый.

   ![image](https://github.com/nlotomsk/mnt-homeworks/assets/93542374/94c202c9-cbc8-4053-a2c2-c582b6efb0c2)

   var_3. Не сохранились изменения

   ![image](https://github.com/nlotomsk/mnt-homeworks/assets/93542374/5576e15a-071f-47df-9c44-30fb7f637440)

   ![image](https://github.com/nlotomsk/mnt-homeworks/assets/93542374/2987e997-c354-4bfc-bba3-5342566bb2d0)

   ![image](https://github.com/nlotomsk/mnt-homeworks/assets/93542374/b9ed20b7-b6f2-4bfd-80da-90ab867acff5)

   ![image](https://github.com/nlotomsk/mnt-homeworks/assets/93542374/4ba9dccf-127f-41c6-8b47-2151c109bbc3)

## Итог

В качестве ответа пришлите подробные скриншоты по каждому пункту задания:

- файл gitlab-ci.yml;
- Dockerfile; 
- лог успешного выполнения пайплайна;
- решённый Issue.

### Важно 
После выполнения задания выключите и удалите все задействованные ресурсы в Yandex Cloud.

## Необязательная часть

Автомазируйте работу тестировщика — пусть у вас будет отдельный конвейер, который автоматически поднимает контейнер в docker или k8s и выполняет проверку, например, при помощи curl. На основе вывода будет приниматься решение об успешности прохождения тестирования.

