# ScraperCloud.com REST API Guidelines

* Scapi
  * [Loader Api Rest](#loader-api-rest)

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

##Request

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

##Response

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
