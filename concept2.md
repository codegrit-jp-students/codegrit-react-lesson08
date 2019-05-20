# Render Props

## Render Propsとは

Render PropsはReact16で登場した新しいReactの機能です。その名前の通り、あるコンポーネントに対してrenderというpropsを設定して使います。render propsはReact要素を返すようなファンクションを取り、render propsのあるコンポーネントは、そのコンポーネントの持つrenderファンクションではなく、render propsに設定されたファンクションをrenderファンクションとして呼び出します。

Render Propsは例えば以下のようにHOC的に利用することが出来ます。

```js
class SomeComponent extends React.Component {
  ...省略
  render() {
    // renderというPropsにReact要素を返すファンクションを渡す
    return (
      <GetCurrentUser render={(data) => (
        <p>
          こんにちは、{data.me ? data.me.name : 'ゲスト'}さん
        </p>
      )}>
    );
  }
}
```

上記では、GetCurrentUser内で、ログイン中のユーザーの情報を取得してユーザー情報をstateに保存することを想定しています。あくまで例ですが以下のようなコンポーネントです。

```js
import React, { Component } from 'react'

class GetCurrentUser extends Component {
  state = {
    isLoggedIn: false,
    me: null
  }
  componentDidMount() {
    const isLoggedIn = this.checkIsLoggedIn
    if (isLoggedIn) {
      this.getMe()
      .then((data) => this.setState({ me: data.user}))
    }
  }
  checkIsLoggedIn = () => {
    ...省略
  }
  getMe = () => {
    ...省略
  }
  render() {
    // 以下の部分でrender propsを利用する。このコンポーネントのステートを引数として渡していることに注目。
    return {this.props.render(this.state)}
  }
}

export default GetCurrentUser;
```

上記のように、render propsが役に立つのはrender propsを渡す側のコンポーネントが、複数のコンポーネント間で共有して使いたいようなファンクションを持っており、そのファンクションによって得たstateを利用したい場合です。

## renderではないPropsを利用する

さて、ここまではrender propsという名前の通り、renderというpropsに対してReact要素を返すファンクションを渡してきましたが、実際にはrender propsに使用するpropsはどんなものでも構いません。

ライブラリなどを利用するときによくあるのはchildren propsにファンクションを渡すケースです。そうすると上記のコードは以下のように書き換えることが出来ます。

```js
import React, { Component } from 'react'

class GetCurrentUser extends Component {
  state = {
    isLoggedIn: false,
    me: null
  }
  componentDidMount() {
    const isLoggedIn = this.checkIsLoggedIn
    if (isLoggedIn) {
      this.getMe()
      .then((data) => this.setState({ me: data.user}))
    }
  }
  checkIsLoggedIn = () => {
    ...省略
  }
  getMe = () => {
    ...省略
  }
  render() {
    // children propsに対してstateを渡す。
    return this.props.children(this.state)
  }
}

export default GetCurrentUser;
```

```js
class SomeComponent extends React.Component {
  ...省略
  render() {
    // renderというPropsにReact要素を返すファンクションを渡す
    return (
      <GetCurrentUser children={(data) => (
        <UserMenu data={data} />
      )}>
    );
  }
}
```

## もう一つの書き方

さて、レッスン7で`props.children`は以下のように書けると説明したことを覚えているでしょうか？ 

```js
const SomeComponent = (props) => {
  return (
    <main>
      {props.children}
    </main>
  )
}

const MainComponent = (props) => {
  return (
    <SomeComponent>
      <div>これはchildrenの内容です。</div>
    </SomeComponent>
  );
}

// render propsの元の形で書いた場合
const MainComponent = (props) => {
  return (
    <SomeComponent children={
      <div>これはchildrenの内容です。</div>
    } />
  );
}
```

上記を応用して上記の例を書き換えると以下のようになります。

```js
// 書き換え後
class SomeComponent extends React.Component {
  ...省略
  render() {
    // renderというPropsにReact要素を返すファンクションを渡す
    return (
      <GetCurrentUser>
        {(data) => {
          <UserMenu data={data} />
        }}
      </GetCurrentUser>
    );
  }
}
```

この書き方は、多くのライブラリで利用されているので出会ったときに混乱しないように覚えておきましょう。次のレッスンで学ぶFormikでもこの書き方を利用します。

## Render Propsに対して渡せるものについて

さて、上述の説明では、分かりやすいように、そのコンポーネントのステートを渡すと書きましたが、実際には渡せるものはなんでも構いません。

例えば、getCurrentUserコンポーネントの中で、loginやlogoutファンクションを実装したとすると、通常のコンポーネントと同様に以下のようにしてPropsを渡せます。

```js
render() {
  const props = {
    login: this.login,
    logout: this.logout,
    ...this.state
  }
  return this.props.children(props)
}
```

## HOCとrender propsのどちらを利用するのか

さて、render propsではHOCと同じ機能を実装出来ることを上記で見てきました。では、この2つの内どちらを選べばよいのでしょうか？ 最近では、Reactの正式な機能ということもあり、HOCに変わってrender propsを利用する機会が増えてきています。ただし、render propsは、ネストが深くなりやすい問題も抱えており、コンポーネントを細かく分けてネストを浅くする必要があります。まだ初心者の内は、コンポーネントを上手く分けることに慣れていないこともあるかと思うので、まずはHOCで実装していくのも良いと思います。

## 更に学ぼう

- [React公式 - 高階 (Higher-Order) コンポーネント](https://ja.reactjs.org/docs/higher-order-components.html)
- [React公式 - レンダープロップ](https://ja.reactjs.org/docs/render-props.html#using-props-other-than-render)