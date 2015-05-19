# Movies

- 構造
- API
	- **GET /groups/:group_name/movies** 動画の一覧の取得
	- **GET /groups/:group_name/movies/:movie_name** 動画の詳細を取得
	- **POST /groups/:group_name/movies** 動画の投稿
	- **PATCH /groups/:group_name/movies/:movie_name** 動画データの編集
	- **DELETE /groups/:group_name/movies/:movie_name** 動画の削除
	
**※太字のAPIは認証が必要**

## 構造

```
{
	"id": 12345678,
	"created": "2015-05-10 18:10",
	"updated": "2015-05-10 18:10",
	"name": "TsumamiGui",
	"description": "The TsumamiGui Movie.",
	"url": "http://sample.amazonaws.com/TsumamiGui",
	"group": <% Group %>,
	"user": <% User %>
}
```

## API

### GET /groups/:group_name/movies

`private`

動画の一覧の取得

#### リクエスト

- URL

```
GET /groups//movies
```

#### レスポンス

- 成功時
	- body
	
	```
	{
		"status": "OK",
		"result": {
			"movies": [ <% Movie %> ]
		}		
	}
	```
	
### GET /groups/:group_id/movies/:movie_name

`private`

動画の詳細を取得

#### リクエスト

- URL

```
GET /groups/Hakaba/movies/TsumamiGui
```

#### レスポンス

- 成功時
	- body
	
	```
	{
		"stauts": "OK",
		"result": {
			"movie": <% Movie %>
		}
	}
	```


### POST /groups/:group_name/movies

`private`

動画の投稿

#### リクエスト

- URL

```
POST /groups/Hakaba/movies
```

- body

```
{
	"name": "TsumamiGui",
	"description": "The TsumamiGui Movie.",
	"binary": 1583 2837 0817 0837 0187
			  3017 0247 1084 7104 0814
			  0182 7401 8274 0981 1938
}
```


#### レスポンス

- 成功時
	- body
	
	```
	{
		"status": "OK",
		"result": {
			"movie": <% Movie %>
		}
	}
	```

### PATCH /groups/:group_name/movies/:movie_name

`private`

動画データの編集

#### リクエスト

- URL

```
PATCH /groups/Hakaba/movies/TsumamiGui
```

- body

```
{
	"name": "TsumamiGui_updated",
	"description": "Updated The TsumamiGui Movie.",
	"binary": 1583 2837 0817 0837 0187
			  3017 0247 1084 7104 0814
			  0182 7401 8274 0981 1938
}
```

#### レスポンス

- 成功時
	- body
	
	```
	{
		"status": "OK",
		"result": {
			"movie": <% Movie %>
		}
	}
	```


### DELETE /groups/:group_name/movies/:movie_name

`private`

動画の削除

#### リクエスト

- URL

```
DELETE /groups/Hakaba/movies/TsumamiGui
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
