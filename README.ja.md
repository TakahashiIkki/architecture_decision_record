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

For example:

  * If you like using Google Drive and online editing, then you can create a Google Doc, or Google Sheet.

  * If you like use source code version control, such as git, then you can create a file for each ADR.

  * If you like using project planning tools, such as Atlassian Jira, then you can use the tool's planning tracker.

  * If you like using wikis, such as MediaWiki, then you can create an ADR wiki.


## How to start using ADRs with git

If you like using git version control, then here is how we like to start using ADRs with git for a typical software project with source code.

Create a directory for ADR files:

```sh
$ mkdir adr
```

For each ADR, create a text file, such as `database.txt`:

```sh
$ vi database.txt
```

Write anything you want in the ADR. See the templates in this repository for ideas.

Commit the ADR to your git repo.


## ADR file name conventions

If you choose to create your ADRs using typical text files, then you may want to come up with your own ADR file name convention.

We prefer to use a file name convention that has a specific format.

Examples:

  * choose_database.md

  * format_timestamps.md

  * manage_passwords.md

  * handle_exceptions.md

Our file name convention:

  * The name has a present tense imperative verb phrase. This helps readability and matches our commit message format.

  * The name uses lowercase and underscores (same as this repo). This is a balance of readability and system usability.

  * The extension is markdown. This can be useful for easy formatting.


## Suggestions for writing good ADRs

Characteristics of a good ADR:

  * Point in Time - Identify when the AD was made

  * Rationality - Explain the reason for making the particular AD

  * Immutable record - The decisions made in a previously published ADR should not be altered

  * Specificity - Each ADR should be about a single AD

Characteristics of a good context in an ADR:

  * Explain your organization's situation and business priorities

  * Include rationale and considerations based on social and skills makeups of your teams

Characteristics of good Consequences in an ADR::

  * Right approach - "We need to start doing X instead of Y"

  * Wrong approach - Do not explain the AD in terms of "Pros" and "Cons" of having made the particular AD

A new ADR may take the place of a previous ADR:

  * When an AD is made that replaces or invalidates a previous ADR, a new ADR should be created


## ADR example templates

ADR example templates that we have collected on the net:

  * [ADR template by Michael Nygard](adr_template_by_michael_nygard.md) (simple and popular)

  * [ADR template by Jeff Tyree and Art Akerman](adr_template_by_jeff_tyree_and_art_akerman.md) (more sophisticated)

  * [ADR template for Alexandrian pattern](adr_template_for_alexandrian_pattern.md) (simple with context specifics)

  * [ADR template for business case](adr_template_for_business_case.md) (more MBA-oriented, with costs, SWOT, and more opinions)

  * [ADR template MADR](adr_template_madr.md) (more Markdown)

  * [ADR template using Planguage](adr_template_using_planguage.md) (more quality assurance oriented)


## For more information

Introduction:

  * [Architectural decision (wikipedia.org)](https://wikipedia.org/wiki/Architectural_decision)

  * [Architecturally significant requirements (wikipedia.org)](https://wikipedia.org/wiki/Architecturally_significant_requirements)

Templates:

  * [Documenting architecture decisions - Michael Nygard (thinkrelevance.com)](http://thinkrelevance.com/blog/2011/11/15/documenting-architecture-decisions)

  * [Markdown Architectural Decision Records (adr.github.io)](https://adr.github.io/madr/) - provided by the [adr GitHub organization](https://adr.github.io/)

  * [Template for documenting architecture alternatives and decisions (stackoverflow.com)](http://stackoverflow.com/questions/7104735/template-for-documenting-architecture-alternatives-and-decisions)

In-depth:

  * [ADMentor XML project (github.com)](https://github.com/IFS-HSR/ADMentor)

  * [Architectural Decision Guidance across Projects: Problem Space Modeling, Decision Backlog Management and Cloud Computing Knowledge (ifs.hsr.ch)](https://www.ifs.hsr.ch/fileadmin/user_upload/customers/ifs.hsr.ch/Home/projekte/ADMentor-WICSA2015ubmissionv11nc.pdf)

  * [The Decision View's Role in Software Architecture Practice (computer.org)](https://www.computer.org/csdl/mags/so/2009/02/mso2009020036-abs.html)

  * [Documenting Software Architectures: Views and Beyond (resources.sei.cmu.edu)](http://resources.sei.cmu.edu/library/asset-view.cfm?assetID=30386)

  * [Architecture Decisions: Demystifying Architecture (utdallas.edu)](https://www.utdallas.edu/~chung/SA/zz-Impreso-architecture_decisions-tyree-05.pdf)

  * [ThoughtWorks Technology Radar: Lightweight Architecture Decision Records (thoughtworks.com)](https://www.thoughtworks.com/radar/techniques/lightweight-architecture-decision-records)

Tools:

  * [Command-line tools for working with Architecture Decision Records](https://github.com/npryce/adr-tools)

  * [Command line tools with python by Victor Sluiter](https://bitbucket.org/tinkerer_/adr-tools-python/src/master/)

Examples:

  * [Repository of Architecture Decision Records made for the Arachne Framework](https://github.com/arachne-framework/architecture)

See also:

  * REMAP (Representation and Maintenance of Process Knowledge)

  * DRL (Decision Representation Language)

  * IBIS (Issue-Based Information System)

  * QOC (Questions, Options, and Criteria)

  * IBM’s e-Business Reference Architecture Framework
