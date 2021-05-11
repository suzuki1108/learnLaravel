# 環境構築手順

※Docekrのappコンテナに入る際の wimpty は Windows から gitbash で入る時のみつける。
（macでは不要）

## コンテナを立ち上げる
```
# Dockerイメージを作成
$ docker-compose build

# Dockerを起動
# -d でバックグランド起動
$ docker-compose up -d

# 起動しているコンテナが表示される
$ docker ps
```

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
