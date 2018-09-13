# Sistema Touch Ticket

## Project Structure:

Important Files:
```
/touch.php      -> MainClass
```
Back-end:
```
/api/
    vendor/     -> Composer
    classes/    -> Classes
    utils/      -> Utils
    admin/      -> Admin Module (Admin Panel)
    mobile/     -> App Module (Android App)
    public/     -> Public Module (E-commerce Site)
    config.php  -> Configurations (AWS, E-mail, JWT, DATABASE)
```
Front-end:
```
painel/                 -> Admin Folder (Contains Angular Build Snapshot)

index.php               -> Site Entry Point (Home)
evento.php              -> Single Event Page
comprar-camarote.php    -> Buy Camarote
pagamento.php           -> Creates a PagSeguro Payment // Generates the order
minhas-compras.php      -> My Orders Page
authorizar-ingresso.php -> Ticket Authorizing Page
carrito.php             -> Shopping Cart accessed by ajax.
login.php               -> User Login (POST).
register.php            -> User Registration (POST).
rest/eventos.php        -> EventList accessed by Ajax.
rest/affiliates         -> Promoter Link Generator.
l.php                   -> Promoter Ticket Authorizing.
decode.php              -> Promoter Ticket URL Generator.
```
Notification Listener:
```
paymentReturn.php       -> Handles PagSeguro Notifications.
```
# Deprecated API
```
rest/       -> This folder contains versioned app api and some deprecated.
rest/3.X    -> Deprecated Mobile App API
rest/4.X    -> Deprecated Mobile App API
```

#System Requirements

- Recomended OS: Ubuntu >=16.04 

## Back-end Server
- PHP: >= 7.0
- Interbase extension: php-interbase
- Imap extenstion: php-imap
- MultiByte string: php-mbstring
- XML: php-simplexml
- YAML: php-yaml
- Composer: composer
- Apache: >= 2.4 with mod_php enabled

Others packages:
- Imagick (convert command)
- Python PIP: weasyprint (for pdf generation)

## Database Server

Firebird: firebird2.5-superclassic

---
# REST API
---
# Base url

``` https://www.eventmix.com.br/ ```

# Request Auhtentication
Every request marked as ```Authentication: Token``` on this document must be made setting the Request header ```Authorization``` with the user token. As follow:
```Authorization: sdas78d9as7d89as7d09a8sd7sad98asd7as89d0sa7d8...```

# Site Configuration
**Site Config**: ```/api/public/config```
**Description**: Returns all the site configuration, like title, colors and so on.
**Method**: ```GET```
**Authentication**:```Not required```
**Params**: ```NONE```
**Request Example**:
```[GET] https://www.eventmix.com.br/api/public/config```
**Response Example**:
```JSON
{
    "id": 1,
    "title": "EventMix - ADM",
    "legalName": "Eventmix Tecnologia e Finanças Ltda",
    "businessId": "20.251.079/0001-30",
    "atentionTime": "Segunda a Sexta das 10h00 às 19h00",
    "facebookFanpageUrl": "",
    "address": "Jardim Aquarius, Rua Armando D Oliveira Cobra, 50",
    "zipCode": "12246-002",
    "phone": "",
    "cellphone": "(12) 9 9675-5877 WhatsApp",
    "email": "contato@eventmix.com.br",
    "favicon": {
        "small": "https://cdn.ecoticket.com.br/content/eventmix/1535460015-Favicon-0-small-64x64.png",
        "medium": "https://cdn.ecoticket.com.br/content/eventmix/1535460017-Favicon-0-medium-256x256.png"
    },
    "logo": {
        "small": "https://cdn.ecoticket.com.br/content/eventmix/1535459604-Logo-0-small-300x150.png",
        "medium": "https://cdn.ecoticket.com.br/content/eventmix/1535459605-Logo-0-medium-600x300.png"
    },
    "user": null,
    "menuItems": [
        {
            "title": "Duvidas Frequentes",
            "url": "/duvidas-frequentes",
            "target": ""
        },
        {
            "title": "Contato",
            "url": "/contato",
            "target": ""
        }
    ]
}
```

