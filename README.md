# Инструкция по работе с Docker

1) Установить docker, выбрав соответствующую ОС.
   https://docs.docker.com/get-docker/
   Убедиться в корректности установки можно с помощью вызова в терминале команды docker version.
   В случае успешной установки в терминале можно будет увидеть информацию о Client и Server.


2) Загрузить официальные образы python и postgres c https://hub.docker.com, выполнив соответствующие команды в
   терминале:
   docker pull postgres
   docker pull python

   Детали по образам можно изучить по ссылкам:
   https://hub.docker.com/_/python
   https://hub.docker.com/_/postgres


3) Создать общую сеть для контейнеров, с помощью команды:
   docker network create my_network


4) Запустить контейнер postgres, с присвоенным именем контейнера db_my_django,
   настроенными переменными окружения (флаг -e) и volumes (флаг -v, c {PWD} справа от ':'), с помощью команды:
   docker run -d --name db_my_django --network my_network -p 5432:5432 -e POSTGRES_PASSWORD=postgres
   -e POSTGRES_DB=new_db -e POSTGRES_HOST_AUTH_METHOD=md5
   -v C:\Users\Vedis\PycharmProjects\tmp\pgdata:/var/lib/postgresql/data postgres


5) Запустить контейнер python, с присвоенным именем контейнера my_django_project, в интерактивном режиме (флаг -it),
   с синxронизацией настроек сети локальной машины и контейнера (настройка --network).
   docker run -d --name my_django_project --network my_network -p 8000:8000 -it python bash


6) Зайти в bash интерпретатор: docker exec -it <айди контейнера> bash
   Находясь в bash интерпретаторе среды контейнера my_django_project, установить django, psycopg2, nano редактор,
   для запуска и настройки django проекта в среде контейнера, выполнив команды:
   pip install django
   pip install psycopg2
   apt-get update
   apt-get install nano
   С помощью команды django-admin находим нужную команду для создания проекта.
   С помощью команды django-admin startproject <название проекта> создаем проект Django


7) Скорректировать настройки в файле settings.py django проекта, открыв файл с помощью команды nano app/settings.py,
   и перейдя к настройкам в словаре 'DATABASES':
   Заменить 'sqlite3' на 'postgresql' для настройки 'ENGINE'.
   Заменить на установленное имя базы данных для настройки 'NAME' (new_db в данном примере).
   Добавить настройку 'USER' со значением 'postgres'.
   Добавить настройку 'PASSWORD' со значением, переданным как переменная окружения.
   Добавить настройку 'HOST' со значением имени контейнера postgres (db_my_django в данном примере).
   Добавить настройку 'PORT' со значением '5432'.
   Добавить '127.0.0.1' в список разрешенных хостов ALLOWED_HOST в том же файле app/settings.py.
   Сохранить изменения, выйти из документа.
   C помощью команды ./manage.py runserver проверяем работу сервера. Нас просят осуществить миграцию.
   С помощью команды ./manage.py migrate осуществляем миграцию.


8) Заходим в Docker-Desktop и перезагружаем контейнеры.


9) Находясь в bash интерпретаторе среды контейнера со значением Image Python(как зайти в bash смотреть в пункте 6), запустить django проект из папки проекта,
   с помощью команды:
   ./manage.py runserver 0.0.0.0:8000
   Страница проекта будет доступна по http://127.0.0.1:8000/ в браузере на хостовой машине.
   Должна появиться стартовая страница проекта Django с изображением ракеты и надписью:
   The install worked successfully! Congratulations!
   You are seeing this page because DEBUG=True is in your settings file and you have not configured any URLs.

# Надеюсь у вас все получится!