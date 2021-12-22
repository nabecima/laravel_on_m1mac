# Version
PHP 7.4.27<br>
nginx 1.20.2<br>
mysql 8.0.27

# Usage
1. 受講生から共有されたプロジェクトをlaravel_on_m1macディレクトリ配下に移動させる(.zipはNG)
1. 以下のコマンドで受講生のプロジェクトをbackendディレクトリ配下にコピー(node_modulesを除外)

    ```
    rsync -r ./アプリフォルダ名/. ./backend --exclude '/node_modules/'
    ```
1. docker-compose.ymlと同じ階層にある.envの`DB_NAME`をプロジェクトで使用するDB名にする。
2. コンテナをバックグラウンドで起動

    ```
    docker compose up -d
    ```

3. コンテナが起動しているか確認(STATUSがrunningになっていればOK)

    ```
    docker compose ps
    ```
4. backendディレクトリ内の.envを編集する
1. .envの内容を反映する

    ```
    docker compose exec app php artisan config:cache
    ```

1. パッケージをインストール

    ```
    docker compose exec app npm install
    ```

1. マイグレーションファイルを適用する

    ```
    docker compose exec app php artisan migrate
    ```

基本的には上記コマンドを入力すればプレビューできます。<br>
その他コマンドを入力する必要がある場合は`docker compose exec app`以降に実行したいコマンドを入れて実行してください