# Docker и NodeJS

- [Приложение](#приложение)
- [Dockerfile](#dockerfile)
- [.dockerignore](#dockerignore)
- [Сборка образа](#сборка-образа)
- [Запуск образа](#запуск-образа)

## Приложение

Тренироваться будем на простеньком серверном приложении написанном под `NodeJS` с использованием библиотеки `express`, которое будет висеть на порту `80` и возвращать строку `Hello World!`.

Файл: `server.js`

```javascript
const express = require('express')
const app = express()
const port = 80

app.get('/', (req, res) => {
    res.send("Hello World!")
})

app.listen(port, () => {
    console.log(`listen on port: ${port}`)
})
```

## Dockerfile

`Dockerfile` - файл который содержит набор инструкций для построения docker образа.

Создаем `Dockerfile` в папке с проектом.

```docker
# syntax=docker/dockerfile:1

FROM node:18

ENV NODE_ENV=production

# Директория приложения
WORKDIR /app

# Копируем package.json и package-lock.json
# в папку /app
COPY ["package.json", "package-lock.json", "./"]

# Подгружаем библиотеки
RUN npm install --production

# Копируем содержимое папки в /app
COPY . .

# Задаем команду для запуска сервера
CMD [ "node", "server.js" ]
```

## .dockerignore

`.dockerignore` - файл содержащий список файлов которые не нужно копировать во время сборки проекта.

```
node_modules
```

## Сборка образа

На `Windows` перед сборкой запускаем `Docker Desktop`.

```
docker build --tag nodejs .
```

> WOW.... Размер образа 1GB O_o

### Посмотреть список существующих образов:

```
docker images

или

docker image ls
```

### Удалить образ:

```
docker image rm nodejs
```

## Запуск образа

### Создаем и запускаем контейнер

```
docker run -d -p 8080:80 --name nodejs-server nodejs
```
- `-d` - запуск в фоновом режиме.
- `-p` - связывает порт 8080 на хосте (вашем компьютере) с портом 80 в контейнере.
- `--name` - имя контейнера.
  
  Если не указать генерируется рандомно.
  
  Используется для управление контейнером.

  Вместо имени можно использовать `CONTAINER ID`, но он неудобен для печати.

- `nodejs` - название образа.

Проверка: http://localhost:8080/

### Список контейнеров.

```
docker ps -a
```

### Остановка контейнера

```
docker stop nodejs-server
```

### Удаление контейнера

```
docker rm nodejs-server
```