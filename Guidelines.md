# ScraperCloud.com REST API Guidelines

* Scapi
  * Crawl
    * [Task manager](#task-manager)
      * [Crear nueva cola](#crear-nueva-cola)
      * [Crear nueva tarea](#crear-nueva-tarea)
      * [Obtener todas las tarea de una cola](#obtener-todas-las-tarea-de-una-cola)
    * [Scheduler task manager](#scheduler-task-manager) 
      * [Elimina una tarea programada](#elimina-una-tarea-programada)
  * [Loader Api Rest](#loader-api-rest)

Task manager
============

# Crear nueva cola

**Request**

 Method | Request URI | Description
------- | ----------- | ------------
POST | /api/task/queue/<queue-id> | Agrego una nueva cola al usuario

**Headers**

 Name | Type | Description
------- | ----------- | ------------
Authorization | string | token

**Test token**
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjMwNzY4MzgsImlhdCI6MTUzMTU0MDgzOCwic3ViIjoiNTZjZmJmYjEtMmJkNC00YTE5LTg2MjQtNzQ2Y2I2MzhiNDg4In0.CNDHxP4gpo2FeHn3Fm-JABOorefcf6syW7qeqBR6AOA
```

**Body**

No body

**Response**

 Status | Message
------- | -----------
201 CREATED | Successfully added queue
409 CONFLICT | Queue already exists

**Request**

```
POST /api/task/queue/my-queue HTTP/1.1
Host: 127.0.0.1:5231
Authorization: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjMwNzY4MzgsImlhdCI6MTUzMTU0MDgzOCwic3ViIjoiNTZjZmJmYjEtMmJkNC00YTE5LTg2MjQtNzQ2Y2I2MzhiNDg4In0.CNDHxP4gpo2FeHn3Fm-JABOorefcf6syW7qeqBR6AOA
Cache-Control: no-cache
Postman-Token: 50efbac6-03f5-0c2a-841c-c89331b614e9
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW
```

**Response**

```
accept: application/json
access-control-allow-headers: X-HTTP-Method-Override, Content-Type, Authorization
access-control-allow-methods: GET,PUT,POST,DELETE
access-control-allow-origin: *
content-length: 46
content-type: application/json; charset=UTF-8
date: Tue, 21 Aug 2018 23:44:04 GMT
server: Werkzeug/0.13 Python/3.6.5

{
    "message": "Successfully added queue"
}
```
# Crear nueva tarea

**Request**

 Method | Request URI | Description
------- | ----------- | ------------
POST | /api/task/queue/<queue-id>/<task-id> | Agrego una nueva tarea a la cola especificada del usuario

**Headers**

 Name | Type | Description
------- | ----------- | ------------
Authorization | string | token

**Test token**

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjMwNzY4MzgsImlhdCI6MTUzMTU0MDgzOCwic3ViIjoiNTZjZmJmYjEtMmJkNC00YTE5LTg2MjQtNzQ2Y2I2MzhiNDg4In0.CNDHxP4gpo2FeHn3Fm-JABOorefcf6syW7qeqBR6AOA
```

**Params**

 Name | Type | Description
------- | ----------- | ------------
priority | int | Between 1 and 9 - Optional - Default 1

**Body**

```
{
	"headers":{
		"Authorization":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjMwNzY4MzgsImlhdCI6MTUzMTU0MDgzOCwic3ViIjoiNTZjZmJmYjEtMmJkNC00YTE5LTg2MjQtNzQ2Y2I2MzhiNDg4In0.CNDHxP4gpo2FeHn3Fm-JABOorefcf6syW7qeqBR6AOA"
	},
	"url":"/api/crawl/scan",
	"method":"post",
	"data":{...}
}
```

**Response**

 Status | Message
------- | -----------
201 CREATED | Successfully added task

**Request**

```
POST /api/task/queue/queue_id-1/mytask?priority=1 HTTP/1.1
Host: 127.0.0.1:5231
Authorization: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjMwNzY4MzgsImlhdCI6MTUzMTU0MDgzOCwic3ViIjoiNTZjZmJmYjEtMmJkNC00YTE5LTg2MjQtNzQ2Y2I2MzhiNDg4In0.CNDHxP4gpo2FeHn3Fm-JABOorefcf6syW7qeqBR6AOA
Content-Type: application/json
Cache-Control: no-cache
Postman-Token: 57a97598-c98c-64e2-1307-ed3a80b211e0

{
	"headers":{
		"Authorization":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjMwNzY4MzgsImlhdCI6MTUzMTU0MDgzOCwic3ViIjoiNTZjZmJmYjEtMmJkNC00YTE5LTg2MjQtNzQ2Y2I2MzhiNDg4In0.CNDHxP4gpo2FeHn3Fm-JABOorefcf6syW7qeqBR6AOA"
	},
	"url":"/api/crawl/scan",
	"method":"post",
	"data":{}
}
```

**Response**

```
accept: application/json
access-control-allow-headers: X-HTTP-Method-Override, Content-Type, Authorization
access-control-allow-methods: GET,PUT,POST,DELETE
access-control-allow-origin: *
content-length: 45
content-type: application/json; charset=UTF-8
date: Wed, 22 Aug 2018 00:37:38 GMT
server: Werkzeug/0.13 Python/3.6.5

{
    "message": "Successfully added task"
}
```

# Obtengo colas y triggers del usuario

**Request**

 Method | Request URI | Description
------- | ----------- | ------------
GET     | /api/task | Obtengo la lista de las tareas

**Headers**

 Method | Type | Description
------- | ----------- | ------------
Authorization | string | token

**Test token**
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjMwNzY4MzgsImlhdCI6MTUzMTU0MDgzOCwic3ViIjoiNTZjZmJmYjEtMmJkNC00YTE5LTg2MjQtNzQ2Y2I2MzhiNDg4In0.CNDHxP4gpo2FeHn3Fm-JABOorefcf6syW7qeqBR6AOA
```

 Status | Message
------- | -----------
200 OK

**Request**

```
GET /api/task HTTP/1.1
Host: 127.0.0.1:5231
Authorization: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjMwNzY4MzgsImlhdCI6MTUzMTU0MDgzOCwic3ViIjoiNTZjZmJmYjEtMmJkNC00YTE5LTg2MjQtNzQ2Y2I2MzhiNDg4In0.CNDHxP4gpo2FeHn3Fm-JABOorefcf6syW7qeqBR6AOA
Cache-Control: no-cache
```

**Response**

```
accept: application/json
access-control-allow-headers: X-HTTP-Method-Override, Content-Type, Authorization
access-control-allow-methods: GET,PUT,POST,DELETE
access-control-allow-origin: *
content-length: 99
content-type: application/json; charset=UTF-8
date: Wed, 22 Aug 2018 00:12:05 GMT
server: Werkzeug/0.13 Python/3.6.5

{
    "queues": {
        "queue_id-1": [
            {
                "task_id": "mytask",
                "headers": {
                    "Authorization": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjMwNzY4MzgsImlhdCI6MTUzMTU0MDgzOCwic3ViIjoiNTZjZmJmYjEtMmJkNC00YTE5LTg2MjQtNzQ2Y2I2MzhiNDg4In0.CNDHxP4gpo2FeHn3Fm-JABOorefcf6syW7qeqBR6AOA"
                },
                "api": "/api/crawl/scan",
                "method": "post",
                "data": {},
                "priority": "1"
            }
        ],
        "queue_id-2": [],
        "my-queue": []
    },
    "triggers": {
        "mytrigger": {
            "task": null
        },
        "mytrigger-2": {
            "task": null
        }
    }
}
```
# Obtener todas las tarea de una cola

**Request**

 Method | Request URI | Description
------- | ----------- | ------------
GET     | /api/task/queue/<queue-id> | Obtengo todas las tareas de una cola

**Headers**

 Method | Type | Description
------- | ----------- | ------------
Authorization | string | token

**Test token**

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjMwNzY4MzgsImlhdCI6MTUzMTU0MDgzOCwic3ViIjoiNTZjZmJmYjEtMmJkNC00YTE5LTg2MjQtNzQ2Y2I2MzhiNDg4In0.CNDHxP4gpo2FeHn3Fm-JABOorefcf6syW7qeqBR6AOA
```

 Status | Message
------- | -----------
200 OK

**Request**

```
GET /api/task/queue/queue_id-1 HTTP/1.1
Host: 127.0.0.1:5231
Authorization: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjMwNzY4MzgsImlhdCI6MTUzMTU0MDgzOCwic3ViIjoiNTZjZmJmYjEtMmJkNC00YTE5LTg2MjQtNzQ2Y2I2MzhiNDg4In0.CNDHxP4gpo2FeHn3Fm-JABOorefcf6syW7qeqBR6AOA
Cache-Control: no-cache
```

**Response**

```
accept: application/json
access-control-allow-headers: X-HTTP-Method-Override, Content-Type, Authorization
access-control-allow-methods: GET,PUT,POST,DELETE
access-control-allow-origin: *
content-length: 803
content-type: application/json; charset=UTF-8
date: Tue, 21 Aug 2018 23:59:03 GMT
server: Werkzeug/0.13 Python/3.6.5

[
    {
        "task_id": "mytask",
        "headers": {
            "Authorization": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjMwNzY4MzgsImlhdCI6MTUzMTU0MDgzOCwic3ViIjoiNTZjZmJmYjEtMmJkNC00YTE5LTg2MjQtNzQ2Y2I2MzhiNDg4In0.CNDHxP4gpo2FeHn3Fm-JABOorefcf6syW7qeqBR6AOA"
        },
        "api": "/api/crawl/scan",
        "method": "post",
        "data": {},
        "priority": "1"
    },
    {
        "task_id": "mytask-dos",
        "headers": {
            "Authorization": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjMwNzY4MzgsImlhdCI6MTUzMTU0MDgzOCwic3ViIjoiNTZjZmJmYjEtMmJkNC00YTE5LTg2MjQtNzQ2Y2I2MzhiNDg4In0.CNDHxP4gpo2FeHn3Fm-JABOorefcf6syW7qeqBR6AOA"
        },
        "api": "/api/crawl/scan",
        "method": "post",
        "data": {},
        "priority": "1"
    }
]
```

Scheduler task manager
======================

# Eliminar una tarea programada

**Request**

 Method | Request URI | Description
------- | ----------- | ------------
DELETE | /api/scheduler/&lt;scheduler-id&gt; | Elimina una tarea programada

**Headers**

 Method | Type | Description
------- | ----------- | ------------
Authorization | string | token

**Test token**
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjMwNzY4MzgsImlhdCI6MTUzMTU0MDgzOCwic3ViIjoiNTZjZmJmYjEtMmJkNC00YTE5LTg2MjQtNzQ2Y2I2MzhiNDg4In0.CNDHxP4gpo2FeHn3Fm-JABOorefcf6syW7qeqBR6AOA
```

 Status | Message | Description
------- | ----------- | -----------
201     | OK          | Successfully remove scheduler task
400     | BAD REQUEST | No job by the id of <scheduler-id> was found

**Request**

```
DELETE /api/scheduler/myscheduler HTTP/1.1
Host: 127.0.0.1:5231
Authorization: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjMwNzY4MzgsImlhdCI6MTUzMTU0MDgzOCwic3ViIjoiNTZjZmJmYjEtMmJkNC00YTE5LTg2MjQtNzQ2Y2I2MzhiNDg4In0.CNDHxP4gpo2FeHn3Fm-JABOorefcf6syW7qeqBR6AOA
Cache-Control: no-cache
```

**Response**

```
accept: application/json
access-control-allow-headers: X-HTTP-Method-Override, Content-Type, Authorization
access-control-allow-methods: GET,PUT,POST,DELETE
access-control-allow-origin: *
content-length: 56
content-type: application/json; charset=UTF-8
date: Wed, 22 Aug 2018 01:26:20 GMT
server: Werkzeug/0.13 Python/3.6.5

{
    "message": "Successfully remove scheduler task"
}
```

# Loader Api Rest
# Loads multiple api rest

**Request**

 Method | Request URI | Description
------- | ----------- | ------------
POST     | /loader | Loader apirest

**Params**

```
Don't required Params
```

**Headers**

Name | Required | Value | Description
---- | -------- | -------- | --------
Content-Type | Required | application/json | Sen data with json
Accept | Optional | image/jpeg | Muestra la ultima imagen del último loader

**Body**

```json
{
	"loaders":[
		{
			"url": "http://127.0.0.1:5000/join",
			"method": "post",
			"data":{
				"files":[
					[
						"mi-foto.jpeg",
						"...",
						"image/jpeg"
					],
					[
						"name.png",
						"...",
						"image/png",
						{"x":-10, "y":-10, "reverse":1}
					]
				]
			}
		},
		{
			"url": "http://127.0.0.1:5000/optimize",
			"method": "post",
			"params": {
				"quality":60,
				"optimize":1,
				"subsampling":1,
				"progressive":1
			}
		},
		{
			"url": "http://127.0.0.1:5000/resize",
			"method": "post",
			"params": {
				"width":300,
				"heigth":200
			}
		}
	]
}
```

## Request

```
POST /loader HTTP/1.1
Host: 127.0.0.1:5000
Content-Type: application/json
Accept: image/jpeg
Cache-Control: no-cache
Postman-Token: 7d2eadce-d668-4dc7-88d9-879eef04056f

{
    "loaders":[
        {
            "url": "/join",
            "method": "post",
            "data":{
				"files":[
					[
						"mi-foto.jpeg",
						"base64Image",
						"image/jpeg"
					],
					[
						"name.png",
						"base64Image",
						"image/png",
						{"x":-10, "y":-10, "reverse":1}
					]
				]
			}
        },
        {
        	"url": "/optimize",
            "method": "post",
            "params": {
		        "quality":60,
		        "optimize":1,
		        "subsampling":1,
		        "progressive":1
            }
        },
        {
        	"url": "/resize",
            "method": "post",
            "params": {
            	"width":300,
		        "heigth":200
            }
        }
    ]
}
```

## Response

```
Content-Length: 13772
Content-Type: application/json
Date: Fri, 24 Aug 2018 12:24:17 GMT
Server: Werkzeug/0.14.1 Python/3.6.6

{
    "data": {
        "files": [
            [
                "mi-foto.jpeg",
                "base64Image",
                "image/jpeg"
            ]
        ]
    }
}
```
