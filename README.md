# Java Docker 環境

Docker 上で Java 25（Eclipse Temurin JDK）を実行するための開発環境です。

## 必要なもの

- Docker
- Docker Compose

## ディレクトリ構成

```
java/
├── Dockerfile      # eclipse-temurin:25-jdk ベースのイメージ
├── compose.yaml    # ./src をコンテナの /app/src にマウント
├── README.md
└── src/
    └── Main.java   # サンプルプログラム
```

`src/` はホストとコンテナで共有されています。ホスト側のエディタで編集したコードを、そのままコンテナ内で実行できます。

## 使い方

### コンテナの起動

```bash
docker compose up -d --build
```

### 単一ファイルを直接実行

コンパイルせずにソースファイルをそのまま実行できます。

```bash
docker compose exec java java Main.java
```

### コンパイルしてから実行

```bash
docker compose exec java javac Main.java
docker compose exec java java Main
```

### コンテナ内のシェルに入る

```bash
docker compose exec java bash
```

シェル内では `/app/src` が作業ディレクトリです。

```bash
java Main.java
```

### コンテナの停止

```bash
docker compose down
```

## Java のバージョンを変更する

`Dockerfile` のベースイメージのタグを変更し、イメージを再ビルドしてください。

```dockerfile
FROM eclipse-temurin:21-jdk
```

```bash
docker compose up -d --build
```
