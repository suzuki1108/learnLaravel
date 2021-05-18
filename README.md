# 環境構築手順(初回環境構築時)

※Docekrのappコンテナに入る際の wimpty は Windows から gitbash で入る時のみつける。
（macでは不要）

① .env.example を .env にファイル名変更
② 上記ファイルのDB接続情報を、docker-compose.yml記載のDB接続情報に書き換える
   ローカル環境では以下情報を設定する。
```
DB_CONNECTION=mysql
DB_HOST=laravel_db
DB_PORT=3306
DB_DATABASE=laravel_db
DB_USERNAME=laravel_user
DB_PASSWORD=laravel_pass
```
③ 以下のコマンドを実行する

```
# Dockerイメージを作成
$ docker-compose build

# Dockerを起動
# -d でバックグランド起動
$ docker-compose up -d

# 起動しているコンテナが表示される
$ docker ps

# appコンテナに入る
$ winpty docker-compose exec app bash

# Laravelプロジェクト移動
$ cd laravel

# composerをインストールする
$ composer install

# ストレージの権限変更
$ chmod 777 -R storage/

$ php artisan key:generate

# マイグレーション実行
$ php artisan migrate

```

④ http://127.0.0.1:80/login にアクセス
   Loginページにアクセスできれば環境構築完了


※以下は備忘録

## Laravelプロジェクト作成
```
# appコンテナに入る
$ winpty docker-compose exec app bash

# Laravelプロジェクト作成
$ composer create-project --prefer-dist laravel/laravel laravel "6.18.*"

# Laravelプロジェクト移動
$ cd laravel

# ストレージの権限変更
$ chmod 777 -R storage/

$ php artisan key:generate
```

## Reactと認証機能の導入
```
# appコンテナに入る
$ winpty docker-compose exec app bash

# laravelプロジェクトに移動
$ cd laravel

# uiライブラリインストール
$ composer require laravel/ui:^1.0 --dev

# ログイン機能＆テーブル作成
$ php artisan ui react --auth
```


## マイグレーション実行
```
# appコンテナに入る
$ winpty docker-compose exec app bash

# laravelプロジェクトに移動
$ cd laravel

# マイグレーション実行
$ php artisan migrate

```
