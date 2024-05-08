# Enjigraph Markdown API
ウェブサイトをMarkdownとして取得できるAPIです。

↓ Enjigraph  
https://www.enjigraph.com/

## レスポンスデータ
下記情報をJSON形式で取得できます。  
・URL  
・Markdown  

## 利用方法
headerにAPI KEYを埋め込み、GETリクエストを送信するだけで簡単にデータを取得できます。

cURLを使った例:
```
curl -H 'X-ENJI-API-KEY : {API KEY}' https://api.enjigraph.com/v1/markdown?url=https://www.enjigraph.com
```

Pythonを使った例:
```
import requests

url = "https://api.enjigraph.com/v1/markdown"

headers = {
    'X-ENJI-API-KEY' : {API KEY}
}

params = {
    "url": "https://www.enjigraph.com"
}

response = requests.get(url, headers=headers, params=params)

if response.status_code == 200:
    json_data = response.json()
    print("成功:", json_data)
else:
    print("失敗:", response.status_code)
```

レスポンス例（成功）:
```
{
    status: "success",
    result: [
        {
           url: "https://www.enjigraph.com/",
	   markdown: "[![](/public/images/Logo.png)](/home)\n\n![](/public/images/lp_top_background.jpg)\n\nEnjigraph,"
        }
    ],
    monthlyLimit: 10000,
    monthlyRequestCount: 980
}
```

レスポンス例（エラー）:
```
{
    status: "error",
    code: MonthlyRequestLimit,
    message: Monthly request limit exceeded. Please upgrade your plan.
}
```

## エラーコード
- apiKeyMissing  
　API KEYがヘッダーに付与されていません。
- apiKeyInvalid  
　API KEYが正しくありません。
- MonthlyRequestLimit  
　月間リクエスト数がプラン上限を超えています。
- ScrapingError
  スクレイピング時に、エラーが発生しました。
