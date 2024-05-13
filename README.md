
---

# FastAPI プロジェクトテンプレート
FastAPIのプロジェクトテンプレートです。プロジェクトに合わせて適宜変更してご利用ください。

## 使用技術

- **API サーバ**: Python 3.12 + FastAPI + Uvicorn  
- **パッケージ管理**: Poetry  
- **データベース**: PostgreSQL  
- **マイグレーション管理**: Alembic

## 環境構築手順

1. リポジトリをクローンします。
   ```bash
   git clone https://github.com/xxxxxxx/xxxxxxx
   ```
2. 必要なインストールとコンテナの立ち上げを行います。
   ```bash
   make init
   ```
3. Poetryのインストールにより仮想環境が作成されますが、インタープリタの読み込みが必要です。一度VSCodeをリロードしてください。
4. クローン時に表示される拡張機能のサジェストを確認し、必要な拡張機能をインストールしてください。

## データベース設定

本プロジェクトはデフォルトでPostgreSQLを使用しています。別のデータベースを使用する場合は、以下の手順でデータベース設定を編集してください：

1. **依存関係の追加**:
   - 使用するデータベースに応じたクライアントライブラリを追加してください。

2. **接続設定の変更**:
   - `.env`ファイルの`DATABASE_URL`を編集し、使用するデータベースに対応する接続情報を設定してください。

3. **データベース接続コードの修正**:
   - `src/settings/database.py`（または該当する設定ファイル）で、接続文字列やエンジン設定を変更してください。

## ライブラリのインストール方法

### `add-lib`コマンドを使用する方法

ライブラリを追加するには、以下のコマンドを実行します。

```bash
make add-lib ライブラリ名
```

例：
```bash
make add-lib requests
```
このコマンドにより、指定したライブラリがPoetryでインストールされ、その後Dockerイメージが再ビルドされます。

### `add-lib`コマンドを使用しない場合

Poetryでライブラリを追加します。
```bash
poetry add ライブラリ名
```
Dockerイメージを再ビルドします。
```bash
docker compose build app
```

## コードスタイルとフォーマッター
- フォーマッター: `ruff`を使用しています。
- コード規約: `ruff`に準拠していますが、一部追加の設定があります。詳細は`pyproject.toml`を確認してください。

## エンドポイントの実装について

このプロジェクトでは、機能単位でディレクトリをまとめる構成を採用しています。

```
api
 ├── sample
    ├── sample_router.py
    ├── sample_schema.py
    └── sample_service.py
```

### ファイル構成の説明

- **sample_router.py**:
  - 他のフレームワークで言うところのコントローラに該当します。URL設定、ヘッダーの検証、リクエストとレスポンスの検証を行います。このファイルに記載されたdocstringはSwagger画面に表示されるため、詳細に記載するようにしてください。

- **sample_schema.py**:
  - Pydanticを使用して、リクエストやレスポンスのデータ型を設定するファイルです。コード量が増えそうな場合は、`schemas`ディレクトリを作成し、その配下にファイルを配置してください。

- **sample_service.py**:
  - ビジネスロジックを処理するファイルです。コード量が増えそうな場合は、`services`ディレクトリを作成し、その配下にファイルを配置してください。

---
