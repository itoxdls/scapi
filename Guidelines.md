# Auth

**Request**

 Method | Request URI | Description
------- | ----------- | ------------
POST | /api/auth | Autenticación de Usuario

**Headers**

No headers

**Params**

 Name | Type | Required | Description
---- | ----- | -------- | ------------
user | string | Required | Nombre de usuario
pass | string | Required | Password del usuario

**Body**

No body

**Response**

Code | Status | Message
---- | ------ | -------
200 | OK | Successfully auth user
400 | BAD REQUEST | User does not exist

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
---- | ----- | -------- | ------------
authcode | string | Required | Hash session del usuario

**Body**

No body

**Response**

Code | Status | Message
---- | ------ | -------
200 | OK | Successfully get token
400 | BAD REQUEST | Authorization Required

```
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Njg1MjA2NDIsImlhdCI6MTUzNjk4NDY0Miwic3ViIjoiMjc3M2M0NTEtZDgwOS00NzQ1LWEzYmQtODdlYjUyMDk0ZTk5In0.LJN2uKJT8REBeH8WhljJAM3JGCiklXJS29Htn5SZP4A"
}
```
**Php example**

```php
$request = new HttpRequest();
$request->setUrl('/api/auth');
$request->setMethod(HTTP_METH_POST);

$request->setQueryData(array(
  'user' => 'user',
  'pass' => 'pass'
));

try {
  $response = $request->send();

  echo $response->getBody();
} catch (HttpException $ex) {
  echo $ex;
}
```

**Python example**

```python
import requests

response = requests.request("POST", "/api/auth", params={
    "user":"user",
    "pass":"pass"
})

print(response.text)
```
