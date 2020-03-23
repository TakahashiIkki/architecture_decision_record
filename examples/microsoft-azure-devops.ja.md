# Microsoft Azure DevOps

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
  * [Implications](#implications)
* [Related](#related)
  * [Related decisions](#related-decisions)
  * [Related requirements](#related-requirements)
  * [Related artifacts](#related-artifacts)
  * [Related principles](#related-principles)
* [Notes](#notes)
  * [Microsoft Devops CI: An Unsatisfying Adventure](#microsoft-devops-ci-an-unsatisfying-adventure)
  * [Hacker News discussion highlights](#hacker-news-discussion-highlights)
  * [Windows Development MVP](#windows-development-mvp)
  * [Edward Thomson (Azure PM) summary](#edward-thomson-azure-pm-summary)


## 概要


### 課題

プロジェクトをビルドし、統合し、デプロイし、ホスティングするのにDevOpsを使いたい。そこでMicrosoft Azure DevOpsを検討している。


  * DevOpsのセットアップ(設定など)や継続的な利用(ビルド時間の短縮など)のために、高速で信頼性のある開発者エクスペリエンスを提供したい。

  * プロジェクトのアプリケーションやデータベースなどをホスティングするために、Microsoft Azureを検討したい。


### 決定事項

Decided against Microsoft Azure DevOps.


### Status

Decided. Open to revisiting if/when new significant info arrives.


## 詳細

### 前提

Accelerateの本にあるような、通常のDevOpsの前提条件はすべて適用される。

  * 高速なビルドは大いに役立つ。これによりフィードバックループが加速される。

  * 他のベンダーの入出力部品と交換できる。たとえば、より高速なビルドサーバを導入したり、独自に選択したバージョン管理システムを使用したり、セルフホスティング型のCIサーバと連携したりできる。

  * 最新のユーザビリティは、開発者エクスペリエンスにとって、そして一貫性、明快さ、セキュリティ、学習曲線の容易さのような繊細な領域においてとても役に立つ。

  * 何かが壊れていたり、問題がある場合は、その問題を効果的にレポートする手段が必要だ。これはセキュリティ関連の問題では特に重要だ。

### 制約

不明。Azureは外部ツールと上手く連携できることを謳ってはいる。

### Positions

Microsoft Azure DevOpsと既存のAWSを使うことを検討した。

Azure DevOps, Azure Pipelines, Azure Repo, Azure spin up of new serverをTerraform経由で実験した。

試しにMicrosoftの担当者からのサポートを受けてみた。

ブログやHacker Newsで仲間から情報を収集した。


### 議論

Azure DevOpsは優れたプロダクト群として宣伝されているが、それらはもうひとつで、うまく連携しておらず、サポートも貧弱である。

Our firsthand experience:

  * AzureのセットアップはUIがごちゃついていて、Microsoftアカウントで使えるものもあれば、そうでないものもある。Azureサインイン、Microsoft.comサインイン、Live.comサインインがあり、すべてが同時に実行される。

  * セットアップ中に小さなセキュリティの問題が発生し、解決策が見つからなかった。様々な方法でそれを多くMicrosoft担当に報告しようとしたが、うまくいかなかった。これをMicrosoftのセキュリティ部門に報告はできたが、Microsoftからは「修正しない」との回答があった。

  * ドキュメントはよく間違っていることもあるし、古くなっているものもある。Microsoftの検索エンジンが貧弱だし、SEOのレベルが低いことがその原因のもなっている。

  * Terraformのセットアップは十分なドキュメントがあり、ちゃんと動く。だが、MicrosoftはTerraformのセットアップ例を
  * Terraform setup is well documented, and works. However, Terraform supoprt is weak compared to AWS because Microsoft is building business relationships with vendors to do chain-through Terraform setup examples.

Our peer experiences:

  * 自分たちで評価した後に、同僚の経験も聞いて回った。私たちの経験を裏付けることになった。

  * ビルド時間に関する問題や、独自のビルドサーバを構築する際の問題もあった。ビルドはビルドパイプラインの中心的な目的であり、私たちは毎日多くのビルドを実行するつもりなので、これらの問題はUIの問題よりもかなり深刻だ。

  * ディスカッションに、Azureのチームメイトは積極的に関与してくれた。これにはMicrosoftに賛辞を送りたい。特にEdward Thomson、Azure PM、コーダに感銘を受けた。

### 考察

Microsoft Azure DevOpsを選ぶと、そうでない場合に比べて3倍近くコストがかかりそうである。

## Related


### Related decisions

If we choose Azure DevOps, there are many related offerings, including Azure Repo, Azure Pipeline, etc. We believe that if we choose Azure Devops, this may make it easier to use more Azure capabilities, or may make it harder to use other vendors' capabilities.

We believe that Microsoft is making great strides in developer experience, and we see Microsoft making large acquisition of developer tools (e.g. GitHub) and dependencies (e.g. Citus).

If we choose Azure DevOps, then we may want to emphasize choosing the Microsoft acquistion offerings, and we may also want to approach the acquisition offerings with more care/assessement because of potential tissue-rejection e.g. staff turnover risk.


### Related requirements

We want build times to be very fast. We accept paying a high premium for this. This is because we want to iterate very fast.

We want reliability to be very high. We accept paying a high premium for this. This is because we are testing high-value use cases, including financial transations, confidential transactions, etc.

Our top 4 devops KPIs include mean time to recovery, which necessitates fast builds and high reliability.


### Related artifacts

We want the build system to output artifacts suitable for using in other systems, such as Artefactory.


### Related principles

Easily reversible. We can evaluate Azure DevOps in parallel with AWS incumbent.


## Notes


### Microsoft Devops CI: An Unsatisfying Adventure

https://toxicbakery.github.io/vsts-devops/microsoft-devops-ci/

Blog post.

"As a software developer, I know first-hand how difficult it is to build quality products quickly and cheaply. It’s an art form that we sometimes get right, and other times devolves into something akin to the Obama era healthcare government site. Our level of control over the resulting product varies, and blame for failure often falls on the wrong people in the decision-making hierarchy. Microsoft’s Azure DevOps (formerly known as Visual Studio Team Services), despite clearly good intentions, is a perfect storm of bad decisions and poor execution."


### Hacker News discussion highlights

https://news.ycombinator.com/item?id=18983586

"We use Azure DevOps extensively at my work and, after having used GitHub, Gitlab, self hosted solutions, Jenkins, TeamCity... Azure DevOps ranks dead last."

"The UI is terribly clunky everywhere. The worst for me are pull requests. Incredibly tough to work with people on a pull request. I can't even point you to "a" particular problem - for us it's broken everywhere."

"Azure Devops is something I want to love. The UI keeps changing, but doesn't fix underlying bugs that have been around for ages."

"The tools are not well integrated, the UI is really slow, there’s no dashboard view of active pull requests, builds, releases, etc for my favorite repos. Build/Deploy times are insanely slow."

"We tried to also use Azure Boards (Work Items, Boards, Backlogs, etc). Ouch. It is a complete UI mess of disjointed ideas. Instead of implementing one thing well, they implemented two dozen things terribly."


### Windows Development MVP

Windows Development MVP here. I feel like I must shoulder some of the responsibility here for not being louder about these issues. But must say, I'm disappointed to hear you're "surprised" about the UX issues. I've been telling your folks the UX is dreadful (e.g. as far back as pre-launch) and kept hearing back "we know, we're fixing it". I'll start formalizing the feedback and push it through the pipes, stay tuned. I'm also local (Bellevue), would love to come in and try to pipeline our relatively simple oss .net/wpf/uwp app. I suspect it'll be an eye opener for the both of us.

Some examples:

* You can't build a pipeline with a git repo. that contains submodules

* Found it impossible to edit the PATH for some custom tooling

* The New Pipeline experience just doesn't make a lot of sense, new users clicking around will eventually end up at the wrong Docs.


### Edward Thomson (Azure PM) summary

I wrote the code that merges your pull requests. Program Manager for at Microsoft for Azure DevOps; formerly a software engineer on version control tools at GitHub, Microsoft, SourceGear.

https://www.edwardthomson.com/

Co-maintainer of libgit2. https://libgit2.github.io

Co-host of All Things Git, the Podcast about Git. https://www.allthingsgit.com/

Curator of Developer Tools Weekly, a newsletter about development tools. https://developertoolsweekly.com/
