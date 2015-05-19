## User

ユーザーを表すモデル

- 構造
- API
	- POST /users ユーザーを作成
	- **PATCH /users/:name** ユーザー情報の更新
	- **DELETE /users/:name** ユーザーの削除

**※太字は認証が必要なAPI**

## 構造

```
{
	"id": 12345678,
	"created", "2015-5-15 18:10",
	"updated", "2015-5-15 18:10",
	"name": "kikurage",
	"email": "kikurage@sample.com", // 認証に使う
	"password": "kikurage_password" // 認証に使う
}
```

## API

### POST /users

ユーザーを作成

#### リクエスト

- URL

```
POST /users
```

#### レスポンス

- 成功時
	- body
	
	```
	{
		"status": "OK",
		"result": <% User %>
	}
	```

- パラメータ不足時
	- body
	
	```
	{
		"status": "NG",
		"result": {
		    "code": 3,
			"type":"id is missng.",
			"detail": {}
		}
	}
	```
- name/emailが既に使われている時
	- body
	
	```
	{
		"stauts": "NG",
		"result": {
			"code": 4,
			"type": "ALREADY_CREATED",
			"detail": {
				"email": "kikurage@sample.com",
				"name": "kikurage"
			}
		}
	}
	```



### PATCH /users/:name

ユーザー情報の更新

`private`

#### リクエスト

- URL

```
patch /users/kikurage
```

#### レスポンス

- 成功時
	- body
	
	```
	{
		"status": "OK",
		"result": <% User %>		
	}
	```

- 認証失敗時
	- body
	
	```
	{
		"status": "NG",
		"result": {
			"code": 2,
			"type":"PERMISSION_DENIED",
			"detail": {}
		}
	}
	```


### DELETE /users/:name

ユーザーの削除

`private`

#### リクエスト

- URL

```
delete /users/kikurage
```

#### レスポンス

- 成功時

```
{
	"status": "OK",
	"result": {}
}
```