# User Authentication
**User authentication**: ```/api/public/login```
**Description**: Authenticates the user using username/password combination
**Method**: ```POST```
**Authentication**: ```NONE```
**Params**: ```RequestBody```
**Request Example**:
```[POST] https://www.eventmix.com.br/api/public/login```
**Headers:**
```Content-Type: application/json```
**RequestBody:**
```JSON
{
    "email": "anonuser@gmail.com",
    "password": "123456"
}
```
**Response Example**:
**Success:**
```CODE: 200```
```JSON
{
    "success": true,
    "field": "email",
    "token": "eyJ0eXAiOiJKV1QiAeOHV8Uy-v3f4guSj7vALcaKWdLG9q1haSck_t19mg",
    "id": 8120,
    "user": {
        "id": 8120,
        "name": "Alberto miranda",
        "email": "allowski@gmail.com",
        "cellphone": "45991547855",
        "zipCode": "85851160",
        "country": ""
    }
}
```
**Failed**:
```CODE 401```
```JSON
{
    "message": "Senha invalida.",
    "related": null,
    "redir": "/login"
}
```

# Check if user email is already registered

**End-point:** ```/api/public/checkIfEmailExists```
**Description:** Checks if an email is registered or not, also validates the input email
**Method**: ```POST```
**Params**: ```RequestBody```
**Request Example**:
```[POST]  https://www.eventmix.com.br/api/public/checkIfEmailExists```
**Headers**:
```Content-Type: application/json```
**RequestBody**:
```JSON
{
    "email":"anonuser@gmail.com"
}
```

**Response Example (Success)**:
```JSON
{
    "id": 8120,
    "exists": true,
    "email": "allowski@gmail.com",
    "name": "Alberto Miranda"
}
```

**Response Example (Not found):**
```JSON
{
    "id": null,
    "exists": false,
    "email": "allowd@gmail.com",
    "name": ""
}
```

# Register a new user / customer

**End-point**: ```https://www.eventmix.com.br```
**Description**: Create a new user profile
**Method:**: ```POST```
**Params**: ```RequestBody```
**Request Example**:
```[POST] https://www.eventmix.com.br/api/public/register```
**Request Body**:
```JSON
{
    "email":"anonuser@gmail.com",
    "password":"super$afePas$Word",
    "name": "Alberto Miranda Dencowski",
    "country": "55",
    "cellphone": "45991547856"
}
```
**Response Example (Success)**:
```CODE 200```
```JSON
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOyTow",
    "ok": true,
    "id": 24092,
    "err": null
}
```
**Response Example (Failed)**:
```CODE 401```
```JSON
{
    "message": "E-mail em uso.",
    "related": null,
    "redir": "/login"
}
```


# Event Listing
**Event List**: ```/api/public/event-list```
**Description**: List all the active events, and cities to display in the front-page.
**Method**: ```GET```
**Authentication**:```Not required```
**Params**: ```?q=QueryString```
**Request Example:**
```[GET] https://www.eventmix.com.br/api/public/event-list?q=Texto+Para+Busca ```
**Response Example:**
```JSON
{
    "q": "",
    "eventos": [
        {
            "id_evento": 1353,
            "nome": "WARUNG TOUR 2018",
            "data": "2018-09-15",
            "dia_mes": "15",
            "mes3": "Set",
            "mes": "Setembro",
            "n_dia_semana": 6,
            "year": 2018,
            "dia_semana": "",
            "data_formatada": "15 de Setembro",
            "hora": "23:00 h",
            "hr_ab": "23:00:00",
            "cidade": "PR - Foz Do Iguaçu",
            "empresa": "3vent",
            "id_cidade": 1,
            "dominio": "www.allingressos.com.br",
            "promo": false,
            "url": "//www.allingressos.com.br/evento/1353/WARUNG-TOUR-2018-em-Foz-Do-Iguaçu/ingressos",
            "lotes_url": "//www.allingressos.com.br/rest/lotes.php?id_evento=1353&evento=warung-tour-2018&cidade=pr-foz-do-iguaçu&ingressos,ingresso",
            "url_enc": "//www.allingressos.com.br/evento.php?id=1353&amp;evento=warung-tour-2018&amp;cidade=pr-foz-do-igua%C3%A7u",
            "thumbnail": "https://cdn.ecoticket.com.br/content/alling/1531925479-thumbnail-1353-medium-512x512.jpg",
            "banner": "https://cdn.ecoticket.com.br/content/alling/1531925023-banner-1353-small-1170x400.jpg"
        },
    ],
    "cidades": [
        {
            "nome": "PY - CIUDAD DEL ESTE",
            "uf": "PY",
            "count": 3,
            "id": 2,
            "url": "index-new.php?id_cidade=2"
        },
        {
            "nome": "PR - FOZ DO IGUAÇU",
            "uf": "PR",
            "count": 4,
            "id": 1,
            "url": "index-new.php?id_cidade=1"
        },
        {
            "nome": "SP - SAO PAULO",
            "uf": "SP",
            "count": 1,
            "id": 69,
            "url": "index-new.php?id_cidade=69"
        }
    ]
    ]
}
```

