# docker_project
- команда для создания контейнера с бд для проекта джанго   
docker run --name db_django -p 5432:5432 
 -e POSTGRES_PASSWORD=postgres
 -e POSTGRES_DB=public 
 -e POSTGRES_HOST_AUTH_METHOD=md5 postgres

- подключение сети контейнера к локальной сети хоста и подключение к Python интерпретатору  
 docker run --network host -it python bash
- скачиваем джанго  
 pip install django

- создание проекта джанго  
 django-admin startproject docker_project
- исправляем настройки бд с помощью редактора nano

- проверяем работу проекта  
  ./manage.py runserver
System check identified no issues (0 silenced).
August 15, 2023 - 14:23:24
Django version 4.2.4, using settings 'docker_project.settings'
Starting development server at http://127.0.0.1:8000/