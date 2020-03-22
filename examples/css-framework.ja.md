# CSSフレームワーク

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


### Issue

Webアプリケーションを作るのに、CSSフレームワークを使いたい。

  * すべての主要ブラウザ、画面サイズで高速で信頼性の高いユーザエクスペリエンスが必要だ。

  * デザイン、レイアウト、UI/UXについて高速なイテレーションを回したい。

  * レスポンシブなアプリケーションにしたい。特にモバイルデバイスのように小さな画面、4Kワイドのような大きな画面、回転するモニタのようなダイナミックな画面などに対応したい。

### Decision

Bulmaを使う。


### Status

Decided on Bulma. Open to new CSS framework choices as they arrive.


## Details


### 前提

モダンで高速で、信頼性があり、レスポンシブなWebアプリケーションを作りたい。

典型的なモダンWebアプリは、いくつかの理由でjQueryの利用を最小限にしたり、一切使わないようにしている。

  * モダンJavaScriptはjQueryが提供する機能を使えるので、jQueryの必要は薄れている。特定の実装を提供する
より良い/高速で/小さなモジュールもある。 

  * jQueryの大抵のアプローチは、直接DOMを操作するもので、モダンJavaScriptフレームワーク(React, Vue, Svelteなど)ではアンチパターンとされている。

  * jQueryは2回ロードされると、自分自身と干渉する。


### 制約

jQueryを使うCSSフレームワークを選んでしまうと、jQueryのインポートを避けにくい。例えば、Semantic UIはjQueryを使うが、Tachyonsは使わない。

ミニマルなCSSフレームワークを選ぶと、じきに必要になるかもしれないフレームワーク部品を使えない。例えばSemantic UIは画像のカルーセルを提供するが、Tachyonsには無い。

### Positions

フレームワークを使わないことも検討した。CSSグリッドはプロジェクトに必要なものの多くを提供してくれるので、これはまだ実行可能なように思える。
We considered using no framework. This still seems viable, especially because CSS grid provides much of what we need for our project..

Bootstrap, Bulma, Foundation, Materialize, Semantic UI, Tachyonsなど、リストアップして多くのCSSフレームワークを検討した。そして、より深い検討するためにSemantic UI(もっともセマンティックなアプローチ)とBulma(今必要とするコンポーネントを提供する中では軽量なアプローチを採用している)の2つに選択肢を絞った。

Semantic UIを検討した。これはタブ、グリッド、ボタンなど、プロジェクトに必要なものを含む多くのコンポーネントを提供する。Semantic UIについて、CDNファイルを使うのと、NPMリポジトリを使うやり方の2つでパイロットを作ってみた。静的HTMLページにおけるセマンティックUIはうまく行ったが、JavaScript SPAを作るのはタイムボックス内には収まらなかった(おもにjQueryのロード問題のため)。私たちは、他のプログラマが私たちと同じ理由で、jQueryに依存しないバージョンを作るようにSemantic UIの開発者に要求しているのを見つけた。それは何年も前からある話のようだが、開発者たちはそれを拒否し続けている。「Semantic UIプロジェクトにはjQueryを使っている箇所が22,000以上もある」からだ。

Semanticを使った例:

```html
<div class="ui top attached tabular menu">
  <a class="item">Alpha</a>
  <a class="item">Bravo</a>
</div>
```

Bulumaを検討した。BlumaはSemantic UIと同様の機能を多く持つが、洗練されたものはそんなにはない。Blumaはモダンな技術で作られていて、jQueryは使っていない。Blumaはサードパーティ製のコンポーネントがいくつかあり、私たちの使いたいものも中にはある。

Bulmaを使った例:

```html
<div class="tabs">
  <ul>
    <li><a>Alpha</a></li>
    <li><a>Bravo</a></li>
  </ul>
</div>
```


### 議論

前述のとおり。

特に、Semantic UIには、技術(つまり、非常に多くのjQueryとのタッチポイントがあること)と、リーダシップ(jQueryフリー化はロードマップや継続的な改善、寄付金の調達を試みるよりも難しい)の両方の観点から要注意フラグがある。

### 考察

jQueryを使わない良いCSSフレームワークを見つけたら、一般的に役に立つし全体的に良いことだ。

## Related

### Related decisions

私たちの選んだCSSフレームワークは、テスト容易性に影響するかもしれない。


### Related requirements

私たちは真にモダンなアプリケーションを速くリリースしたい。

古い依存関係(特にjQuery)を使う、古いフレームワーク(Semantic UI)を使うことで、時間を無駄にしたくない。

### Related artifacts

CSSを使うHTMLすべてに影響する。


### Related principles

Easily reversible.

Need for speed.


## 注意事項

何か注意事項があればここに記す。
