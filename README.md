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


[link1]:https://qiita.com/ucan-lab/items/90f74ce801618830e4fc
