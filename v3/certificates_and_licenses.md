# Сертификаты и лицензии
Метод позволяет получить информацию о сертификатах и лицензиях.

## 1. Параметры запроса

Для получения информации о сертификатах необходим запрос `certficates`.

Данный запрос выполняется с наличием обязательного фильтра: `first: 5`, число задает количество выданных ответов от нового к старым.


## Пример запроса


``` graphql query company {
  company(ogrn: "1021300660149") {
    ogrn
    fullName
    certificates {
      list(first: 3) {
        id
        regNumber
        status
        type
        documentType
        startDate
        endDate
        product {
          name
        }
        applicant {
          ... on ForeignOrganization {
            registrationNumber
            name
          }
          ... on Company {
            ogrn
            fullName
          }
          ... on Individual {
            ogrnip
            firstName
            middleName
            lastName
          }
        }
        manufacturer {
          ... on ForeignOrganization {
            registrationNumber
            name
          }
          ... on Company {
            ogrn
            fullName
          }
          ... on Individual {
            ogrnip
            firstName
            middleName
            lastName
          }
          ... on UnverifiedEntity {
            name
          }
        }
      }
      statistics {
        totalCount
      }
    }
  }
}
```

## Пример ответа:
```json
{
  "data": {
    "company": {
      "ogrn": "1021300660149",
      "fullName": "ОБЩЕСТВО С ОГРАНИЧЕННОЙ ОТВЕТСТВЕННОСТЬЮ \"ХЛЕБОЗАВОД\"",
      "certificates": {
        "list": [
          {
            "id": "5d4bda47d9d67b0072e50e17",
            "regNumber": "ТС N RU Д-RU.ПТ61.В.01259",
            "status": "ARCHIVAL",
            "type": "DECLARATION",
            "documentType": "Архивный",
            "startDate": 1424995200,
            "endDate": 1518652800,
            "product": {
              "name": "Изделия булочные: Батоны простые,   Батоны нарезные,   Батоны с изюмом,  Батоны подмосковные,  Батоны особые,  Булочная мелочь,   Сайки,   Сайки с изюмом,   Калачи московские,   Булочки с маком,   Хлебцы оренбургские,   Булочки столичные,   Рожки сдобные,   Булка ярославская сдобная,  Булочка московская,  Булка черкизовская,   Арнауты,   Изделия хлебобулочные плетеные московские,   Ситнички московские."
            },
            "applicant": null,
            "manufacturer": {
              "ogrn": "1021300660149",
              "fullName": "ОБЩЕСТВО С ОГРАНИЧЕННОЙ ОТВЕТСТВЕННОСТЬЮ \"ХЛЕБОЗАВОД\""
            }
          },
          {
            "id": "5d4bda47d9d67b0072e51552",
            "regNumber": "ТС N RU Д-RU.ПТ61.В.01260",
            "status": "ARCHIVAL",
            "type": "DECLARATION",
            "documentType": "Архивный",
            "startDate": 1424995200,
            "endDate": 1518652800,
            "product": {
              "name": "Хлеб из пшеничной муки: Хлеб пшеничный из муки высшего, первого и второго сортов,  Хлеб ромашка,  Хлеб домашний подовой штучный,  Каравай сувенирный штучный,  Каравай русский  штучный,  Хлеб домашний подовой штучный,  Хлеб красносельский подовой штучный,  Хлеб степной  формовой штучный,  Матнакаш штучный,   Хлеб молочный подовой и формовой штучный."
            },
            "applicant": null,
            "manufacturer": {
              "ogrn": "1021300660149",
              "fullName": "ОБЩЕСТВО С ОГРАНИЧЕННОЙ ОТВЕТСТВЕННОСТЬЮ \"ХЛЕБОЗАВОД\""
            }
          },
          {
            "id": "5d4bda47d9d67b0072e518b9",
            "regNumber": "ТС N RU Д-RU.ПТ61.В.01258",
            "status": "ARCHIVAL",
            "type": "DECLARATION",
            "documentType": "Архивный",
            "startDate": 1424995200,
            "endDate": 1518652800,
            "product": {
              "name": "Хлеб дарницкий"
            },
            "applicant": null,
            "manufacturer": {
              "ogrn": "1021300660149",
              "fullName": "ОБЩЕСТВО С ОГРАНИЧЕННОЙ ОТВЕТСТВЕННОСТЬЮ \"ХЛЕБОЗАВОД\""
            }
          }
        ],
        "statistics": {
          "totalCount": 3
        }
      }
    }
  }
}
```

## 2. Параметры запроса
Запрос необходимый для получения полей связанных с лицензиями компании: `licenses`

## Пример запроса
``` graphql
query company {
  company(ogrn: "1120280023270") {
    ogrn
    fullName
    licenses {
      number
      licenseDate
      startDate
      endDate
      activities
      locations
      licenser
    }
  }
}
```

## Пример ответа:

``` json
{
  "data": {
    "company": {
      "ogrn": "1120280023270",
      "fullName": "ОБЩЕСТВО С ОГРАНИЧЕННОЙ ОТВЕТСТВЕННОСТЬЮ \"1+1\"",
      "licenses": [
        {
          "number": "ЛО-02-01-003479",
          "licenseDate": 1416528000,
          "startDate": 1416528000,
          "endDate": null,
          "activities": [
            "Медицинская деятельность (за исключением указанной деятельности, осуществляемой медицинскими организациями и другими организациями, входящими в частную систему здравоохранения, на территории инновационного центра \"Сколково\")"
          ],
          "locations": [
            "450105, Республика Башкортостан, г. Уфа, Октябрьский район, ул. Ю.Гагарина, 74/1"
          ],
          "licenser": "Министерство здравоохранения Республики Башкортостан"
        }
      ]
    }
  }
}
```
