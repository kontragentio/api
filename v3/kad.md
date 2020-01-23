# Картотека Арбитражных дел
Метод позволяет получить детализированную информацию по Арбитражным делам компании.

## Параметры запроса

Для получения информации по Арбитражным делам необходим запрос `kad` внутри выбранной компании.

Должны быть заданы обязательные фильтры: `first` и `filter:sideType`.

* ``(first: 57)`` -фильтр для получения информации по последним делам, где число указывает на количество запрошенных последних дел компании.

* ``(filter: {sideType:RESPONDENT})`` - фильтр, сортирующий дела по причастности.
  1. `RESPONDENT` - для поиска дел, в которых компания была Ответчиком
  2. `PLAINTIFF` - для поиска дел, в которых компания была Истцом
  3. `THIRD` - для поиска дел, в которых компания была Третьим лицом
  4. `Other` - другой участник, для случаев, если первые три фильтра не подходят для позиции компании по делу.

* ``(After:cursor)`` - инструмент для пагинации дел.

* `results: ["DISMISSED"]` - фильтр по результату дела.

  1. `DISMISSED` - проиграно
  2. `PENDING` - рассматривается
  3. `SATISFIED` - удовлетворено
  4. `TERMINATED` - прекращено
  5. `SATIDFIED_PARTIALLY` - удовлетворено частично
  6. `WITHOUT_CONSIDERING` - оставлено без рассмотрения

* `years [2018,2019]` - для отображения дел за определенный период


* `id` - для поиска дел по guId

* `caseNumber` - для поиска по номеру Дела (например: А21-12253/2018)

* `categories` - для фильтрации дел по категориям
  1. `ADMINISTRATIVE` - Административные
  2. `CIVIL` - Гражданские
  3. `BANKRUPTCY_SIMPLE` - Банкротство, рассматриваемое в упрощенном порядке
  4. `BANKRUPTCY` - Банкротство
  5. `CIVIL_SIMPLE` - Гражданские дела, рассматриваемые в упрощенном порядке
  6. `ADMINISTRATIVE_SIMPLE` - Административные дела, рассматриваемые в упрощенном порядке
  7. `OTHER` - Другие дела



## Пример запроса
```graphql query {
  company(ogrn: "1117746390277") {
    kad(first:2 filter:{sideType:PLAINTIFF})
    {
      edges {
        kadId
        outcome
        caseProgress
        sides{
          kadId
          type
          entity{
            __typename
          }
        }
        category{
          code
          name
        }
        isCertain
        instances {
          id
          isCurrent
          outcome
          type
          court{
            tag
            name
          }
          suit{
            number
            date
            initialClaimSum
          }
          documents{
            date
            isCourtDecision
            type
            fileUrl
            fileName
            hearingDate
          }

        }
        cursor
      }
      updatedAt
      statistics{
        totalCount}
    }
  }
}
```


