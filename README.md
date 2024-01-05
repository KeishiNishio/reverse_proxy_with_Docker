# Dockerによるリバースプロキシの実装

# プロジェクト概要

このプロジェクトでは、React (JavaScript) と Flask (Python) を使用して、シンプルな開発環境を構築します。Nginxをリバースプロキシとして使用し、ユーザーが`http://localhost`にアクセスすると、Reactで構築されたフロントエンドから「大阪」というボタンが表示されます。このボタンをクリックすると、Flaskで構築されたバックエンドから「USJが有名です」というレスポンスが返され、フロントエンドで表示されます。

[システム構成図](https://github.com/KeishiNishio/reverse_proxy_with_Docker/blob/main/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202024-01-06%202.46.59.png)


## 技術スタック

- フロントエンド: React (JavaScript)
- バックエンド: Flask (Python)
- リバースプロキシ: Nginx
- コンテナオーケストレーション: Docker Compose

## 機能

- ローカルホスト上でのフロントエンドとバックエンドの連携
- ボタンクリックによるバックエンドからのレスポンスの表示
- Nginxを使用したリバースプロキシの設定

## ディレクトリ構成

- `backend/`: Flaskアプリケーションを含むディレクトリ。Dockerfile、[app.py](http://app.py/)、requirements.txtを含む。
- `frontend/`: Reactアプリケーションを含むディレクトリ。buildフォルダ、node_modules、public/index.html、srcフォルダ、Dockerfile、package-lock.json、package.jsonを含む。
- `nginx/`: Nginxの設定ファイルdefault.confを含むディレクトリ。
- `docker-compose.yml`: Docker Composeを使ったサービスの起動設定。

## セットアップ方法

1. Dockerネットワークの作成:
    
    ```bash
    docker network create nginx-network
    
    ```
    
2. フロントエンドの依存関係のインストール等
    
    ```bash
    cd frontend
    npm install
    export NODE_OPTIONS=--openssl-legacy-provider
    npm run build
    cd ..
    
    ```
    
3. Docker Composeを使用してサービスのビルドと起動:
    
    ```bash
    docker-compose build --no-cache
    docker-compose up -d
    
    ```
    

## 他の便利なコマンド

- Dockerキャッシュの削除、ネットワーク確認、コンテナ状況確認などのコマンド
1. システム全体のDockerキャッシュを削除

```bash
docker system prune --all --force
```

1. 設定したネットワークにコンテナが所属しているか確認

```bash
docker network inspect nginx-network
```

1. コンテナの状況確認

```bash
docker ps -a
```

1. 存在する全てのコンテナを停止

```bash
docker stop $(docker ps -aq) || true
```

1. 存在する全てのコンテナを削除

```bash
docker rm -f $(docker ps -aq) || true
```

## 参考文献

[docker+react+python+fastapiで簡単な開発環境をリバースプロキシを使用して構築する](https://cloudsmith.co.jp/blog/virtualhost/docker/2022/12/2241971.html)
