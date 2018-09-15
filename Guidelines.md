Auth
============

# Auth

**Request**

 Method | Request URI | Description
------- | ----------- | ------------
POST | /api/auth | Autenticación de Usuario

**Headers**

Name | Required | Value | Description
---- | -------- | -------- | --------
Content-Type | Required | application/json | Sen data with json
Accept | Optional | image/jpeg | Muestra la ultima imagen del último loader

**Params**

 Name | Type | Required | Description
------- | ----------- | ------------
user | string | Required | Nombre de usuario
pass | string | Required | Password del usuario

**Body**

No body

**Response**

 Status | Message
------- | ----------- | ------------
201 | string | Successfully added queue
409 | string | Required | Password del usuario

```
{
    "authcode": "2773c451-d809-4745-a3bd-87eb52094e99"
}
```

# Token

**Request**

 Method | Request URI | Description
------- | ----------- | ------------
POST | /api/auth/token | Obtener el token del usuario

**Headers**

No headers

**Params**

 Name | Type | Required | Description
------- | ----------- | ------------
authcode | string | Required | Ej. hash session del usuario Ej. ae81aad5-0b00-4fc0-b6f7-3a582db02315

**Body**

No body

**Response**

 Code | Status | Message
------- | ----------- | ------------
200 | OK | Successfully added queue
400 | BAD REQUEST | Authorization Required

```
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Njg1MjA2NDIsImlhdCI6MTUzNjk4NDY0Miwic3ViIjoiMjc3M2M0NTEtZDgwOS00NzQ1LWEzYmQtODdlYjUyMDk0ZTk5In0.LJN2uKJT8REBeH8WhljJAM3JGCiklXJS29Htn5SZP4A"
}
```
