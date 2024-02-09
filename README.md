# Ads board

## Описание

Проект представляет собой backend-часть для сайта объявлений. 
Предполагает реализацию следующего функционала:

- Авторизация и аутентификация пользователей.
- Распределение ролей между пользователями (пользователь и админ).
- Восстановление пароля через электронную почту (не обязательно).
- CRUD для объявлений на сайте (админ может удалять или редактировать все объявления, а пользователи только свои).
- Под каждым объявлением пользователи могут оставлять отзывы.
- В заголовке сайта можно осуществлять поиск объявлений по названию.


## Подготовка к работе с проектом

### Шаг 1: Клонирование проекта
1. Зайти в терминал
2. С помощью команды `cd` перейти в директорию, где будет находиться проект
3. Клонировать проект
```bash
git clone https://github.com/KatyshaVtyrina/Ads-board-.git
```

### Шаг 2: Настройка окружения
1. В директории проекта создать файл `.env`

3. Записать в файл следующие настройки
```bash
POSTGRES_DB=название базы данных (skymarket)
POSTGRES_USER=имя пользователя (postgres)
POSTGRES_PASSWORD=пароль
POSTGRES_HOST = db
POSTGRES_PORT=5432
```
*В проекте есть шаблон файла .env - `.env_example`

### Шаг 3: Создание образа и запуск проекта
Выполнить команду в терминале
```bash
docker-compose up --build  
```


### Шаг 4: Загрузка данных
Выполнить команды
```bash
docker-compose exec app python3 manage.py loaddata users.json
docker-compose exec app python3 manage.py loaddata ad.json
docker-compose exec app python3 manage.py loaddata comments.json
```


## Работа с сервисом через Postman

1. Получить токен
```bash
POST: http://localhost:8000/api/token/
body: {
  "email": <электронная почта>,
  "password": <пароль>
  }
```
2. Подключить авторизацию по токену

3. Эндпоинты:
1) Создание объявления
```bash
POST: http://localhost:8000/api/ads/
body: {
    "title": "Компьютер недорого",
    "price": 10000,
    "description": "Компьютер недорого"
  } 
  
      *image, created_at - необязательны для заполнения 
```
2) Просмотр детальной информации об объявлении
```bash
GET: http://localhost:8000/api/ads/<id_объявления>/
```
3) Просмотр всех объявлений
```bash
GET: http://localhost:8000/api/ads/
```
4) Редактирование объявления
```bash
PUT: http://localhost:8000/api/ads/<id_объявления>/
PATCH: http://localhost:8000/api/ads/<id_объявления>/
```
5) Удаление объявления
```bash
DELETE: http://localhost:8000/api/ads/<id_объявления>/
```
6) Просмотр отзывов определенного объявления
```bash
GET: http://localhost:8000/api/ads/<id_объявления>/comments
```
7) Просмотр конкретного отзыва определенного объявления
```bash
GET: http://localhost:8000/api/ads/<id_объявления>/comments/<id_отзыва>/
```
8) Изменение отзыва
```bash
PUT: http://localhost:8000/api/ads/<id_объявления>/comments/<id_отзыва>/
PATCH: http://localhost:8000/api/ads/<id_объявления>/comments/<id_отзыва>/
```
9) Удаление отзыва
```bash
DELETE: http://localhost:8000/api/ads/<id_объявления>/comments/<id_отзыва>/
```

## Просмотр документации
### Swagger
```bash
http://localhost:8000/swagger/
```
### Redoc
```bash
http://localhost:8000/redoc/
```