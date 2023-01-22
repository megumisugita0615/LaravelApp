# BlogApp
ブログアプリのリポジトリです。

## 環境構築・動作確認

リポジトリをクローン

`https`
```
git clone https://github.com/megumisugita0615/BlogApp.git
```

`ssh`
```
git clone git@github.com:megumisugita0615/BlogApp.git
```

ディレクトリを移動
```
cd BlogApp/App 
```

.envを作成
```
cp .env.example .env
```

.envの内容を書き換え
```
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=blogapp
DB_USERNAME=sail
DB_PASSWORD=password
```

composer, laravelをインストール
```
make install
```
うまくいかない場合はターミナルに貼り付け・実行
```
docker run --rm \
	-u "$(id -u):$(id -g)" \
	-v "$(pwd):/var/www/html" \
	-w /var/www/html \
	laravelsail/php81-composer:latest \
	composer install --ignore-platform-reqs
```

Laravelの設定開始
```
make build
```

※マイグレーション・シーディングがうまくいかない場合
```
composer dump-autoload
make cache
make dbfresh
make db seed
```

`npm run dev`まで完了したら[http://localhost](http://localhost)にアクセス
<img width="1440" alt="スクリーンショット 2022-12-05 22 33 20" src="https://user-images.githubusercontent.com/106021148/205650001-4d2df7ce-7a39-45a7-bb3b-5672f3089002.png">


## その他
- 特になし
