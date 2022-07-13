# Персональные токены доступа в GitHub

Как я понял, `токены` пришли на замену пароля для защиты аккаунта от несанкционированного доступа. Смысл в том, что при работе с вашими репозиториями больше не нужно использовать пароль от аккаунта. В место пароля  используем токен.

Разумно, здорово.

## Создание токена

Что бы получить персональный токен заходим в настройки аккаунта `Settings`.

![Settings](assets/github-access-token/20220713_110535.png)

Слева в меню выбираем `Developer settings`.

![Developer settings](assets/github-access-token/20220713_110842.png)

В меню выбираем `Personal access token`.

![Personal access token](assets/github-access-token/20220713_111136.png)

Создаем новый токен `Generate new token`.

![Generate new token](assets/github-access-token/20220713_111911.png)

Указываем заметки `Note`, время жизни `Expiration` и разрешения для токена `Scopes`. 

![Установки](assets/github-access-token/20220713_111426.png)

Полученный токен используем вместо пароля при работе с репозиториями.