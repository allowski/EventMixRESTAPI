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

# Authorize ticket usage

**End-point**: ```/api/public/authorizeTicket```  
**Method**: ```POST```  
**Authentication**: ```Token```   
**Params**: ```RequestBody```  
**Example Request**:  
```[GET] https://www.eventmix.com.br/api/public/authorizeTicket```
**Request Body**  
```JSON
{
   "id":2401269,
   "sectorName":"PISTA",
   "categoryName":"PROMOCIONAL",
   "isAuthorized":false,
   "authorized":{
      "name":"Alberto Miranda Dencowski",
      "email":"allowski@gmail.com",
      "document":"07990248131",
      "country":"55"
   }
}
```

**Response example**  
```JSON
{
   "ok":true,
   "errCode":1,
   "validation":{
      "name":true,
      "email":true,
      "document":true,
      "country":true,
      "namex":[
         true,
         true
      ],
      "ok":true
   },
   "profile":{
      "id":8120,
      "name":"Alberto Miranda Dencowski",
      "email":"allowski@gmail.com",
      "cellphone":"4599154785",
      "document":"321121233213",
      "zipCode":"85851200",
      "country":"55",
      "address":"Rua Bartolomeu de Gusm\u00e3o",
      "addressNumber":"12344",
      "city":"Foz do Igua\u00e7u",
      "complement":"",
      "state":"PR"
   },
   "err":null,
   "validationA":{
      "name":false,
      "email":false,
      "document":false,
      "country":true,
      "namex":[
         false,
         false
      ],
      "ok":false
   }
}
```

# Get user profile
**End-point**: ```/api/public/getProfile```  
**Method**: ```GET```  
**Authentication**: ```Token```   
**Params**: ```NONE```  
**Example Request**:  
```[GET] https://www.eventmix.com.br/api/public/getProfile```

**Response example**  
```JSON
{

}
```

# Update user profile

**End-point**: ```/api/public/updateUserProfile```  
**Method**: ```POST```  
**Authentication**: ```Token```   
**Params**: ```RequestBody```  
**Example Request**:  
```[GET] https://www.eventmix.com.br/api/public/updateUserProfile```
**Request Body**  
```JSON
{
   "id":8120,
   "name":"Alberto Miranda Dencowski",
   "email":"allowski@gmail.com",
   "cellphone":"4599154785",
   "document":"321121233213",
   "zipCode":"85851200",
   "country":"55",
   "address":"Rua Bartolomeu de Gusmão",
   "addressNumber":"12344",
   "city":"Foz do Iguaçu",
   "complement":"",
   "state":"PR"
}
```

**Response example**  
```JSON
{
   "id":8120,
   "name":"Alberto Miranda Dencowski",
   "email":"allowski@gmail.com",
   "cellphone":"4599154785",
   "document":"321121233213",
   "zipCode":"85851200",
   "country":"55",
   "address":"Rua Bartolomeu de Gusm\u00e3o",
   "addressNumber":"12344",
   "city":"Foz do Igua\u00e7u",
   "complement":"",
   "state":"PR"
}
```

# Get static pages

**End-point**: ```/api/public/page```  
**Method**: ```GET```  
**Authentication**: ```NONE```   
**Params**: ```?param1={pageId}```  
**Example Request**:  
```[GET] https://www.eventmix.com.br/api/public/page?param1=duvidas-frequentes```

