# Vue.js
## Vue.jsのツボとコツ　第1章～第3章
### 基礎

[vscode Vue拡張　VSCode+Vue.jsを使用するならインストールするべき拡張機能と設定](https://iwb.jp/vscode-vuejs-extensions-install-settings/)

ESLint *
.eslintrc.jsonにeslint-plugin-vueを忘れずに。※後で調べる


Vue日本公式サイト
https://jp.vuejs.org/v2/guide/

vueダウンロード版
開発最新版
https://jp.vuejs.org/js/vue.js

本番最新版
https://jp.vuejs.org/js/vue.min.js



CDN　

#### jsDelivr
公式サイト　https://www.jsdelivr.com/
開発バージョン最新版
\<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
本番バージョン最新版(警告出力機能なし。軽量)
\<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.min.js"></script>

#### UNPKG
公式サイト　https://www.unpkg.com/
開発最新版
https://unpkg.com/vue/dist/vue.js
本番最新版
https://unpkg.com/vue/dist/vue.min.js

##### 特定のバージョンを利用する場合
jsDelivr
開発バージョン最新版
https://cdn.jsdelivr.net/npm/vue@2.6.6/dist/vue.js
本番バージョン最新版(警告出力機能なし。軽量)
https://cdn.jsdelivr.net/npm/vue@2.6.6/dist/vue.min.js
  
UNPKGも同様にvueの後に  @2.6.6　のバージョン番号を付ける

##### vue.jsを読み込む場所
\<script>タグでHTMLに読み込むだけでOK
記述場所
 - <\head>でもOK。<\/body>直前でもOK
**ただし、Vue.jsのプログラムの記述よりも先に記述すること**

---

Vue.jsを使うとjsのデータとDOMが自動的につながる

```js
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <title>サンプル</title>
  </head>
  <body>
    <div id="app">
      {{price}}円
    </div>
    <script src="https://jp.vuejs.org/js/vue.js"></script>
    <script>
      let app = new Vue({
        el: "#app",
        data: {
          price: 0,
        },
      });
      app.price = 1000; // データを更新する
    </script>
  </body>
</html>
```

---
[Vue material](https://vuematerial.io/)
vue.jsから利用できる
マテリアルデザインのUIコンポーネント集
  
[Bootstrap Vue](https://bootstrap-vue.js.org/)  
CSSとjsのフレームワークbootstrapを、Vue.jsに対応させたもの
  

Vue.js公式サイトのリンクからのリソース集
vue.jsで使えるツールやUIコンポーネントを検索できる
[Vue Curated](https://curated.vuejs.org/)

[Awesome Vue](https://github.com/vuejs/awesome-vue)


---

## リアクティブシステム
データの変化が即座にDOMに反映される

## リアクティブデータ
リアクティブシステムの管理下に置かれたデータのこと


##### マスタッシュ
{{}} vueのテンプレート構文の1つ　※口ひげ

### データバインディング
アプリケーションのデータをDOMと結びつけること
vueのテンプレート構文あ、データバインディングをサポートしている

---

### 条件付きレンダリング

v-if
vielse

```js
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <title>サンプル</title>
  </head>
  <body>
    <div id="app">
      <div v-if="stock==0">売り切れです</div>
      <div v-else>{{price}}円</div>
    </div>
    <script src="https://jp.vuejs.org/js/vue.js"></script>
    <script>
      let app = new Vue({
        el: "#app",
        data: {
          price: 0,
          stock: 0,
        },
      });
      app.price = 1000; // データを更新する
      app.stock = 10; // app.stock=0の時売り切れ表示に
    </script>
  </body>
</html>
```


### リストバインディング
繰り返しのテンプレート構文
v-for="item in list"
```
data: {
          list: [
            { name: '商品A', price: 1000 },
            { name: '商品B', price: 2000 },
            { name: '商品C', price: 980 }
          ]
        }
```


```js
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <title>サンプル</title>
  </head>
  <body>
    <div id="app">
      <ul>
        <li v-for="item in list">{{item.name}}　{{item.price}}円</li>
      </ul>
    </div>
    <script src="https://jp.vuejs.org/js/vue.js"></script>
    <script>
      let app = new Vue({
        el: '#app',
        data: {
          list: [
            { name: '商品A', price: 1000 },
            { name: '商品B', price: 2000 },
            { name: '商品C', price: 980 }
          ]
        }
      });
    </script>
  </body>
</html>
```
---

### F12のElementsとConsoleをデバッグに活用する
consoleで変数への値の代入
ElementsでHTMLに直接干渉できる
jsの途中のデータの確認に活用
  
console.logの場合

```js
    <script>
      // console.log()の活用 2020年4月10日
      let today = new Date();

      let year = today.getFullYear();
      let month = today.getMonth() + 1;
      let day = today.getDate();

      console.log(year + "年" + month + "月" + day + "日");
    </script>
```

#### Vue.js devtools
Chrome拡張機能。F12にVueタブを追加。素早くvueをデバッグ可能
[Vue.js devtools](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=ja)

---

### 基本的なファイル構成
#### 一般的なアプリケーションの設計モデル
MVC
View →　Controller →　Model

#### Vue.jsのアプリケーションの設計モデル
#### MVVM
View ←双方向データバインディング→　ViewModel →　Model
ViewModelはコントローラーと近い役割を担うが、
コントローラー＝描画処理に介入しない
ビューモデル＝データバインディングを通してモデルとビューを自動的に結びつけることができる

### Vue.Jsアプリケーションのファイル構成
Vue.Jsアプリケーションでは、
ビュー：HTMLとCSS
モデル：js
ビューモデル：Vue.js本体
が担当する。ファイル構成は上記の区分けとなる。

### Vue.Jsアプリケーションの雛形

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>サンプル</title>
    <link rel="stylesheet" href="main2_2.css" />
  </head>
  <body>
    <div id="app">
      {{message}}
    </div>
    <script src="https://jp.vuejs.org/js/vue.js"></script>
    <script src="main2_2.js"></script>
  </body>
</html>
```

```js
var app = new Vue({
  el:'#app',
  data:{
    message:'Hello Vue!'
  }
});
```
### Vue.jsのオプション構成と役割

```js

// 100個のボールが画面内を飛び跳ねるjsを作る

// データを全部バラバラに定義する
// 現実的ではない
let x1, x2, x3, ...x1., x100;  // x座標
let y1, y2, y3, ...y1., y100;  // y座標
let sx1, sx2, sx3, ...sx1., sx100;  // 速度のx成分
let sy1, sy2, sy3, ...sy1., sy100;  // 速度のy成分

// データを配列で定義する
// 可読性に問題あり
// 変数を増やす際に名前の重複を避けるため、名前の規則が増え、管理が難しくなっていく
let x = [], y = [] , sx = [], sy []; // 座標と速度

// モノの種類だけ変数が必要になる
let ball_x = [], ball_y = [], ball_sx = [], ball_sy =[]; //ボールの座標と速度
let ball_color = [], ball_size = []; //ボールの色とサイズ
let car_x = [], car_y = [],car_sx =[], car_sy =[]; //自動車の座標と速度
let car_maker = [], car_number =[]; //自動車のメーカーとナンバー
// ...どんどん増えていく。。。
```

##### jsもオブジェクト表記を使えば、オブジェクトが持つプロパティやメソッドを1つの変数で扱えるようになり、コードがスッキリする

・動くモノ(ボール、自動車)：**オブジェクト**
・モノの属性を現す量(座標、速度、色、大きさ)：**プロパティ**
・モノが行う動作(走る、跳ねる、笑う)：**メソッド**

### jsのオブジェクト表記

#### プロパティの定義

オブジェクトのプロパティは次にように定義する
`let obj = { プロパティ値: 値 };`
  
オブジェクトを変数に代入することで、プロパティが参照できるようになる
`obj.プロパティ名`
  
オブジェクトが複数のプロパティを持つ場合は、プロパティ名と値の組み合わせを、半角「,」カンマで区切る
`let obj = { プロパティ名: 値, プロパティ名: 値, プロパティ名: 値 };`
  
  
座標値(X,Y)をプロパティに持つボールオブジェクトは次のように表せる
リスト4

```js
// プロパティを持つオブジェクト

// 元の書式
let ball = {x:10, y:50};

// 改行とインデントで見やすく表示
let ball = { 
  x: 10, 
  y: 50 
};

// 座標をブラウザのコンソールに表示
console.log(ball.x); // =>10が出力される
console.log(ball.y); // =>50が出力される
```
#### オブジェクトの階層化

リスト4のxプロパティとyプロパティは、「座標」という1つのオブジェクトとみなすこともできる。
この座標オブジェクトにposという名前を付けると、pos(※位置)プロパティとしてまとめることができる。
  
リスト5
```js
// オブジェクトの階層化
// 元の書式
let ball = { pos: { x: 10, y: 50 } };

// 改行とインデントで見やすく表示
let ball = {
  pos: {
    x: 10,
    y: 50
  }
};

// 座標をブラウザのコンソールに表示
console.log(ball.pos.x); // =>10が出力される
console.log(ball.pos.y); // =>50が出力される
```
上記のように、オブジェクトを使う側のプログラムからは、「ボール.座標.X成分」のように階層化すると可読性が向上する。
##### Vue構文では階層化されたオブジェクトを使うので覚えておく

---

### メソッドの定義
オブジェクトのメソッドは次のように定義する
`let obj { メソッド名: function(引数){処理} }`

一見異なるように見えるが、**プロパティと書き方はまったく同じ**
 - jsでは関数そのものもオブジェクトとして扱える
 - obj.プロパティ名でプウロパティ値が参照できるのと同様に、obj.メソッド名でメソッドを参照できる

関数をオブジェクトとして扱うときに**関数オブジェクト**という呼び方をすることもある
ただ1つの違いとして、関数には「実行せよ」と指示するための構文が必要
jsで関数を実行するとき、window.alert()やdocument.write()のように記述するが、これはオブジェクトが持つメソッド名に()を付けることで、**参照ではなく実行だ**
ということを表している
`obj.メソッド名(引数);`
  
リスト6　オブジェクトのメソッド
ボールオブジェクトに、ボールを移動させるメソッドを追加する
```js
// リスト6 ボールオブジェクトに、ボールを移動させるメソッドを追加する
let ball = {
  pos: {
    x: 10,
    y: 50
  },
  move: function (x, y) {
    this.pos.x += x;
    this.pos.y += y;
  }
}
// 座標をブラウザのコンソールに出力
console.log(ball.pos.x); // =>10が出力される
console.log(ball.pos.y); // =>50が出力される
// ボールをx方向に5、y方向に3動かす
ball.move(5, 3);
// 座標をブラウザのコンソールに出力する
console.log(ball.pos.x); // =>15が出力される
console.log(ball.pos.y); // =>53が出力される

```

#### オブジェクトの設計図とインスタンス
リスト6で、ballは単なる変数ではなく、プロパティやメソッドを持ったオブジェクトらしい存在とみなせる
しかし、100個のボールすべてについてリスト6のようなオブジェクトをletで宣言しなくてはならない
 - オブジェクトの設計図を1つ作り、それを複製すれば全く同じボールをいくつでも作れる
 - このような考え方を**オブジェクト指向**と呼ぶ
 - オブジェクトの**設計図となる定義をクラス**と呼ぶ
 - クラスをもとに生成したオブジェクトをインスタンス、生成することをインスタンス化と呼ぶ

#### 「動くモノ」クラス

thisはクラス自身を指す。
 - this.posは、このMovableクラスがposという名前のプロパティを持つことの宣言。
 - 同様に、this.moveは、Movableクラスがmoveという名前のメソッドを持つことの宣言
  
MovableクラスにMovable(10,50)のように2つの引数を与えて呼び出すと、this.posの行が**実行され**、このとき引数がそのままposプロパティのx,yに代入される
つまり、Movableクラスから生成したオブジェクトのposプロパティの初期値になる
  
また、Movableクラスから1つのボールインスタンスを生成する
リスト7,8
```js
// リスト7,8 Movableクラスからインスタンスを生成する
// 「動くモノ」クラスの定義
let Movable = function (x, y) {
  this.pos = {
    x: x,
    y: y
  };
  this.move = function (x, y) {
    this.pos.x += x;
    this.pos.y += y;
  };
}
// ボールのインスタンスを生成する
let ball = new Movable(10, 50); // =>最初の座標値を指定
// ボールをx方向に5、y方向に3動かす
ball.move(5, 3);
// 座標をブラウザのコンソールに出力する
console.log(ball.pos.x); // 15
console.log(ball.pos.y); // 53

```
クラスのインスタンスを生成するには、クラス名と同じ名前の関数にnewを付けて呼び出す。
上記のように、インスタンスを生成する特別な役割を持つ関数をコンストラクタ(※構築する人やモノ)と呼ぶ
##### newで生成したインスタンスは、letで宣言した変数に代入しておく
`let obj = new クラス名(引数);`
クラスが引数を持つかどうかは、クラスの仕様によるが、多くの場合、
インスタンス化したオブジェクトが持つプロパティに初期値を与える目的で引数が使われる

#### Movableクラスからインスタンスを生成する
##### ブラウザの画面のランダムな位置に100個のボールを描画する
リスト9
```js
////////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////////
// リスト9 Movableクラスからインスタンスを生成する
// ブラウザの画面のランダムな位置に100個のボールを描画する
// ボールは<div>●</div>で表現し、CSSでオブジェクトのプロパティと結びつける

// 「動くモノ」クラスの定義
let Movable = function (x, y) {
  this.pos = {
    x: x,
    y: y
  };
  this.move = function (x, y) {
    this.pos.x += x;
    this.pos.y += y;
  };
}
// ボールオブジェクトを格納する空の配列を用意する
let ball = [];
// 100個分の繰り返し
for (let i = 0; i <= 100; i++) {
  // ボールオブジェクトのインスタンスを生成する
  ball[i] = new Movable(
    Math.floor(Math.random() * window.innerWidth),
    Math.floor(Math.random() * window.innerHeight)
  );
}
// ボールをブラウザに描画する
// Document インターフェイスはブラウザーに読み込まれたウェブページを表し、 DOM ツリーであるウェブページのコンテンツへのエントリーポイントとして働きます。
// DOM ツリーは <body> や <table> など、多数の要素を持ちます。これはページの URL を取得したり文書で新たな要素を作成するなど、文書全体に関わる機能を提供します。

for (let i = 0; i <= 100; i++) {
  // style="top:**px; left:**px;"
  document.write('<div class="ball" style="top:' + ball[i].pos.y + 'px; left:' + ball[i].pos.x + 'px; ">●</div>');
}
```
```css
.ball {
  position: absolute;
  color: #b3a3e7;
}
```
#### Vueのオプション構成
Vueでは、上記のようなボールのような単体のオブジェクトを**コンポーネント**と呼ぶ
1つ以上のコンポーネントを組み合わせたものがアプリケーションであると考える
以後、**コンポーネントと呼んだ場合、1個のボールオブジェクトのことをイメージする**
  
##### Vueアプリケーションは、`new Vue({...})`でコンポーネントを作成することから始まる
 - **Vue**はフレームワーク側で定義されているクラスで、コンポーネントの中で使うデータやメソッドはあらかじめ引数として渡す
   - この場合、引数は単純な数値や文字列では扱いきれないので、役割に応じた名前を持つプロパティとして、オブジェクト表記を使う

そのため、**Vueクラスは、new Vue(x,y, ...)ではなく `new Vue({...})`のようにコンストラクタの引数にオブジェクトを受け取る**ことになっている
```js
//書式
let obj = new Vue({オブジェクト});
```
ただ、どんなオブジェクトでも渡せるわけではない
Vueクラスの中で定められている、決まった名前のプロパティを持っている必要がある
|プロパティ名|役割|
|-|-|
|el|コンポーネントのインスタンスをどのHTML要素に結びつけるかを定義する|
|data|コンポーネントが保持するデータを定義する|
|methods|コンポーネントが持つメソッドを定義する|
|filters|コンポーネントが持つフィルターを定義する|
|computed(※有償)|コンポーネントが持つ算出プロパティを定義する|
|watch|コンポーネントが持つウォッチャを定義する|
|※注※|コンポーネントのライフハックサイクルを定義する|
```js
// 書式
let app = new Vue({ プロパティ名: 値, プロパティ名: 値, プロパティ名: 値, ...});
```
  
具体的には以下のようなコードとなる
##### リスト10 Vueのオプション構成
```js
let app = new Vue({  // Vueクラスをappに代入
  el: '#app',
  data: {
    // コンポーネントが保持するデータをここに定義する
  },
  methods: {
    // コンポーネントが持つメソッドをここに定義する
  },
  filters: {
    // コンポーネントが持つフィルターをここに定義する
  }, compted: {  //(※有償)
    // コンポーネントが持つ算出プロパティをここに定義する
  }, watch: {
    // コンポーネントが持つウォッチャをここに定義する
  }
});
```
ほかにも、
- props.....コンポーネント間でデータを受け渡すをする
 - 独自のディレクティブを定義できる.....directives
など、多くのプロパティがサポートされている
これらのプロパティを特に**オプション**と呼ぶ(口語として)
公式ガイドで上記の用法を確認できる

#### elオプション
elオプションは、`new Vue{(...)}`で生成したコンポーネントのインスタンスをHTML要素に結びつけるためのプロパティ
リスト11　elオプションの書式例
```html
html
<div id="ball">●</div>
```
```js
js
let ball = new Vue({
  el: '#ball'
});

```
##### elプロパティの値には、結びつけたいHTMLCSSセレクタか、HTML要素を返す関数を記述できる
リスト11と同じことを関数で記述した場合
リスト12 elオプション(関数で指定)
```html
html
<div id="ball">●</div>
```
```js
js
let ball = new Vue({
  el: document.querySelecter('#ball')
});

```
### オプション、プロパティ、オブジェクトについて
オプション...便宜上使われる
しかし、
jsでは**elはプロパティ名**であり
`{el:"#app"}`はelプロパティと値をセットにした**オブジェクト**である
#### - el.....プロパティ名
#### - `{el:"#app"}`.....オブジェクト

---

#### dataオプション
リスト13　dataオプションにデータを定義する
HTMLのテンプレート側にマスタッシュで\{{$data}}と記述すると、現在のdataオプションの内容が出力される。
\<pre>タグで囲むと整形された表示が得られるので活用する


```js
let ball = new Vue({
  el: '#ball',
  data: {
    pos: {
      x: 0, y: 0
    },
    radius: 20
  }
});

// ボールをx方向へ100px,y方向へ100px動かす
ball.move(100,100);

// ボールの半径を40pxに変更する
ball.radius = 40;
```
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>サンプル</title>
    <link rel="stylesheet" href="main2_3_9.css" />
  </head>
  <body>
    <div id="ball">
      <pre>{{$data}}</pre>
    </div>
    <script src="https://jp.vuejs.org/js/vue.js"></script>
    <script src="main2_3_13.js"></script>
  </body>
</html>
```

#### methodsオプション
methodsオプションには、コンポーネント(ボール)が持つメソッドを定義する
1つ1つのメソッドは、オブジェクト表記で「`メソッド名:関数定義`」のようにあらわす
ボールコンポーネントにmoveメソッドを追加する
リスト14　methodsオプションにメソッドを定義する
```js
let ball = new Vue({
  el: '#ball',
  data: {
    pos: {
      x: 0, y: 0
    },
    radius: 20
  },
  methods: {
    move: function (x, y) {
      this.pos.x += x;
      this.pos.y += y;
    }
  }
});

```
#### ライフサイクルハック
ライフサイクルハックは、
 - コンポーネントがDOMと結びついた瞬間
 - DOMからコンポーネントが削除された瞬間
など、いくつかの特殊なタイミングでVueが自動的にコンポーネントへ通知を送ってくれる仕組み
  
ライフサイクルハックをコンポーネントに定義するには「`ハック名:関数定義`」
のようにオブジェクト表記を使う
ただしハック名は、あらかじめ決まっている
##### コンポーネントの一生
生成前　＞　生成後　＞　連結前　＞　連結後　＞　更新前　＞　更新後　＞
破棄前　＞　破棄後
↑それぞれにVueを通知
  
#### コンポーネントのライフサイクルハック
|サイクル|ハック名|発生するタイミング|
|-|-|-|
|生成前|beforeCreate|コンポーネントのインスタンスが生成された直後|
|生成後|created|コンポーネントのインスタンスが生成され、Vueがコンポーネントのリアクティブデータを監視する準備が終わった時|
|連結前|beforeMount|コンポーネントのインスタンスがDOMと結びつくとき|
|連結後|mounted|コンポーネントのインスタンスがDOMと結びついた直後|
|更新前|beforeUpdate|コンポーネントが持つリアクティブデータが更新され、DOMに反映される前|
|更新後|updated|コンポーネントが持つリアクティブデータが更新され、DOMに反映された直後|
|破棄前|beforeDestroy|コンポーネントのインスタンスが破棄される直前|
|破棄後|destroyed|コンポーネントのインスタンスが破棄される直後|


#### ライフサイクルハックを使った初期化
コンポーネントのデータを初期化したいとき、単純な数値や文字列ならdataオプションンに直接記述すれば済むが、
サーバーからデータを読み込むような複雑な処理が必要な場合は、dataオプションでは対応できない
**そのような場合、createdライフサイクルハックに初期化処理を記述する
  
リスト15　ライフサイクルハックを使った初期化
```js
// リスト15 ライフサイクルハックを使った初期化
let ball = new Vue({
  el: '#app',
  data: {
    products: []
  },
  created: function () {
    // 商品リストをサーバーから読み込み、this.productsに代入する
  }
});

```
#### ディレクティブ
コンポーネントを結び付けたHTML要素はVueの監視下に置かれ、
「`-v`」で始まる独自の属性を併用することで様々な機能が利用できる。
これらを**ディレクティブ**と呼ぶ
##### 「`v-bind`」は、コンポーネントのデータとHTML要素を同期させる代表的なディレクティブ
  
#### スコープ
javaのスコープと同じ。有効範囲
```js
// リスト16 変数のスコープ
function sample(){
  let x =10;
}
// 以下はスコープの範囲外
console.log(x); // =>Uncaught ReferenceError: x is not defined
```
変数xは{...}の内部でしか参照できない
ローカルスコープ.....関数の中でのみ有効
グローバルスコープ.....関数の外側のどこからでも参照できる
グローバルスコープの注意点は、ほかの開発者やほかのライブラリと変数名が重なると誤作動を起こす
原則ローカルスコープを使ったほうが、コンポーネントの独立性が保たれ、使いやすい、拡張しやすい部品になる

---

## レンダリング(ページを描画する)
### テキストにバインドする
HTMLのテキスト部分にマスタッシュで\{\{ プロパティ名 }}を記述すると、アプリケーションの**dataオプションに定義したプロパティの値が、その場所に置き換わって出力**される

```html
html

{{ プロパティ名 }}

```
・リスト2_4_1　テキストの出力
・リスト2_4_2 式を使った出力
```html
html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script src="https://jp.vuejs.org/js/vue.js"></script>
  </head>
  <body>
    <!-- リスト2_4_1 テキストの出力
<div id="app">
  {{message}}
</div> -->

    <!-- リスト2_4_2 式を使った出力 -->
    <!-- リスト2_4_2 式を使った出力
 {{ ... }}にはjsの式も記述できる。
 以下は三項演算子を使った例 -->
    <div id="app">
      {{lang == 'ja' ? message_ja : message_en}}
    </div>
    <script src="main2_4_1.js"></script>
  </body>
</html>
```
```js
// // リスト2_4_1 テキストの出力
// let app = new Vue({
//   el: '#app',
//   data: {
//     message: 'こんにちは'
//   }
// });

// リスト2_4_2 式を使った出力
let app = new Vue({
  el: '#app',
  data: {
    message_en: 'Hello!',
    message_ja: 'こんにちは!',
    lang: 'ja'
  }
});
```

三項演算子
`条件式 ? 条件成立の場合に実行する式 : 不成立の場合に実行する式`

#### 制御用のプロパティを活用する
上記のlang:のように表示内容を切り替えるためのプロパティを用意すればコードが後々スッキリする
表示内容が決まっている（メッセージの値）はなるべく直接変更しない
  
式が長く複雑になる場合は、後述の算出プロパティの利用を検討する

### 属性にバインドする
```html
html

<要素名 v-bind: 属性名="プロパティ名">

属性にバインドするには、バインドしたいデータのプロパティ名を属性の値に記述し、属性名の前に v-bind を付ける
```
  
```html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script src="https://jp.vuejs.org/js/vue.js"></script>
  </head>
  <body>
    <div id="app">
      <!-- <input type="text" v-bind:value="こんにちは"　と表示される /> -->
      <input type="text" v-bind:value="message" />
    </div>

    <script src="main2_4_3.js"></script>
  </body>
</html>
```

```js
let app = new Vue({
  el: '#app',
  data: {
    message: 'こんにちは'
  }
})
```

### \{\{...}}は属性には使えない
\{\{...}}はマスタッシュと呼ばれる特殊なテンプレート構文
 - **要素内容にバインドするときだけ**使える
 - **属性にバインドしたいときは、プロパティ名を\{\{...}}で囲まない**こと

### スタイル(style)属性にバインドする
要素に直接スタイルシートを指定する場合、`style="CSSプロパティ名:値;"`と記述するが、
Vue.jsをバインドしたいときは、CSSのプロパティ名をキャメルケースに置き換える
値にはバインドしたいアプリケーションのプロパティ名を記述する
```
<要素名 v-bind:style="{CSSのプロパティ名(キャメルで): アプリケーションのプロパティ名}">
```
  
文字の表示サイズをバインドする例
リスト2-4-4　style属性にバインドする
下記の場合、40pxをバインドさせている
```html
html

    <script src="https://jp.vuejs.org/js/vue.js"></script>
  </head>
  <body>
    <div id="app">
      <!-- リスト2-4-4　style属性にバインドする -->
      <!-- <p style="fontsize: 40px;">文字サイズは40pxです</p>を出力する -->
      <p v-bind:style="{fontsize: pSize}">文字サイズは{{pSize}}です</p>
    </div>
```
```js
// リスト2-4-4　style属性にバインドする
let app = new Vue({
  el: '#app',
  data: {
    pSize: '40px'
  }
});
```
#### 複数のスタイルをまとめて指定するとき
HTMLでは
`style="font-size:30px; color: red;"`
のように;で区切るが、

Vueでバインドする場合は
`{fontSize:pSize, color: pColor;}`
のようにカンマで区切る
※つまりjsのオブジェクト表記そのものの書き方で記述する

### クラス(class)属性にバインドする
class属性にバインドするときもオブジェクト表記を使う
`<要素名 v-bind:class="{class名(キャメルケース): class名を出力する条件式}">`
style属性にバインドするときとの違いは、オブジェクトの値が「そのclass名を出力するための条件を表す」という点
ただし、テンプレートに長文を書くと可読性が低下するので、
**条件式を実行した結果をdataオプションのプロパティに持たせて、プロパティ名を代わりに記述する**とシンプルになる
  
リスト2-4-5　クラス属性にバインドする
```html
    <title>Document</title>
    <link rel="stylesheet" href="main2_4_5.css" />
    <script src="https://jp.vuejs.org/js/vue.js"></script>
  </head>
  <body>
    <!-- リスト2-4-5　class属性にバインドする -->
    <!-- 要素の先頭文字だけをcapitalizeで大文字に変換 -->
    <div id="app">
      <p v-bind:class="{capitalize: isCapital}">hello vue!</p>
    </div>
```
```js
// リスト2-4-5　class属性にバインドする
let app = new Vue({
  el: '#app',
  data: {
    isCapital: true
  }
});
```

```css
.capitalize {
  text-transform: capitalize;
}
```


上記は、要素の先頭文字だけを大文字に変換するスタイルに**capitalizeというclass名を付け**、このclass名を出力するかどうかをisCapitalというプロパティにに保持させた例
DOMには以下が出力され、ブラウザにはHello Vue が描画される
`<p class="capitalize">hello vue!</p>`
ブラウザのコンソールでapp.isCapitalの値をfalseにすると、pタグの出力内容も、ブラウザの描画内容も小文字に戻る
  
isCapitalがtrueならオン、falseならオフ役割
**isCapitalがtrueなら、HTMLのpタグ内のclass名が出力**され、
**falseなら出力されない(よってCSSの効果が出ない)**

  
### リストデータをバインドする
リストとは複数のデータを1つにまとめて扱いやすくしたもの
jsでは配列を使って表す
v-forを使うと、要素の配列データをバインドできる
`<要素名 v-for="配列要素を代入する変数名 in 配列の変数名">...</要素名>`
  
リスト2-4-6　リストデータをバインドする
```html
  <body>
    <!-- リスト2-4-6　リストデータをバインドする -->
    <div id="app">
      <table border="1">
        <tr>
          <th>商品コード</th>
          <th>商品名</th>
        </tr>
        <!-- 繰り返しが実行されている間、itemにはproductsの配列要素である商品1件文のオブジェクトそのものを指す -->
        <tr v-for="item in products">
          <td>{{item.code}}</td>
          <td>{{item.name}}</td>
        </tr>
      </table>
    </div>
```

```js
// リスト2-4-6　リストデータをバインドする
let app = new Vue({
  el: '#app',
  data: {
    products: [
      { code: 'A01', name: 'プロダクトA' }, //配列要素[0]
      { code: 'B01', name: 'プロダクトB' }, //配列要素[1]
      { code: 'C01', name: 'プロダクトC' } //配列要素[2]
    ]
  }
});
```

配列要素には数値や文字列などのデータ以外にも、オブジェクトを入れることもできる
```
[オブジェクト,オブジェクト,オブジェクト]

[{プロパティ名: 値}, {プロパティ名: 値}, {プロパティ名: 値}]

[
  {プロパティ名: 値}, 
  {プロパティ名: 値}, 
  {プロパティ名: 値}
]
```
リスト6のようにオブジェクトが複数のプロパティを持つ場合は、カンマで区切る
これにproductsというポロパティ名を付けて、dataオプションのプロパティにすると、リスト6になる
  
繰り返しが実行されている間、itemにはproductsの配列要素である商品1件文のオブジェクトそのものを指す
そのため、すべての商品の商品コードはitem.codeで参照でき、\{\{item.code}}と記述した場所にバインドされる
#### v-forの「配列要素を代入する変数名」はなんでもOK
リスト6ではitem
一般的にはitem,element,ele のように、それが配列要素とわかる変数名が使われる
複数形productsのsを外して`v-for="product in products"` としても良い

### 重要　繰り返す要素にはKeyを指定する
単純な配列データを描画するだけならリスト6でよいが、問題が起こる
画面に削除ボタンがあって、1件目のデータを削除した場合
 - A01の行がDOMからは削除されない。VueはA01へB01を移し替え、B01へC01を移し替える。
 - そして最後にC01のノードだけを削除する。効率的に描画するために、ノードの移動や削除を抑え、なるべく使いまわそうとする
 - その結果、バインドしている配列の要素番号インデックスとDOMノードがずれてしまい、配列要素の並び替えや追加を行ったときに正しく動作しない原因となる
##### 上記の問題を回避するために
v-forで繰り返す1つ1つの配列要素を区別できる値を、keyという名前の属性を使ってバインドすることが**公式でも強く推奨**されている
リスト6の場合は、商品コードで配列要素を区別できるので、次のように書き換える
  
リスト7　繰り返して出力する要素にkeyを指定する
```html
  <body>
    <!-- リスト2-4-7　繰り返して出力する要素にkeyを指定する -->
    <div id="app">
      <table border="1">
        <tr>
          <th>商品コード</th>
          <th>商品名</th>
        </tr>
        <tr v-for="item in products" v-bind:key="item.code">
          <td>{{item.code}}</td>
          <td>{{item.name}}</td>
        </tr>
      </table>
    </div>
```

### 条件付きで描画する
v-if
v-show
##### v-if
v-ifを記述した要素は、
 - 条件式が成立した場合...DOMに出力される
- 条件式が成立しない場合...DOMに出力されない
`<要素名 v-if="条件式">条件式が成立する場合の出力内容</要素名>`
  
データが特定の条件を満たした場合だけ出力する例
リスト8　v-ifの使用例
```html
  <body>
    <!-- リスト2-4-8　データが特定の条件を満たした場合だけ出力する例 -->
    <!-- priceが1000未満：文字列を表示 -->
    <!-- priceが1000以上の場合：v-ifの条件式を満たさないので、span要素そのものが出力されない -->
    <div id="app">
      {{price}}円<span v-if="price < 1000">セール実施中！</span>
    </div>
```

```js
// リスト2-4-8　データが特定の条件を満たした場合だけ出力する例
let app = new Vue({
  el: '#app',
  data: {
    price: 980
  }
});
```
 - priceが1000未満：文字列を表示
 - priceが1000以上の場合：**v-ifの条件式を満たさないので、span要素そのものが出力されない**

#### 複数の条件式を指定する(v-if,v-else-if,v-else)
```
<要素名 v-if="条件式">条件式が成立する場合の出力内容</要素名>
<要素名 v-else="条件式">条件式が不成立の場合の出力内容</要素名>

<要素名 v-if="条件式1">条件式1が成立する場合の出力内容</要素名>
<要素名 v-else-if="条件式2">条件式2が成立する場合の出力内容</要素名>
<要素名 v-else=条件式1も2も不成立の場合の出力内容</要素名>
```
  
**商品に在庫があれば在庫数を表示し、在庫がなければ「在庫切れです」を表示する例（リスト9）**
リスト9　v-if,v-elseの使用例
```html
  <body>
    <!-- リスト2-4-9　商品に在庫があれば在庫数を表示し、在庫がなければ「在庫切れです」を表示する例 -->
    <div id="app">
      <span v-if="stock >= 1">残り{{stock}}個です</span>
      <span v-else>在庫切れです</span>
    </div>
    <script src="main2_4_9.js"></script>
  </body>
```

```js
// リスト2-4-9　商品に在庫があれば在庫数を表示し、在庫がなければ「在庫切れです」を表示する例
let app = new Vue({
  el: '#app',
  data: {
    stock: 10
  }
});
```

#### まとまった範囲を切り替えるにはtemplate
広い範囲をまとめて切り替えたい場合<\tamplate>を使う
```
<tamplate v-if="条件式">
...
...
</template>
```
#### templateタグはDOMに出力されない
<\tamplate>はVue独自のものではなく、HTML5で策定されたタグ
tamplateタグで囲った部分をテンプレートとして、jsなどのスクリプトによって
新たにHTMLを挿入、複製したりするために使う
上記の理由からtemplateタグ自身はブラウザに出力されない
### v-show 条件式が成立する場合だけ要素を表示する
v-showを記述した要素は、**指定した条件式が成立する場合だけ表示され、不成立の場合は表示されない**
`<要素名 v-show="条件式">条件式が成立する場合の表示内容</要素名>`
  
次の例では、価格の後ろにセール実施中は表示されないが、DOMには出力される(リスト10)
リスト10　v-showの使用例
```html
    <!-- リスト2-4-10　価格の後ろにセール実施中は表示されないが、DOMには出力される -->
    <div id="app">
      {{price}}円<span v-show="price < 1000">セール実施中</span>
    </div>
    <script src="main2_4_10.js"></script>
  </body>
```
```js
// リスト2-4-10　価格の後ろにセール実施中は表示されないが、DOMには出力される
let app = new Vue({
  el: '#app',
  data: {
    price: 1280
  }
});
```
##### v-ifの場合
 - 条件式が成立した場合：DOMに出力される
 - 成立しない場合：DOMに出力されない(代わりにHTMLのコメント記号<\!---->が出力される)
##### v-showの場合
 - 条件式が成立した場合：必ずDOMに出力される
 - 成立しない場合：**必ずDOMに出力される(画面はdisplay:noneのスタイルが適用されることで非表示になる)**

#### 注意
 - **v-showは、v-else-ifやv-elseと組み合わせて複数の条件式を指定できない**
 - **templateタグにv-showを使うこともできない**

##### v-showの特徴
```
・要素はDOMに出力される(CSSのdisplay:noneで非表示になるだけ)
・v-else-ifやv-elseと組み合わせできない
・<template v-show="..."></template>と喜寿することはできない
```
#### v-ifとv-showの使い分け
- DOMの更新はブラウザにとって負担が大きい
 - タブで表示内容を切り替えるような場面で使うと、タブ切り替えのたびにノードの追加と削除が発生してしまう
 - v-showのほうが高速に描画(DOMは更新されずCSSで画面非表示にしてるだけなので)。
リスト10のように、**表示されたページの中で、ユーザーが操作を行ってもデータの状態が変わらない場合は、v-ifを使っても良い**

## フィルター(描画用にデータを加工する)
フィルターとは、マスタッシュ{{...}}でテンプレートにバインドしたデータがテキストとして出力される前に、何らかの加工を加えることができる機能のこと
  
例
・1,280円のカンマ区切り
・小数点以下の端数を丸める
   
上記の機能を、**元のデータには一切変更を加えずに、描画するときだけ加工できる**ので便利

#### グローバルスコープにフィルターを登録する
汎用的なフィルターは、Vue.jsが用意してくれる`Vue.filter()`メソッドを使ってグローバルスコープに登録すると、すべてのコンポーネントから共通で利用できるようになる
`Vue.filter( フィルター名, 関数オブジェクト);`
第一引数はフィルター名、第二引数には**具体的な加工を行う関数**を記述
  
金額を3桁ずつカンマで区切った書式で出力するフィルターを作成し、グローバルスコープに登録する
リスト2-5-1　フィルターを登録する
```js
// リスト2-5-1　金額を3桁ずつカンマで区切った書式で出力するフィルターを作成し、グローバルスコープに登録する
Vue.filter('number_format', function (val) {
  return val.toLocaleString();
});

let app = new Vue({
  el: '#app',
  data: {
    price: 1000
  }
});
```
Vue.filter()は、new Vue()実行よりも前に定義すること
順番を逆にした場合、コンソールエラーになる
```
※Vue warn:Failed to resolve filter:number_format
※number_formatという名前のフィルターの解決に失敗した
```

テキストにバインドしたデータにフィルターを適用する場合は、次のように書く
`{{ プロパティ名 | フィルター名 }}`
`{{ price | number_format }}`
```
    <div id="app">
      <!-- 2-5-2　フィルターを適用する -->
      {{ price | number_format }}
    </div>
```
    
要素の属性にバインドしたデータにフィルターを適用する場合は、次のように書く
`<要素名 v-bind:属性名="プロパティ名 | フィルター名">`

```html
  <body>
    <!-- リスト2-5-1　金額を3桁ずつカンマで区切った書式で出力するフィルターを作成し、グローバルスコープに登録する -->
    <div id="app">
      <!-- 2-5-2　フィルターを適用する。1,000を表示 -->
      {{ price | number_format }}
    </div>
    <script src="main2_5_1.js"></script>
  </body>
  ```

### ローカルスコープにフィルターを登録する
filterオプションを使ってコンポーネントの中に登録したフィルター※は、そのコンポーネントの中だけで使えるローカルスコープとなり、ほかのコンポーネントからは隠蔽される
```js
※参考
let app = new Vue ({
  el: '#app',
  filters: {
  //コンポーネントが持つフィルターをここに定義
  }
});
```
特定のコンポーネントの中だけで使う固有のフィルターは、ならべくローカルスコープに登録したほうが、コンポーネントの独立性を保てる
  
リスト1と全く同じフィルターをコンポーネント内に登録すると以下のようになる
リスト　2-5-3
```js
let app = new Vue({
  el: '#app',
  data: {
    price: 1000
  },
  // 2-5-3 リスト1と同じフィルターをコンポーネントの中に登録する
  filters: {
    number_format: function (val) {
      return val.toLocaleString();
    }
  }
});
```
##### filtersオプションは、その中に定義するプロパティの値が関数オブジェクトである点を除くと、dataオプションと構造は同じ
```
・new Vue({...})の{...}はオブジェクト
　・el、data、filtersはそれぞれのオブジェクトが持つ「プロパティの名前」
　・filters{...}の{...}もオブジェクト
　・number_formatはそのオブジェクトが持つ「プロパティの名前」
　　・number_formatプロペティの値であるfunctionは関数オブジェクトだが、「オブジェクト」であることに変わりはない
```
書式
`filters: { フィルター名 | 関数オブジェクト }`
##### 複数のフィルターを繋げる
2つ以上のフィルター名を「|」で繋ぐと、フィルターが連鎖的に適用される
適用される順番は、左から右になる
```html
書式
複数のフィルターを繋げる
{{ プロパティ名 | フィルター名 | フィルター名 }}

属性にバインドする場合も同様
<要素名 v-bind:属性名="プロパティ名 | フィルター名 | フィルター名">
```
  
リスト3を拡張して、通貨単位の「円」を付けた描画に対応させる
リスト4　フィルターを組み合わせて使用する
```html
  <body>
    <div id="app">
      <!-- リスト4　フィルターを組み合わせて使用する -->
      <!-- 1000円　1,000円と表示される -->
      {{price | unit}} {{ price | number_format | unit}}
    </div>
    <script src="main2_5_4.js"></script>
  </body>
```
```js
let app = new Vue({
  el: '#app',
  data: {
    price: 1000
  },
  // 2-5-4 フィルターを組み合わせて使用する
  filters: {
    // 金額を3桁カンマ編集するフィルター
    number_format: function (val) {
      return val.toLocaleString();
    },
    unit: function (val) {
      return val + '円';
    }
  }
});
```
1つのフィルターにいろんな加工をさせるよりも、**小さな加工を行うフィルターを別々に登録したほうが、テンプレート側で使い分けがしやすくなる**

### 算出プロパティ（再利用可能な加工済みデータ）
#### 算出プロパティとは？
算出プロパティは、**アプリケーションのデータに基づいて何らかの加工を行った結果を返すプロパティ**
 - 通常のプロパティと同じように使える
 - マスタッシュ{{...}}で単純に出力するだけでなく、配列を返す算出プロパティを定義すれば、v-forでリストデータを繰り返し出力する場面にも使える

```
書式
//算出プロパティはコンポーネントのcomputed(※計算された)オプションの中に定義する
compted: { 算出プロパティ名: 関数オブジェクト }
```
  
今年がうるう年かどうかを判定する算出プロパティを定義する
リスト2-6-1　今年がうるう年かどうかを判定する算出プロパティ
```html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script src="https://jp.vuejs.org/js/vue.js"></script>
  </head>
  <body>
    <div id="app">
      <!-- リスト2-6-1　今年がうるう年かどうかを判定する算出プロパティ -->
      調べたい年：<input type="text" v-model="year" /><br />
      {{year}}年は{{isUrudoshi ? 'うるう年です' : 'うるう年ではありません'}}
    </div>
    <script src="main2_6_1.js"></script>
  </body>
</html>
```

```Js
let app = new Vue({
  el: '#app',
  data: {
    year: (new Date()).getFullYear()
  },
  computed: {
// リスト2-6-1　今年がうるう年かどうかを判定する算出プロパティ
    isUrudoshi: function () {
      // うるう年=「4で割れて100で割り切れない」または「400で割り切れる」場合
      if ((this.year % 4 == 0) && (this.year % 100 != 0) || (this.year % 400 == 0)) {
        return true;
      } else { //うるう年ではない
        return false;
      }
    }
  }
});
```
テンプレートにisUrudoshiと記述するだけで、複雑な判定ができる
  
### 算出プロパティはキャッシュされる
算出プロパティが**テンプレートやメソッドの中で参照されると、Vueはその時の値をキャッシュ（記憶）する**
 - そして再び同じ算出プロパティが参照されたとき、キャッシュから値を取り出す(参照のたびに同じ処理を行うのは無駄なので)
しかし、算出プロパティの中で使っている**リアクティブデータ※が更新されると、Vueはキャッシュをしてて算出プロパティを再度実行する**
Vueは算出プロパティとリアクティブデータの依存関係を常に監視している
※リアクティブデータ：データの変化が常にDOMに反映されるリアクティブシステムの管理下に置かれたデータのこと
  
算出プロパティがキャッシュされる様子を確認するために、以下の例を見る
リスト2-6-2　リアクティブデータと依存関係のない算出プロパティ
```html
    <div id="app">
      <!-- リスト2-6-2　リアクティブデータと依存関係のない算出プロパティ -->
      <div v-show="show">
        <p>now1: "{{ now1() }}"</p>
        <p>now2: "{{ now2 }}"</p>
      </div>
    </div>
```
```js

let app = new Vue({
  el: '#app',
  data: {
    show: true
  },
  methods: { //メソッド
    // 現在日時を返すメソッド
    now1: function () {
      return (new Date()).toLocaleString();
    }
  },
  computed: { //算出プロパティ
    // 現在日時を返す算出プロパティ
    now2: function () {
      return (new Date()).toLocaleString();
    }
  }
});
```
上記を実行すると、now1,2ともに同じ日時が表示されるが
ブラウザのコンソールから
app.show=false　を入力後、
app.show=true　で再度日時を表示すると
**now1は日時が更新される** = **メソッドは再描画のたびに更新(再実行)**されている
**now2は日時が更新されない(最初の表示のまま)** = **算出プロパティはキャッシュ**されている
算出プロパティは依存関係のあるリアクティブデータが更新されない限りキャッシュが参照され続けることを示している
 - 算出プロパティ now2 は現在日時をフォーマットして返しているだけで、**dataオブジェクトに定義しているリアクティブデータshowとの依存関係がない**ので、再描画しても最初の日時のまま表示か変わらない
  
#### 算出プロパティが適した場面
ECサイトの商品一覧ぺージで、ユーザーが検索条件を指定して商品を絞り込んだ結果に対して、
購入者の評価が高い順に並び変える場面をイメージする
 - 並び変えるたびに元の商品リストを検索するよりも、いったん**商品リストを絞り込んだ検索結果をキャッシュしておいて、それを元に並び替えを行ったほうが、無駄な処理が省ける**
 - 加工したデータをテンプレート内で頻繁に利用する場面では、**メソッドで毎回加工するよりも
 算出プロパティで加工してバインドしたほうが、パフォーマンスがよくなる**
  
## イベントハンドリング（ユーザーの操作を検知する）

#### よく使われるイベント
blur...フォーム要素からフォーカスが外れたとき
focus...フォーム要素にフォーカスが当たった時
select...フォーム要素内のテキストが選択されたとき
change...フォーム要素の選択肢や入力内容が変更されたとき
submit...フォームを送信しようとしたとき
reset...フォームがリセットされたとき
load...画像やスクリプトなどリソースの読み込みが完了したとき
scroll...要素の内容がスクロールした
resize...ウィンドウのサイズが変更されたとき
click
keydown,up,press
mousemove...マウスカーソルが要素内で動いたとき
mouseover...マウスカーソルが要素内に入ったとき
mouseout...外に出たとき
mouseup...要素内でマウスのボタンを押したとき
touthstart...要素を指でタッチしたとき
touthmove...要素をタッチした指でドラッグしたとき
touthend...要素をタッチした指を離したとき
  
#### イベントハンドラの登録(v-onディレクティブ)
Vueでイベントハンドラを登録するには v-onディレクティブを使う
`<要素名 v-on: イベント名="ハンドラ名">`
イベントハンドラはmethodsオプションに関数オブジェクトとして定義する
`methods: { ハンドラ名: 関数オブジェクト }`
   
クリックイベントの使用例
リスト2-7-1
```html
  <body>
    <div id="app">
      <!-- リスト2-7-1 削除ボタンを押すたびに在庫が1減る。0になると在庫切れになる -->
      <template v-if="stock >= 1">
        <span class="num">残り{{stock}}個</span>
        <button class="btn" v-on:click="onDeleteItem">削除</button>
      </template>
      <template v-else>在庫切れ</template>
    </div>
    <script src="main2_7_1.js"></script>
```
```js
// リスト2-7-1 削除ボタンを押すたびに在庫が1減る。0になると在庫切れになる
let app = new Vue({
  el: '#app',
  data: {
    stock: 10
  },
  methods: {
    // 削除ボタンのイベントクリックハンドラ
    onDeleteItem: function () {
      this.stock--;
    }
  },
});
```
リスト2-7-1と同じことをVueを使わずに書いた場合
リスト2-7-2 Vue未使用
```html
  <body>
    <!-- リスト2-7-2 Vue未使用-->
    <div id="app">
      <span class="num"></span>
      <button class="btn">削除</button>
    </div>
```
```js
//  リスト2-7-2 Vue未使用
// 頻繁にアクセスする要素を事前に取得
let app = document.querySelector('#app');
let btn = app.querySelector('.btn');
let num = app.querySelector('.num');

// 在庫数の初期化
let stock = 10;

// ボタンにイベントハンドラを割り当てる
btn.addEventListener('click', onDeleteItem);

// 削除のボタンのイベントクリックハンドラ
function onDeleteItem() {
  stock--;
  updateStock(); //表示を更新する
}

// 在庫数の表示を更新するメソッド
function updateStock() {
  if (stock >= 1) {
    num.textContent = '残り' + stock + '個';
  } else {
    app.removeChild(btn); //ボタンを削除する
    num.textContent = '在庫切れ';
  }
}

// 在庫数の初期値を表示する
updateStock();
```
`addEventListener('click', onDeleteItem);`
は第一引数にイベント名、第二引数にイベントハンドラを指定する
 - **イベントハンドラを要素と結びつけるという目的は、Vueのイベントハンドリングと同じ**

 #### コンポーネントの外側へのイベントハンドリング
v-onディレクテブでイベントハンドラを登録できるのは、**elオプションに指定したコンポーネント'※#appなど'のスコープ内にある要素に限られる**
つまり`<div id=""app></div>`の**外側にある要素や、ウィンドウ自体に発生するイベントにはv-onは検知できない**
 - 検知できないイベント:
   - ページが読み込まれたときに発生するloadイベント
   - ウィンドウサイズが変わった時に発生するresizeイベント
   - ページスクロールのscrollイベントなどが該当する
  
##### これらはVueに頼らずにaddEventListener関数を使ってイベントハンドラを登録する
**登録するタイミングは早いほうが良い**ので、createやmountedライフサイクルハックを検討する
ただし、**Vueを介さずに登録したイベントハンドラは、不要になったタイミングで`removeEventListener`関数を呼び出して解除**しなければならない
  
ウィンドウのresizeイベントをハンドリングする例
リスト2-7-3 resizeイベントのハンドリング
```html
    <!-- リスト2-7-3 resizeイベントのハンドリング-->
<div id="app">
  ウィンドウの横幅：{{width}}<br>
  ウィンドウの高さ：{{height}}
</div>
```
```js

let app = new Vue({
  el: '#app',
  data: {
    // ウィンドウサイズ
    width: window.innerWidth,
    height: window.innerHeight
  },
  // イベントハンドラを登録  
  created: function () {
    addEventListener('resize', this.resizeHandler);
  },
  // イベントハンドラを解除
  beforeDestroy: function () {
    removeEventListener('resize', this.resizeHandler)
  },
  methods: {
    // イベントハンドラ
    // Vueでは$eventの変数名でイベントオブジェクトを受けとる
    resizeHandler: function ($event) {
      // 現在のウィンドウサイズでプロパティを更新
      this.width = $event.target.innerWidth;
      this.height = $event.target.innerHeight;
    }
  }
});
```
イベントが発生したとき、ブラウザは**イベントオブジェクト**という特別なオブジェクトを生成していイベントハンドラの引数に渡す
イベントオブジェクトの中には、イベントが発生したDOMノードそのものを表すtargetオブジェクトや、そのイベントに関する様々な情報が格納されている
  
 - Vueでは$eventの変数名でイベントオブジェクトを受けとる
 - 上記では、resizeイベントの発生元はwindowオブジェクトなので、targetにはwindowオブジェクトが代入されている
  - そのため、windowオブジェクトが持つinnerHeightやWidthといったプロパティをtargetから引き出すことができる

```
innerHeightやWidth

水平スクロールバー（表示されている場合）を含む、ブラウザウィンドウの ビューポート (viewport) の高さを返します。

intViewportHeight は、window.innerHeight プロパティの値を保持します。

window.innerHeight プロパティは、読み込み専用です。また、デフォルトの値はありません。window.innerHeight プロパティは、ピクセル数を表す整数を保持します。
```
  
マウスでクリックした場所の座標値を追跡する例
リスト2-7-4　resizeイベントのハンドリング
```html
    <!-- リスト2-7-4 resizeイベントのハンドリング-->
    <!-- マウスでクリックした場所の座標値を追跡する例 -->
    <div id="app">
      <p>マウスカーソルの位置：{{point.x}}, {{point.y}}</p>
    </div>
```
```js
// リスト2-7-4 resizeイベントのハンドリング
// マウスでクリックした場所の座標値を追跡する例
let app = new Vue({
  el: '#app',
  data: {
    point: {
      x: 0,
      y: 0
    }
  },
  created: function () {
    // イベントハンドラを登録
    addEventListener('click', this.mousemoveHandler);
  },
  // イベントハンドラを解除
  beforeDestroy: function () {
    removeEventListener('click', this.mousemoveHandler);
  },
  // mousemoveイベントハンドラ
  methods: {
    mousemoveHandler: function ($event) {
      this.point.x = $event.clientX;
      this.point.y = $event.clientY;
    }
  }
});
```
マウスカーソルを動かすたびにイベントハンドラが実行される
イベントオブジェクトのclientX,Yには現在のマウスカーソルの位置が入っているので、コンポーネント側にもx,y座標を持ったpointプロパティを用意して、値の更新を行っている
 - マウスを動かすとデータとDOMが更新される

### ウォッチャ（データの変更を監視する）
ウォッチャとは、データの変更を監視してくれる機能
**監視したいデータと、データが変更されたときに実行したいハンドラをあらかじめ登録しておけば、Vueが自動的にデータの変更を検知してハンドラを呼び出してくれる**
 - イベントハンドリング(v-on)と似ているが、**ハンドラが呼び出されるタイミングが、イベントではなくデータの変更ある点が異なる**
   
dataオプションに登録したデータはVueの監視下に置かれることによって、データバインディングのようなリアクティブな振る舞いが可能になる
ウォッチャもまた、リアクティブシステムを特徴づける機能である

#### ウォッチャの登録(watchオプション)
ウォッチャは、watchオプションに登録する
`watch: { 監視したいプロパティ名: 関数オブジェクト }`
- ハンドラは、メソッド、フィルター、算出プロパティと同様に、**関数オブジェクトとして定義する**
 - ウォッチャに登録した関数オブジェクトは、**第一引数に変化後の値**を受け取り、**第二引数に変化前の値**を受け取る
  
ウォッチャの使用例
リスト2-8-1
```html
    <!-- リスト2-8-1 ウォッチャの使用例-->
    <div id="app">
      <template v-if="stock >=1 ">
        <span class="num">残り{{stock}}個</span>
        <button class="btn" v-on:click="onDeleteItem">削除</button>
      </template>
      {{message}}
    </div>
```
```js
let app = new Vue({
  el: '#app',
  data: {
    message: '',
    stock: 10
  },
  methods: {
    // 削除ボタンのクリックイベントハンドラ
    onDeleteItem: function () {
      this.stock--;
    }
  },
  watch: {
    // 在庫数が変化したときに呼び出されるハンドラ
    stock: function (newStock, oldStock) {
      if (newStock == 0) {
        this.message = '売り切れ';
      }
    }
  }
});
```
**在庫が0になった時、messageの内容が自動的に更新される**
 - そのため**テンプレート側にmessageを表示するかどうかの条件分岐を記述する必要がなくなり**、HTMLがスッキリする
  
#### 算出プロパティとウォッチャの使い分け
リスト1のウォッチャは算出プロパティに置き換えることができる
リスト2-3-2　算出プロパティへの置き換え
```html
  <body>
    <!-- リスト2-8-2 算出プロパティへの置き換え-->
    <div id="app">
      <template v-if="stock >=1 ">
        <span class="num">残り{{stock}}個</span>
        <button class="btn" v-on:click="onDeleteItem">削除</button>
      </template>
      {{statusMessage}}
    </div>
```
```js
// リスト2-8-2 算出プロパティへの置き換え
let app = new Vue({
  el: '#app',
  data: {
    message: '',
    stock: 10
  },
  methods: {
    // 削除ボタンのクリックイベントハンドラ
    onDeleteItem: function () {
      this.stock--;
    }
  },
  computed: {
    // 加工したメッセージを返すプロパティ ※status状態
    statusMessage: function () {
      if (this.stock == 0) {
        return '売り切れ';
      }
      return '';
    }
  }
});
```

上記のように、対象とするプロパティが返すデータを、アプリケーションに保持された他のデータの状態に応じて切り替えたい場合は、算出プロパティを使ってもよい
しかし、**返したいデータをアプリケーションの外部から取得しなければならない場合は、算出プロパティではハンドラが処理を終えるまで再描画されないので、ユーザーを待たせてしまう**
**ウォッチャなら、Ajaxを使ってユーザーの待ち時間を減らし、ブラウザに負荷がかからないようにハンドラの実行速度を整理でき**、より快適なインターフェースを提供できる

  
#### ウォッチャで算出プロパティを監視する
dataオプションのプロパティだけでなく、computedオプションの算出プロパティも監視できる
算出プロパティを監視して、メッセージが変化したときに何らかの処理を行うようにする
リスト2-8-3　算出プロパティを監視する
```html
  <body>
    <div id="app">
      <template v-if="stock >=1 ">
        <span class="num">残り{{stock}}個</span>
        <button class="btn" v-on:click="onDeleteItem">削除</button>
      </template>
      {{statusMessage}}
    </div>
```
```js
// リスト2-8-2 算出プロパティへの置き換え
let app = new Vue({
  el: '#app',
  data: {
    message: '',
    stock: 10
  },
  methods: {
    // 削除ボタンのクリックイベントハンドラ
    onDeleteItem: function () {
      this.stock--;
    }
  },
  computed: {
    // 加工したメッセージを返すプロパティ ※status状態
    statusMessage: function () {
      if (this.stock == 0) {
        return '売り切れ';
      }
      return '';
    }
  },
  watch: {
    // ステータスの変化を監視するウォッチャ(0になったらc.lを表示する)
    statusMessage: function () {
      console.log('商品のステータスが変化しました');
    }
  }
});
```
##### ウォッチャが役立つ場面
 - データが更新されたとき、サーバー間の通信など重い処理が発生する場面
 - ユーザのようっさによって、高い頻度で処理が発生する場面
  
### フォーム入力とデータバインディング
#### 双方向のデータバインド

フォーム入力バインディングは、コンポーネントが持つデータと、ユーザーがフォームコントロール（テキストボックスやラジオボタンなど）から入力する内容を双方向にバインドする機能
  
フォーム入力をバインドするにはv-modelディレクティブを使う
`<要素名 v-model="プロパティ名">`
  
リスト2-9-1　単純なフォーム入力バインディング
```html
    <script src="https://jp.vuejs.org/js/vue.js"></script>
  </head>
  <body>
    <div id="app">
      <input type="text" v-model="year" />
      <p>{{year}}</p>
    </div>
```
```js
let app = new Vue({
  el: '#app',
  data: {
    // テキストボックスの初期値は当年
    year: (new Date()).getFullYear()
  }
});
```
コンポーネント側であらかじめyearに初期値を設定しているので、そのままDOMに反映される
このままだと通常のデータバインディングと同じだが、
**テキストボックスの中身を書き変えると、ボックスの下にバインドしてる{{year}}も消費が変わる**
**フォームコントロールの内容がDOMにすぐ反映される**

##### 何が起こっているのか？
このときVueの中ではイベントハンドリングが行われている。
 - ボックスに文字入力するとinputイベントが発生
 - ひらがな、漢字を入力している場合は、Enterキーで入力候補を確定するとchangeイベントが発生する
  - こタイミングでVueは、v-modelに指定したプロパティに現在の入力内容を代入する
  すると、Vueのリアクティブシステムによって
  **「入力内容の変化→データの更新→DOMに反映」という流れが自動化される**
#### 注意点
通常HTMLのフォームコントロールに初期値を設定するには
value属性、checked属性、selected属性を使うが、
**v-modelを指定したフォームではこれらの設定値が無視される**
理由はv-modelを指定したフォームコントロールはVueの監視下に置かれ、**バインドしてるコンポーネントのデータが優先されるから。**
そのため、**コンポーネント側のdataオプションで初期値を設定しなければならない**
  
#### テキストボックス(改行できない入力欄)
テキストボックスへのバインドは次のように行う
`<input type="text" v-model="プロパティ名">`
 - 半角入力モードの時：1文字入力ごとにDOMに反映される
 - 全角入力モードの時：Enterで候補を確定するまでDOMに反映されない
**入力モードに関係なく1文字ごとにDOMに入力したい場合は、v-modelに頼らずにv-bind**を行い、v-onでinputイベントをハンドリングする
  
リスト2-9-2　入力文字をDOMへリアルタイムに反映する
```html
    <div id="app">
      <input type="text" v-on:input="yearInputHandler" v-bind="year" />
      <p>{{year}}</p>
    </div>
```
```js
// リスト2-9-2　入力文字をDOMへリアルタイムに反映する
let app = new Vue({
  el: '#app',
  data: {
    // テキストボックスの初期値は当年
    year: (new Date()).getFullYear()
  },

  methods: {
    // 「年」のinputハンドラ
    yearInputHandler: function ($event) {
      // 直接データを更新する
      this.year = $event.target.value;
    }
  }
});
```
##### 日本語入力をリアルタイムに反映するには、inputイベントハンドラを使う
  
### テキストエリア(改行できる入力欄)
テキストエリアへのバインドは以下のように行う
`<textarea v-model="プロパティ名"></textarea>`
HTMLでは<\textarea>...<\/textarea>で囲まれた内側にテキストを記述するが、**Vueでは次のように記述しても双方向のバインドにはならないので注意**
リスト2-9-3　一方通行のバインディング
```html
    <!-- リスト2-9-3　一方通行のバインディング -->
    <div id="app">
      <textarea>{{messsage}}</textarea>
      <pre>入力内容：{{message}}</pre>
    </div>
```
```js
// リスト2-9-3　一方通行のバインディング
let app = new Vue({
  el: '#app',
  data: {
    message: 'これは一方通行のバインドです'
  }
});
```
テキストエリアに文字を打っても、下部のmessageの文字表示のDOMは更新されない(フォームコントロールの内容を更新してもDOMに反映されない)
**入力内容をコンポーネント側に伝えたい場合はv-modelを使う**
  
### チェックボックス
単体のチェックボックスと、複数のチェックボックスをグループ化して扱う場合とで、データの扱い方が少し異なる
  
単体のチェックボックスは次のようにバインドする
`<input type="checkbox" v-model="プロパティ名>`
 - v-modelでバインドしたプロパティには真偽値true,falseが設定される
 チェック有：true　無し：false
 そのためそのままプロパティをそのまま描画すると、true,falseの文字列が表示される
 - そこで、真偽値ではなく文字列をなバインドする方法がある

チェックボックスに特別な属性**true-valueとfalse-valueを使うと、真偽値の代わりに任意の文字列をバインドできる**
リスト2-9-4　チェックボックスに文字列をバインドする
```html
    <!-- リスト2-9-4　チェックボックスに文字列をバインドする -->
    <div id="app">
      <p>ケーキはお好きですか？：{{answer}}</p>
      <input
        type="checkbox"
        id="cake"
        v-model="answer"
        true-value="はい"
        false-value="いいえ"
      />
      <label for="cake">チェックしてください</label>
    </div>
```
```js
// リスト2-9-4　チェックボックスに文字列をバインドする
let app = new Vue({
  el: '#app',
  data: {
    answer: 'はい　か　いいえを出力します'
  }
});
```
  
### 複数のチェックボックス

 - アンケートフォームなどで回答を複数選択する場合、複数のチェックボックスをグループ化する必要がある
 - このとき、1つ1つのチェックボックスに別々のプロパティをバインドするのではなく、**グループに対して1つのプロパティをバインドする**ことを覚えておく
```
<input tyoe="checkbox" v-model="プロパティ名" value="値1">
<input tyoe="checkbox" v-model="プロパティ名" value="値2">
<input tyoe="checkbox" v-model="プロパティ名" value="値3">
```
バインドしたプロパティは、チェックを付けたチェックボックスのvalue値を配列要素とする配列になる
**チェックを付けたものだけが配列に入る**
  
3つの選択肢をグループ化した例
リスト2-9-5　グループ化したチェックボックスにバインドする
```html
      <!-- リスト2-9-5　グループ化したチェックボックスにバインドする -->
      <p>ご注文をお選びください：{{selection}}</p>
      <label>
        <input type="checkbox" v-model="answer" value="ケーキ" />ケーキ</label
      >
      <label>
        <input type="checkbox" v-model="answer" value="紅茶" /> 紅茶</label
      >
      <label>
        <input
          type="checkbox"
          v-model="answer"
          value="コーヒー"
        />コーヒー</label
      >
```
```js
// リスト2-9-5　グループ化したチェックボックスにバインドする
let app = new Vue({
  el: '#app',
  data: {
    answer: []
  },
  computed: {
    // チェック内容を連結した文字列を返す算出プロパティ
    selection: function () {
      return this.answer.join();
    }
  }
});
```
 - バインドされるデータは配列なので、あらかじめ空の配列[]を宣言しておく
 - また、配列のままでは描画がやりにくいので、jsの`join()`関数で配列要素を連結した文字列を返す算出プロパティを使っている
**文字列に変換する算出プロパティを用意しておくと便利**

##### point
 - **単体のチェックボックスは真偽値(true,false)**
 - **複数のチェックボックスは文字列型の配列**
  
### ラジオボタン(2つ以上の選択肢から1つを選ぶ)
ラジオボタンは次のようにバインドする
```
<input type="radio" v-model="プロパティ名" value="値1">
<input type="radio" v-model="プロパティ名" value="値2">
<input type="radio" v-model="プロパティ名" value="値3">
```
複数のチェックボックスのグループ化と同様に、ラジオボタンにバインドするプロパティにはvalue値が代入される
  
3つの選択肢から1つを選択する例
リスト2-9-6　ラジオボタンにバインドする
```html
      <!-- リスト2-9-6　ラジオボタンにバインドする -->
      <p>当店のサービスはいかがでしたか？：{{answer}}</p>
      <label>
        <input type="radio" v-model="answer" value="素晴らしい" />素晴らしい</label>
      <label>
        <input type="radio" v-model="answer" value="普通" /> 普通</label>
      <label>
        <input
          type="radio"
          v-model="answer"
          value="まだまだ"/>まだまだ</label>
    </div>
```
```Js
// リスト2-9-6　ラジオボタンにバインドする
let app = new Vue({
  el: '#app',
  data: {
    answer: '選択してください'
  },
});
```
ラジオボタンはグループ内で1つしか選択できないので、
バインドしたプロパティは文字列型となる（よって配列は必要ない）
リスト6では、**選択するとv-modelによってバインドされたvalue値が表示される**
  
### セレクトボックス（プルダウン方式の選択肢)
あまり見かけないが、セレクトボックスにmultiple属性をつけると複数選択が可能になる
単一選択と複数選択とで扱い方が少し違う

#### 単一選択の場合
multiple属性をつけないセレクトボックスは単一選択になる
単一選択のセレクトボックスは次のようにバインドする
```html
<select v-model="プロパティ名">
  <option value="値1">選択肢1</option>
  <option value="値2">選択肢2</option>
  <option value="値3">選択肢3</option>
</select>
```
  
単一のセレクトボックスにバインドする例
リスト2-9-7　単一のセレクトボックスにバインドする
```html
    <div id="app">
      <!-- リスト2-9-7　単一のセレクトボックスにバインドする -->
      <p>当店のご利用頻度は？：{{answer}}</p>
      <select v-model="answer">
        <option disabled value="">選択してください</option>
        <!--option要素のdisabled属性は、option要素を無効にする属性。disabled属性が存在する場合、そのoption要素は無効になる。-->
        <option value="初めて">初めて</option>
        <option value="週一回以上">週一回以上</option>
        <option value="月二回以上">月二回以上</option>
        <option value="半年に一回">半年に一回</option>
      </select>
```
```js
// リスト2-9-7　単一のセレクトボックスにバインドする
let app = new Vue({
  el: '#app',
  data: {
    answer: 'ここに回答を表示'
  }
});
```
 - 単一のセレクトボックスにバインドされる値は文字列型
文字列に変換するプロパティを用意しておくと便利

#### 複数選択の場合
複数選択のセレクトボックスも、バインドの方法は単一の場合と同じ
```html
<select v-model="プロパティ名" multipre>
  <option value="値1">選択肢1</option>
  <option value="値2">選択肢2</option>
  <option value="値3">選択肢3</option>
</select>
```
ただし、**複数選択のセレクトボックスにバインドするプロパティは配列**になるので、
**コンポーネントのdataオプションに配列を用意しておく**ことに注意
  
リスト2-9-8　複数選択のセレクトボックスにバインドする
```html
      <!-- リスト2-9-8　複数選択のセレクトボックスにバインドする
 -->
      <p>分類：{{selectedCategory}}</p>
      <select v-model="category" multiple>
        <option value="宿泊費">宿泊費</option>
        <option value="食費">食費</option>
        <option value="交通費">交通費</option>
      </select>
    </div>
    <script src="main2_9_8.js"></script>
  </body>
```
```js
// リスト2-9-8　複数選択のセレクトボックスにバインドする
let app = new Vue({
  el: '#app',
  data: {
    category: []
  },
  computed: {
    // 選択された分類を返す算出プロパティ
    selectedCategory: function () {
      // 1件以上選択されている場合、選択された値を連結した文字列を返す
      return this.category.length >= 1 ? this.category.join() : '';
    }
  }
});
```
複数選択はシフトキー
  
### セレクトボックスの選択肢にバインドする
セレクトボックスの選択肢を動的に生成したい場合
 - option要素のvalue値と要素内容を持つオブジェクトの配列を用意して、v-forで繰り返し出力する
  
#### リスト2-9-9　セレクトボックスの選択肢にバインドする
```html
    <div id="app">
      <!-- リスト2-9-9　セレクトボックスの選択肢にバインドする
 -->
      <p>当店のご利用頻度は？：{{answer}}</p>
      <select v-model="answer">
        <!--disabled※無効ディセイボウ-->
        <option disabled value="">選択してください</option>
        <option
          v-for="item in options"
          v-bind:value="item.label"
          v-bind:key="item.code"
          >{{item.label}}</option
        >
      </select>
```
```js
// リスト2-9-9　セレクトボックスの選択肢にバインドする
let app = new Vue({
  el: '#app',
  data: {
    answer: '',
    options: [
      { code: 'ans1', label: '初めて' },
      { code: 'ans2', label: '週一回' },
      { code: 'ans3', label: '半年に一回' }
    ]
  }
});
```
  
### カレンダー(日付の選択)
とある商品の購入ページで、到着希望日をカレンダーで入力数例
リスト2-10-1　カレンダーにバインドする
```html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script src="https://jp.vuejs.org/js/vue.js"></script>
  </head>
  <body>
    <div id="app">
      <!-- リスト2-10-1　カレンダーにバインドする -->
      <!-- input要素には当日日付が最初から表示される -->
      <p>ご希望到着日：{{arrival_date}}</p>
      <input type="date" v-model="arrival_date" />
    </div>
    <script src="main2_10_1.js"></script>
  </body>
</html>
```
```js
// リスト2-10-1　カレンダーにバインドする
let app = new Vue({
  el: '#app',
  data: {
    arrival_date: null
  },
  created: function () {
    // 初期値を設定する
    this.arrival_date = this.formatDate(new Date());
  },
  methods: {
    // 日付を YYYY-MM-DDに整形するメソッド
    formatDate: function (dt) {
      let y = dt.getFullYear();
      let m = ('00' + (dt.getMonth() + 1)).slice(-2);
      let d = ('00' + dt.getDate()).slice(-2);
      let result = y + '-' + m + '-' + d;
      return result;
    }
  }
});
```
カレンダーの外観はブラウザによって異なる
HTMLの仕様上、type ="date"のinput要素に設定できる初期値は
YYYY-MM-DD形式の文字列でなければならない
そのため、createdライフサイクルハックを使って、コンポーネントがDOMに結びつく前にarrival_dateプロパティに初期値を設定している
  
#### 応用1(日付に選択範囲を制限する)
上記では過去の日付が選択できてしまう
ユーザーの誤入力を防ぐために、翌日以降の日付しか選択できないようにする
  
リスト2-9-11　カレンダーの選択範囲を制限する
```html
    <div id="app">
      <!-- リスト2-9-11　カレンダーの選択範囲を制限する -->
      <!-- input要素には当日日付が最初から表示される -->
      <p>ご希望到着日：{{arrival_date}}</p>
      <input type="date" v-model="arrival_date" v-bind:min="min_date" />
    </div>
```
```js
// リスト2-9-11　カレンダーの選択範囲を制限する
let app = new Vue({
  el: '#app',
  data: {
    arrival_date: null,
    min_date: null
  },
  created: function () {
    // 翌日の日付を初期値とする
    let dt = new Date(); //new Date()の結果：Sun Apr 19 2020 13:53:51 GMT+0900 (日本標準時) {}
    dt.setDate(dt.getDate() + 1);
    this.arrival_date = this.formatDate(dt);
    // 翌日の日付を最小値とする
    this.min_date = this.arrival_date;
  },
  methods: {
    // 日付を YYYY-MM-DDに整形するメソッド
    formatDate: function (dt) { //メソッド名のformatDateの命名は自由
      let y = dt.getFullYear();
      let m = ('00' + (dt.getMonth() + 1)).slice(-2);
      let d = ('00' + dt.getDate()).slice(-2);
      let result = y + '-' + m + '-' + d;
      return result;
    }
  }
});
```
type="date"(※カレンダー)のinput要素に、min属性に最小値を設定すると、それ以前の日付は選択できなくなるHTMLの仕様を利用する
あらかじめcreatedライフサイクルハックであs他の日付を代入したプロパティを用意しておき、min属性にバインドしている
実行すると、input要素には明日の日付が表示され、明日以降の日付しか選択できなくなる
  
#### 応用例2(レンジ入力とカラー選択を同期する)
スライダーを動かして大まかな数値を入力できる`type="range"`や、
カラーパレットから色を選択できる`type="color"`もバインドできる
2-8のウォッチャを利用して、この2つを連動させる
  
```
<FIELDSET>はフォームの入力項目をグループ化する際に使用します。 グループの先頭には、<LEGEND>～</LEGEND>で入力項目グループにタイトルをつけます。

フォームの入力項目をグループ化することで、Tabキーなどでグループ間を簡単に移動できるという利点があります。
```
リスト2-9-12　フォームコントロールの同期
```html
    <div id="app">
      <!-- リスト2-9-12　フォームコントロールの同期 -->
      <fieldset>
        <legend>あなたの好きな色は？：</legend>
        <input type="color" v-model="color"/>{{color}}<br>
        赤：<input type="range" v-model.number="red" min="0" max="255" />{{red}}<br>

        緑：<input type="range" v-model.number="green" min="0" max="255" />{{green}}<br>
        
        青：<input type="range" v-model.number="blue" min="0" max="255" />{{blue}}<br>
      </fieldset>
    </div>
```
```js
// リスト2-9-12　フォームコントロールの同期
let app = new Vue({
  el: '#app',
  data: {
    color: '#000000',
    red: 0,
    green: 0,
    blue: 0,
  },
  computed: {
    // 赤緑青を配列で返す算出プロパティ
    colorElement: function () {
      return [this.red, this.green, this.blue];
    }
  },
  watch: {
    // 赤緑青いずれかの変更を監視する
    colorElement: function (newRGB, oldRGB) {
      // 赤緑青を2桁の16進数表記に変換する
      let r = ('00' + newRGB[0].toString(16).toUpperCase()).slice(-2);
      let g = ('00' + newRGB[1].toString(16).toUpperCase()).slice(-2);
      let b = ('00' + newRGB[2].toString(16).toUpperCase()).slice(-2);
      // #RRGGBB 形式の文字列で更新する
      this.color = '#' + r + g + b;
    },
    // カラーパレットの選択変更を監視する
    color: function (newColor, oldColor) {
      this.red = parseInt(newColor.substr(1, 2), 16); // 0始まりの1:1文字目から2文字抽出。16進数にして返す
      this.green = parseInt(newColor.substr(3, 2), 16);// 0始まりの3:3文字目から2文字抽出。
      this.blue = parseInt(newColor.substr(5, 2), 16);
    }
  }
});
```
  
#### 重要ポイント
1つ目：tyoe="range"のスライダーは0-255までの範囲の数値を入力させたい
 - **HTMLの仕様上、input要素からの入力値は文字列型**なので、
 `.number`修飾子を付けて数値型に変換すること

  
2つ目：**カラーパレットとスライダーのどちらかを変更したときに、もう一方の値を更新するために、ウォッチャを使ってそのタイミングを確保している**点
  
3つ目：red,green,blueの3つのプロパティに対して1つ１つウォッチャを定義するとPGが冗長になるので、**red,green,blueを配列に詰め込んで返す算出プロパティをcolorElementという名前で定義**し、**この算出プロパティをウォッチャで監視している**点
 - **ウォッチャの監視対象が配列の場合、配列要素のどれか1つでも更新されればハンドラが呼び出される性質を利用している**
  
`parseInt`とは、文字列を整数に変換するJavaScriptのグローバル関数です。
```
// parseIntは次のような書き方で使用することができます。
parseInt(str)
parseInt(str, int)

// praseInt(str)の場合
// strはstringの略称で、文字列を意味します。
parseInt("123");

// parseInt(str, int)の場合
// intの部分は、基数です。
変換前の数値を何進数で表現しているかについての指定をする基準を指定します。
// この基準を指定する数値を、基数と呼びます。
// 基数には、2進数、8進数、10進数、16進数を指定することができます。
2進数は、数値を0と1だけで表現した数値です。

8進数は、数値を0で始まり0から7までの数字で表現したものです。

10進数は、私達が日常使用している0から9までの数値を使用して表現したものです。

16進数は、数値を0x又は0Xで始まり0から9までの数字かAからFまでの記号で表現したものです。英文字はaからfでも同じ意味を表します。
```
  
### 制御をサポートする3つの修飾子
v-modelディレクティブには、フォーム入力バインディングをサポートする3つの修飾子が用意されている
修飾子は`v-model`に続けて、`v-model.lazy`のように使う
  
**.lazy(入力値が変わるとすぐに同期する)**
 - `.lazy修飾子`を指定したフォームコントロールは、changeイベントが発生したタイミングでデータバインドが行われる
 - 全角入力で候補を確定したタイミングではなく、入力欄からフォーカスを外したときに初めてDOMが更新される
  
**.number(入力値を自動で数値型に変換する)**
 - `.number修飾子`を指定したフォームコントロールは、バインドしてるプロパティに数値型の値が代入される。
  - **ブラウザのデフォルト仕様ではinput要素が持つ値は文字列型**であることに加えて、**jsはデータ型に関する制約が緩く、「数字（=文字列）」と「数字（=文字列でない）」を相互に代入できてしまう**
 そのため、**数値をバインドする場合は、`.number`を付けて**、意図しない動作を防ぐ
  
**.trim(余分なスペースを取り除く)**
 - `.trim修飾子`を**テキストボックスやエリアにつけておくと、入力された文字列の前後の空白（スペース）や改行などを自動的に除去してからデータに代入**してくれる
 - ユーザーの誤入力防止に役立つ
  
### トランジション(表示の切り替えを滑らかにする)
#### トランジションとは
transition（※遷移）とは、
 - 要素がふわっと浮き上がる心地よい表示効果を与える
 - 要素の色や大きさなどを連続的に変化させ、アニメーション効果を与えたりする機能

**Vueは、スタイルシートを利用したCSSトランジション**と、**リアクティブデータを使ったトランジションをサポート**している
ここではCSSトランジションの基本事項のみ解説する
  
CSSトランジションの本質は、**数値で表現できる量を2つの状態間で連続的に変化させる**こと。
一般的に
TVアニメ、映画:1秒に24コマ
TV:1秒に30コマ
1つ1つのコマをフレームと呼び、フレームが多いほど、途切れなく滑らかに見える
  
### CSSトランジション
CSSのtransitionプロパティを使うと、2つの状態間のスタイルをブラウザが連続的に変化させてくれるので、簡易アニメーションが実現できる
CSSのopacity(※不透明度) プロパティを使ったフェードイン・アウトのイメージをする
  
トランジションは前半(Enterフェーズ)と、後半(Leaveフェーズ)に別 れ、
前半では以下の3つのスタイルが使われている
 - トランジション開始前のスタイル.....opacity:0
 - トランジション終了後のスタイル.....opacity:1
 - トランジションの継続に必要なスタイル.....transitionプロパティ
  
**後半でも上記と同じ3つのスタイル**が使われている
 - トランジション開始前のスタイル.....opacity:0
 - トランジション終了後のスタイル.....opacity:1
 - トランジションの継続に必要なスタイル.....transitionプロパティ
**開始と終了の間のスタイルは、ブラウザが自動的に計算してくれる**
  
上記のように、役割の異なる6つのスタイルを時間の経過に合わせて、
適用・解除することで様々なエフェクトを生み出す
  
通常、6つのスタイルはclass名をつけて管理するが、要素にclassを動的に適用したり解除するにはjsを使わねばならず、自分で記述するのは大変
しかし、Vueが定めているルールに沿ったclass名を使えば、classの適用、解除はVueがやってくれる
Vueが定めているデフォルトのclass名は以下の通り
**CSSトランジションのデフォルトのclass名**
|class名|役割|
|-|-|
|v-enter|Enterフェーズ開始前のスタイルを定義するclass|
|v-enter-to|Enterフェーズ終了時のスタイルを定義するclass|
|v-enter-active|Enterフェーズ継続中のスタイルを定義するclass|
|v-leave|Leaveフェーズ開始前のスタイルを定義するclass|
|v-leave-to|Leaveフェーズ終了時のスタイルを定義するclass|
|v-leave-active|Leaveフェーズ継続中のスタイルを定義するclass|
  
`v-enter-active`と`v-leave-active`は、トランジションの継続時間や変化させたいCSSプロパティ名を指定するために使う
  
**CSSトランジション用classの適用と解除をVueに任せるには、トランジションを適用したい要素を`<transition>`タグで囲む**
```html
<transition>～～</transition>
```
**トランジションが発生するのは`<transition>要素</transition>`で囲んだ要素がDOMに挿入されたり削除されたりするタイミング**
  
ボタンで要素の表示・非表示を切り替える例
リスト2-10-1　フェードイン・フェードアウト
```html
    <title>Document</title>
    <link rel="stylesheet" href="main2_10_1.css" />
    <script src="https://jp.vuejs.org/js/vue.js"></script>
  </head>
  <body>
    <div id="app">
      <!-- リスト2-10-1　フェードイン・フェードアウト -->
      <button v-on:click="show =!show">表示を切り替える</button>
      <transition>
        <p v-if="show">
          吾輩は猫である。<br />
          名前はまだ無い。<br />
          どこで浮かれたかとんと見当がつかぬ。
        </p>
      </transition>
    </div>
    <script src="main2_10_1.js"></script>
```
```js
// リスト2-10-1　フェードイン・フェードアウト
let app = new Vue({
  el: '#app',
  data: {
    show: true  //trueの時は文字を表示、false:非表示
  }
});
```
```css
/* リスト2-10-1　フェードイン・フェードアウト */
/* Enterフェーズ開始前と、Leaveフェーズ終了後のスタイル */
/* opacity(※不透明度) */
.v-enter,
.v-leave-to {
  opacity: 0;
}

/* Enterフェーズ終了時と、Leaveフェーズ開始時のスタイル */
/* デフォルトでは表示されている要素には、opacity: 1をしなくてもよいので、.v-enter-to,.v-leaveは省略できる */
.v-enter-to,
.v-leave {
  opacity: 1;
}

/* Enterフェーズ継続中と、Leaveフェーズ継続中のスタイル */
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s; /* 表示の切り替えにかかる時間0.5秒。長いほど時間かかる */
}
```
ボタンを押すたびにshowプロパティの値が、false,true,falseと変わるので、
`v-if`の判定結果も交互に変化し、文章にトランジション効果がかかる
  
 - 上記のように、EnterフェーズとLeaveフェーズの動作が互いに逆再生の関係にある場合は、
`v-enter`と`v-leave-to`、
`v-enter-to`と`v-leave`、
`v-enter-active`と`v-leave-active`
は同じスタイルを指定することになるので、上記のようにセレクタをまとめることができる
 - デフォルトでは表示されている要素には、`opacity: 1`をしなくてもよいので、`.v-enter-to,.v-leave`は省略できる
  
#### class名の先頭部分を自分で指定する
`<transition name="fade">`にように、`<transition>`要素にname属性を指定すると、先頭を
**「 v-* 」**ではなく、**「 fade-* 」**に付け替えたclass名が使えるようになる
 - フェードはfadeで始まる
 - スライドインはslideInで始まる
といったように、エフェクトの種類を表す名前を付けておくと便利
  
リスト2-10-2　name属性値でエフェクトを分類する
```html
    <div id="app">
      <!-- リスト2-10-2　name属性値でエフェクトを分類する -->
      <button v-on:click="show =!show">表示を切り替える</button>
      <transition name="fade">
        <p v-if="show">
          吾輩は猫である。<br />
          名前はまだ無い。<br />
          どこで浮かれたかとんと見当がつかぬ。
        </p>
      </transition>
      <transition name="slideInLeft">
        <p v-if="show">
          吾輩は猫である。<br />
          名前はまだ無い。<br />
          どこで浮かれたかとんと見当がつかぬ。
        </p>
      </transition>
    </div>
```
```js
// リスト2-10-2　name属性値でエフェクトを分類する
let app = new Vue({
  el: '#app',
  data: {
    show: true  //trueの時は文字を表示、false:非表示
  }
});
```
```css
/* リスト2-10-2　name属性値でエフェクトを分類する */
/* シンプルなフェードイン */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

/* 左からスライドイン */
.slideInLeft-enter-active,
.slideInLeft-leave-active {
  transition: opacity 0.5s, transform 0.5s;
}
.slideInLeft-enter,
.slideInLeft-leave-to {
  opacity: 0;
  transform: translateX(-100%); /*表示が消えるとき、x-100%（画面の左側の位置)に戻る。x100%なら右端に戻る*/
}
.slideInLeft-enter-to,
.slideInLeft-leave {
  transform: translateX(0%); /* スライドが戻るとき右に0%の位置に戻る。10%なら右に10%の位置に一度行く */
}
```
  
#### カスタムトランジションクラス(class名を自分で指定する)
CSSトランジションの実装をサポートする外部のライブラリを使いたいとき、ライブラリ側で決まっているclass名を使わなければならないことがある
 - そのような場合、次の属性を使えば、`v-enter`や`v-leave`の代わりに、指定したclass名が適用されるようになる
  
**カスタムトランジションクラスを定義する属性名**
|属性名|役割|
|-|-|
|enter-class|Enterフェーズ開始前のスタイルを定義するclass|
|enter-to-class|Enterフェーズ終了時のスタイルを定義するclass|
|enter-active-class|Enterフェーズ継続中のスタイルを定義するclass|
|leave-class|Leaveフェーズ開始前のスタイルを定義するclass|
|leave-to-class|Leaveフェーズ終了時のスタイルを定義するclass|
|leave-active-class|Leaveフェーズ継続中のスタイルを定義するclass|
  
外部のライブラリ[animate.css](https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.min.css)を使って、ズーム効果を適用する
リスト2-10-3　カスタムトランジションクラスの使用例
```html
    <title>Document</title>
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.min.css"
    />
    <script src="https://jp.vuejs.org/js/vue.js"></script>
  </head>
  <body>
    <div id="app">
      <!-- リスト2-10-3　カスタムトランジションクラスの使用例 -->
      <button v-on:click="show =!show">表示を切り替える</button>
      <transition
        name="zoom"
        enter-active-class="animated zoomIn"
        leave-active-class="animated zoomOut"
      >
        <p v-if="show">
          吾輩は猫である。<br />
          名前はまだ無い。<br />
          どこで浮かれたかとんと見当がつかぬ。
        </p>
      </transition>
    </div>
    <script src="main2_10_3.js"></script>
```
```js
// リスト2-10-3　カスタムトランジションクラスの使用例
let app = new Vue({
  el: '#app',
  data: {
    show: true  //trueの時は文字を表示、false:非表示
  }
});
```
```css
/* animate.cssが用意してくれているので何も書かなくてOK! */
```
  
  
### animate.css
#### https://daneden.github.io/animate.css/
animated、zoomIN、zoomOutはanimate.cssが提供しているclass名
回転や振動など、手軽に使えるエフェクトがclass名で提供されている
  
### 仮想DOMとは？
 - VueはデータとDOMを効率的に同期させるために、仮想DOMという仕組みを持っている。
 - 仮想DOMとは、Vueの監視下にあるリアクティブデータに基づいてVueがメモリー上に構築する仮想的なDOMである。
 - リアクティブデータが変化すると、Vueは実際のDOMを更新する前に仮想DOMに対して操作を行う。
 - このときVueは、本当に更新しなくてはならない差分だけを仮想DOMから抽出して、それを元にして実際のDOMへノードの追加や削除を行う。差分だけを適用することで、描画処理のパフォーマンスを向上させている
   
2つのp要素にバインドした**データを入れ替える処理を行ったとき、要素そのものを入れ替えるのではなく、要素内容のテキストノードだけを入れ替えるこ**とで、描画が効率化される
  
言い換えると、Vueはなるべく既存のノードを再利用しようとする
これが原因で弊害が生じることがある
 - 配列を繰り返して描画する場面
 - v-ifディレクティブで描画を切り替える場面
で**ノードとデータの対応関係にズレが生じる**ことがある
この問題の回避に、**要素にユニークなkey属性値を付けることで、Vueにノードをキチンと区別させることが推奨**されている

