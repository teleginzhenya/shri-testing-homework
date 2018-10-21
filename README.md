# Домашнее задание: автотесты

Вам дано приложение на JavaScript и нужно написать для него автотесты: интеграционные тесты на интерфейс и модульные тесты на серверную часть.

## Предметная область

Приложение отображает в браузере информацию из git репозитория: список коммитов, файловую систему для выбранного коммита, содержимое выбранного файла (поддерживаются только текстовые форматы). Для удобства навигации на каджой странице отображаются "хлебные крошки".

## Как запустить

```sh
git clone git@github.com:dima117/shri-testing-homework.git
cd shri-testing-homework.git
npm i
npm start
```

## Интеграционные тесты

Сценарии для интеграционных тестов

- на всех страницах (история коммитов, просмотр файловой системы, просмотр содержимого файла) правильно отображается их содержимое;
- правильно работают переходы по страницам
  - из списка коммитов на список файлов
  - из списка файлов во вложенную папку
  - из списка файлов на страницу отдельного файла
  - переходы по хлебным крошкам

## Модульные тесты

- нужно добавить в README список логических блоков системы и их сценариев
- для каждого блока нужно написать модульные тесты
- если необходимо, выполните рефакторинг, чтобы реорганизовать логические блоки или добавить точки расширения

## Логические блоки и сценарии

- app

  - /
    - возвращает статус 200 при роуте
  - /files/:hash/\*?
    - возвращать статус 200 для рут папки
    - возвращать статус 200 для любой другой папки
    - возвращать статус 500 при некорректном `hash`
  - /content/:hash/\*?
    - возвращать статус 200 для файла из рут папки
    - возвращать статус 200 для файла из любой другой папки
    - возвращать статус 500 при некорректном `hash`
  - возвращать статус 404 при несуществующем роуте

- git

  - gitHistory
    - возвращает корректные данные, работает пагинация
  - gitFileTree
    - возвращает корректные данные, когда есть `path`
    - возвращает корректные данные, когда нет `path`
  - gitFileContent
    - возвращает корректные данные, когда есть `hash`
    - возвращает корректные данные, когда нет `hash`

- helpers

  - getOffset
    - корректно возвращать сдвиг
  - parseFileTreeItem
    - корректно делит строку на `type`, `hash` и `path`
  - parseHistoryItem
    - корректно делит строку на `hash`, `author`, `timestamp` и `msg`

- navigation

  - buildFolderUrl
    - возвращает корректный путь, когда есть `path`
    - возвращает корректный путь, когда нет `path`
  - buildFileUrl
    - возвращает корректный путь
  - buildObjectUrl
    - возвращает корректный url для `type="tree"`
    - возвращает корректный url для `type="blob"`
    - возвращает # для иных случаев
  - buildBreadcrumbs
    - возвращает массив, первым элементом которого является объект `{ text: 'HISTORY', href: '/' }`
    - возвращает правильный массив, когда нет `hash` и нет `path`
    - возвращает правильный массив, когда есть `hash` и нет `path`
    - возвращает правильный массив, когда есть `hash` и вложенность 1 уровня
    - возвращает правильный массив, когда есть `hash` и вложенность 2 уровня
    - возвращает правильный массив, когда есть `hash`, вложенность 1 уровня и файл
    - возвращает правильный массив, когда есть `hash`, вложенность 2 уровня и файл

- contentController

  - возвращает корректные данные и рендерит их
  - показывает контент файла, если это `blob`
  - возвращает ошибку в иных случаях

- filesController

  - возвращает корректные данные и рендерит их
  - возвращает ошибку в иных случаях

- indexController

  - возвращает корректные данные и рендерит их
  - возвращает ошибку в иных случаях
