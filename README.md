# Запуск docker-compose
## Описание проекта
Приложение YaMDb состоит из нескольких сервисов, запущеные в разных, связанных контейнерах:
- База Данных PostgreSQL
- Nginx и Gunicorn
- [Django-проект YaMDb](https://github.com/Denis-Guselnikov/api_yamdb)
  
## Для реализации проекта используются:
- Python 3.7.9
- Django 2.2.16
- Django REST Framework 3.12.4
- gunicorn 20.0.4
- psycopg2-binary
- docker
- docker-compose

## Запуск проекта
- Клонировать репозиторий https://github.com/Denis-Guselnikov/infra_sp2
- Для работы с Базой Данных в (infra_sp2/infra/nginx) создайте файл .env с переменными

```
DB_ENGINE=django.db.backends.<указываем, с какой БД работаем> 

DB_NAME=<Имя базы данных> 

POSTGRES_USER=<логин для подключения к базе данных>

POSTGRES_PASSWORD=<пароль для подключения к БД>

DB_HOST=<название сервиса (контейнера)>

DB_PORT=<порт для подключения к БД>
```

- Запустите контейнеры:
```
docker-compose up -d
```

- Выполните миграции:
```
docker-compose exec web python manage.py migrate
```

- Создайте суперюзера:
```
docker-compose exec web python manage.py createsuperuser
```

- Подгрузите статику:
```
docker-compose exec web python manage.py collectstatic --no-input
```

- Заполните базу данными:
```
docker-compose exec web python manage.py loaddata fixtures.json
```

- Проект доступен по адресам:
<br> [http://localhost/](http://localhost/)
<br>[http://localhost/admin/]( http://localhost/admin) - админ панель
<br>[http://localhost/redoc/](http://localhost/redoc/) - документация проекта
