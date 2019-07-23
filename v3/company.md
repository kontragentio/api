# Карточка российской организации
Метод позволяет осуществлять получить детализированную информацию о российских
организациях.

## Параметры
| Параметр | Тип | Формат | Описание |
| ------ | ------ | ------ | ------ |
| `ogrn` | GET | строка из 13 цифр, необязательный | ОГРН организации |
| `inn` | GET | строка 10 цифр, необязательный | ИНН организации |
| `kpp` | GET | строка 9 цифр, необязательный | КПП организации |

В запросе должен быть передан по крайней мере один из этих параметров, достаточный
для идентификации одной организации – ОГРН или ИНН+КПП. Если КПП организации
неизвестен, рекомендуем воспользоваться методом search.

## Пример запроса
```graphql
{
  company(ogrn: "1117746390277") {
    fullName
    shortName
    egrulFullName: fullName(autoCorrection: false)
    form {
      compact
      full
      code
    }
    ogrn
    inn
    kpp
    okato
    okpo
    okogu
    oktmo
    okfs
    isBank
    bik
    status {
      isLiquidated
      text
      grnDate
    }
    registrationDate
    terminationDate
    taxInspection {
      grnDate
      authority {
        code
        name
      }
    }
    taxation {
      averageEmployeesNumber
      taxSystemsApplication
      rsmpRegistry {
        category
        description
        employees
        products {
          code
          name
          innovative
        }
        inclusionDate
      }
      taxesPaid {
        values {
          year
          data {
            code
            amount
          }
        }
      }
      taxOffenses {
        values {
          year
          finesAmount
        }
      }
      taxArrears {
        values {
          year
          data {
            code
            taxAmount
            penaltiesAmount
            finesAmount
            totalAmount
          }
        }
      }
    }
    authorizedCapital {
      grnDate
      amount
    }
    address {
      grnDate
      full
      postalCode
      country
      federalDistrict
      area
      region {
        full
        code
        name
        type
      }
      city {
        full
        name
        type
      }
      street
      house
      housing
    }
    head {
      grnDate
      position
      head {
        ... on Person {
          inn
          firstName
          middleName
          lastName
        }
        ... on Company {
          fullName
          shortName
          ogrn
          inn
          kpp
        }
      }
    }
    founders {
      grnDate
      share
      amount
      founder {
        ... on Person {
          inn
          firstName
          middleName
          lastName
        }
        ... on Company {
          inn
          fullName
          shortName
        }
        ... on ForeignOrganization {
          inn
          registrationNumber
          name
          address {
            full
          }
        }
      }
    }
    okveds {
      grnDate
      code
      description
      isPrimary
    }
  }
}
```
## Пример ответа
```json
{
  "data": {
    "company": {
      "fullName": "ОБЩЕСТВО С ОГРАНИЧЕННОЙ ОТВЕТСТВЕННОСТЬЮ \"ЕАЕ- КОНСАЛТ\"",
      "shortName": "ООО \"ЕАЕ- КОНСАЛТ\"",
      "egrulFullName": "ОБЩЕСТВО С ОГРАНИЧЕННОЙ ОТВЕТСТВЕННОСТЬЮ \"ЕАЕ- КОНСАЛТ\"",
      "form": {
        "compact": "ООО",
        "full": "Общество с ограниченной ответственностью",
        "code": "12300"
      },
      "ogrn": "1117746390277",
      "inn": "7731407330",
      "kpp": "773401001",
      "okato": "45371000000",
      "okpo": "91581037",
      "okogu": "45283582000",
      "oktmo": "4210014",
      "okfs": "16",
      "isBank": false,
      "bik": null,
      "status": {
        "isLiquidated": false,
        "text": null,
        "grnDate": 0
      },
      "registrationDate": 1305676800,
      "terminationDate": null,
      "taxInspection": {
        "grnDate": 1510531200,
        "authority": {
          "code": "7734",
          "name": "Инспекция Федеральной налоговой службы № 34 по г.Москве"
        }
      },
      "taxation": {
        "averageEmployeesNumber": 1083,
        "taxSystemsApplication": [
          "OSNO"
        ],
        "rsmpRegistry": null,
        "taxesPaid": {
          "values": [
            {
              "year": "2017",
              "data": [
                {
                  "code": "Страховые взносы на обязательное медицинское страхование работающего населения, зачисляемые в бюджет Федерального фонда обязательного медицинского страхования",
                  "amount": 3587778165
                },
                {
                  "code": "Страховые и другие взносы на обязательное пенсионное страхование, зачисляемые в Пенсионный фонд Российской Федерации",
                  "amount": 5711289621
                },
                {
                  "code": "Транспортный налог",
                  "amount": 3682000
                },
                {
                  "code": "Налог на имущество организаций",
                  "amount": 2307490
                },
                {
                  "code": "Налог на добавленную стоимость",
                  "amount": 24939658861
                },
                {
                  "code": "Налог на прибыль",
                  "amount": 2030422248
                }
              ]
            },
            {
              "year": "2018",
              "data": []
            }
          ]
        },
        "taxOffenses": {
          "values": [
            {
              "year": "2017",
              "finesAmount": 0
            },
            {
              "year": "2018",
              "finesAmount": 0
            }
          ]
        },
        "taxArrears": {
          "values": [
            {
              "year": "2017",
              "data": [
                {
                  "code": "Налог на прибыль",
                  "taxAmount": 607000,
                  "penaltiesAmount": 19500,
                  "finesAmount": 121300,
                  "totalAmount": 747800
                }
              ]
            },
            {
              "year": "2018",
              "data": []
            }
          ]
        }
      },
      "authorizedCapital": {
        "grnDate": 1458777600,
        "amount": 5000000
      },
      "address": {
        "grnDate": 1510531200,
        "full": "123308, г. Москва, ул. Демьяна Бедного, д. 24, к. 1, пом. iv эт 2 ком 38",
        "postalCode": "123308",
        "country": "Российская Федерация",
        "federalDistrict": "Центральный",
        "area": null,
        "region": {
          "full": "город Москва",
          "code": "77",
          "name": "Москва",
          "type": "город"
        },
        "city": null,
        "street": "ул. Демьяна Бедного",
        "house": "д. 24",
        "housing": "к. 1"
      },
      "head": {
        "grnDate": 1545955200,
        "position": "Генеральный директор",
        "head": {
          "inn": "772879284519",
          "firstName": "Алексей",
          "middleName": "Александрович",
          "lastName": "Рябушев"
        }
      },
      "founders": [
        {
          "grnDate": 1458777600,
          "share": 0.32,
          "amount": 1600000,
          "founder": {
            "inn": "770400220540",
            "firstName": "Александр",
            "middleName": "Сергеевич",
            "lastName": "Кислицын"
          }
        },
        {
          "grnDate": 1386288000,
          "share": 0.68,
          "amount": 3400000,
          "founder": {
            "inn": "7734682952",
            "fullName": "ОБЩЕСТВО С ОГРАНИЧЕННОЙ ОТВЕТСТВЕННОСТЬЮ \"ГРУППА КОМПАНИЙ \"ЭНЕРГЕТИКА, СИСТЕМНАЯ ИНТЕГРАЦИЯ\"",
            "shortName": "ООО \"ГРУППА КОМПАНИЙ \"ЭНСИ\""
          }
        }
      ],
      "okveds": [
        {
          "grnDate": 1305676800,
          "code": "63.11.1",
          "description": "Деятельность по созданию и использованию баз данных и информационных ресурсов",
          "isPrimary": true
        },
        {
          "grnDate": 1305676800,
          "code": "41.20",
          "description": "Строительство жилых и нежилых зданий",
          "isPrimary": false
        },
        {
          "grnDate": 1305676800,
          "code": "43.29",
          "description": "Производство прочих строительно-монтажных работ",
          "isPrimary": false
        },
        {
          "grnDate": 1305676800,
          "code": "43.39",
          "description": "Производство прочих отделочных и завершающих работ",
          "isPrimary": false
        },
        {
          "grnDate": 1305676800,
          "code": "46.19",
          "description": "Деятельность агентов по оптовой торговле универсальным ассортиментом товаров",
          "isPrimary": false
        },
        {
          "grnDate": 1305676800,
          "code": "46.90",
          "description": "Торговля оптовая неспециализированная",
          "isPrimary": false
        },
        {
          "grnDate": 1305676800,
          "code": "47.9",
          "description": "Торговля розничная вне магазинов, палаток, рынков",
          "isPrimary": false
        },
        {
          "grnDate": 1305676800,
          "code": "61.10",
          "description": "Деятельность в области связи на базе проводных технологий",
          "isPrimary": false
        },
        {
          "grnDate": 1305676800,
          "code": "62.01",
          "description": "Разработка компьютерного программного обеспечения",
          "isPrimary": false
        },
        {
          "grnDate": 1305676800,
          "code": "62.02",
          "description": "Деятельность консультативная и работы в области компьютерных технологий",
          "isPrimary": false
        },
        {
          "grnDate": 1305676800,
          "code": "62.09",
          "description": "Деятельность, связанная с использованием вычислительной техники и информационных технологий, прочая",
          "isPrimary": false
        },
        {
          "grnDate": 1305676800,
          "code": "63.11",
          "description": "Деятельность по обработке данных, предоставление услуг по размещению информации и связанная с этим деятельность",
          "isPrimary": false
        },
        {
          "grnDate": 1305676800,
          "code": "70.22",
          "description": "Консультирование по вопросам коммерческой деятельности и управления",
          "isPrimary": false
        },
        {
          "grnDate": 1305676800,
          "code": "72.19",
          "description": "Научные исследования и разработки в области естественных и технических наук прочие",
          "isPrimary": false
        },
        {
          "grnDate": 1305676800,
          "code": "73.11",
          "description": "Деятельность рекламных агентств",
          "isPrimary": false
        }
      ]
    }
  }
}
```

Кроме того, для запроса данных по нескольким организациям существует метод `companies`, который принимает
в качестве параметра массив ОГРН:
```graphql
{
  companies(ogrns: ["1117746390277", "1036605194240"]) {
    fullName
    shortName
    egrulFullName: fullName(autoCorrection: false)
  }
}
```
Ответ: 
```json
{
  "data": {
    "companies": [
      {
        "fullName": "\"ВЕКТОР\"",
        "shortName": "ООО \"ВЕКТОР\"",
        "egrulFullName": "\"ВЕКТОР\""
      },
      {
        "fullName": "ОБЩЕСТВО С ОГРАНИЧЕННОЙ ОТВЕТСТВЕННОСТЬЮ \"ЕАЕ- КОНСАЛТ\"",
        "shortName": "ООО \"ЕАЕ- КОНСАЛТ\"",
        "egrulFullName": "ОБЩЕСТВО С ОГРАНИЧЕННОЙ ОТВЕТСТВЕННОСТЬЮ \"ЕАЕ- КОНСАЛТ\""
      }
    ]
  }
}
```