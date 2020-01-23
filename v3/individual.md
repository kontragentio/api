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
query {individual(ogrnip: "304234914700470", inn: "234900794855") {
    ogrnip
    inn
    firstName
    middleName
    lastName
    gender
    type
    citizenship
    terminationDate
    status {
      currentStatus
      futureStatus
      reorganizationParticipants{
        company{
          fullName
        }
        futureStatus
      }
      text
      grnDate
    }
    taxInspection {
      grnDate
      authority{
        code
        name
      }
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
    }thirdParty{
    hh{
      openVacancies
      updated
      companyUrl
      certainty
    }
  }
  okpo
  personalData{
    snils
    birthDate
    birthPlace
    address
  }
  registration{
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
  pfr{
    regNumber
    grnDate
    authority{
      code
      name
    	}
  	}
  fss{
    regNumber
    grnDate
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
        "currentStatus": "ACTIVE",
        "futureStatus": null,
        "reorganizationParticipants": [],
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
        "full": "Краснодарский край",
        "postalCode": null,
        "country": "Российская Федерация",
        "federalDistrict": "Южный",
        "region": {
          "full": "Краснодарский край",
          "code": "23",
          "name": "Краснодарский",
          "type": "край"
        },
        "city": null,
        "area": null,
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
      ],
      "thirdParty": {
        "hh": null
      },
      "okpo": null,
      "personalData": {
        "snils": null,
        "birthDate": null,
        "birthPlace": null,
        "address": null
      },
      "registration": {
        "grnDate": 1085529600,
        "typeOfCreation": null,
        "authority": {
          "code": "2375",
          "name": "Межрайонная инспекция Федеральной налоговой службы № 16 по Краснодарскому краю"
        }
      },
      "pfr": {
        "regNumber": "033010011209",
        "grnDate": 1263945600,
        "authority": {
          "code": "033010",
          "name": "Управление Пенсионного фонда РФ в г.Славянске-на-Кубани Краснодарского края"
        }
      },
      "fss": null
    }
  }
}
```
