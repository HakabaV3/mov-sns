## Groups

グループを表すモデル

- 構造
- API
	- GET /groups グループの一覧を取得
	- **GET /groups/:group_name** グループの詳細を取得
	- **POST /groups グループの作成**
	- **DELETE /groups/:group_name** グループの削除

**※太字は認証が必要なAPI**

## 構造

```
{
	"id": 12345678,
	"created": "2015-5-15 18:10",
	"updated": "2015-5-15 18:10",
	"name": "Hhakaba",
	"description": "This is a programming group.",
	"owner": <% User %>,
	"users": [ // 認証されたuserが参加していなければ空の配列
		<% User %>
	]
}
```

## API

### GET /groups

グループの一覧を取得

#### リクエスト

- URL

```
GET /groups
```

#### レスポンス

- 成功時
	- body
	
	```
	{
		"status": "OK",
		"result": {
			"groups": [ <% Group %> ]
		}
	}
	```

### GET /groups/:group_name

グループの詳細を取得

#### リクエスト

- URL

```
GET /groups/Hakaba
```

#### レスポンス

- 成功時（認証済みuserがgroupに参加している）
	- body
	
	```
	{
		"status": "OK",
		"result": {
			"id": 12345678.
			"created": "2015-05-10 18:10",
			"updated": "2015-05-10 18:10",
			"name": "Hakaba",
			"description": "This is a programming group.",
			"users": [ <% User %> ]
		}
	}
	```

- 成功時（認証していないor参加していない）
	- body
	
	```
	{
		"status": "OK",
		"result": {
			"id": 12345678.
			"created": "2015-05-10 18:10",
			"updated": "2015-05-10 18:10",
			"name": "Hakaba",
			"description": "This is a programming group.",
			"users": []
		}
	}
	```


### POST /groups

`private`

グループの作成

#### リクエスト

- URL

```
POST /groups
```

- body

```
{
	"group_name": "Hakaba"
}
```

#### レスポンス

- 成功時
	- body
	
	```
	{
		"status": "OK",
		"result": {
			<% Group %>
		}
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

- nameが既に使われている
	- body

	```
	{
		"stauts": "NG",
		"result": {
			"code": 4,
			"type": "ALREADY_CREATED",
			"detail": {
				"name": "Hakaba"
			}
		}
	}
	```

### DELETE /groups/:group_name

`private`

グループの削除

#### リクエスト

- URL

```
DELETE /groups/Hakaba
```

#### レスポンス

- 成功時
	- body
	
	```
	{
		"status": "OK",
		"result": {}
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

- 認証は成功しているが、オーナーではない
	- body
	
	```
	{
		"status": "NG",
		"result": {
			"code": 2,
			"type": "PERMISSION_DENIED",
			"detail": {
				"owner_name": "kikurage",
				"user_name": "stogu"
			}
		}
	}
	```












