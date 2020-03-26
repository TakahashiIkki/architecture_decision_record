# Programming languages

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


## Summary


### 課題

ソフトウェアのプログラミング言語を何にするか決める必要がある。Webアプリケーションに適したフロントエンドのプログラミング言語と、サーバアプリケーションに適したバックエンドのプログラミングの、大きく分けて2つが必要だ。


### 決定事項

フロントエンドにはTypeScriptを使う。

バックエンドにはRustを使う。


### ステータス

決定。
新しい代替案があったらまたオープンにする。

## Details


### Assumptions

フロントエンドアプリケーションは:
The front-end applications are typical:

  * Typical users and interactions

  * Typical browsers and systems

  * Typical developments and deployments

The front-end applications is likely to evolve quickly:

  * 開発やデプロイ、イテレーションが簡単で速くできることを保証したい。

  * 私たちは型安全などの検査性を重視していて、それを実現できるならもう少し努力してもいいと考えている。

  * レガシーとの互換性は必要ない。

The back-end applications are higher-than-typical:

  * 品質、特に証明可能性、信頼性、セキュリティなどで通常より高めの目標がある。

  * ほぼリアルタイムについて高い目標がある。つまりVMのGCで処理が止まってほしくない。

  * 関数プログラミング、特に並行性、マルチコア処理、メモリ安全には高い目標がある。

コンパイル時の安全性と実行時の速度のためなら、コンパイル時間が遅いことは許容する。


### 制約

Amazon Lamdaなど主要なクラウドプロバイダーのFaaSサービスでは使える言語に制約がある。


### Positions

これらの言語を検討した:

  * C

  * C++

  * Clojure

  * Elixir

  * Erlang

  * Elm

  * Flow

  * Go

  * Haskell

  * Java

  * JavaScript

  * Kotlin

  * Python

  * Ruby

  * Rust

  * TypeScript



### 議論

言語毎の検討概要:

  * C: 安全性が低いので棄却; Rustはほとんど全てでより良くできる。

  * C++: rejected because it's a mess; Rush can do nearly everything better.

  * Clojure: excellent modeling; best Lisp approximation; great runtime on the JVM.

  * Elixir: excellent runtime including deployability and concurrency; excellent developer experience; relatively small ecosystem.

  * Erlang: excellent runtime including deployability and concurrency; challenging developer experience; relatively small ecosystem.

  * Elm: looks very promising; IBM is publishing major case studies with good resutls; smaller ecosystem.

  * Flow: interesting improvement over JavaScript; however; developers are moving away from it.

  * Go: excellent developer experience; excellent concurrency; but a track record of bad decisions that cripple the language.

  * Haskell: best functional language; smaller developer community; hasn't achieved enough published production successes.

  * Java: excellent runtime; excellent ecosystem; sub-par developer experience.

  * JavaScript: most popular language ever; most widespread ecosystem.

  * Kotlin: fixes so much of Java; excelent backing by JetBrains; good published cases of porting from Java to Kotlin.

  * Python: most popular language for systems administration; great analytics tooling; good web frameworks; but abandonded by Google in favor of Go.

  * Ruby: best developer experience ever; best web frameworks; nicest community; but very slow; somewhat hard to package.

  * Rust: best new language; zero-abstraction emphasis; concurrency emphasis; however relatively small ecosystem; and has deliberate limits on some kinds of compiler accelerations e.g. direct memory access needs to be explicitly unsafe.

  * TypeScript: adds types to JavaScript; great transpiler; growing developer emphasis on porting from JavaScript to TypeScript; strong backing from Microsoft.

VMにはランタイム機能を提供するために複雑さが増す、といった今すぐには必要ないトレードオフがあると判断した。

We believe that our core decision is driven by two cross-cutting concerns:

  * For fastest runtime speed and tightest system access, we would choose JavaScript and C.

  * For close-to-fastest runtime speed and close-to-tightest system access, we choose TypeScript and Rust.

Honorable mentions go to the VM languages and web frameworks that we would choose if we wanted a VM lanauge:

  * Closure and Luminous

  * Java and Spring

  * Elixir and Phoenix


### Implications

Front-end developers will need to learn TypeScript. This is likely an easy learning curve if the developer's primary experience is using JavaScript.

Back-end developers will need to learn Rust. This is likely a moderate learning curve if the developer's primary experience is using  C/C++, and a hard learning curve if the developer's primary experience is using Java, Python, Ruby, or similar memory-managed languages.

TypeScript and Rust are both relatively new. This means that many tools do not yet have documentation for these languages. For example, the devops pipeline will need to be set up for these languages, and so far, none of the devops tools that we are evaluating have default examples for these langauges.

Compile times for TypeScript and Rust are quite slow. Some of this may be due to the newness of the languages. We may want to look at how to mitigate slow compile times, such as by compile-on-demand, compile-concurrency, etc.

IDE support for these languages is not yet ubiquitous and not yet first-class. For example, JetBrains sells the PyCharm IDE for first-class support for Python, but does not sell and IDE with first-class support for Rust; instead, JetBrains can use a Rust plug-in that provides perhaps 80% of Rust language support vis a vis Python language support.


## Related


### Related decisions

We will aim toward ecosystem choices that align with these langauges.

For example, we want to choose an IDE that has good capabilties for these languages.

For example, for our front-end web framework, we are more-likley to decide on a framework that tends to aim toward TypeScript (e.g. Vue) than a framework that tends to aim toward plain JavaScript (e.g. React).


### Related requirements

私たちのツールチェーン全体で、これらの言語をサポートしなければならない。


### Related artifacts

いくつかの機密情報を環境変数へエクスポートすることが予想される。


### Related principles

二度計測して、一度構築する。
Measure twice, build once. We are prioritizing some safety over some speed.

Runtime is more valuable than compile time. We are prioritizing customer usage over developer usage.


## Notes

Any notes here.
