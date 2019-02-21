# Карточка индивидуального предпринимателя
Метод позволяет осуществлять получить детализированную информацию о российских
ИП.

## Параметры
| Параметр | Тип | Формат | Описание |
| ------ | ------ | ------ | ------ |
| `ogrnip` | GET | строка из 15 цифр, необязательный | ОГРНИП |
| `inn` | GET | строка 10 цифр, необязательный | ИНН индивидуального предпринимателя |

Одно из полей `ogrnip` или `inn` обязательно должно быть передано.

## Пример запроса
```graphql
{
  individual(ogrnip: "304234914700470", inn: "234900794855") {
    ogrnip
    inn
    firstName
    middleName
    lastName
    gender
    email
    type
    citizenship
    registrationDate
    terminationDate
    status {
      isLiquidated
      text
      grnDate
    }
    taxInspection {
      code
      name
    }
    form {
      compact
      full
      code
    }
    address {
      full
      postalCode
      country
      federalDistrict
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
      area
      street
      house
      housing
      grnDate
    }
    okveds {
      code
      description
      grnDate
      isPrimary
    }
  }
}
```

## Пример ответа
```json
{
  "data": {
    "individual": {
      "ogrnip": "304234914700470",
      "inn": "234900794855",
      "firstName": "Клавдия",
      "middleName": "Александровна",
      "lastName": "Симакова",
      "gender": "FEMALE",
      "type": "Индивидуальный предприниматель",
      "citizenship": "RF_CITIZEN",
      "terminationDate": null,
      "status": {
        "text": null,
        "grnDate": 0
      },
      "taxInspection": {
        "grnDate": 1519603200,
        "authority": {
          "code": "2370",
          "name": "Межрайонная инспекция Федеральной налоговой службы № 11 по Краснодарскому краю"
        }
      },
      "form": {
        "compact": "ИП",
        "full": "Индивидуальный предприниматель",
        "code": "50101"
      },
      "address": {
        "full": "Краснодарский край, р-н Славянский, г. Славянск-на-кубани",
        "postalCode": null,
        "country": "Российская Федерация",
        "federalDistrict": "Южный",
        "region": {
          "full": "Краснодарский край",
          "code": "23",
          "name": "Краснодарский",
          "type": "край"
        },
        "city": {
          "full": "г. Славянск-на-кубани",
          "name": "Славянск-на-кубани",
          "type": "г."
        },
        "area": "р-н Славянский",
        "street": null,
        "house": null,
        "housing": null,
        "grnDate": 1459036800
      },
      "okveds": [
        {
          "code": "47.1",
          "description": "Торговля розничная в неспециализированных магазинах",
          "grnDate": 1085529600,
          "isPrimary": true
        },
        {
          "code": "47.11.1",
          "description": "Торговля розничная замороженными продуктами в неспециализированных магазинах",
          "grnDate": 1085529600,
          "isPrimary": false
        },
        {
          "code": "47.19",
          "description": "Торговля розничная прочая в неспециализированных магазинах",
          "grnDate": 1085529600,
          "isPrimary": false
        },
        {
          "code": "47.24",
          "description": "Торговля розничная хлебом и хлебобулочными изделиями и кондитерскими изделиями в специализированных магазинах",
          "grnDate": 1085529600,
          "isPrimary": false
        },
        {
          "code": "47.29.3",
          "description": "Торговля розничная прочими пищевыми продуктами в специализированных магазинах",
          "grnDate": 1085529600,
          "isPrimary": false
        },
        {
          "code": "47.73",
          "description": "Торговля розничная лекарственными средствами в специализированных магазинах (аптеках)",
          "grnDate": 1085529600,
          "isPrimary": false
        },
        {
          "code": "47.74",
          "description": "Торговля розничная изделиями, применяемыми в медицинских целях, ортопедическими изделиями в специализированных магазинах",
          "grnDate": 1085529600,
          "isPrimary": false
        },
        {
          "code": "47.75",
          "description": "Торговля розничная косметическими и товарами личной гигиены в специализированных магазинах",
          "grnDate": 1085529600,
          "isPrimary": false
        }
      ]
    }
  }
}
```
