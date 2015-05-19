## Invitations

- 構造
- API
	- GET /groups/:group_name/invitations グループへの招待一覧を取得
	- **GET /groups/:group_name/invitations/:user_name** 招待の詳細を取得する
	- **POST /groups/:group_name/invitations** 招待を作成する
	- **DELETE /groups/:group_name/invitations/:user_name** 招待を削除する
	
**※太字は認証が必要なAPI**

## 構造

```
{
	"id": 12345678,
	"created": "2015-05-18 18:10",
	"updated": "2015-05-18 18:10",
	"owner": <% User %>,
	"target": <% User %>,
	"group": <% Group %>
}
```

## API

### GET /groups/:group_name/invitations

グループへの招待一覧を取得

#### リクエスト

- URL

```
GET /groups/Hakaba/invitations 
```

#### レスポンス

- 成功時
	- body
	
	```
	{
		"status": "OK",
		"result": {
			"invitations": [ <% Invitation %> ]
		}
	}
	```
	
### GET /groups/:group_name/invitations/:user_name

`private`

招待の詳細を取得する。  
該当グループに参加しているユーザーが閲覧できる。

#### リクエスト

- URL

```
GET /groups/Hakaba/invitations/stogu
```

#### レスポンス

- 成功時
	- body
	
	```
	{
		"status": "OK",
		"result": {
			"invitation": <% Invitation %>
		}
	}
	```

- 招待が存在しない時
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

### POST /groups/:group_name/invitations

`private`

招待を作成する

#### リクエスト

- URL

```
POST /groups/Hakaba/invitations
```

- body

```
{
	"user_name": "stogu"
}
```

#### レスポンス

- 成功時
	- body
	
	```
	{
		"status": "OK",
		"result": {
			"invitation": <% Invitation %>
		}
	}
	```
	
- 既に招待が作成されている
	- body
	
	```
	{
		"status": "NG",
		"result": {
			"code": 4,
			"type": "ALREADT_CREATED",
			detail: {
				"user_name": "stogu",
				"group_name": "Hakaba"
			}
		}
	}
	```

### DELETE /groups/:group_name/invitations/:user_name

`private`

招待を削除する

#### リクエスト

- URL

```
DELETE /groups/Hakaba/invitations/stogu
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

