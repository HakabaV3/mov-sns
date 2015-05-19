## Join

- 構造
- API
	- GET /groups/:group_name/join グループ参加者一覧を取得
	- **POST /groups/:group_name/joins/:user_name** グループに参加する
	- **DELETE /groups/:group_name/joins/:user_name** グループから退会する

**※太字は認証が必要なAPI**

## 構造

```
{
	"id": 12345678,
	"created": "2015-5-12 18:10",
	"updated": "2015-5-12 18:10",
	"user": <% User %>,
	"group": <% Group %>
}
```

## API

### GET /groups/:group_name/join

グループ参加者一覧を取得

#### リクエスト

- URL

```
GET /gruops/Hakaba/join
```

#### レスポンス

- 成功時
	- body
	
	```
	{
		"status": "OK",
		"result": {
			"join": [<% User %>]
		}
	}
	```
	
- グループに参加しているユーザーがいない
	- body
	
	```
	{
		"stauts": "NG",
		"result": {
			"code": 4,
			"type": "NOT_FOUND",
			"detail": {
				"group_name": "Hakaba"
			}
		}
	}
	```
	
### POST /groups/:group_name/join/:user_name

`private`

グループに参加する

#### リクエスト

- URL

```
POST /groups/Hakaba/join/stogu
```

#### レスポンス

- 成功時
	- body
	
	```
	{
		"status": "OK",
		"result": {
			"join": [<% User %>]
		}
	}
	```

- 認証失敗時
	- body
	
	```
	{
		"status": "NG",
		"result": {
			"code": 4,
			"type":"PERMISSION_DENIED",
			"detail": {}
		}
	}
	```

- 招待されていない時
	- body
	
	```
	{
		"status": "NG",
		"result": {
			"code": 4,
			"type": "NOT_FOUND",
			"detail": {
				"group_name": "Hakaba",
				"user_name": "stogu"
			}
		}
	}
	```

- 既に参加している時
	- body
	
	```
	{
		"status": "NG",
		"result": {
			"code": 4,
			"type": "ALREADY_CREATED",
			"detail": {
				"group_name": "Hakaba",
				"user_name": "stogu"
			}
		}
	}
	```

### DELETE /groups/:group_name/join/:user_name

`private`

グループから退会する

#### リクエスト

- URL

```
DELETE /groups/Hakaba/join/stogu
```

#### レスポンス

- 成功時
	- body
	
	```
	{
		"stauts": "OK",
		"result": {}
	}
	```





