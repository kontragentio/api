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
``` graphql query {
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
    verification{
      date{
        first
        last}
      isVerified
      data{
        address {
          actual
          postal}
        tax{
          system
          employees
        }
        contacts{
          website
          phone
          email
        }
        bankAccounts{
          bankName
          bankNameShort
          current
          correspondentAccount
          bic
        }
        description
      }
    }
    status{

      currentStatus
      futureStatus
      text
      grnDate
      reorganizationParticipants{
        company{ogrn}
        futureStatus
      }
    }
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
        products{
          code
          name
          innovative
        }
        inclusionDate
      }
      taxesPaid {
        layout{
          allTaxes{
            code
            order
            displayName
          }}
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
        layout{
          allTaxes{
            code
            order
            displayName
          }
        }
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
      room
    }
    management{
      grnDate
      position
      code
      phone
      head{... on Person{
        firstName
        lastName
        inn
        birthPlace
        snils
        birthDate
      }
      ...on Company{
        fullName
        ogrn
        inn
        kpp
        okato
        okfs
        okogu
      }}
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
    terminationDate
    predecessors{
      fullName
      ogrn
    }
    beneficiaries{
      type ... on Beneficiaries{
        entities{
          type
          share
          entity{...on Person{firstName}}
        }
      }
    }successors{
      fullName
      ogrn
    }
    pfr {
      regNumber
      grnDate
      authority{
        code
        name
      }}
    fss {
      regNumber
      grnDate
      authority{
        code
        name
      }
    }thirdParty{
      hh{
        openVacancies
        updated
        companyUrl
        certainty
      }
    }contacts{
      emails
      phones
      website
    }registryHolder{
      grnDate
      company{
        fullName
      }
    }registration{
      grnDate
      typeOfCreation{
        code
        name
      }
      authority{
        code
        name
      }
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
      "verification": {
        "date": {
          "first": 1567158589,
          "last": 1567158589
        },
        "isVerified": true,
        "data": {
          "address": {
            "actual": "123308, г. Москва, ул. Демьяна Бедного, д. 24, к. 1, пом. iv эт 2 ком 38",
            "postal": "123308, г. Москва, ул. Демьяна Бедного, д. 24, к. 1, пом. iv эт 2 ком 38"
          },
          "tax": {
            "system": "osno",
            "employees": "1083"
          },
          "contacts": {
            "website": null,
            "phone": "+79194477505",
            "email": "a.zernin@yandex.ru"
          },
          "bankAccounts": [
            {
              "bankName": "ПАО СБЕРБАНК",
              "bankNameShort": "ПАО СБЕРБАНК",
              "current": "40702810638050013199",
              "correspondentAccount": "30101810400000000225",
              "bic": "044525225"
            }
          ],
          "description": null
        }
      },
      "status": {
        "currentStatus": "ACTIVE",
        "futureStatus": null,
        "text": null,
        "grnDate": 0,
        "reorganizationParticipants": []
      },
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
          "layout": {
            "allTaxes": [
              {
                "code": "Налог на добавленную стоимость",
                "order": 10,
                "displayName": "Налог на добавленную стоимость (НДС)"
              },
              {
                "code": "Налог на прибыль",
                "order": 20,
                "displayName": "Налог на прибыль"
              },
              {
                "code": "Налог, взимаемый в связи с  применением упрощенной  системы налогообложения",
                "order": 30,
                "displayName": "Налог по УСН"
              },
              {
                "code": "Единый налог на вмененный доход для отдельных видов  деятельности",
                "order": 40,
                "displayName": "Налог на вменённый доход"
              },
              {
                "code": "Налог, взимаемый в связи с  применением патентной системы  налогообложения",
                "order": 50,
                "displayName": "Налог по ПСН"
              },
              {
                "code": "Единый сельскохозяйственный налог",
                "order": 60,
                "displayName": "Единый сельскохозяйственный налог"
              },
              {
                "code": "Налог на доходы физических лиц",
                "order": 70,
                "displayName": "Налог на доходы физических лиц (НДФЛ)"
              },
              {
                "code": "Страховые взносы на обязательное медицинское страхование работающего населения, зачисляемые в бюджет Федерального фонда обязательного медицинского страхования",
                "order": 80,
                "displayName": "Взносы в фонд медицинского страхования"
              },
              {
                "code": "Страховые и другие взносы на обязательное пенсионное страхование, зачисляемые в Пенсионный фонд Российской Федерации",
                "order": 90,
                "displayName": "Взносы в пенсионный фонд"
              },
              {
                "code": "Страховые взносы на обязательное социальное страхование на случай временной нетрудоспособности и в связи с материнством",
                "order": 100,
                "displayName": "Взносы в фонд социального страхования"
              },
              {
                "code": "Налог на имущество организаций",
                "order": 110,
                "displayName": "Налог на имущество организаций"
              },
              {
                "code": "Транспортный налог",
                "order": 120,
                "displayName": "Транспортный налог"
              },
              {
                "code": "Земельный налог",
                "order": 130,
                "displayName": "Земельный налог"
              },
              {
                "code": "Водный налог",
                "order": 140,
                "displayName": "Водный налог"
              },
              {
                "code": "Налог на добычу полезных ископаемых",
                "order": 150,
                "displayName": "Налог на добычу полезных ископаемых (НДПИ)"
              },
              {
                "code": "Налог на игорный",
                "order": 160,
                "displayName": "Налог на игорный бизнес"
              },
              {
                "code": "Акцизы, всего",
                "order": 170,
                "displayName": "Акцизы"
              },
              {
                "code": "Торговый сбор",
                "order": 180,
                "displayName": "Торговый сбор"
              },
              {
                "code": "Утилизационный сбор",
                "order": 190,
                "displayName": "Утилизационный сбор"
              },
              {
                "code": "Задолженность и перерасчеты по ОТМЕНЕННЫМ НАЛОГАМ  и сборам и иным обязательным платежам  (кроме ЕСН, страх. Взносов)",
                "order": 200,
                "displayName": "Задолженность и перерасчеты по отменённым налогам и сборам и иным обязательным платежам"
              },
              {
                "code": "НЕНАЛОГОВЫЕ ДОХОДЫ, администрируемые налоговыми органами",
                "order": 210,
                "displayName": "Неналоговые доходы, администрируемые налоговыми органами"
              },
              {
                "code": "Регулярные платежи за добычу полезных ископаемых (роялти) при выполнении соглашений о разделе продукции",
                "order": 220,
                "displayName": "Регулярные платежи за добычу полезных ископаемых (роялти) при выполнении соглашений о разделе продукции"
              },
              {
                "code": "Сборы за пользование объектами животного мира  и за пользование объектами ВБР",
                "order": 230,
                "displayName": "Сборы за пользование объектами животного мира  и за пользование объектами ВБР"
              },
              {
                "code": "Государственная пошлина",
                "order": 240,
                "displayName": "Государственная пошлина"
              }
            ]
          },
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
              "data": [
                {
                  "code": "НЕНАЛОГОВЫЕ ДОХОДЫ, администрируемые налоговыми органами",
                  "amount": 0
                },
                {
                  "code": "Транспортный налог",
                  "amount": 3682000
                },
                {
                  "code": "Страховые взносы на обязательное социальное страхование на случай временной нетрудоспособности и в связи с материнством",
                  "amount": 0
                },
                {
                  "code": "Налог на прибыль",
                  "amount": 0
                },
                {
                  "code": "Налог на добавленную стоимость",
                  "amount": 23297092400
                },
                {
                  "code": "Страховые и другие взносы на обязательное пенсионное страхование, зачисляемые в Пенсионный фонд Российской Федерации",
                  "amount": 6001277923
                },
                {
                  "code": "Налог на имущество организаций",
                  "amount": 816400
                },
                {
                  "code": "Страховые взносы на обязательное медицинское страхование работающего населения, зачисляемые в бюджет Федерального фонда обязательного медицинского страхования",
                  "amount": 3962759927
                }
              ]
            },
            {
              "year": "2019",
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
            },
            {
              "year": "2019",
              "finesAmount": 0
            }
          ]
        },
        "taxArrears": {
          "layout": {
            "allTaxes": [
              {
                "code": "Налог на добавленную стоимость",
                "order": 10,
                "displayName": "Налог на добавленную стоимость (НДС)"
              },
              {
                "code": "Налог на прибыль",
                "order": 20,
                "displayName": "Налог на прибыль"
              },
              {
                "code": "Налог, взимаемый в связи с  применением упрощенной  системы налогообложения",
                "order": 30,
                "displayName": "Налог по УСН"
              },
              {
                "code": "Единый налог на вмененный доход для отдельных видов  деятельности",
                "order": 40,
                "displayName": "Налог на вменённый доход"
              },
              {
                "code": "Налог, взимаемый в связи с  применением патентной системы  налогообложения",
                "order": 50,
                "displayName": "Налог по ПСН"
              },
              {
                "code": "Единый сельскохозяйственный налог",
                "order": 60,
                "displayName": "Единый сельскохозяйственный налог"
              },
              {
                "code": "Налог на доходы физических лиц",
                "order": 70,
                "displayName": "Налог на доходы физических лиц (НДФЛ)"
              },
              {
                "code": "Страховые взносы на обязательное медицинское страхование работающего населения, зачисляемые в бюджет Федерального фонда обязательного медицинского страхования",
                "order": 80,
                "displayName": "Взносы в фонд медицинского страхования"
              },
              {
                "code": "Страховые и другие взносы на обязательное пенсионное страхование, зачисляемые в Пенсионный фонд Российской Федерации",
                "order": 90,
                "displayName": "Взносы в пенсионный фонд"
              },
              {
                "code": "Страховые взносы на обязательное социальное страхование на случай временной нетрудоспособности и в связи с материнством",
                "order": 100,
                "displayName": "Взносы в фонд социального страхования"
              },
              {
                "code": "Налог на имущество организаций",
                "order": 110,
                "displayName": "Налог на имущество организаций"
              },
              {
                "code": "Транспортный налог",
                "order": 120,
                "displayName": "Транспортный налог"
              },
              {
                "code": "Земельный налог",
                "order": 130,
                "displayName": "Земельный налог"
              },
              {
                "code": "Водный налог",
                "order": 140,
                "displayName": "Водный налог"
              },
              {
                "code": "Налог на добычу полезных ископаемых",
                "order": 150,
                "displayName": "Налог на добычу полезных ископаемых (НДПИ)"
              },
              {
                "code": "Налог на игорный",
                "order": 160,
                "displayName": "Налог на игорный бизнес"
              },
              {
                "code": "Акцизы, всего",
                "order": 170,
                "displayName": "Акцизы"
              },
              {
                "code": "Торговый сбор",
                "order": 180,
                "displayName": "Торговый сбор"
              },
              {
                "code": "Утилизационный сбор",
                "order": 190,
                "displayName": "Утилизационный сбор"
              },
              {
                "code": "Задолженность и перерасчеты по ОТМЕНЕННЫМ НАЛОГАМ  и сборам и иным обязательным платежам  (кроме ЕСН, страх. Взносов)",
                "order": 200,
                "displayName": "Задолженность и перерасчеты по отменённым налогам и сборам и иным обязательным платежам"
              },
              {
                "code": "НЕНАЛОГОВЫЕ ДОХОДЫ, администрируемые налоговыми органами",
                "order": 210,
                "displayName": "Неналоговые доходы, администрируемые налоговыми органами"
              },
              {
                "code": "Регулярные платежи за добычу полезных ископаемых (роялти) при выполнении соглашений о разделе продукции",
                "order": 220,
                "displayName": "Регулярные платежи за добычу полезных ископаемых (роялти) при выполнении соглашений о разделе продукции"
              },
              {
                "code": "Сборы за пользование объектами животного мира  и за пользование объектами ВБР",
                "order": 230,
                "displayName": "Сборы за пользование объектами животного мира  и за пользование объектами ВБР"
              },
              {
                "code": "Государственная пошлина",
                "order": 240,
                "displayName": "Государственная пошлина"
              }
            ]
          },
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
            },
            {
              "year": "2019",
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
        "housing": "к. 1",
        "room": "пом. iv эт 2 ком 38"
      },
      "management": [
        {
          "grnDate": 1545955200,
          "position": "Генеральный директор",
          "code": "02",
          "phone": null,
          "head": {
            "firstName": "Алексей",
            "lastName": "Рябушев",
            "inn": "772879284519",
            "birthPlace": null,
            "snils": null,
            "birthDate": null
          }
        }
      ],
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
      ],
      "predecessors": [],
      "beneficiaries": {
        "type": "ESTABLISHED",
        "entities": [
          {
            "type": "PERSON",
            "share": 1,
            "entity": {
              "firstName": "Александр"
            }
          }
        ]
      },
      "successors": [],
      "pfr": {
        "regNumber": "087906027793",
        "grnDate": 1510790400,
        "authority": {
          "code": "087906",
          "name": "Государственное учреждение - Главное Управление Пенсионного фонда РФ №9 по г. Москве и Московской области муниципальный район Хорошево-Мневники г.Москвы"
        }
      },
      "fss": {
        "regNumber": "772513738077251",
        "grnDate": 1305849600,
        "authority": {
          "code": "7725",
          "name": "Филиал №25 Государственного учреждения - Московского регионального отделения Фонда социального страхования Российской Федерации"
        }
      },
      "thirdParty": {
        "hh": {
          "openVacancies": 27,
          "updated": "2020-01-22T21:23:33Z",
          "companyUrl": "https://hh.ru/employer/988038",
          "certainty": true
        }
      },
      "contacts": {
        "emails": [],
        "phones": [],
        "website": null
      },
      "registryHolder": null,
      "registration": {
        "grnDate": 1305676800,
        "typeOfCreation": {
          "code": "11",
          "name": "Создание юридического лица"
        },
        "authority": {
          "code": "7746",
          "name": "Межрайонная инспекция Федеральной налоговой службы № 46 по г. Москве"
        }
      }
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
