### praktikum_diplom

<!-- (Николай, привет. Если ты можешь, прими пожалуйста диплом в таком виде. У меня крайний срок сегодня(25.11) его сдать, иначе 40к придется заплатить. Я честно пытался его привести в боевое состояние, но так и не смог одолеть 500 ошибку(наставники тоже в замешательстве). Всю эту неделю со времени твоего последнего ревью, я старался, но увы. Если ты мне сможешь помочь, я буду тебе очень признателен.) -->

![workflow](https://github.com/Rocker9137/foodgram-project-react/actions/workflows/main.yml/badge.svg)

## Стек технологий

[![Python](https://img.shields.io/badge/-Python-464646?style=flat-square&logo=Python)](https://www.python.org/)
[![Django](https://img.shields.io/badge/-Django-464646?style=flat-square&logo=Django)](https://www.djangoproject.com/)
[![Django REST Framework](https://img.shields.io/badge/-Django%20REST%20Framework-464646?style=flat-square&logo=Django%20REST%20Framework)](https://www.django-rest-framework.org/)
[![PostgreSQL](https://img.shields.io/badge/-PostgreSQL-464646?style=flat-square&logo=PostgreSQL)](https://www.postgresql.org/)
[![Nginx](https://img.shields.io/badge/-NGINX-464646?style=flat-square&logo=NGINX)](https://nginx.org/ru/)
[![gunicorn](https://img.shields.io/badge/-gunicorn-464646?style=flat-square&logo=gunicorn)](https://gunicorn.org/)
[![docker](https://img.shields.io/badge/-Docker-464646?style=flat-square&logo=docker)](https://www.docker.com/)
[![GitHub%20Actions](https://img.shields.io/badge/-GitHub%20Actions-464646?style=flat-square&logo=GitHub%20actions)](https://github.com/features/actions)
[![Yandex.Cloud](https://img.shields.io/badge/-Yandex.Cloud-464646?style=flat-square&logo=Yandex.Cloud)](https://cloud.yandex.ru/)

## Описание проекта
# Foodgram - «Продуктовый помощник»

Это онлайн-сервис и API для него. На этом сервисе пользователи могут публиковать рецепты, подписываться на публикации других пользователей, добавлять понравившиеся рецепты в список «Избранное», а перед походом в магазин скачивать сводный список продуктов, необходимых для приготовления одного или нескольких выбранных блюд.

Проект использует базу данных PostgreSQL. Проект запускается в трёх контейнерах (nginx, PostgreSQL и Django) (контейнер frontend используется лишь для подготовки файлов) через docker-compose на сервере. Образ с проектом загружается на Docker Hub.

Проект доступен по [адресу](http://51.250.26.230/)

Документация к API доступна [здесь](http://51.250.26.230/api/docs/)

Админ: rocker9137@yandex.ru

Пароль: Admin9137

В документации описаны возможные запросы к API и структура ожидаемых ответов. Для каждого запроса указаны уровни прав доступа.

## Запуск проекта с помощью Docker

1. Склонируйте репозиторий на локальную машину.

    ```
    git clone git@github.com:Rocker9137/foodgram-project-react.git
    ```

2. Создайте .env файл в директории backend/foodgram/, в котором должны содержаться следующие переменные для подключения к базе PostgreSQL:

    ```
    DB_ENGINE=django.db.backends.postgresql
    DB_NAME=postgres
    POSTGRES_USER=postgres
    POSTGRES_PASSWORD=postgres
    DB_HOST=db
    DB_PORT=5432
    ```

3. Перейдите в директорию infra/ и выполните команду для создания и запуска контейнеров.
    ```
    sudo docker-compose up -d --build
    ```
> Возможна команда **$ sudo docker compose up -d --build** (зависит от версии docker compose)

> В Windows команда выполняется без **sudo**

4. В контейнере backend выполните миграции, создайте суперпользователя и соберите статику.

    ```
    sudo docker-compose exec backend python manage.py migrate
    sudo docker-compose exec backend python manage.py createsuperuser
    sudo docker-compose exec backend python manage.py collectstatic --no-input 
    ```

5. Загрузите в бд ингредиенты командой ниже.

    ```
    sudo docker-compose exec backend python manage.py loaddata ingredients.json
    ```

6. Готово! Ниже представлены доступные адреса проекта:
    -  http://localhost/ - главная страница сайта;
    -  http://localhost/admin/ - админ панель;
    -  http://localhost/api/ - API проекта
    -  http://localhost/api/docs/redoc.html - документация к API

---

### После каждого обновления репозитория (push в ветку master) будет происходить:

1. Проверка кода на соответствие стандарту PEP8 (с помощью пакета flake8)
2. Сборка и доставка докер-образов frontend и backend на Docker Hub
3. Разворачивание проекта на удаленном сервере
4. Отправка сообщения в Telegram в случае успеха

## Автор
**[Мокроусов Алексей](https://github.com/Rocker9137)** - создание api, деплой на сервер.
