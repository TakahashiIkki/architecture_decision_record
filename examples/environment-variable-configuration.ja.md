# 環境変数の設定

Contents:

* [Summary](#summary)
  * [Issue](#issue)
  * [Decision](#decision)
  * [Status](#status)
* [Details](#details)
  * [Assumptions](#assumptions)
  * [Constraints](#constraints)
  * [Positions](#positions)
  * [Argument](#argument)
  * [Implications ](#implications)
* [Related](#related)
  * [Related decisions](#related-decisions)
  * [Related requirements](#related-requirements)
  * [Related artifacts](#related-artifacts)
  * [Related principles](#related-principles)
* [Notes](#notes)


## 概要


### 課題

そのデプロイ環境に応じて異なる挙動ができるように、成果物/バイナリ/ソースを超えてアプリケーション
We want our applications to be configurable beyond artifacts/binaries/source, such that one build can behave differently depending on its deployment environment.

  * これを達成するため、環境変数の設定を使いたい。

  * バージョン管理されたファイルを使って、設定を管理したい。

  * 設定可能なものや関連するデフォルトのような開発者エクスペリエンスを提供したい。

### 決定事項

関連するデフォルトファイルとスキーマファイル.envファイルを使う。

### ステータス

決定
新しい機能が出てきたらそれについて検討のためOpenにする。

## Details


### Assumptions

アプリケーションコードと環境依存のコードを分離することが望ましい。アプリケーションは、開発環境、テスト環境、でも環境、本番環境など、異なる環境で異なる動作をする必要があると想定する。

「12 factor app」のプラクティスと、その関連の「15 factor app」のプラクティスを支持する。

これまでのプロジェクトの多くで`.env`ファイルや同様の`.env`ディレクトリを使ってきた。これらをバージョン管理の対象外にしておき、代わりに他の手段でデプロイし、バージョニングし、管理するのが一般的な方法だ。

### 制約

ソースコード管理(SCM)のバージョン管理システム(VCS)から秘密を守りたい。
We want to keep secrets out of our source code management (SCM) version control system (VCS).

一般的なソフトウェアフレームワークやライブラリとの互換性を目指したい。例えばNodeには、環境変数の設定を読み取るための"dotenv"というモジュールがある。

### Positions

いくつかのアプローチを検討した:

  * `config.js`ファイルにappの設定を保存する。

  * `.env`ファイルに環境毎の設定を保存する。

  * ライセンスサーバのようなよく知られた場所から、設定を取ってくる。

### 議論

We selected the approach of a file .env because:

  * It is popular including among experts.

  * It follows the pattern of `.env` files which our teams have successfully used many times on many projects.

  * It is simple. Notably,  We are fine for now with the significant trade-offs that we see, such as a lack of audit capabilities as compared to an approach of a license server.


### Implications 

We need to figure out a way to separate environment variable configuration that is public from any secrets management.


## Related


### Related decisions

We expect all our applications to use this approach.

We will plan to upgrade any of our applications that use a less-capable approach, such as hardcoding in a binary or in source code.

We will keep as-is any of our applications that use a more-capable approach, such as a licensing server.


### Related requirements

We will add devops capabilities for the files, including hooks, tests, and continuous integration.

We need to train all developer teammates on this decision.



### Related artifacts

Each area where we deploy will need its own .env file and related files.


### Related principles

Easily reversible.


## Notes


Example file `.env`:

```env
NAME=Alice Anderson
EMAIL=alice@example.com
```

Example file `.env.defaults`:

```env
NAME=Joe Doe
EMAIL=joe@example.com
```

Example file `.env.schema` with just the keys:

```env
NAME
EMAIL
```
