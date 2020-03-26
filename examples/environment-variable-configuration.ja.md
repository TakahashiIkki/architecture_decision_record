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

そのデプロイ環境に応じて異なる挙動ができるように、成果物/バイナリ/ソースを超えてアプリケーションを設定できるようにしたい。

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

ソースコード管理(SCM)のバージョン管理システム(VCS)で秘密を漏らさないようにした。

一般的なソフトウェアフレームワークやライブラリとの互換性を目指したい。例えばNodeには、環境変数の設定を読み取るための"dotenv"というモジュールがある。

### Positions

いくつかのアプローチを検討した:

  * `config.js`ファイルにappの設定を保存する。

  * `.env`ファイルに環境毎の設定を保存する。

  * ライセンスサーバのようなよく知られた場所から、設定を取ってくる。

### 議論

.envファイルのアプローチを選択した理由は以下のとおりである。

  * 熟練者にもなじみがある。

  * `.env`　ファイルのパターンは、私たちのチームで多くプロジェクトでよく使っていて上手く行っている。

  * シンプルである。ライセンスサーバのアプローチと比較して監査機能が不足しているなど、主要なトレードオフに関しては、今のところ問題ない。


### Implications

どのような機密管理からも公開されている環境変数設定を分離する方法を見いだす必要がある。


## Related


### Related decisions

すべてのアプリケーションがこのアプローチを使うことを期待する。

バイナリまたはソースコードにハードコーディングされているような、あまりよろしくない手法を使っているアプリケーションはアップグレードする計画だ。

ライセンスサーバなど、より高機能な手法を使用するアプリケーションは、現状のまま維持する。


### Related requirements

フック、テスト、CIなど、ファイルにDevOps機能を追加するだろう。

この決定において、すべてのチームメイトの開発者を教育する必要がある。



### Related artifacts

デプロイする各環境で、.envファイルとその関連ファイルを必要とする。


### Related principles

簡単に元に戻せる。

## Notes


`.env` ファイルの例:

```env
NAME=Alice Anderson
EMAIL=alice@example.com
```

`.env.defaults` ファイルの例:

```env
NAME=Joe Doe
EMAIL=joe@example.com
```

`.env.schema`の例。キーのみをもつ。

```env
NAME
EMAIL
```
