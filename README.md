# laradock5

## 意気込み
- 2,30回練習する

## 参考
[Laravelの開発環境をLaradockを使って構築する][link1]

## 手順
1. 作業ディレクトリをcloneする
    ```
    cd ~/git
    git clone ...laradock5.git
    ```

1. 作業ディレクトリに移動する
    ```
    cd ~/git/laradock5
    ```

1. laradockをクローンする
    ```
    git clone https://github.com/laradock/laradock.git
    ```

1. laradockのenv-exampleを.envに複製する

1. laradockの.gitディレクトリを削除する

1. laradockの.gitignoreファイルから.envを消す

1. mysql/my.cnfの[mysqld]に`default-authentication-plugin=mysql_native_password`が無ければ追記する

1. .envのportを書き換える
    - NGINX_HOST_HTTP_PORT: 80 -> 20080
    - MYSQL_PORT: 3306 -> 23306
    - PMA_PORT: 8080 -> 28080

1. Dockerを起動する
    ```
    docker-compose up -d nginx mysql workspace phpmyadmin
    ```

1. workspaceコンテナに接続する。ユーザ指定が重要。コンテナ内で作られたファイルへの権限をhost側で得るため
    ```
    docker-compose exec --user=laradock workspace bash
    ```

1. workspaceコンテナ内でlaravel初期化する
    ```
    composer create-project laravel/laravel sampleapp --prefer-dist
    ```

1. **laradockの**.envを編集する
    - APP_CODE_PATH_HOST: ../ -> ../sampleapp/

1. **laradockの**.envを変更したのでdockerを再起動する
    ```
    # docker-compose restart では不可の模様
    docker-compose down
    docker-compose up -d nginx mysql workspace phpmyadmin
    ```

1. **laravelの**.gitignoreから.envを削除する

1. **laravelの**.envを編集する
    - 編集前
      ```
      DB_CONNECTION=mysql
      DB_HOST=127.0.0.1
      DB_PORT=3306
      DB_DATABASE=laravel
      DB_USERNAME=root
      DB_PASSWORD=
      ```

    - 編集後
      ```
      DB_CONNECTION=mysql
      DB_HOST=mysql
      DB_PORT=3306
      DB_DATABASE=default
      DB_USERNAME=default
      DB_PASSWORD=secret
      ```


[link1]:https://qiita.com/ucan-lab/items/90f74ce801618830e4fc
