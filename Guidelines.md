# ScraperCloud.com REST API Guidelines

* Scapi
  * Crawl
    * [Task manager](#task-manager)
    * [Scheduler task manager](#scheduler-task-manager) 
  * [Loader Api Rest](#loader-api-rest)

Task manager
============

# Obtengo colas y triggers del usuario

**Request**

 Method | Request URI | Description
------- | ----------- | ------------
GET     | /api/task_manager | Obtengo la lista de las tareas

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
GET /api/task_manager HTTP/1.1
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

Scheduler task manager
======================

# Eliminar un proceso scan del segundo plano

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
DELETE /api/scheduler_task_manager/myscheduler HTTP/1.1
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
        	"url": "http://127.0.0.1:5000/join",
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
