# docker_project

1. docker network create my-network
2. docker run -d --name django_app --network my-network -p 8000:8000 -it python bash
3. docker run -d --name postgres-container --network my-network -p 5432:5432 -e POSTGRES_PASSWORD=postgres -e
   POSTGRES_DB=lab -e POSTGRES_HOST_AUTH_METHOD=md5 postgres
4. Захожу в постгрес docker exec -it <айди контейнера> psql -U postgres
5. Создаю там бд create database mydb
6. Захожу в Python docker exec -it <айди контейнера> bash
7. Установка зависимостей
8. Захожу в джанго
9. Создание проекта
10. Настройки DATABASES = {
    'default': {
    'ENGINE': 'django.db.backends.postgresql',
    'NAME': 'mydb',
    'USER': 'myuser',
    'PASSWORD': 'mypassword',
    'HOST': 'postgres-container', # Имя контейнера PostgreSQL
    'PORT': '5432',
    }
    }
10. Миграции
11. перезапуск докеров
12. запуск через ./manage.py runserver 0.0.0.0:80000/