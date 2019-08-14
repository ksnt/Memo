## Next.jsでハローワールド

190812

### 参考サイト

https://blog.bltinc.co.jp/entry/2019/06/20/200000


Next.jsに入門したかったので上記のサイトを参考にさせていただき、環境構築等を行ってみました。
上記サイトと環境は違いますが、同じようにやってみたらできました。ただ、`@zeit/next-typescript`を使うことは推奨されていなかったりというようなことはあるようです。バージョンの違いゆえのことだと思われます。


### 環境

Ubuntu18.04
node v10.16.0
npm 6.9.0

### インストールが前提とされるもの

1. npm
1. node.js
1. git


### 環境構築

作業ディレクトリを作成してGitHubで管理する。

```
$ mkdir myproject
$ cd myproject/
$ git init
$ nano .gitignore
$ cat .gitignore
node_modules/
.next
dist
$ git add .
$ git commit -m "initial commit"
$ git remote add origin git@github.com/user/myproject.git
$ git push --set-upstream origin master
```

環境を初期化
```
$ npm init -y
```

これでmyproject/にpackage.jsonができる。

### ReactとNext.jsをインストール
```
$ npm install --save react react-dom next
```

- memo
sudoをつけないとPermission Errorがでてしまった。`~/.npm/_cacache/...`のファイルが原因らしい

```
$ sudo npm install --save react react-dom next
....
+ react@16.9.0
+ react-dom@16.9.0
+ next@9.0.3
added 628 packages from 296 contributors and audited 9449 packages in 84.071s
found 0 vulnerabilities
```

`package.json`に以下を追記する

```
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "next"    // ここを追加
  },
```


### サーバーサイドレンダリングをしてみる

Next.jsは`pages/`を自動的に読み込んでルーティングするため、`pages/`を`myproject`の下に作成する

```
$ mkdir pages
$ cd pages/
```

ルーティングの`/`は`index.js`に当たるので、`index.js`を作成する

```
import Link from 'next/link'

const Index = () => (
  <div>
    <Link href="/about">
      <a>About Page</a>
    </Link>
    <p>Hello Next.js</p>
  </div>
)

export default Index
```

Next.jsは普通のリンクタグ(おそらく a hrefのこと)では毎回サーバーに問い合わせてしまうらしい。
SAPと同じ動きをさせるためには`Link`タグを使うとよいらしい。

以下のコードによって、最初のレンダリングはサーバーサイドで行われるが、ページ遷移はブラウザで行うような仕組みにできるらしい。このことで、毎度サーバーに問い合わせる必要がないためコンテンツの表示が早くなり、かつ無駄な通信も減らすことできる。（ブラウザへの負荷をかけることにはなる？）

遷移ページ先の/aboutページを`pages/`に`about.js`という名前で作成する

```
const About = () => (
  <div>
    <a>This is About Page</a>
  </div>
)

export default About
```

開発環境を実行してみる。するとこんな感じ。
```
$ npm run dev

> myproject@1.0.0 dev /home/ksn/working_space/sandbox/NextJS_sandbox/myproject
> next

[ wait ]  starting the development server ...
[ info ]  waiting on http://localhost:3000 ...
[ ready ] compiled successfully - ready on http://localhost:3000
[ wait ]  compiling ...
[ ready ] compiled successfully - ready on http://localhost:3000
```

これで`localhost:3000`にアクセスすると`Hello Next.js`と表示され`About`という表示で`/about`へのリンクが張られている。

## TypeScriptを使う

### Typescriptの準備

Typescriptのライブラリをインストールする

```
$ sudo npm install --save @zeit/next-typescript
```

`myproject/`の下に`next.config.js`を作成する。（とりあえず今は何が書かれているのかは分からない）


```
const withTypescript = require('@zeit/next-typescript')
module.exports = withTypescript()

```

次に、`.babelrc`を作成。(とりあえずなぜなのかは分からない)

```
{
  "presets": [
    "next/babel",
    "@zeit/next-typescript/babel"
  ]
}

```

さらに`tsconfig.json`を作成。下記のリポジトリのREADMEを読んで最新の情報を参考にするのが良いらしい。

https://github.com/zeit/next-plugins/tree/master/packages/next-typescript

```
{
  "compilerOptions": {
    "allowJs": true,
    "allowSyntheticDefaultImports": true,
    "jsx": "preserve",
    "lib": ["dom", "es2017"],
    "module": "esnext",
    "moduleResolution": "node",
    "noEmit": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "preserveConstEnums": true,
    "removeComments": false,
    "skipLibCheck": true,
    "sourceMap": true,
    "strict": true,
    "target": "esnext"
  }
}

```

`pages/index.jsx`を`pages/index.tsx`に拡張子を変えて保存する。


この状態で`$ npm run dev`するとエラーが。
```
It looks like you're trying to use TypeScript but do not have the required package(s) installed.

Please install typescript, @types/react, and @types/node by running:

	npm install --save-dev typescript @types/react @types/node
```

エラーメッセージに従い、インストールしてみる。
```
$sudo npm install --save-dev typescript @types/react @types/node
....
+ @types/react@16.9.1
+ @types/node@12.7.1
+ typescript@3.5.3
added 5 packages from 59 contributors and audited 9582 packages in 30.201s
found 0 vulnerabilities
```

出来たっぽいので再度`$ npm run dev`してみる。

すると、

```
@zeit/next-typescript is no longer needed since Next.js has built-in support for TypeScript now. Please remove it from your next.config.js
```
というメッセージが。どうやらNext.jsはもはやTypeScriptのためのビルトインサポートを持っているからだとか。で、参考サイトの方法でインストールしたものは消した方が良いらしい。


ちなみに、`@zeit/next-typescript`を削除しなくても`localhost:3000`で無事「Hello Next.js」という表示を見ることが出来た。

が、削除しておく。

```
$ sudo npm remove @zeit/next-typescript
```

勿論`localhost:3000`のページに変化も問題もない。


