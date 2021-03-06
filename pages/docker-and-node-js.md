# Docker и NodeJS

- [Приложение](#приложение)
- [Dockerfile](#dockerfile)
- [.dockerignore](#dockerignore)
- [Сборка образа](#сборка-образа)
- [Запуск образа](#запуск-образа)
- [Доступ к данным контейнера](#доступ-к-данным-контейнера)

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

На `Windows` перед сборкой запускаем `Docker Desktop` и ждем когда запустится.

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

Проверка: [http://localhost:8080/](http://localhost:8080/)

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

## Где брать образы

[https://hub.docker.com/](https://hub.docker.com/)

Ранее, в `Dockerfile` было указано `FROM node:18`. Это не какая то магия, это тип и версия образа который Docker скачивает с сайта [https://hub.docker.com/](https://hub.docker.com/) и затем помещает в него наше приложение. 

Читая информацию о образах node на сайте [https://hub.docker.com/_/node](https://hub.docker.com/_/node) узнаем, что есть версия `alpine` и `slim`. 

- `alpine` - образ на базе легковесного [Alpine linux](https://www.alpinelinux.org/).
- `slim` - не рекомендованная, урезанная версия образа с минимумом для запуска node приложений.

Пробуем, и а результате получаем следующие размеры образа:

- `node:18` - 1 Gb
- `node:18-alpine` - 179 Mb
- `node:18-slim` - 242 Mb

## Доступ к данным контейнера

Официальная документация: [https://docs.docker.com/storage/](https://docs.docker.com/storage/)

### Типы хранилищ

- `Volume` (том) - некое хранилище расположенное в дебрях Docker'а которое привязывается к пути (папке) в контейнере.
- `Bind` (привязка) - связывает папку в контейнере с папкой хоста (компьютера).
- `tmpfs` - том в виртуальной памяти. Быстро, но данные не сохранятся и будут доступны только во время сессии хоста (при перезагрузке или выключении все пропадет).

### Приоритет хранилища

__Важно__: папка хранилища важнее папки контейнера. Иначе говоря, не папка контейнера расщаривается в хранилище а папка хранилища расшаривается в контейнер. 

Не получится расшарить корневую систему контейнера, что бы посмотреть как там все устроено или папку приложения, что бы поглядеть как оно там живет. При попытке связать папку приложения `/app` с пустой папкой на диске `c:/myappfolder` при запуске контейнер выдаст ошибку, так как папка `/app` окажется пуста и системе будет нечего запускать.

Будьте внимательны, создавайте отдельные папки для обмена данными, например `/app/uploads`.

### Связь с хранилищем

При запуске контейнера можно указать параметр `mount` или `-v` / `-volume`. Параметры делают одно и тоже, но `-v` более компактный, а `mount` более подробный.

Привязка папки хоста:

```
docker run -v z:\uploads:/app/uploads -d -p 80:80 --name container-name container-image 
```

Привязка к тому (volume):

```
docker volume create volume_name
docker run -v volume_name:/app/uploads -d -p 80:80 --name container-name container-image 
```

Управление томами:

```
# Создать.
docker volume create volume_name

# Информация о томе.
docker volume inspect volume_name

# Удалить том.
docker volume rm volume_name
```