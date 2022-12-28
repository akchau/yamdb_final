![.github/workflows/main.yml](https://github.com/akchau/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

# yamdb

Проект для коллекционеров искуства

# Запуск
1. Клонируйте репозиторий
```bash
git clone git@github.com:akchau/yamdb_final.git
cd yamdb_final
```

2. Создайте файл виртупльного окружения. Запишите в него ваши переменные.
```bash
touch infra/.env
cp example.env .env
```

3. Разверните приложение
```bash
docker-compose up -d --build
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input
docker-compose exec web python manage.py loaddata fixtures.json
```
Приложение будет доступно
http://localhost/admin


## Регистрации пользователей
- Пользователь отправляет POST-запрос на добавление нового пользователя с параметрами email и username на эндпоинт /api/v1/auth/signup/.
- YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на адрес email.
- Пользователь отправляет POST-запрос с параметрами username и confirmation_code на эндпоинт /api/v1/auth/token/, в ответе на запрос ему приходит token (JWT-токен).
- При желании пользователь отправляет PATCH-запрос на эндпоинт /api/v1/users/me/ и заполняет поля в своём профайле (описание полей — в документации).
## Описание эндпоинтов и функционала:

Все функции и эндпоинты описаны в документации:
```
http://127.0.0.1:8000/redoc/
```
## Заполнение базы данных

Для заполнения базы данных данными предоставленными с проектом используйте команду 
```
python3 manage.py fill_db

