# API сервиса Контрагентио
Контрагентио API – это SaaS-сервис для автоматического получения сведений о российских организациях (ЮЛ и ИП) и проявления должной осмотрительности при выборе контрагентов.

## Общие сведения
- Базовый URL для методов API расположен по адресу https://api.kontragent.io/v3/graphql
- Обмен данными с сервисом  осуществляется по протоколу HTTPS.
- Формат данных запроса – GraphQL.
- Формат данных ответа – JSON.
- Параметры в запроса должны быть в кодировке UTF-8 и закодированы для передачи в URL (http://en.wikipedia.org/wiki/Percent-encoding).

## Начало работы с GraphQL
С точки зрения технологий работа с языком запросов GraphQL ничем не отличается от работы с обычным REST API, но
если вы не знакомы с GraphQL, то рекомендуем ознакомиться со следующими материалами:
* [Introduction to GraphQL](http://graphql.org/learn/) (англ.) – официальный вводный курс от разработчика.
* [Что же такое этот GraphQL?](https://habrahabr.ru/post/326986/) – перевод статьи Sacha Greif "Что же такое этот GraphQL?" на Habrahabr

## Аутентификация
Для доступа к методам сервиса требуется передавать аутентификационный JWT-токен в заголовке Authorization по схеме Bearer (при работе с песочницей токен необходимо указать в поле "Токен авторизации"). Для получения токена напишите нам на sales@kontragent.io.

## Работа с песочницей
Для того, чтобы вам было удобнее тестировать свои запросы, мы подготовили специальную песочницу, которая  расположена по адресу https://sandbox.kontragent.io. Песочница позволяет использовать средства автокомплита, автоматической валидации и форматирования запросов. Для получения подсказок по возможным полям запроса нажмите [Shift + Пробел или Ctrl +  Пробел](https://i.imgur.com/J33l5tp.png).

## Программное взаимодействие с API
Чтобы запросить данные у GraphQL API из вашей информационной системы, вам достаточно отправить POST-запрос.
Пример простого запроса, который получит полное наименование для организации с ОГРН 1047796788930 с помощью CURL:
```
curl -X POST \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer YOUR-API-TOKEN-HERE" \
     -d '
        {
          "query": "query someRandomQueryName($ogrn: String) { company(ogrn: $ogrn) { fullName } }",
          "variables": {
            "ogrn": "1047796788930"
          },
          "operationName": "someRandomQueryName"
        }
     ' \
     https://api.kontragent.io/v3/graphql
```

## Методы и документация
Полная документация ко всем методам расположена в [песочнице](https://sandbox.kontragent.io.). Для того, чтобы получить сведения об интересующих данных, нажмите на вкладку Docs в [правом верхнем углу экрана](https://i.imgur.com/LBt2OML.png).

Далее приведены ссылки на примеры получения некоторых данных:
* [Поиск по российским организациям и ИП](./v3/search.md)
* [Карточка российской организации](./v3/company.md)
* [Карточка индивидуального предпринимателя](./v3/individual.md)
* [Печатные формы отчетов](./v3/reports.md)
* [Сертификаты и лицензии](./v3/certificates_and_licenses.md)
* [Риски](./v3/compliance.md)
* [Банкротства и существенные факты](./v3/fedresurs.md)
* [Исполнительные производства](./v3/fssp.md)
* [Проверки](./v3/inspections.md)
* [Изменения в ЕГРЮЛ/ЕГРИП](./v3/records.md)
* [Картотека Арбитражных Дел](./v3/kad.md)
## Контакты и техподдержка
Для получения токена доступа к API напишите нам на sales@kontragent.io
По вопросам работы с API обращайтесь на support@kontragent.io

## Changelog

### 23 января 2020 г.
* Добавлены [Сертификаты и лицензии](./v3/certificates_and_licenses.md)
* Добавлены [Риски](./v3/compliance.md)
* Добавлены [Банкротства и существенные факты](./v3/fedresurs.md)
* Добавлены [Исполнительные производства](./v3/fssp.md)
* Добавлены [Проверки](./v3/inspections.md)
* Добавлены [Изменения в ЕГРЮЛ/ЕГРИП](./v3/records.md)
* Добавлена [Картотека Арбитражных Дел](./v3/kad.md)
* Обновлена документация

### 23 июля 2019 г.
* Добавлены [печатные формы отчетов](./v3/reports.md)
* Обновлена документация
