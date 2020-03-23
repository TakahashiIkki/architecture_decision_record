# Architecture decision record (ADR)

ADRはアーキテクチャ上の重要な意思決定を、そのコンテキストや結果とともに記録した文書です。

Contents:

* [What is an architecture decision record?](#what-is-an-architecture-decision-record)
* [How to start using ADRs](#how-to-start-using-adrs)
* [How to start using ADRs with tools](#how-to-start-using-adrs-with-tools)
* [How to start using ADRs with git](#how-to-start-using-adrs-with-git)
* [ADR file name conventions](#adr-file-name-conventions)
* [Suggestions for writing good ADRs](#suggestions-for-writing-good-adrs)
* [ADR example templates](#adr-example-templates)
* [For more information](#for-more-information)


## ADRとは何か?

**architecture decision record** (ADR) はアーキテクチャ上の重要な意思決定を、そのコンテキストや結果とともに記録した文書です。

**architecture decision** (AD) とは重要な要求に対するソフトウェア設計上の選択を指します。

**architecture decision log** (ADL) とは、あるプロジェクト(または組織)のために、作成されメンテされている、すべてのADRを指します。

**architecturally-significant requirement** (ASR) は、ソフトウェアシステムのアーキテクチャに影響を与える要求のことで、計測可能でなくてはなりません。

これらすべては、**architecture knowledge management** (AKM)のトピックの範疇です。

この文書のゴールは、ADRの全体感がスッと理解できるようにし、それらの作り方や追加の情報をとこで見れるかを示すことです。

略語:

  * **AD**: architecture decision

  * **ADL**: architecture decision log

  * **ADR**: architecture decision record

  * **AKM**: architecture knowledge management

  * **ASR**: architecturally-significant requirement


## ADRを使い始める

ADRを使い始めるために、このセクションについてチームメイトと話合いましょう。

Decision identification:

  * そのADはどれくらい緊急で、どのくらい重要でしょうか?

  * それは今決めなきゃいけないでのしょうか? それとも、もっと分かるまで待てるでしょうか?

  * Both personal and collective experience, as well as recognized design methods and practices, can assist with decision identification.

  * Ideally maintain a decision todo list that complements the product todo list.

意思決定:

  * 多くの意思決定技法があります。一般的なものからソフトウェアアーキテクチャ固有のものまで。例えばダイアログマッピングなど。

  * グループでの意思決定は、活発な研究テーマです。


決定の成立と施行:

  * ADはソフトウェアの設計で使われる; したがって開発者、運用者も含むシステムのステークホルダーと会話し、彼らに受け入れられるものでなくてはならない。

  * アーキテクチャ的に明らかなコーディングスタイルと、アーキテクチャ上の課題と意思決定にフォーカスしたコードレビューは、2つの関連したプラクティスです。

  * また、ソフトウェアの進化において、ソフトウェアシステムを近代化する際には、ADもまた再検討されなくてはならない。

決定の共有 (任意):

  * 多くのADはプロジェクト横断的に繰り返し発生します。

  * したがって、明示的なナレッジマネジメント戦略を採用するのであれば、過去の決定に関する経験が、良いものでも悪いものでも、再利用可能な貴重な資産となるでしょう。

  * グループでの意思決定は、活発な研究テーマです。

決定文書:

  * 意思決定のためのテンプレートやツールは数多く存在します。

  * アジャイルコミュニティ、例えばNygardのADRを参照してください。

  * IBM UMFや、CapitalOneのTyreeとAkermanが提唱するテーブルレイアウトなど、従来のソフトウェアエンジニアリングおよびアーキテクチャ設計プロセスを参照してください。

決定のガイド:

  * The steps above are adopted from the Wikipedia entry on [Architectural Decision](https://en.wikipedia.org/wiki/Architectural_decision)

  * A number of decision making techniques exists, both general ones and software and software architecture specific ones, for instance, dialogue mapping.


## How to start using ADRs with tools

You can start using ADRs with tools any way you want.

例えば:

  * Google Driveを使ってオンラインで編集するのが好みならば、Google DocsやGoogle Spreadsheetが使える。

  * gitのようなバージョン管理システムを使うのが好みならば、ADR毎にファイルを作ればよい。

  * JIRAのようなプロジェクト計画ツールが好みであれば、ツールのプランニングトラッカーを使うと良い。

  * MediaWikiのようなWikiが好みであれば、ADR wikiを作ると良い


## gitを使ったADRの始め方

gitを使うのが好きな人のために、典型的なソフトウェアプロジェクトのためのgitでのADRの始め方をここに示す。

ADRファイルを置くためのディレクトリを作る:

```sh
$ mkdir adr
```

各ADRのために、`database.txt` のようなテキストファイルを作る:

```sh
$ vi database.txt
```

ADRに必要なことを書き込む。このリポジトリにADRのテンプレートがあるので、それを参照しよう。

ADRをgitリポジトリにコミットする。


## ADRのファイル命名規約

テキストファイルを使ってADRを作るのであれば、ADRファイルの命名規約が欲しくなるだろう。


以下のファイル命名規約を使うとよい。

例:

  * choose_database.md

  * format_timestamps.md

  * manage_passwords.md

  * handle_exceptions.md

ファイル命名規約:

  * 名前には現在時制の命令動詞句を使う。これは可読性を高め、コミットメッセージのフォーマットにも合う。

  * 名前には小文字とアンダースコアを使う。これは読みやすさとシステムでの扱いやすさのバランスだ。

  * 拡張子はマークダウンのものにする。簡単にフォーマッティングするのに便利だから。

## 良いADRを書くための提言

良いADRの特徴:

  * 時点 - いつADが作られたかを特定できる

  * 合理性 - そのADを作らなきゃいけない理由を説明されている

  * 不変性 - 前に公開したADRでなされた決定は変えてはならない

  * 特殊性 - それぞれのADRは1つのADについてのものでなくてはならない

ADRにおける良いコンテキストの性質:

  * 組織の状況やビジネス上の優先度が説明されている

  * チームの社会的構成とスキル構成に基づいた合理性と検討を含める。

ADRにおける良い結果の性質:

  * 正しいアプローチ - 「Yの代わりにXを始める必要がある」

  * 間違ったアプローチ - あるADを作った際の利点/欠点への言及がない。

新たなADRは以前のADRに取って代わることがある:

  * 以前のADRを置き換えたり、無効にするADが発生したら、新たにADRを作ったほうが良い。


## ADRのテンプレート例

私たちがネット上で収集したADRのテンプレート例:

  * [ADR template by Michael Nygard](adr_template_by_michael_nygard.md) (simple and popular)

  * [ADR template by Jeff Tyree and Art Akerman](adr_template_by_jeff_tyree_and_art_akerman.md) (more sophisticated)

  * [ADR template for Alexandrian pattern](adr_template_for_alexandrian_pattern.md) (simple with context specifics)

  * [ADR template for business case](adr_template_for_business_case.md) (more MBA-oriented, with costs, SWOT, and more opinions)

  * [ADR template MADR](adr_template_madr.md) (more Markdown)

  * [ADR template using Planguage](adr_template_using_planguage.md) (more quality assurance oriented)


## 追加情報

Introduction:

  * [Architectural decision (wikipedia.org)](https://wikipedia.org/wiki/Architectural_decision)

  * [Architecturally significant requirements (wikipedia.org)](https://wikipedia.org/wiki/Architecturally_significant_requirements)

テンプレート:

  * [Documenting architecture decisions - Michael Nygard (thinkrelevance.com)](http://thinkrelevance.com/blog/2011/11/15/documenting-architecture-decisions)

  * [Markdown Architectural Decision Records (adr.github.io)](https://adr.github.io/madr/) - provided by the [adr GitHub organization](https://adr.github.io/)

  * [Template for documenting architecture alternatives and decisions (stackoverflow.com)](http://stackoverflow.com/questions/7104735/template-for-documenting-architecture-alternatives-and-decisions)

より深く:

  * [ADMentor XML project (github.com)](https://github.com/IFS-HSR/ADMentor)

  * [Architectural Decision Guidance across Projects: Problem Space Modeling, Decision Backlog Management and Cloud Computing Knowledge (ifs.hsr.ch)](https://www.ifs.hsr.ch/fileadmin/user_upload/customers/ifs.hsr.ch/Home/projekte/ADMentor-WICSA2015ubmissionv11nc.pdf)

  * [The Decision View's Role in Software Architecture Practice (computer.org)](https://www.computer.org/csdl/mags/so/2009/02/mso2009020036-abs.html)

  * [Documenting Software Architectures: Views and Beyond (resources.sei.cmu.edu)](http://resources.sei.cmu.edu/library/asset-view.cfm?assetID=30386)

  * [Architecture Decisions: Demystifying Architecture (utdallas.edu)](https://www.utdallas.edu/~chung/SA/zz-Impreso-architecture_decisions-tyree-05.pdf)

  * [ThoughtWorks Technology Radar: Lightweight Architecture Decision Records (thoughtworks.com)](https://www.thoughtworks.com/radar/techniques/lightweight-architecture-decision-records)

ツール:

  * [Command-line tools for working with Architecture Decision Records](https://github.com/npryce/adr-tools)

  * [Command line tools with python by Victor Sluiter](https://bitbucket.org/tinkerer_/adr-tools-python/src/master/)

例:

  * [Repository of Architecture Decision Records made for the Arachne Framework](https://github.com/arachne-framework/architecture)

あわせて読もう:

  * REMAP (Representation and Maintenance of Process Knowledge)

  * DRL (Decision Representation Language)

  * IBIS (Issue-Based Information System)

  * QOC (Questions, Options, and Criteria)

  * IBM’s e-Business Reference Architecture Framework
