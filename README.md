# docker-lamp2


## ディレクトリ解説
```
docker-lamp2
├── html .............. ここにレビュー対象のリポジトリをcloneする
│   └── index.php ..... phpinfo();
├── mysql5.7
│   ├── mysql ......... 起動すると作られる。データ永続化用
│   ├── mysqlvolume ... mysqlコンテナにマウントされる。ホストとのフィアル受け渡し用
│   └── my.cnf
├── php7.2
│   ├── Dockerfile
│   └── php.ini
├── .gitignore
├── docker-compose.yml
└── README.md
```

## 環境構築手順
### レビュー対象ブランチ(https://github.com/takazumik/yokuwakaru/tree/feature/twitter)
1. docker-lamp2をcloneする。以降cloneしたリポジトリ内でCUI操作する
    ```
    git clone https://github.com/Yuzunoha/docker-lamp2.git
    cd docker-lamp2
    ```
1. 起動する
    ```
    docker-compose up -d
    ```
1. htmlにレビュー対象ブランチをcloneする
    ```
    cd html
    git clone https://github.com/takazumik/yokuwakaru/tree/feature/twitter
    cd yokuwakaru
    git checkout feature/twitter
    ```
1. phpmyadminでレビュー対象のsqlをインポートする。
    - ブラウザで `localhost:10040` にアクセスする
    - yokuwakaru/mini_bbs.sqlをインポートする
1. レビュー対象のDB接続情報をfixする
    - yokuwakaru/dbconnect.php を適宜編集する
      `host=localhost` -> `host=mysql`
1. 環境構築完了
    - ブラウザで `localhost:10080/yokuwakaru` にアクセスする


## 参考
- [docker-compose で PHP7.2 + Apache + MySQL + phpMyAdmin 環境を構築][link1]
- [Docker Composeを使ってLAMP環境を構築する：前編][link2]


[link1]:https://qiita.com/naente_dev/items/d259ea84c172deeff7d8
[link2]:https://qiita.com/rockinruuula1227/items/83f3f1406f339083ef3f
