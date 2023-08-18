# Инструкция по работе с Dockerfile и docker-compose

1) Создаем django проект или заходим в существующий проект.


2) Создаем внутри проекта Dockerfile(обычно он находится в корневой папке проекта).


3) Описываем внутри Dockerfile инструкции для построения Docker-образа:
   FROM python:3

   WORKDIR /code

   COPY /requirements.txt /code/

   RUN pip install -r requirements.txt

   COPY . . 


4) Создаем docker-compose.yml(расширение либо yaml, либо yml).


5) Определим все компоненты приложения, их настройки и взаимодействия:


### Версия

Версия docker-compose: `version: '3'`

### Сервисы

- `db`:
  - `image: postgres`
  - `environment:`
    - `POSTGRES_PASSWORD: mypassword`
    - `PGDATA: /var/lib/postgresql/data/pgdata`
- `app`:
  - `build: .`
  - `command: python manage.py runserver 0.0.0.0:8000`
  - `ports:`
    - `'8000:8000'`
  - `depends_on:`
    - `db`



6) Cобираем образ с помощью команды:
   docker-compose build


7) Запустите контейнеры с помощью команды:
   docker-compose up


8) Применяем миграции с помощью команды:
   docker-compose exec app python manage.py migrate



   