**Response example**  
```JSON
{"code":200,"id":16,"title":"D\u00favidas Frequentes","body":"","system":false,"url":"duvidas-frequentes","subPages":[{"title":"1. Cadastro","body":"<p>Entre no menu&nbsp;<strong>Cadastro<\/strong>, cadastre os seus dados.<\/p>\n\n<p>ATEN&Ccedil;&Atilde;O&nbsp;N&atilde;o esque&ccedil;a de informar o seu CPF\/RG e dados corretamente.<\/p>"},{"title":"2. Formas de Pagamento","body":"<p><img src=\"http:\/\/192.241.204.130\/static\/tarjetas\/visa.png\" \/>&nbsp;<img src=\"http:\/\/192.241.204.130\/static\/tarjetas\/master.png\" \/>&nbsp;<img src=\"http:\/\/192.241.204.130\/static\/tarjetas\/elo.png\" \/>&nbsp;<img src=\"http:\/\/192.241.204.130\/static\/tarjetas\/amex.png\" \/><\/p>\n\n<p>ATEN&Ccedil;&Atilde;O: Somente aceitamos cart&otilde;es de cr&eacute;dito.<\/p>\n\n<p><strong>ATEN&Ccedil;&Atilde;O ESTRANGEIRO:<\/strong> Caso n&atilde;o estiver no Brasil, consulte a sua operadora.<\/p>"},{"title":"3. Como receber meus ingressos","body":"<p>O Ingresso ser&aacute; enviado em Formato PDF.<br \/>\nO recebimento do ingresso esta vinculado com o e-mail utilizado no cadastro do site, sendo o mesmo da compra na operadora do titular do cart&atilde;o,<br \/>\nRecebimento do ingresso autom&aacute;tico no email.<br \/>\nO ingresso ser&aacute; Validado na Portaria do Evento.<br \/>\nCaso n&atilde;o receba o ingresso entrar em contato conosco.<\/p>"},{"title":"4. Obrigat\u00f3rio","body":"<p>O ingresso dever&aacute; ser impresso usando Google Chrome ou Adobe PDF Reader.<br \/>\n<strong>ATEN&Ccedil;&Atilde;O:&nbsp;Obrigat&oacute;rio o preenchimento dos campos abaixo do Ingresso recebido com os dados pedidos e apresentados na Valida&ccedil;&atilde;o do Evento.<\/strong><\/p>\n\n<p><strong>Quais documentos preciso apresentar para entrar com meu ingresso?<\/strong><br \/>\nPara compras feitas com cart&atilde;o de cr&eacute;dito &eacute; indispens&aacute;vel a apresenta&ccedil;&atilde;o da m&iacute;dia pl&aacute;stica juntamente com um documento oficial com foto. Preencher dados abaixo do Ingresso recebido no email.<\/p>\n\n<p><strong>Outra pessoa pode entrar com os ingressos por mim?<\/strong><br \/>\nCaso voc&ecirc; n&atilde;o possa estar presente no evento o portador do ingresso dever&aacute; ter Procura&ccedil;&atilde;o do comprador\/titular assinada e conhecida firma.<\/p>\n\n<p>Para compras feitas com cart&atilde;o de cr&eacute;dito, o respons&aacute;vel dever&aacute; apresentar:<br \/>\n1. Um documento seu oficial com foto;&nbsp;<br \/>\n2. A procura&ccedil;&atilde;o preenchida, impressa e assinada;&nbsp;<br \/>\n3. C&oacute;pia simples do documento oficial do titular da compra;<br \/>\n4. C&oacute;pia simples do cart&atilde;o de cr&eacute;dito utilizado na compra.<\/p>"},{"title":"5. Meia entrada","body":"<p>O que devo apresentar para comprovar a meia-entrada? Em cumprimento do DECRETO FEDERAL N&ordm; 8.537, DE 5 DE OUTUBRO DE 2015, os ingressos meia-entrada s&atilde;o v&aacute;lidos para:<\/p>\n\n<p><strong>Estudantes e Professores dos Ensinos Infantil, Fundamental, M&eacute;dio, T&eacute;cnico, Gradua&ccedil;&atilde;o e P&oacute;s Gradua&ccedil;&atilde;o.<\/strong><br \/>\nComprova&ccedil;&atilde;o: Apresenta&ccedil;&atilde;o da CIE (Carteira de Identifica&ccedil;&atilde;o Estudantil) no momento da aquisi&ccedil;&atilde;o do ingresso e na entrada do local de realiza&ccedil;&atilde;o do evento. Mais informa&ccedil;&otilde;es no site: www.documentodoestudante.com.br<\/p>\n\n<p><strong>Pessoas com idade igual ou superior a 60 anos<\/strong><br \/>\nComprova&ccedil;&atilde;o: Apresenta&ccedil;&atilde;o de documento oficial com foto no momento da aquisi&ccedil;&atilde;o do ingresso e na entrada do local de realiza&ccedil;&atilde;o do evento.<\/p>\n\n<p><strong>Jovens de baixa renda<\/strong>&nbsp;com idade entre 15 e 29 anos inscritos no Cad&Uacute;nico (Cadastro &Uacute;nico para Programas Sociais do Governo Federal). Comprova&ccedil;&atilde;o: Apresenta&ccedil;&atilde;o da carteirinha da Identidade Jovem acompanhada de documento de identifica&ccedil;&atilde;o com foto no momento da aquisi&ccedil;&atilde;o do ingresso e na entrada do local de realiza&ccedil;&atilde;o do evento.<\/p>\n\n<p><strong>Pessoas com Necessidades Especiais (PNE) e Acompanhante<\/strong>&nbsp;Comprova&ccedil;&atilde;o: Para o PNE, apresenta&ccedil;&atilde;o do cart&atilde;o de Benef&iacute;cio de Presta&ccedil;&atilde;o Continuada da Assist&ecirc;ncia Social da pessoa com defici&ecirc;ncia ou de documento emitido pelo INSS que ateste a aposentadoria. Para o Acompanhante: Apresenta&ccedil;&atilde;o de declara&ccedil;&atilde;o de necessidade de acompanhante que pode ser feita pela pr&oacute;pria pessoa PNE ou do Acompanhante + apresenta&ccedil;&atilde;o de documento oficial com foto no momento da aquisi&ccedil;&atilde;o do ingresso e na entrada do local de realiza&ccedil;&atilde;o do evento.<\/p>\n\n<p><strong>IMPORTANTE: &Eacute; OBRIGAT&Oacute;RIA E INDISPENS&Aacute;VEL A APRESENTA&Ccedil;&Atilde;O DE DOCUMENTO QUE COMPROVE O DIREITO AO BENEF&Iacute;CIO NO MOMENTO DA COMPRA E NO ACESSO AO EVENTO PARA CADA INGRESSO ADQUIRIDO COM O BENEF&Iacute;CIO DA MEIA-ENTRADA.<\/strong><\/p>\n\n<p>Em algumas cidades h&aacute; legisla&ccedil;&atilde;o espec&iacute;fica sobre o benef&iacute;cio da Meia-entrada podendo haver outros benef&iacute;cios e meios de comprova&ccedil;&atilde;o. Deste modo, quando houver, prevalece a descri&ccedil;&atilde;o detalhada da lei local. Para mais detalhes sobre outros grupos de benefici&aacute;rios, verifique a lei vigente de sua cidade ou estado<\/p>"},{"title":"6. Cancelamento da compra","body":"<p><strong>Posso cancelar a minha compra?<\/strong><\/p>\n\n<p><strong>Pol&iacute;tica de Compras no Site<\/strong><\/p>\n\n<p><strong>Cancelamento de Compras<\/strong>&nbsp;Conforme o C&oacute;digo de Defesa do Consumidor (Artigo 49), somente ser&atilde;o aceitos pedidos de cancelamentos de compras solicitados at&eacute; 7 dias ap&oacute;s o pedido, desde que n&atilde;o ultrapasse o limite de 48hs antes do in&iacute;cio do evento, descontada a taxa de postagem (correios), se houver.<\/p>\n\n<p>Ap&oacute;s o prazo mencionado acima, n&atilde;o &eacute; poss&iacute;vel desistir da compra, uma vez que os valores s&atilde;o repassados aos organizadores dos eventos, e os mesmos n&atilde;o ficam em poder da EventMix.<\/p>\n\n<p><strong>Pol&iacute;tica de Compras na Rede Pontos de Venda<\/strong><\/p>\n\n<p><strong>Cancelamentos de Compras:<\/strong>&nbsp;Para compras realizadas na nossa rede de Ponto de Venda, n&atilde;o haver&aacute; devolu&ccedil;&atilde;o dos valores pagos pelos ingressos ou pelos servi&ccedil;os prestados; salvo nos casos que se enquadram no item abaixo, efetuaremos o reembolso dos valores.<\/p>\n\n<p><strong>Cancelamentos, Trocas de Hor&aacute;rios e Datas de Eventos:<\/strong>&nbsp;Clientes que compraram ingressos nos pontos de venda devem seguir orienta&ccedil;&otilde;es espec&iacute;ficas de cada evento, pois os procedimentos neste caso ser&atilde;o formatados para cada evento. Nesse caso, favor entrar em contato atrav&eacute;s dos nossos telefones ou website, na op&ccedil;&atilde;o Fale Conosco.<\/p>\n\n<p>As devolu&ccedil;&otilde;es s&atilde;o sempre realizadas conforme a forma de pagamento utilizada no momento da compra.<\/p>\n\n<p><strong>Cart&atilde;o de Cr&eacute;dito:<\/strong>&nbsp;O estorno total do valor pago pelo ingresso &eacute; feito diretamente na operadora do cart&atilde;o de cr&eacute;dito e o valor ser&aacute; creditado integralmente na sua pr&oacute;xima fatura.<\/p>\n\n<p><strong>ATEN&Ccedil;&Atilde;O&nbsp;Lembramos que ap&oacute;s o evento, n&atilde;o ser&atilde;o realizados cancelamentos e devolu&ccedil;&otilde;es de valores.<\/strong><\/p>"},{"title":"7. Pagamentos","body":"<p><strong>Como funciona a compra por Cart&atilde;o de Cr&eacute;dito<\/strong><\/p>\n\n<p>Nossa tecnologia garante que os dados do seu cart&atilde;o de cr&eacute;dito sejam enviados diretamente para a sua operadora, garantindo sigilo no momento da compra. A EventMix n&atilde;o armazena os dados de cart&otilde;es de cr&eacute;dito.<\/p>\n\n<p><strong>Confirma&ccedil;&atilde;o de Pagamento:<\/strong><\/p>\n\n<p>A autoriza&ccedil;&atilde;o para pagamento por cart&atilde;o de cr&eacute;dito &eacute; on-line, ou seja, &eacute; realizada automaticamente ap&oacute;s a conclus&atilde;o da sua compra. &Eacute; normal que demore alguns minutos para que a transa&ccedil;&atilde;o seja efetivada junto &agrave; operadora. Caso voc&ecirc; n&atilde;o receba a confirma&ccedil;&atilde;o imediatamente ap&oacute;s a compra, aguarde alguns minutos. O pagamento via cart&atilde;o de cr&eacute;dito est&aacute; sujeito &agrave; aprova&ccedil;&atilde;o da administradora do cart&atilde;o.<\/p>\n\n<p><strong>Parcelamento via Cart&atilde;o:<\/strong><\/p>\n\n<p>A disponibilidade para parcelamento do seu pedido somente no valor acima de R$ 700,00 (setecentos reais), &eacute; disponibilizado somente para compras com cart&atilde;o de cr&eacute;dito.<\/p>\n\n<p><strong>Seguran&ccedil;a para compras via Cart&atilde;o de Cr&eacute;dito:<\/strong><\/p>\n\n<p>Um dos nossos principais prop&oacute;sitos &eacute; prezar pela seguran&ccedil;a na utiliza&ccedil;&atilde;o de cart&otilde;es de cr&eacute;dito no site da EventMix. Por este motivo, as operadoras de cart&atilde;o possuem a seguran&ccedil;a das compras que passam por uma an&aacute;lise a fim de que sejam evitadas fraudes com o uso indevido de cart&otilde;es de terceiros. Para garantir sua seguran&ccedil;a, poderemos confirmar alguns dados por telefone ou e-mail e\/ou solicitar que voc&ecirc; forne&ccedil;a informa&ccedil;&otilde;es adicionais para verificar sua identidade, como por exemplo c&oacute;pias digitalizadas de seus documentos<\/p>"},{"title":"8. Geral","body":"<p><strong>O que &eacute; a taxa de Administrativa\/Conveni&ecirc;ncia?<\/strong><\/p>\n\n<p>A EventMix &eacute; uma empresa prestadora de servi&ccedil;os que tem como prop&oacute;sito aproximar as pessoas de experi&ecirc;ncias nos eventos ao vivo. N&oacute;s trabalhamos fazendo a intermedia&ccedil;&atilde;o de vendas entre o Organizador do Evento e voc&ecirc;, o nosso p&uacute;blico final.<\/p>\n\n<p>Nosso relacionamento com o Organizador do Evento prev&ecirc; o repasse integral dos valores dos ingressos, sendo a taxa de Administrativa\/Conveni&ecirc;ncia a remunera&ccedil;&atilde;o dos servi&ccedil;os prestados pela nossa empresa. Com ela buscamos oferecer uma melhor infra-estrutura, para que voc&ecirc; possa comprar ingressos de maneira mais r&aacute;pida e segura, seja em casa atrav&eacute;s da Internet ou da nossa Rede de Pontos de Venda.<\/p>\n\n<p><strong>Para mais informa&ccedil;&otilde;es sobre nossos servi&ccedil;os<\/strong>, ficaremos felizes em atender voc&ecirc; em nossa Central de Atendimento por telefone ou ent&atilde;o pela se&ccedil;&atilde;o Fale Conosco.<\/p>"}],"err":null}
```
