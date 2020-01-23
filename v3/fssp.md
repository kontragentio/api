# Федеральная служба судебных приставов
Метод позволяет получить информацию об исполнительных производствах ФССП.

## Параметры запроса

Для получения информации о делах ФССП необходим запрос `enforcementProceedings` внутри выбранной компании.



## Пример запроса

``` graphql
query company {
  company(ogrn: "1113123006842") {
    ogrn
    fullName
    enforcementProceedings {
      list {
        number
        date
        proceedingStatus
        totalNumber
        debtor {
          name
          address
        }
        executiveDocument {
          number
          date
          type
          object
          executionObject
        }
        debtAmount {
          due
          remaining
        }
        bailiffDepartment {
          name
          address
        }
      }
      statistics {
        totalCount
        openCount
      }
    }
  }
}
```


## Пример ответа
``` json
{
  "data": {
    "company": {
      "ogrn": "1113123006842",
      "fullName": "ОБЩЕСТВО С ОГРАНИЧЕННОЙ ОТВЕТСТВЕННОСТЬЮ \"2&2\"",
      "enforcementProceedings": {
        "list": [
          {
            "number": "41507/19/31010-ИП",
            "date": 1553731200,
            "proceedingStatus": "CLOSED",
            "totalNumber": null,
            "debtor": {
              "name": "ОБЩЕСТВО С ОГРАНИЧЕННОЙ ОТВЕТСТВЕННОСТЬЮ \"2&2\"",
              "address": "РОССИЯ,308007, , ,БЕЛГОРОД Г, ,НЕКРАСОВА УЛ,6А,,"
            },
            "executiveDocument": {
              "number": "2949",
              "date": 1553558400,
              "type": "Акт органа, осуществляющего контрольные функции",
              "object": null,
              "executionObject": "Взыскание налогов и сборов, включая пени"
            },
            "debtAmount": {
              "due": 0,
              "remaining": 0
            },
            "bailiffDepartment": {
              "name": "ОСП по г. Белгороду",
              "address": "308015, БЕЛГОРОДСКАЯ ОБЛАСТЬ, Г.БЕЛГОРОД, УЛ. КОТЛОЗАВОДСКАЯ,25"
            }
          },
          {
            "number": "43518/19/31010-ИП",
            "date": 1553817600,
            "proceedingStatus": "CLOSED",
            "totalNumber": null,
            "debtor": {
              "name": "ОБЩЕСТВО С ОГРАНИЧЕННОЙ ОТВЕТСТВЕННОСТЬЮ \"2&2\"",
              "address": "РОССИЯ,308007, , ,БЕЛГОРОД Г, ,НЕКРАСОВА УЛ,6А,,"
            },
            "executiveDocument": {
              "number": "4319",
              "date": 1553644800,
              "type": "Акт органа, осуществляющего контрольные функции",
              "object": null,
              "executionObject": "Взыскание налогов и сборов, включая пени"
            },
            "debtAmount": {
              "due": 0,
              "remaining": 0
            },
            "bailiffDepartment": {
              "name": "ОСП по г. Белгороду",
              "address": "308015, БЕЛГОРОДСКАЯ ОБЛАСТЬ, Г.БЕЛГОРОД, УЛ. КОТЛОЗАВОДСКАЯ,25"
            }
          }
        ],
        "statistics": {
          "totalCount": 2,
          "openCount": 0
        }
      }
    }
  }
}
```