# Event Page
**Event Page**: ```/api/public/event-page```
**Description**: List all the event tickets, points of sale and gives details about the given event id.
**Method**: ```GET```
**Authentication**:```Not required```
**Params**: ```?param1={eventId}```
**Request Example:**
```[GET] https://www.eventmix.com.br/api/public/event-page?param1=3040```
**Response Example:**
```JSON
{
    "err": null,
    "event": {
        "name": "Só House Music 2",
        "startDate": "2018-09-29 16:17:23",
        "endDate": "2018-09-29 16:17:23",
        "id": 3040,
        "city": "PIRACICABA",
        "description": "Proibida a entrada de menores de 18 anos.",
        "address": "Av Maria Elisa, 283",
        "local": "Villa Francesa Eventos",
        "banner": "https://cdn.ecoticket.com.br/content/eventmix/1536023140-banner-3040-small-1170x400.jpg",
        "thumbnail": "https://cdn.ecoticket.com.br/content/eventmix/1536023111-thumbnail-3040-medium-512x512.jpg",
        "map": "",
        "pdvs": [
            {
                "name": "TENIS MANIA",
                "address": "R. Rangel Pestana, 834 - Centro",
                "city": "Piracicaba - SP  - SP  (Dinheiro/ Cartão Crédito e Debito) c/ taxa.",
                "phone": "(19) 3402-9406"
            },
            {
                "name": "KINGS SHOPP PIRACICABA",
                "address": "Av. Limeira, 722 , Areião",
                "city": "Piracicaba - SP  (Dinheiro/ Cartão Crédito e Debito) c/ taxa.",
                "phone": "(19) 3927-4756"
            }
        ],
        "tickets": [
            {
                "name": "PISTA",
                "id": 1797,
                "open": false,
                "items": [
                    {
                        "id": 11655,
                        "limited": false,
                        "currency": "BRL",
                        "name": "FEMININO",
                        "description": "CONSOME R$ 30,00",
                        "price": 33,
                        "qty": 0,
                        "items": null
                    },
                    {
                        "id": 11656,
                        "limited": false,
                        "currency": "BRL",
                        "name": "MASCULINO",
                        "description": "CONSOME R$ 50,00",
                        "price": 55,
                        "qty": 0,
                        "items": null
                    }
                ]
            },
            {
                "name": "BANGALÔ",
                "id": 1801,
                "open": false,
                "items": [
                    {
                        "id": 11668,
                        "limited": true,
                        "currency": "BRL",
                        "name": "RESERVADO P/10 PESSOAS",
                        "description": "R$ 100,00 Consuma por pessoa",
                        "price": 3000,
                        "qty": 0,
                        "items": [
                            {
                                "number": 1,
                                "selected": false,
                                "free": true
                            },
                            {
                                "number": 2,
                                "selected": false,
                                "free": true
                            },
                            {
                                "number": 3,
                                "selected": false,
                                "free": true
                            },
                            {
                                "number": 4,
                                "selected": false,
                                "free": true
                            }
                        ]
                    }
                ]
            }
        ]
    }
}
```
# Check out process

