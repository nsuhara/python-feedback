# FlaskでRESTful Webサービスを作成する

- [FlaskでRESTful Webサービスを作成する](#flask%e3%81%a7restful-web%e3%82%b5%e3%83%bc%e3%83%93%e3%82%b9%e3%82%92%e4%bd%9c%e6%88%90%e3%81%99%e3%82%8b)
  - [はじめに](#%e3%81%af%e3%81%98%e3%82%81%e3%81%ab)
    - [目的](#%e7%9b%ae%e7%9a%84)
    - [実行環境](#%e5%ae%9f%e8%a1%8c%e7%92%b0%e5%a2%83)
    - [ソースコード](#%e3%82%bd%e3%83%bc%e3%82%b9%e3%82%b3%e3%83%bc%e3%83%89)
    - [関連する記事](#%e9%96%a2%e9%80%a3%e3%81%99%e3%82%8b%e8%a8%98%e4%ba%8b)
  - [Feedback REST API](#feedback-rest-api)
  - [0. 開発環境の構成](#0-%e9%96%8b%e7%99%ba%e7%92%b0%e5%a2%83%e3%81%ae%e6%a7%8b%e6%88%90)
  - [1. 開発環境の設定](#1-%e9%96%8b%e7%99%ba%e7%92%b0%e5%a2%83%e3%81%ae%e8%a8%ad%e5%ae%9a)
    - [仮装環境を作成する](#%e4%bb%ae%e8%a3%85%e7%92%b0%e5%a2%83%e3%82%92%e4%bd%9c%e6%88%90%e3%81%99%e3%82%8b)
    - [仮装環境を設定する](#%e4%bb%ae%e8%a3%85%e7%92%b0%e5%a2%83%e3%82%92%e8%a8%ad%e5%ae%9a%e3%81%99%e3%82%8b)
    - [環境変数を設定する](#%e7%92%b0%e5%a2%83%e5%a4%89%e6%95%b0%e3%82%92%e8%a8%ad%e5%ae%9a%e3%81%99%e3%82%8b)
    - [Visual Studio Code - 仮装環境を設定する](#visual-studio-code---%e4%bb%ae%e8%a3%85%e7%92%b0%e5%a2%83%e3%82%92%e8%a8%ad%e5%ae%9a%e3%81%99%e3%82%8b)
    - [Visual Studio Code - PYTHONPATHを設定する](#visual-studio-code---pythonpath%e3%82%92%e8%a8%ad%e5%ae%9a%e3%81%99%e3%82%8b)
  - [2. ローカル/本番環境の設定](#2-%e3%83%ad%e3%83%bc%e3%82%ab%e3%83%ab%e6%9c%ac%e7%95%aa%e7%92%b0%e5%a2%83%e3%81%ae%e8%a8%ad%e5%ae%9a)
    - [ローカル環境の設定値を定義する](#%e3%83%ad%e3%83%bc%e3%82%ab%e3%83%ab%e7%92%b0%e5%a2%83%e3%81%ae%e8%a8%ad%e5%ae%9a%e5%80%a4%e3%82%92%e5%ae%9a%e7%be%a9%e3%81%99%e3%82%8b)
    - [本番環境の設定値を定義する](#%e6%9c%ac%e7%95%aa%e7%92%b0%e5%a2%83%e3%81%ae%e8%a8%ad%e5%ae%9a%e5%80%a4%e3%82%92%e5%ae%9a%e7%be%a9%e3%81%99%e3%82%8b)
    - [Flaskから環境設定を読み込む](#flask%e3%81%8b%e3%82%89%e7%92%b0%e5%a2%83%e8%a8%ad%e5%ae%9a%e3%82%92%e8%aa%ad%e3%81%bf%e8%be%bc%e3%82%80)
  - [3. 静的コード解析ツールの設定](#3-%e9%9d%99%e7%9a%84%e3%82%b3%e3%83%bc%e3%83%89%e8%a7%a3%e6%9e%90%e3%83%84%e3%83%bc%e3%83%ab%e3%81%ae%e8%a8%ad%e5%ae%9a)
    - [ツールをインストールする](#%e3%83%84%e3%83%bc%e3%83%ab%e3%82%92%e3%82%a4%e3%83%b3%e3%82%b9%e3%83%88%e3%83%bc%e3%83%ab%e3%81%99%e3%82%8b)
    - [ツールを設定する](#%e3%83%84%e3%83%bc%e3%83%ab%e3%82%92%e8%a8%ad%e5%ae%9a%e3%81%99%e3%82%8b)
    - [ツールを実行する](#%e3%83%84%e3%83%bc%e3%83%ab%e3%82%92%e5%ae%9f%e8%a1%8c%e3%81%99%e3%82%8b)
  - [4. パッケージの管理](#4-%e3%83%91%e3%83%83%e3%82%b1%e3%83%bc%e3%82%b8%e3%81%ae%e7%ae%a1%e7%90%86)
    - [個別でインストールする](#%e5%80%8b%e5%88%a5%e3%81%a7%e3%82%a4%e3%83%b3%e3%82%b9%e3%83%88%e3%83%bc%e3%83%ab%e3%81%99%e3%82%8b)
    - [パッケージリスト(requirements)を作成する](#%e3%83%91%e3%83%83%e3%82%b1%e3%83%bc%e3%82%b8%e3%83%aa%e3%82%b9%e3%83%88requirements%e3%82%92%e4%bd%9c%e6%88%90%e3%81%99%e3%82%8b)
    - [一括でインストールする](#%e4%b8%80%e6%8b%ac%e3%81%a7%e3%82%a4%e3%83%b3%e3%82%b9%e3%83%88%e3%83%bc%e3%83%ab%e3%81%99%e3%82%8b)
    - [個別でアンインストールする](#%e5%80%8b%e5%88%a5%e3%81%a7%e3%82%a2%e3%83%b3%e3%82%a4%e3%83%b3%e3%82%b9%e3%83%88%e3%83%bc%e3%83%ab%e3%81%99%e3%82%8b)
    - [一括でアンインストールする](#%e4%b8%80%e6%8b%ac%e3%81%a7%e3%82%a2%e3%83%b3%e3%82%a4%e3%83%b3%e3%82%b9%e3%83%88%e3%83%bc%e3%83%ab%e3%81%99%e3%82%8b)
  - [5. MTV(MVC)モデルの開発](#5-mtvmvc%e3%83%a2%e3%83%87%e3%83%ab%e3%81%ae%e9%96%8b%e7%99%ba)
    - [モデルの概要](#%e3%83%a2%e3%83%87%e3%83%ab%e3%81%ae%e6%a6%82%e8%a6%81)
    - [一般モデルとFlask/Djangoモデルの対比と特徴](#%e4%b8%80%e8%88%ac%e3%83%a2%e3%83%87%e3%83%ab%e3%81%a8flaskdjango%e3%83%a2%e3%83%87%e3%83%ab%e3%81%ae%e5%af%be%e6%af%94%e3%81%a8%e7%89%b9%e5%be%b4)
    - [M:Modelを作成する](#mmodel%e3%82%92%e4%bd%9c%e6%88%90%e3%81%99%e3%82%8b)
    - [T:Templateを作成する](#ttemplate%e3%82%92%e4%bd%9c%e6%88%90%e3%81%99%e3%82%8b)
    - [V:Viewを作成する](#vview%e3%82%92%e4%bd%9c%e6%88%90%e3%81%99%e3%82%8b)
    - [共通処理を作成する](#%e5%85%b1%e9%80%9a%e5%87%a6%e7%90%86%e3%82%92%e4%bd%9c%e6%88%90%e3%81%99%e3%82%8b)
    - [Flaskの起動処理を作成する](#flask%e3%81%ae%e8%b5%b7%e5%8b%95%e5%87%a6%e7%90%86%e3%82%92%e4%bd%9c%e6%88%90%e3%81%99%e3%82%8b)
  - [6. DBのマイグレーション](#6-db%e3%81%ae%e3%83%9e%e3%82%a4%e3%82%b0%e3%83%ac%e3%83%bc%e3%82%b7%e3%83%a7%e3%83%b3)
    - [Flask-Migrateを使ってマイグレーションする](#flask-migrate%e3%82%92%e4%bd%bf%e3%81%a3%e3%81%a6%e3%83%9e%e3%82%a4%e3%82%b0%e3%83%ac%e3%83%bc%e3%82%b7%e3%83%a7%e3%83%b3%e3%81%99%e3%82%8b)
    - [Flask-Migrateを使わずにマイグレーションする](#flask-migrate%e3%82%92%e4%bd%bf%e3%82%8f%e3%81%9a%e3%81%ab%e3%83%9e%e3%82%a4%e3%82%b0%e3%83%ac%e3%83%bc%e3%82%b7%e3%83%a7%e3%83%b3%e3%81%99%e3%82%8b)
  - [7. Flaskの起動](#7-flask%e3%81%ae%e8%b5%b7%e5%8b%95)
  - [8. クラアント側の処理(サンプル)](#8-%e3%82%af%e3%83%a9%e3%82%a2%e3%83%b3%e3%83%88%e5%81%b4%e3%81%ae%e5%87%a6%e7%90%86%e3%82%b5%e3%83%b3%e3%83%97%e3%83%ab)
    - [レコードを全件取得する](#%e3%83%ac%e3%82%b3%e3%83%bc%e3%83%89%e3%82%92%e5%85%a8%e4%bb%b6%e5%8f%96%e5%be%97%e3%81%99%e3%82%8b)
    - [レコードを1件取得する](#%e3%83%ac%e3%82%b3%e3%83%bc%e3%83%89%e3%82%921%e4%bb%b6%e5%8f%96%e5%be%97%e3%81%99%e3%82%8b)
    - [レコードを作成する](#%e3%83%ac%e3%82%b3%e3%83%bc%e3%83%89%e3%82%92%e4%bd%9c%e6%88%90%e3%81%99%e3%82%8b)
    - [レコードを更新する](#%e3%83%ac%e3%82%b3%e3%83%bc%e3%83%89%e3%82%92%e6%9b%b4%e6%96%b0%e3%81%99%e3%82%8b)
    - [レコードを削除する](#%e3%83%ac%e3%82%b3%e3%83%bc%e3%83%89%e3%82%92%e5%89%8a%e9%99%a4%e3%81%99%e3%82%8b)

## はじめに

Webサービス(Feedback)を用いて各種手順をご紹介します。

`Mac環境の記事ですが、Windows環境も同じ手順になります。環境依存の部分は読み替えてお試しください。`

### 目的

この記事を最後まで読むと、次のことができるようになります。

| No.  | 概要                         | キーワード                  |
| :--- | :--------------------------- | :-------------------------- |
| 1    | 開発環境の設定               | 環境変数                    |
| 2    | ローカル/本番環境の設定      | instance_relative_config    |
| 3    | 静的コード解析ツールの設定   | pylint                      |
| 4    | パッケージの管理             | pip                         |
| 5    | MTV(MVC)モデルの開発         | Flask-SQLAlchemy, Blueprint |
| 6    | DBのマイグレーション         | flask, Flask-Migrate        |
| 7    | Flaskの起動                  | flask                       |
| 8    | クラアント側の処理(サンプル) | requests                    |

### 実行環境

| 環境             | Ver.    |
| :--------------- | :------ |
| macOS Catalina   | 10.15.2 |
| Python           | 3.7.3   |
| Flask-Migrate    | 2.5.2   |
| Flask-SQLAlchemy | 2.4.1   |
| Flask            | 1.1.1   |
| requests         | 2.22.0  |

### ソースコード

実際に実装内容やソースコードを追いながら読むとより理解が深まるかと思います。是非ご活用ください。

[GitHub](https://github.com/nsuhara/python-feedback.git)

### 関連する記事

- [Flask](http://flask.palletsprojects.com)
- [Flask-SQLAlchemy](https://flask-sqlalchemy.palletsprojects.com)
- [Flask-Migrate](https://flask-migrate.readthedocs.io)
- [Blueprint](https://flask.palletsprojects.com/en/1.0.x/blueprints/)
- [Pylint](http://pylint.pycqa.org/en/latest/)

## Feedback REST API

| Service     | Method | Endpoint                            | Example               |
| :---------- | :----- | :---------------------------------- | :-------------------- |
| Healthcheck | GET    | /feedback/healthcheck               | /feedback/healthcheck |
| Read All    | GET    | /feedback/records                   | /feedback/records     |
| Read One    | GET    | /feedback/records/<<int:record_id>> | /feedback/records/123 |
| Create      | POST   | /feedback/records                   | /feedback/records     |
| Update      | PUT    | /feedback/records/<<int:record_id>> | /feedback/records/123 |
| Delete      | DELETE | /feedback/records/<<int:record_id>> | /feedback/records/123 |

## 0. 開発環境の構成

すべてのコマンドラインは、`feedback-api`をカレントディレクトリとして実行します。

```tree.sh
feedback-api
├── .env
├── .flaskenv
├── .pylintrc
├── .venv
├── .vscode
├── README.md
├── app
│   ├── __init__.py
│   ├── client
│   │   ├── __init__.py
│   │   ├── create.py
│   │   ├── delete.py
│   │   ├── read_all.py
│   │   ├── read_one.py
│   │   └── update.py
│   ├── config.py
│   ├── feedback
│   │   ├── __init__.py
│   │   ├── common
│   │   │   ├── __init__.py
│   │   │   └── utility.py
│   │   ├── models
│   │   │   ├── __init__.py
│   │   │   └── feedback.py
│   │   ├── static
│   │   │   └── __init__.py
│   │   ├── templates
│   │   │   └── __init__.py
│   │   └── views
│   │       ├── __init__.py
│   │       └── feedback.py
│   ├── requirements.txt
│   ├── run.py
│   └── tests
│       └── __init__.py
├── instance
│   ├── config.py
│   └── db.sqlite3
└── migrations
```

## 1. 開発環境の設定

```tree.sh
feedback-api
├── .env
├── .flaskenv
├── .venv
├── .vscode
```

### 仮装環境を作成する

1. コマンドラインを実行する。

    ```procedure.sh
    ~$ python -m venv .venv
    ```

2. feedback-api配下に`.venv`フォルダが作成される。開発環境毎にパッケージ管理が可能となる。

### 仮装環境を設定する

1. コマンドラインを実行する。ターミナルに`(.venv)`と表示される。

    ```procedure.sh
    ~$ source .venv/bin/activate
    (.venv) ~$
    ```

2. 設定を解除する場合は`deactivate`を実行します。ターミナルから`(.venv)`が消える。

    ```procedure.sh
    (.venv) ~$ deactivate
    ~$
    ```

### 環境変数を設定する

1. コマンドラインを実行する。

    ```procedure.sh
    (.venv) ~$ export PYTHONPATH=app/
    (.venv) ~$ export FLASK_APP=app/run.py
    (.venv) ~$ export FLASK_ENV=development
    ```

2. or 上記コマンドラインを`.flaskenv`ファイルに記述して実行する。

    ```procedure.sh
    (.venv) ~$ source .flaskenv
    ```

### Visual Studio Code - 仮装環境を設定する

1. `command + shift + p`を同時に押下してコマンドパレットを表示する。

2. `Python: Select Interpreter`を選択する。

3. `.venv`のパスを選択する。feedback-api配下に`.vscode`フォルダが作成される。

### Visual Studio Code - PYTHONPATHを設定する

本設定がない場合は、ディレクトリパスの異なるimportが認識されない。

1. feedback-api配下に`.env`ファイルを作成して以下を記述する。

    ```procedure.sh
    PYTHONPATH=app/
    ```

2. Visual Studio Codeのウィンドウを再読み込みする。

## 2. ローカル/本番環境の設定

```tree.sh
feedback-api
├── app
│   ├── config.py
│   ├── run.py
├── instance
│   ├── config.py
```

### ローカル環境の設定値を定義する

1. feedback-api配下に`instance`フォルダを作成して、その配下に`config.py`を作成する。

    ```config.py
    """instance/config.py
    """

    import os

    DEBUG = True
    # SECRET_KEY is generated by os.urandom(24).
    SECRET_KEY = '\xf7\xf4\x9bb\xd7\xa8\xdb\xee\x9f\xe3\x98SR\xda\xb0@\xb7\x12\xa4uB\xda\xa3\x1b'
    STRIPE_API_KEY = ''

    SQLALCHEMY_DATABASE_URI = 'sqlite:///{db_path}/{db_name}'.format(**{
        'db_path': os.path.dirname(os.path.abspath(__file__)),
        'db_name': 'db.sqlite3'
    })
    SQLALCHEMY_TRACK_MODIFICATIONS = True
    SQLALCHEMY_ECHO = True
    ```

### 本番環境の設定値を定義する

1. feedback-apiのapp配下に`config.py`を作成する。

    ```config.py
    """app/config.py
    """

    import os

    DEBUG = False
    SECRET_KEY = os.getenv('SECRET_KEY', '')
    STRIPE_API_KEY = os.getenv('STRIPE_API_KEY', '')

    SQLALCHEMY_DATABASE_URI = os.getenv('SQLALCHEMY_DATABASE_URI', '')
    SQLALCHEMY_TRACK_MODIFICATIONS = False
    SQLALCHEMY_ECHO = False
    ```

1. 環境変数を設定する。

    ```procedure.sh
    (.venv) ~$ export SECRET_KEY=<本番設定値>
    (.venv) ~$ export STRIPE_API_KEY=<本番設定値>
    (.venv) ~$ export SQLALCHEMY_DATABASE_URI=<本番設定値>
    (.venv) ~$ export SQLALCHEMY_TRACK_MODIFICATIONS=<本番設定値>
    (.venv) ~$ export SQLALCHEMY_ECHO=<本番設定値>
    ```

### Flaskから環境設定を読み込む

1. Flask()の引数に`instance_relative_config`を設定する。

1. `True`を設定した場合は`instance/config.py`から設定値を読み込む。

1. `False`を設定した場合は`app/config.py`から設定値を読み込む。

    ```run.py
    """app/run.py
    """

    # ~省略~

    app = Flask(__name__, instance_relative_config=True)
    app.config.from_pyfile('config.py')

    # ~省略~
    ```

## 3. 静的コード解析ツールの設定

```tree.sh
feedback-api
├── .pylintrc
├── .venv
├── app
```

### ツールをインストールする

1. `pylint`をインストールする。`.venv`にインストールされる。

    ```procedure.sh
    (.venv) ~$ pip install pylint
    ```

### ツールを設定する

1. 設定ファイルを作成する。

    ```procedure.sh
    (.venv) ~$ pylint --generate-rcfile > .pylintrc
    ```

2. 不要なコードチェックを無効化する(サンプル)。

    1. 変数名の大文字チェックを無効化(invalid-name)
    2. ソースコードの類似チェックを無効化(too-few-public-methods)
    3. SQLAlchemyクラスの定義チェックを無効化(SQLAlchemy定義の参照で警告となるため)(SQLAlchemy)
    4. scoped_session関数の定義チェックを無効化(db.sessionの呼び出しで警告となるため)(scoped_session)

    ```.pylintrc
    # ~省略~

    disable=print-statement,

            # ~省略~

            invalid-name,               # add
            too-few-public-methods      # add

    # ~省略~

    ignored-classes=optparse.Values,thread._local,_thread._local,
                    SQLAlchemy,         # add
                    scoped_session      # add

    # ~省略~
    ```

### ツールを実行する

1. `pylint`を実行する。解析結果をみてソースコードを修正する。

    ```procedure.sh
    (.venv) ~$ pylint app/
    ```

## 4. パッケージの管理

```tree.sh
feedback-api
├── .venv
├── app
│   ├── requirements.txt
```

### 個別でインストールする

1. コマンドラインを実行する。

    ```procedure.sh
    (.venv) ~$ pip install Flask-Migrate
    (.venv) ~$ pip install Flask-SQLAlchemy
    (.venv) ~$ pip install Flask
    (.venv) ~$ pip install requests
    ```

### パッケージリスト(requirements)を作成する

1. コマンドラインを実行する。

    ```procedure.sh
    (.venv) ~$ pip freeze > app/requirements.txt
    ```

### 一括でインストールする

1. コマンドラインを実行する。

    ```procedure.sh
    (.venv) ~$ pip install -r app/requirements.txt
    ```

### 個別でアンインストールする

1. コマンドラインを実行する。

    ```procedure.sh
    (.venv) ~$ pip uninstall Flask-Migrate
    (.venv) ~$ pip uninstall Flask-SQLAlchemy
    (.venv) ~$ pip uninstall Flask
    (.venv) ~$ pip uninstall requests
    ```

### 一括でアンインストールする

1. コマンドラインを実行する。

    ```procedure.sh
    (.venv) ~$ pip uninstall -r app/requirements.txt
    ```

## 5. MTV(MVC)モデルの開発

```tree.sh
feedback-api
├── app
     ├── __init__.py
     ├── feedback
     │   ├── __init__.py
     │   ├── common
     │   │   ├── __init__.py
     │   │   └── utility.py
     │   ├── models
     │   │   ├── __init__.py
     │   │   └── feedback.py
     │   ├── static
     │   │   └── __init__.py
     │   ├── templates
     │   │   └── __init__.py
     │   └── views
     │       ├── __init__.py
     │       └── feedback.py
     ├── run.py
```

### モデルの概要

| 機能 | 意味       | 概要                                                     |
| :--- | :--------- | :------------------------------------------------------- |
| M    | Model      | アプリケーションデータ、ビジネスルール、ロジック、関数。 |
| V    | View       | グラフや図などの任意の情報表現。                         |
| C    | Controller | 入力を受け取りmodelとviewへの命令に変換する。            |
| T    | Template   | MVCモデルのV(View)相当。画面表示を担う。                 |

### 一般モデルとFlask/Djangoモデルの対比と特徴

- Flask/Djangoモデルの`T:Template`は、一般モデルの`V:View`に相当する。
- Flask/Djangoモデルの`V:View`は、一般モデルの`C:Controller`に相当する。

| Flask/Djangoモデル | 一般モデル   | 参考                   |
| :----------------- | :----------- | :--------------------- |
| M:Model            | M:Model      | app/feedback/models    |
| T:Template         | V:View       | app/feedback/templates |
| V:View             | C:Controller | app/feedback/views     |
| Resource           | Resource     | app/feedback/static    |

### M:Modelを作成する

1. SQLAlchemyのインスタンスを生成する。

    ```__init__.py
    """app/feedback/models/__init__.py
    """

    from flask_sqlalchemy import SQLAlchemy

    db = SQLAlchemy()


    def init():
        """init
        """
        db.create_all()
    ```

2. SQLAlchemyのクラス(`db.Model`)を継承してModelを作成する。

    ```feedback.py
    """app/feedback/models/feedback.py
    """

    from datetime import datetime

    from feedback.models import db


    class Feedback(db.Model):
        """Feedback
        """
        __tablename__ = 'feedback'

        id = db.Column(db.Integer, primary_key=True, autoincrement=True)
        service = db.Column(db.String(255), nullable=False)
        title = db.Column(db.String(255), nullable=False)
        detail = db.Column(db.String(255), nullable=False)
        created_date = db.Column(
            db.DateTime, nullable=False, default=datetime.utcnow)

        def __init__(self, service, title, detail):
            self.service = service
            self.title = title
            self.detail = detail

        def to_dict(self):
            """to_dict
            """
            return {
                'id': self.id,
                'service': self.service,
                'title': self.title,
                'detail': self.detail,
                'created_date': self.created_date
            }
    ```

### T:Templateを作成する

1. Flask/Djangoモデルの`T:Template`は、一般モデルの`V:View`に相当する。HTMLを用いてTemplateを作成する。

`本Webサービスは、View機能を持たないため作成しない。`

### V:Viewを作成する

1. Flask/Djangoモデルの`V:View`は、一般モデルの`C:Controller`に相当する。`Blueprint`でルートを定義してViewを作成する。

    ```feedback.py
    """app/feedback/views/feedback.py
    """

    from flask import Blueprint, jsonify, redirect, request, url_for

    from feedback.common.utility import err_response
    from feedback.models import db
    from feedback.models.feedback import Feedback

    feedback = Blueprint('feedback', __name__, url_prefix='/feedback')


    @feedback.route('/healthcheck', methods=['GET'])
    def healthcheck():
        """healthcheck
        """
        return jsonify({
            'status': 'healthy'
        }), 200


    @feedback.route('/records', methods=['GET'])
    def read_all():
        """read_all
        """
        records = Feedback.query.all()
        return jsonify([record.to_dict() for record in records]), 200


    @feedback.route('/records/', methods=['GET'])
    def redirect_read_all():
        """redirect_read_all
        """
        return redirect(url_for('feedback.read_all'))


    @feedback.route('/records/<int:record_id>', methods=['GET'])
    def read_one(record_id=None):
        """read_one
        """
        record = Feedback.query.filter_by(id=record_id).first()
        return jsonify(record.to_dict()), 200


    @feedback.route('/records', methods=['POST'])
    def create():
        """create
        """
        payload = request.json
        service = payload.get('service')
        title = payload.get('title')
        detail = payload.get('detail')

        record = Feedback(service=service, title=title, detail=detail)
        db.session.add(record)
        db.session.commit()

        response = jsonify(record.to_dict())
        response.headers['Location'] = '/feedback/records/%d' % record.id

        return response, 201


    @feedback.route('/records/<int:record_id>', methods=['PUT'])
    def update(record_id=None):
        """update
        """
        record = Feedback.query.filter_by(id=record_id).first()

        payload = request.json
        record.service = payload.get('service')
        record.title = payload.get('title')
        record.detail = payload.get('detail')
        db.session.commit()

        return jsonify(record.to_dict()), 204


    @feedback.route('/records/<int:record_id>', methods=['DELETE'])
    def delete(record_id=None):
        """delete
        """
        record = Feedback.query.filter_by(id=record_id).first()

        db.session.delete(record)
        db.session.commit()

        return jsonify(None), 204


    @feedback.errorhandler(404)
    @feedback.errorhandler(500)
    def errorhandler(error):
        """errorhandler
        """
        return err_response(error=error), error.code
    ```

### 共通処理を作成する

1. Utilityを作成する。

    ```utility.py
    """app/feedback/common/utility.py
    """

    from flask import jsonify


    def err_response(error):
        """err_response
        """
        return jsonify({
            "code": error.code,
            "name": error.name,
            "description": error.description,
        })
    ```

### Flaskの起動処理を作成する

1. Flaskのインスタンスを生成する。

    ```run.py
    """app/run.py
    """

    import os

    from flask import Flask
    from flask_migrate import Migrate

    from feedback.common.utility import err_response
    from feedback.models import db
    from feedback.views.feedback import feedback

    app = Flask(__name__, instance_relative_config=True)
    app.config.from_pyfile('config.py')

    app.register_blueprint(feedback)

    db.init_app(app)
    Migrate(app, db)


    @app.errorhandler(404)
    @app.errorhandler(500)
    def errorhandler(error):
        """errorhandler
        """
        return err_response(error=error), error.code


    def main():
        """main
        """
        host = os.getenv('HOST', '0.0.0.0')
        port = int(os.getenv('PORT', '5000'))
        app.run(host=host, port=port)


    if __name__ == '__main__':
        main()
    ```

## 6. DBのマイグレーション

### Flask-Migrateを使ってマイグレーションする

1. コマンドラインを実行する。

    ```procedure.sh
    (.venv) ~$ flask db init
    (.venv) ~$ flask db migrate
    (.venv) ~$ flask db upgrade
    ```

### Flask-Migrateを使わずにマイグレーションする

1. コマンドラインを実行する。`flask shell`の実行に環境変数の設定が必要となる。

    ```procedure.sh
    (.venv) ~$ flask shell
    >>> from feedback.models import init
    >>> init()
    >>> exit()
    ```

2. or 直接`create_all()`を実行する。

    ```procedure.sh
    (.venv) ~$ flask shell
    >>> from feedback.models import db
    >>> db.create_all()
    >>> exit()
    ```

## 7. Flaskの起動

1. コマンドラインを実行する。`flask run`の実行に環境変数の設定が必要となる。

    ```procedure.sh
    (.venv) ~$ flask run
    ```

## 8. クラアント側の処理(サンプル)

```tree.sh
feedback-api
├── app
     ├── __init__.py
     ├── client
          ├── __init__.py
          ├── create.py
          ├── delete.py
          ├── read_all.py
          ├── read_one.py
          └── update.py
```

### レコードを全件取得する

```read_all.py
"""app/client/read_all.py
"""

import requests

get_url = '{host}:{port}/feedback/records'.format(**{
    'host': 'http://127.0.0.1',
    'port': '5000'
})

res = requests.get(url=get_url)

print(res.status_code)
print(res.text)
```

### レコードを1件取得する

```read_one.py
"""app/client/read_one.py
"""

import requests

get_url = '{host}:{port}/feedback/records/{record_id}'.format(**{
    'host': 'http://127.0.0.1',
    'port': '5000',
    'record_id': '1'
})

res = requests.get(url=get_url)

print(res.status_code)
print(res.text)
```

### レコードを作成する

```create.py
"""app/client/create.py
"""

import json

import requests

post_url = '{host}:{port}/feedback/records'.format(**{
    'host': 'http://127.0.0.1',
    'port': '5000'
})
post_data = json.dumps({
    'service': 'create_service',
    'title': 'create_title',
    'detail': 'create_detail'
})
post_headers = {
    'Content-Type': 'application/json'
}

res = requests.post(url=post_url, data=post_data, headers=post_headers)

print(res.status_code)
print(res.text)
```

### レコードを更新する

```update.py
"""app/client/update.py
"""

import json

import requests

update_url = '{host}:{port}/feedback/records/{record_id}'.format(**{
    'host': 'http://127.0.0.1',
    'port': '5000',
    'record_id': '1'
})
update_data = json.dumps({
    'service': 'update_service',
    'title': 'update_title',
    'detail': 'update_detail'
})
update_headers = {
    'Content-Type': 'application/json'
}

res = requests.put(url=update_url, data=update_data, headers=update_headers)

print(res.status_code)
print(res.text)
```

### レコードを削除する

```delete.py
"""app/client/delete.py
"""

import requests

delete_url = '{host}:{port}/feedback/records/{record_id}'.format(**{
    'host': 'http://127.0.0.1',
    'port': '5000',
    'record_id': '1'
})

res = requests.delete(delete_url)

print(res.status_code)
print(res.text)
```
