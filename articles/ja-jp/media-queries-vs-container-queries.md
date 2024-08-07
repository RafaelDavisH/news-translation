---
title: メディアクエリ vs コンテナクエリ – どちらを使うべきで、いつ使うべきか？
date: 2024-07-10T15:09:21.001Z
authorURL: ""
originalURL: https://www.freecodecamp.org/news/media-queries-vs-container-queries/
translator: ""
reviewer: ""
---

Webが進化するにつれて、ウェブ開発者としての私たちの生活を楽にすることを目的とした新しいツールやアイデアが次々と登場しています。これにより、古い方法を維持するか、完全に新しいものに切り替えるかを選択する必要があります。しかし、これが常に二者択一の解決策を求めるときに、理想的なアプローチは両方の概念を理解し、それぞれの強みと弱みを比較して、最も適切なアプリケーションを決定することです。この記事では、CSSのメディアクエリとコンテナクエリに対してまさにそれを行います。

## 目次

- [レスポンシブウェブデザインと内在的ウェブデザイン](#responsive-and-intrinsic-web-design)
- [メディアクエリとは？](#what-are-media-queries)
- [コンテナクエリとは？](#what-are-container-queries)
- [実際の比較と主な違い](#real-life-comparison-and-key-differences)
- [どちらを使うべきか、いつ使うべきか？](#which-should-you-use-and-when)
- [結論](#conclusion)

## レスポンシブウェブデザインと内在的ウェブデザイン

2010年以前、ウェブ開発者は主にデスクトップで動作するウェブサイトを作成することができました。しかし、イーサン・マーコットがレスポンシブウェブデザイン（RWD）の概念を導入しました。これは、MDNによると、_複数のデバイスに対応するための設計方法_として定義されています。これにより、メディアクエリがRWDのコンポーネントとして採用されました。

しかし最近では、ジェン・シモンズが定義した内在的ウェブデザイン、つまりコンテキストに応じて変化するコンポーネントを作成する必要性へのシフトが見られます。そしてこれを可能にするのがコンテナクエリです。

## メディアクエリとは？

メディアクエリは、特定の条件が満たされた場合に特定のスタイルを要素に適用するためのルールです。一般的には、デバイスごとにウェブサイトがレスポンシブであることを保証するために、ビューポートの幅を照会するために使用されます。

メディアクエリは、@mediaルールに続いて括弧内の条件と括弧内の表現によって特徴づけられます。例えば、デバイスのビューポート幅に基づいてdivの背景色を変更したい場合、以下のようにします。

```css
/* モバイル */
@media (max-width: 480px) {
  .mysite {
    background-color: red;
  }
}
```

上記のコード例では、ビューポートの最大幅が480pxになると、クラスがmysiteの<div>に背景色を赤にするように求めています。

**ヒント**：max-widthはデスクトップ優先のデザインを前提としており、より小さいものをターゲットにしています。モバイル優先のデザインでは、より大きな画面をターゲットにするためにmin-widthを使用します。

## コンテナクエリとは？

コンテナクエリは、要素の親コンテナのサイズに基づいて特定のスタイルを適用するためのルールです。これは、ページ内の個々のコンテナ内の変化に応答する能力を望むウェブ開発者の長年の質問に対する答えです。

```css
.header {
   container: mysite / inline-size;
}

@container mysite (min-width: 600px) {
   .maincard {
	   grid-template-column: 1fr 1fr;
    }
   .item {
       background-color: green;
    }
}
```

上記のコードでは、まず変更を加えたいコンテナを定義します。私たちの場合、headerコンテナ内のitemクラスの要素に変更を加えたいとします。コンテナに名前（オプショナル）とタイプを付けることでこれを実現できます。

次に、@containerルールを使用して条件をチェックし、満たされた場合にいくつかのスタイルを適用します。最小幅が600pxの場合、背景色を緑にし、グリッド列を2つにしたいということです。

**ヒント**：コンテナに直接変更を加えるためにコンテナを定義しません。その子に変更を加えるためです。つまり、headerコンテナ自体に変更を加えたい場合、別のコンテナ（例：コンテナA）内にネストし、コンテナAをクエリしてその子（header）に影響を与える必要があります。

## メディアクエリとコンテナクエリの比較

両方の動作を理解した上で、実際の例を見てみましょう。以下のCodePenには、4つの要素がレイアウトされています。最初の2つはコンテナクエリでスタイリングされ、下の2つはメディアクエリでスタイリングされています。ビューポートのサイズを変えて、要素がどのように応答するかを確認できます。

![mqvscq-demo](https://www.freecodecamp.org/news/content/images/2024/06/mqvscq-demo.png)

メディアおよびコンテナクエリのCodePenデモ：Miriam Suzanneに触発されたプロジェクト。

See the Pen [MQ vs CQ (from MS)][8] by Ophy Boamah ([@ophyboamah][9]) on [CodePen][10].

### メディアクエリとコンテナクエリの主な違い

![comparetable](https://www.freecodecamp.org/news/content/images/2024/06/comparetable.png)

主な違いの要約、以下で詳しく説明

### ビューポートベース vs コンテナベース

メディアクエリは、ビューポート（ブラウザ全体のウィンドウ）のサイズに基づいてスタイルを適用します。これは、レイアウトが全体の画面サイズに応じて変化することを意味し、モバイル、タブレット、デスクトップなど、異なるデバイスに合わせてデザインを調整するのに適しています。

一方、コンテナクエリは、配置されているコンテナ要素のサイズに基づいてスタイルを適用します。これにより、個々のコンポーネントはビューポートサイズではなく、自分自身のサイズに応じて外観を調整できるため、ウェブページの異なる部分で非常に柔軟で再利用可能です。

メディアクエリはビューポートのサイズに依存するため、本当にモジュール式のコンポーネントを作成するには効果が薄い場合があります。一部のスタイルを調整すると、特に複雑なレイアウトでは他の部分に思わぬ影響を与えることがあります。加えて、コンポーネントが大きなレイアウト内で独立して適応する必要があるシナリオでは、不十分になることがあります。この結果として、CSSのメンテナンスが難しくなることがあります。

それに対して、コンテナクエリはコンテナのサイズに基づいてスタイルを定義できるため、モジュール性と柔軟性を促進します。これにより、自己完結型で適応力のあるコンポーネントを作成でき、ウェブサイトのさまざまな部分で予期しない変更なしに再利用できます。これにより、再利用性が向上します。

その結果、コンポーネントが自身のレイアウトと外観を調整できる、より適応性の高いデザインが実現します。これは、現代のコンポーネントベースのデザインシステムにおいて非常に有用です。

### 複雑さとメンテナンス

大規模なプロジェクトでは、数多くのメディアクエリを管理するのが厄介になることがあります。ブレイクポイントや特別なケースの数が増えるにつれて、CSSが複雑化し、メンテナンスが難しくなります。時間が経つと、コードベースが膨れ上がり、管理が難しくなることがあります。

コンテナクエリは、大規模なプロジェクトにおけるCSSのメンテナンスを簡素化できます。スタイルをコンポーネント固有かつコンテキストに応じたものに保つことで、CSSはより整理され、モジュール化されます。これにより、グローバルなブレイクポイントの管理の複雑さが軽減され、メンテナンスが容易になり、より整理されたコードベースが実現します。

## どちらを使用すべきか、いつ使用すべきか？

![finalsection](https://www.freecodecamp.org/news/content/images/2024/06/finalsection.png)

メディアクエリ vs コンテナクエリ (画像提供: _[web.dev][11]_)

前のセクションですべて説明したことは、インフォームド・ディシジョンを行うためのものです。これら二つのコンセプトがどう比較されるかを理解した上で、以下の要因を考慮してください:

### 理解と快適さ

それぞれのコンセプトについてどれくらい理解しているか？ コンテナクエリは比較的新しいですが、メディアクエリ同様に、学習と実験に時間を費やせば、学習曲線はそれほど恐ろしいものではありません。したがって、理解が深く、快適に使える方を実際のプロジェクトで使用することで、作業が楽になります。

### プロジェクトの要件と複雑さ

使用しているデザインアプローチは何で、プロジェクトの複雑さはどれくらいか？ プロジェクトの設計アプローチがこれらのどちらが最適かを決定することもあります。さらに、複雑なプロジェクトほどコードのメンテナンスが難しくなるので、管理できるものを使うことが重要です。

### 未来のトレンドとコラボレーション

レスポンシブデザインの未来はますます本質的なものになってきています。個々のコンテンツの変化に基づいてコンポーネントの応答性が求められるようになっており、ここでコンテナクエリが最も活躍します。

しかし、メディアクエリもすぐにはなくならないでしょう。さまざまなデバイスに対する完璧なレスポンシブデザインを実現するために、両方を併用することも可能です。

## 結論

コンテナクエリがCSSで再利用可能なコンポーネントを作成できる可能性は興味深いですが、ウェブページをレスポンシブにするためにメディアクエリを完全に置き換えるにはまだ準備が整っていないかもしれません。

現時点では、両方を使用して、それぞれが最も適した場所で利用するのが最善です。両方の利点と欠点を理解するためにさらに実験することで、適切な判断ができるでしょう。

以下は便利なリソースです：

-   [freeCodeCamp on Media Queries][12]
-   [Ahmad Shadeed on Container Queries][13]
-   [How to Use Media Queries and Container Queries][14]

[1]: #responsive-and-intrinsic-web-design
[2]: #what-are-media-queries
[3]: #what-are-container-queries
[4]: #how-do-media-queries-and-container-queries-compare
[5]: #which-should-you-use-and-when
[6]: #conclusion
[7]: https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design
[8]: https://codepen.io/ophyboamah/pen/YzbaROw
[9]: https://codepen.io/ophyboamah
[10]: https://codepen.io
[11]: http://web.dev/
[12]: https://www.freecodecamp.org/news/learn-css-media-queries-by-building-projects/
[13]: https://ishadeed.com/article/css-container-query-guide/
[14]: https://www.youtube.com/watch?v=2rlWBZ17Wes

