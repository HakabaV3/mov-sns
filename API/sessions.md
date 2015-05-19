## Sessions

認証状態を表すモデル。

- 構造
- API
	- POST /sessions/email emailでの認証を行う 
	- **POST /sessions/refresh※** 認証済みユーザーの確認
	- **DELETE /sessions※** 認証情報を削除する

**※太字は認証が必要なAPI**

## 構造

```
{
	"id": 12345678,
	"created": "2015-5-15 18:10",
	"updated": "2015-5-15 18:10",
	"user": <% User %>, //認証されたユーザー
	"token": "19830817503872500801_1" //トークン
}
```

## API

### POST /sessions/email

メールアドレスでログイン

#### リクエスト

- URL

```
POST /sessions/email
```

- body

```
{
	"email": "kikurage@sample.com",
	"password": "kikurage_password"
}
```


#### レスポンス

- 成功時
	- body
	
	```
	{
		"status": "OK",
		"result": {
			<% Session %>
		}
	}
	```
	
- email or passwordが間違っている時
	- body
	
	```
	{
		"status": "NG",
		"result": {
			"code": 3,
			"type":"INVALID_PARAMETER",
			"detail": {
				"email": "kikurage@sample.com",
				"password": ""
			}
		}
	}
	```
- パラメータ不足時
	- body
	
	```
	{
		"status": "NG",
		"result": {
			"code": 3,
			"type": "email is missing.",
			"detail": {}
		}
	}
	```

	
### POST /sessions/refresh

`private`

トークンの更新
 
#### リクエスト

- URL

```
POST /sessions/refresh
```

#### レスポンス

- 成功時
	- body
	
	```
	{
		"status": "OK",
		"result": {
			<% Session %>
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

### DELETE /sessions

`private`

認証情報の削除

#### リクエスト

- URL

```
DELETE /sessions
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






