# チャレンジ8

## 目的

- RenderPropsに慣れる
- を利用してAuthentication(ユーザー認証)を扱う

## チャレンジの取り組み方

1. スターターファイルのリポジトリを、フォークして自分のGitHubアカウントにリポジトリを作りましょう。
2. マイルストーンごとに要件に合うようにファイルを編集していきます。
3. 分からない部分があれば、テキストを復習して、再度チャレンジしてみましょう。
4. 再チャレンジしてしばらく考えても分からない場合はチャットでメンターに質問しましょう。
5. 完了したら、GitHubリポジトリをメンターにシェアしてください。(質問時に既にシェアしている場合は、レビューを直接依頼しましょう。)
6. メンターから課題レビューが届きます。
7. ビデオチャットの際は、分からない点を更に突っ込んで聞いたり、より良い書き方を聞いてみましょう。

## 概要

このレッスンではチャレンジ7で作成したチャットリストに対して、Render Propsを利用して、ログインの有無によって異なる表示を行うようにします。

## 完成イメージ

![codegrit-react-ch08-image](https://firebasestorage.googleapis.com/v0/b/codegrit-images.appspot.com/o/codegrit-react%2FLesson08%2Fchallenge%2Fcodegrit-react-ch08-image.gif?alt=media&token=f76bf26e-f8af-41f6-8358-ff8a6346d6b5)

## スターターファイル

- [codegrit-jp-students/react-ch08-starter](https://github.com/codegrit-jp-students/codegrit-react-ch08-starter)

上記のURL先のリポジトリをフォークして、コードを書き進めて行きましょう。

## マイルストーン１

スターターファイルには、チャレンジ7のファイルに加えて、Auth, LogoutLink, LoginBoxという3つのコンポーネントが既にあります。LogoutLink, LoginBoxの2つは既に完成しているので変える必要はありません。

Authコンポーネント及び、AppコンポーネントにRender Propsを利用して変更を加えて、完成イメージと同じものが出来るようにしましょう。

### 要件

- Authコンポーネントを完成させましょう

Authコンポーネントでは、簡単のためlocalStorageにログインユーザーを保存し、マウント時にlocalStorageからユーザー情報を取り出しています。

既に完成している、loginファンクションと初期stateを参考にして、logoutファンクションを実装しましょう。

また、childrenに対して全ての必要なファンクション、ステートを渡しましょう。

- Appコンポーネントを完成させましょう。

AuthコンポーネントのRender Propsとして、LogoutLink, LoginBox, Chatのそれぞれのコンポーネントを呼び出しましょう。

ログアウトしている場合はLoginBoxのみを、ログイン中はLogoutLinkとChatの両方を表示します。

## 評価

課題の後、以下の２つについてメンターにフィードバックをお願いします。

1. 要件のカバー度: 1.全く出来なかった 2.ほとんど出来なかった 3. 半分ほどは出来た 4.8割ほどは出来た 5. 全部出来た
2. 難易度: 1. とても難しかった 2. 難しかった 3. ちょうど良かった 4. 簡単だった 5. とても簡単だった