**End-point**: ```/api/public/checkout```
**Description**: Create a new order, and payment entry on pagseguro.
**Params**: ```RequestBody```
**Method**: ```POST```
**Authentication**: ```Token```
**Request Example**:
```[POST] https://www.eventmix.com.br/api/public/checkout```
**Request Body**:
```JSON
{
   "cart":[
      {
         "name":"PRIVATES",
         "id":1821,
         "open":false,
         "items":[
            {
               "id":11761,
               "limited":true,
               "currency":"BRL",
               "name":"RESERVADO P/ 20 PESSOAS",
               "description":"Consumação R$ 500 p/ pessoa",
               "price":60000,
               "qty":0,
               "items":[
                  {
                     "number":1,
                     "selected":false,
                     "free":false
                  },
                  {
                     "number":2,
                     "selected":false,
                     "free":false
                  },
                  {
                     "number":3,
                     "selected":false,
                     "free":false
                  },
                  {
                     "number":4,
                     "selected":false,
                     "free":false
                  }
               ],
               "lastAdded":false
            }
         ]
      },
      {
         "name":"PISTA",
         "id":1820,
         "open":false,
         "items":[
            {
               "id":11758,
               "limited":false,
               "currency":"BRL",
               "name":"PROMOCIONAL",
               "description":"*Meia promocional com doação de 1kg de alimento",
               "price":46,
               "qty":1,
               "items":null,
               "lastAdded":true
            }
         ]
      }
   ],
   "order":{
      "email":"",
      "country":"",
      "name":"",
      "phone":"",
      "password":"",
      "cellphone":"",
      "transactionCode":""
   }
}
```

**Response example:**
```JSON
{
   "jwtErr":{

   },
   "token":{
      "token":"eyJ0eXAiOiJKV1g",
      "ok":true,
      "id":24091,
      "err":null
   },
   "order":{
      "id":1935691
   },
   "errors":[
      null
   ],
   "response":{
      "code":"DECFA05738380C533464CFB7D4717F35",
      "date":"2018-09-13T14:40:13.000-03:00"
   },
   "ok":true
}
```

>>> Note:
>>> Use the responseObject.response.code value to open the PagSeguro LightBox to proceed to the payment.

# Pagseguro LightBox Usage

```JS
PagSeguroLightbox({
    code: result.response.code
}, {
    success : function(transactionCode) {
       swal2({
        title: 'Pagamento concluido',
        text: '',
        type: 'success'
      }); 
    },
    abort: () => {
        this.restService.cancelOrder(result.order.id).subscribe(() => {});
        swal2({
            title: 'Pagamento cancelado',
            text: '',
            type: 'error'
        });
    }
});
```

# List User Orders
**End-point**: ```/api/public/orderList```
**Method**: ```GET```
**Authentication**: ```Token```
**Params**: ```NONE```
**Example Request**:
```[GET] https://www.eventmix.com.br/api/public/orderList```
```JSON
{
   "orders":[
      {
         "id":1935691,
         "datetime":"2018-09-13 14:40:12",
         "currency":"BRL",
         "amount":"150",
         "eventName":"EVENTO DEMONSTRA\u00c7\u00c3O",
         "status":"T"
      }
   ],
   "err":null
}
```

# Get Order Details
**End-point**: ```/api/public/order```
**Method**: ```GET```
**Authentication**: ```Token```
**Params**: ```?param1={orderId}```
**Example Request**:
```[GET] https://www.eventmix.com.br/api/public/order?param1=1935691```
**Response Example**
```JSON
{
   "id":"1935691",
   "eventName":"EVENTO DEMONSTRA\u00c7\u00c3O",
   "items":[
      {
         "id":2401553,
         "sectorName":"AREA VIP",
         "categoryName":"OPEN BAR",
         "isAuthorized":false,
         "authorized":{
            "name":"",
            "email":"",
            "document":""
         }
      }
   ]
}
```