## Пример ответа
```json {
  "data": {
    "company": {
      "kad": {
        "edges": [
          {
            "kadId": "e2164d42-0daa-463f-b79e-b3946a0c0e8b",
            "outcome": "PENDING",
            "caseProgress": "Рассматривается в первой инстанции",
            "sides": [
              {
                "kadId": "01fa75bb-c6c8-4f37-bd4b-9acae79dd730",
                "type": "PLAINTIFF",
                "entity": {
                  "__typename": "Company"
                }
              },
              {
                "kadId": "359f263b-3914-4766-a4ec-9480a27d50e4",
                "type": "RESPONDENT",
                "entity": {
                  "__typename": "Company"
                }
              }
            ],
            "category": {
              "code": "CIVIL_SIMPLE",
              "name": "экономические споры по гражданским правоотношениям"
            },
            "isCertain": true,
            "instances": [
              {
                "id": "5cf9ff60-31e0-4767-a55f-750a9cc5ca5e",
                "isCurrent": true,
                "outcome": "PENDING",
                "type": "FIRST",
                "court": {
                  "tag": "MSK",
                  "name": "АС города Москвы"
                },
                "suit": {
                  "number": "А40-203974/2019",
                  "date": 1564963200,
                  "initialClaimSum": 1052803.93
                },
                "documents": [
                  {
                    "date": 1567520209,
                    "isCourtDecision": false,
                    "type": "Материалы по делу",
                    "fileUrl": null,
                    "fileName": "Материалы по делу",
                    "hearingDate": 0
                  },
                  {
                    "date": 1565342519,
                    "isCourtDecision": false,
                    "type": "Определение",
                    "fileUrl": "http://kad.arbitr.ru/PdfDocument/e2164d42-0daa-463f-b79e-b3946a0c0e8b/b60efee0-b29b-4c51-a5bc-c0f15cdeca2d/A40-203974-2019_20190809_Opredelenie.pdf",
                    "fileName": "О принятии заявления к производству с рассмотрением в порядке упрощенного производства",
                    "hearingDate": 0
                  },
                  {
                    "date": 1564992120,
                    "isCourtDecision": false,
                    "type": "Заявление",
                    "fileUrl": null,
                    "fileName": "Исковое заявление",
                    "hearingDate": 0
                  }
                ]
              }
            ],
            "cursor": "e2164d42-0daa-463f-b79e-b3946a0c0e8b"
          },
          {
            "kadId": "9191fdfe-c61c-4a1e-9bec-040202a4ccf1",
            "outcome": "PENDING",
            "caseProgress": "Рассматривается в первой инстанции",
            "sides": [
              {
                "kadId": "3b835ea1-f3a2-4e59-8196-a08422499822",
                "type": "PLAINTIFF",
                "entity": {
                  "__typename": "UnverifiedEntity"
                }
              },
              {
                "kadId": "621ea477-fdb5-4f3b-8f8b-39cc43d92f91",
                "type": "RESPONDENT",
                "entity": {
                  "__typename": "UnverifiedEntity"
                }
              },
              {
                "kadId": "dde2cd5d-be68-45a1-bead-d16218b897c7",
                "type": "RESPONDENT",
                "entity": {
                  "__typename": "UnverifiedEntity"
                }
              }
            ],
            "category": {
              "code": "CIVIL_SIMPLE",
              "name": "экономические споры по гражданским правоотношениям"
            },
            "isCertain": false,
            "instances": [
              {
                "id": "ca188cd6-d8f6-401c-a5a8-d509abefd493",
                "isCurrent": true,
                "outcome": "PENDING",
                "type": "FIRST",
                "court": {
                  "tag": "NNOV",
                  "name": "АС Нижегородской области"
                },
                "suit": {
                  "number": "А43-38900/2019",
                  "date": 1568246400,
                  "initialClaimSum": 131327.59
                },
                "documents": [
                  {
                    "date": 1570004166,
                    "isCourtDecision": false,
                    "type": "Документы по запросу суда",
                    "fileUrl": null,
                    "fileName": "Документы по запросу суда",
                    "hearingDate": 0
                  },
                  {
                    "date": 1568581200,
                    "isCourtDecision": false,
                    "type": "Определение",
                    "fileUrl": "http://kad.arbitr.ru/PdfDocument/9191fdfe-c61c-4a1e-9bec-040202a4ccf1/71742cec-cd34-4783-9911-227ec142aeee/A43-38900-2019_20190916_Opredelenie.pdf",
                    "fileName": "Принять к производству заявление (исковое заявление) в порядке упрощенного производства (ст.228 АПК)",
                    "hearingDate": 0
                  },
                  {
                    "date": 1568235600,
                    "isCourtDecision": false,
                    "type": "Заявление (исковое заявление)",
                    "fileUrl": null,
                    "fileName": "Исковое заявление (ст.125 АПК)",
                    "hearingDate": 0
                  }
                ]
              }
            ],
            "cursor": "9191fdfe-c61c-4a1e-9bec-040202a4ccf1"
          }
        ],
        "updatedAt": 1552348800,
        "statistics": {
          "totalCount": 3
        }
      }
    }
  }
}
```
