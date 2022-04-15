# Exchange Backend sever

## [Ссылка на проект](https://besthack.alersh.ru/) 

## Запуск
Создать базу данных Postgres и инициализировать ее данными из файла ./src/database/init.sql

В корневой директории создать файл .env следующего вида

```
PORT=5000 # Порт
ALLOW_LIST=http://localhost:3000 https://alersh.ru # Настройки CORS


# Данные для подключения к БД
PGUSER=a.ershkov
PGHOST=localhost
PGPASSWORD=52752862
PGDATABASE=exchange
PGPORT=5432

# Ключ для шифрования jwt токена
PRIVATE_KEY=key

# Ключ для апи https://finnhub.io/docs/api/stock-candles
FINNHUB_KEY=sandbox_c9a7hoiad3icvte9hu2g

# Списко акции которые хотим получать и обновлять
SYMBOLS=AAPL,IBM
```


```bash

npm ci

# Парсим базовую информацию об акциях
npm run parseStocks

# Парсим информацию о цене. Можно поставить джобу на крон и через опредленное время обновлять цену. Цель таких решений, эконмия запросов в апи
npm run parseQuotes

# Для разработки (Для продовой разработки можно использовать что-то вроде pm2 или forever)
npm run dev 
```

## Технические решение

Построен на Node JS + Typescript + Express. Для авторизации используем jwt токен с id пользователя внури, чтобы не поднимать in-memory базу вроде redis.

Из интересных технических решений сделали общие тайпинги и утилиты для фронта и бека. Оформили в виде npm пакета https://www.npmjs.com/package/besthack_exchange_api_typings_and_utils

Конфиг апи находится в ./src/api/index.ts
