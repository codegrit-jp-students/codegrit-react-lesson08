# Higher Order Component

## 複数のコンポーネントで共有したほうが良いデータやファンクション

例えば、ログインしているユーザーのデータや、データの更新に対する対応を行うファンクションなどは、複数のコンポーネントで実装する機会があります。この際にコンポーネントごとに同じファンクションの呼び出しやログインしているユーザーのデータ取得を行うということも出来ますがコード量も多くなり管理が大変です。

こうしたケースでは、Higher Order ComponentやRender Propsを利用すると便利です。このレッスンではそれぞれについて、使い方を解説していきます。

## Higher Order Componentとは

`Higher Order Component`は、コンポーネントを引数として取り、コンポーネントにデータを付与した上で新しいコンポーネントを返すようなファンクションを指します。

Higher Order ComponentはReactにもとから組み込まれている機能ではなく、Reactコミュニティの中からReactを利用する上でのベスト・プラクティスの一つとして生まれてきました。Higher Order Componentはその名の通り、引数として与えられたコンポーネントより上の改装にあるコンポーネントという意味です。

Higher Order Componentの基本的な書き方は以下の通りです。

```js
import React, { Component } from 'react';

// Higher Order Component

function genHigherOrderComponent = (component) => {
  class HigherOrderComponent extends Component {
    ...コンポーネント内の記述
  }
  return HigherOrderComponent
}

// genHigherOrderComponentを利用するコンポーネント

class SomeComponent extends Component {
  ...コンポーネント内の記述
}

// 作成したSomeComponentを引数としてgenHigherOrderComponentファンクションを返す。
// genHigherOrderComponentは新しいコンポーネントを生成して返す。

export default genHigherOrderComponent(SomeComponent)
```

## Higher Order Componentを使う

Reactに慣れ親しんでいない内は、Higher Order Componentを自分で作成する機会は少ないでしょう。ただ、Reactのライブラリを使う中でHigher Order Componentを使う機会が今後あるかと思います。今後、そのような機会がある時にHigher Order Componentとは何かを理解していないと、そのライブラリが裏で何をしているのか理解できないまま、ただマニュアル通りに使うという状態になってしまいます。これを避けるためにも、Higher Order Componentについて理解を深めましょう。

また、Reactに慣れてきて、複数コンポーネントで似たようなファンクションを利用していたり、共通のデータの取得を何度も行っていると気づいたらHigher Order Componentを少しずつ導入していきましょう。