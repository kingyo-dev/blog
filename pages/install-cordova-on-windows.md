# Установка и настройка Apache Cordova на Windows для создания приложения на Android

- [Установка Open JDK (Java Development Kit)](#установка-open-jdk-java-development-kit)
- [Установка Gradle](#установка-gradle)
- [Установка Android Studio](#установка-android-studio)
- [Установка Apache Cordova](#установка-apache-cordova)
- [Создание проекта](#создание-проекта)
- [Запуск проекта](#запуск-проекта)
- [Сборка проекта](#сборка-проекта)
- [Иконка приложения](#иконка-приложения)

`Apache Cordova` позволяет программистам создавать приложения для мобильных устройств с помощью `CSS3`, `HTML5` и `JavaScript`, вместо того, чтобы использовать конкретные платформы API, такие как `Android`, `IOS` или `Windows Phone`.

# Установка Open JDK (Java Development Kit)

`Open JDK` - комплект разработчика приложений на `Java`.

Скачать и распаковать в папку с программами: [openjdk-11.0.2_windows-x64_bin.zip](https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2_windows-x64_bin.zip)

Страница скачивания OpenJDK: [https://jdk.java.net/archive/](https://jdk.java.net/archive/)

Добавляем переменную окружения `JAVA_HOME`:

```
JAVA_HOME = z:\Programs\jdk\jdk-11.0.2
```

![JAVA_HOME](assets/install-cordova-on-windows/20220724_145002.png)

Добавляем путь в `PATH`

```
z:\Programs\jdk\jdk-11.0.2\bin
```

![PATH](assets/install-cordova-on-windows/20220724_145254.png)

# Установка Gradle

`Gradle` - пакетный менеджер для Java.

Скачать и распаковать в папку с программами: [https://gradle.org/releases/](https://gradle.org/releases/)

Добавляем путь в `PATH`

```
z:\Programs\gradle-7.4.2\bin
```

![jdk-18.0.1.1\bin](assets/install-cordova-on-windows/20220724_145112.png)


# Установка Android Studio

`Android Studio` - среда разработки приложений для `Android`.

Скачать и распаковать в папку с программами или установить: [https://developer.android.com/studio#downloads](https://developer.android.com/studio#downloads)

Я использую `zip` версию (No .exe installer), по этому порядок действий может отличаться от инсталлятора.

Запускаем `studio64.exe`.

Импортирование настроек - импортировать нечего, устанавливаем в `Do not import`.

![Import Android Studio Settings](assets/install-cordova-on-windows/20220724_134840.png)

Помощь в улучшении `Android Studio` - выбираем по вкусу.

![Help Improve Android Studio](assets/install-cordova-on-windows/20220724_135042.png)

Тип инсталляции - выборочная (`custom`).

![Install Type](assets/install-cordova-on-windows/20220724_135233.png)

Указываем папку с JDK которое будет использовать Gradle для сборки проектов.

![JDK Folder](assets/install-cordova-on-windows/20220724_135538.png)

Выбираем тему редактора.

![Theme](assets/install-cordova-on-windows/20220724_135708.png)

Указываем папку где будут храниться файлы `Android SDK`.

![Android SDK](assets/install-cordova-on-windows/20220724_135856.png)

![Android SDK folder](assets/install-cordova-on-windows/20220724_140015.png)

Соглашаемся с лицензией и скачиваем компоненты Android SDK.

![License](assets/install-cordova-on-windows/20220724_140240.png)

Ждем окончания загрузки и установки компонент.

![Download Components](assets/install-cordova-on-windows/20220724_140340.png)

На этом моменте мастер настроек заканчивается и Вас направляют в окно приветствия `Android Studio`.

Настройки сохраняются в папку:

```
%APPDATA%/Google/AndroidStudio2021.2
```

Для меня это:

```
c:\Users\Ivan\AppData\Roaming\Google\AndroidStudio2021.2
```

> Если удалить папку настроек, то мастер настроек запуститься вновь при запуске `studio64.exe`.

Идем в настройки `Android SDK` - `Projects` / `More Actions` / `SDK Manager`

![SDK Manager](assets/install-cordova-on-windows/20220724_141439.png)

В разделе `Appearance & Behavior` \ `System Settings` \ `Android SDK` \ `SKD Tools` указываем следующие компоненты:

- Android SDK Command-line Tools (latest)

![Android SDK Command-line Tools (latest)](assets/install-cordova-on-windows/20220724_142129.png)

Жмем `Apply` и загружаем указанные пакеты.

![Download](assets/install-cordova-on-windows/20220724_142643.png)

Ставим галочку на `Show Package Details` и подключаем `Android SDK Build Tools` версии `30.0.3`. Установленную по умолчанию версию можно отключить.

![30.0.3](assets/install-cordova-on-windows/20220724_142855.png)

Жмем `Apply`, качаем пакеты.

Жмем `OK` и возвращаемся в окно приветствия.

Добавляем системную переменную `ANDROID_SDK_ROOT` указывающую на папку в которой хранится SDK.

```
ANDROID_SDK_ROOT = `z:\Programs\android-sdk`
```

![ANDROID_SDK_ROOT](assets/install-cordova-on-windows/20220724_143651.png)

Узнать, путь к Android SDK на вашей машине можно в настройках SDK - `Android SDK` - `Projects` / `More Actions` / `SDK Manager`

![Android SDK Location](assets/install-cordova-on-windows/20220724_144108.png)

Добавляем в `PATH` следующие пути:

- z:\Programs\android-sdk\cmdline-tools\latest\bin
- z:\Programs\android-sdk\platform-tools
- z:\Programs\android-sdk\emulator
- z:\Programs\android-sdk\build-tools\33.0.0

![PATH](assets/install-cordova-on-windows/20220724_144718.png)

Возвращаемся в `Android Studio` и заходим в `Projects` / `More Actions` / `Virtual Device Manager`

![Virtual Device Manager](assets/install-cordova-on-windows/20220724_145536.png)

Жмем `Create Device`.

![Create Device](assets/install-cordova-on-windows/20220724_145807.png)

Выбираем модель устройства которое будет эмулироваться.

![Select Device](assets/install-cordova-on-windows/20220724_150031.png)

Выбираем интересующую нас операционную систему. Если активен пункт `download` жмем его, для того что бы скачать образ системы.

![Select a system image](assets/install-cordova-on-windows/20220724_150214.png)

Указываем имя устроиства `default`. Это важно, так как `Cordova` по умолчанию будет использовать устройство с именем `default` при отладке вашего проекта. Иначе, придется указывать имя устройства в ручную, что усложнит команду запуска.

![AVD Name](assets/install-cordova-on-windows/20220724_150519.png)

Запускаем созданное устройство для того, что бы убедится в том, что оно работает.

![Run](assets/install-cordova-on-windows/20220724_150904.png)

![Android](assets/install-cordova-on-windows/20220724_151013.png)

# Установка Apache Cordova

Для установки `Apache Cordova` нежен пакетный менеджер `npm` который входит в состав `NodeJS`.

Скачать и установить NodeJS: [https://nodejs.org/en/download/](https://nodejs.org/en/download/)

Устанавливаем `Apache Cordova`.

```
npm install cordova -g
```

# Создание проекта

```
cordova create MyApp
cd MyApp
cordova platform add android
```

В папку `www` помещаем файлы вашего веб приложения (страницы).

# Запуск проекта

```
cordova run android
```

![Hello World!](assets/install-cordova-on-windows/20220724_213534.png)

По умолчанию cordova запускает приложение на эмуляторе с именем `default`. Для того, что бы указать какой эмулятор использовать указываем параметр `--target="name"`.

```
cordova run android --target="Nexus_One_API_25"
```

![--target="Nexus_One_API_25"](assets/install-cordova-on-windows/20220724_214457.png)

Получить список устройств можно следующим образом:

```
cordova run android --list
```

![--list](assets/install-cordova-on-windows/20220724_214308.png)

# Подпись проекта

Генерируем ключ:

```
keytool -genkey -v -keystore myapp.keystore -alias myapp -keyalg RSA -keysize 2048 -validity 10000
```

Создаем файл `build.json`.

```json
{
    "android": {
        "debug": {
            "keystore": "./myapp.keystore",
            "storePassword": "123123",
            "alias": "myapp",
            "password" : "123123",
            "keystoreType": "jks",
            "packageType": "apk"
        },
        "release": {
            "keystore": "./myapp.keystore",
            "storePassword": "123123",
            "alias": "myapp",
            "password" : "123123",
            "keystoreType": "jks",
            "packageType": "apk"
        }
    }
}
```

По умолчанию для `release` используется `"packageType": "bundle"` и выходной файл имеет формат `.aab`. По непроверенной мной информации файл формата `.aab` нужен для публикации на маркете.

# Сборка проекта

```
cordova build android --release
```

![cordova build android --release](assets/install-cordova-on-windows/20220724_215805.png)

# Иконка приложения

Для иконки нужно несколько `png` разного размера.

В проекте создаем папку `/resource/android/icon` и помещаем туда картинки с иконками.

В `config.xml` добавляем.

```xml
<platform name="android">
    <icon src="resource/android/icon/ldpi.png" width="36" height="36" density="ldpi" />
    <icon src="resource/android/icon/mdpi.png" width="48" height="48" density="mdpi" />
    <icon src="resource/android/icon/hdpi.png" width="72" height="72" density="hdpi" />
    <icon src="resource/android/icon/xhdpi.png" width="96" height="96" density="xhdpi" />
    <icon src="resource/android/icon/xxhdpi.png" width="144" height="144" density="xxhdpi" />
    <icon src="resource/android/icon/xxxhdpi.png" width="192" height="192" density="xxxhdpi" />
</platform>
```