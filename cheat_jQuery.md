# jQuery

[【jQuery入門】CDNでjQuery本体を読み込む方法と選び方まとめ]([https://www.ameamelog.com/jquery-cdn/)
[jQueryファイルの読み込み方法(CDNや直接ダウンロード)]([https://www.flatflag.nir87.com/cdn-1346)
 * CDN（Contents Delivery Network）

```js
Google
↓動いた
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
```

```js
本家
↓動いた
<script src="https://code.jquery.com/jquery-3.4.1.js"></script>

↓動かない
<script src="https://code.jquery.com/jquery-3.4.1.js"
integrity="sha256-hVVnYaiADRTO2PzUGmuLJr8BLUSjGIZsDYGmIJLv2b8="
crossorigin="anonymous"></script>
```


----
jQueryを読み込む（ダウンロードファイルを使う場合）
```html
html
<body>
  <script src="js/jquery-3.4.1.min.js"></script>  //jQueryを読み込む
  <script src="js/app.js"></script>
</body>
```
---
##### jQueryの動作チェック
```js
'use strict'

// PG実行準備ができたらbody要素にp要素を追加してテキストを表示する

$(document).ready(function(){
  $('body').html('<p>jQueryの動作チェック</p>');
});
```
#### jQueryにおいて「\$()」は関数
結論から言うと、jQueryにおいて「\$()」は関数です。 JavaScriptにおいて「\$（ドルマーク）」は、特別な意味を持ちません。 なので、jQueryにおいては、「\$」という名前の関数ということになります。
 * \$にはjQの機能を提供するjQueryオブジェクトが代入されているので、ドルマークを通じて様々なプロパティやメソッドを利用することができる
 * 基本的な使い方は、\$(セレクタ)と書いて、目的の要素を取得し、そのメソッドを利用して様々な操作を実行していく

---

##### 拡張ツール
 ・jQuery Code Snippets
 　jqと入力すると候補を表示してくれる

---

### 基本形
 $('`#menu dt`').`slideToggle()`;
 
 $('`セレクタで要素を取得`').`メソッド()で操作`;

「#menu dt」というセレクタに該当する要素の表示/非表示を切り替える
* $()はjQueryメソッドの短縮形
```js
js
$('`#menu dt`').`slideToggle()`;

jQuery('`#menu dt`').`slideToggle()`;　//どちらの書き方でもOK 
```
---
#### イベントは専用のメソッドで設定する

 * body要素にクリックイベントを登録する例
 ```js
$('body').click(function () { 
  //実行したい処理
});

 //j　※qcli で候補表示が可能
 ```
#### jQueryを利用したプログラムの記述場所
jsプログラムではHTML要素の準備ができた後に実行されることが重要だった。
そのため、これまでjsファイルを読み込むscript要素を、\</body>の直前に書いてきた。
 * jQでも同じようにする必要があるが、\</body>の直前に書く代わりに、**HTML要素の準備ができたときに発生するredyイベントを利用する**書き方も一般的である
 * jQではreadyメソッドを使用していくが、省略形がある。
 **$()の中に無名関数を書いた場合もreadyメソッドと同じ働きをする。**

```js
js
//readyメソッドを利用した書き方
$(document).ready(function(){
  //ここにjsのプログラムを書く
});

// S()を利用したよりシンプルな書き方
$(function(){
  //ここにjsのプログラムを書く
});
```
---
#### セレクタの書き方
基本はCSSのセレクタと同じ
##### 基本構文
$('#sample')
\$(`'セレクタ'`)
```js
js
//セレクタの利用例
$('#sample'); ...id='sample'の要素を選択
$('#sample p'); ...id='sample'の要素の子孫要素pを選択
$('#sample > p'); ...id='sample'の要素の子孫要素pを選択

```
---
CSSと同じ形式以外にも、様々なセレクタの指定方法がある。
たとえば**documentオブジェクトなど、HTML要素を表すオブジェクトはそのまま引数に指定することができる**
また、引数にHTMLタグを書くと新しいHTML要素を作成できる
```js
// HTML文章全体を選択したい場合
$(document);
```

見慣れないセレクタの書き方に出会ったときは、
[jQueryのリファレンス](https://api.jquery.com/category/selectors/)を参照する
[jQueryのリファレンス日本語版](http://semooh.jp/jquery/)

---

### jQueryオブジェクト
ｊQueryのさまざまな機能を提供する
$(セレクタ)で操作するHTML要素を選択すると、**選択したHTML要素を含む「jQueryオブジェクト」が戻り値として得られる**
このjQオブジェクトがjQの様々な機能をメソッドとして提供してくれる。
jQオブジェクトは基本的に「jQueryオブジェクト」を戻り値として返すため、さらに.ドットで繋げば様々な処理をまとめて記述していくことができる。

```js
// jQueryオブジェクトのメソッド
$('body').html('<p>jQueryの動作チェック</p>');
// body要素を取得して、内容のHTMLを書き換え

// メソッドチェーン(メソッドを繋げて記述)
$(セレクタ).メソッドA().メソッドB ...;

```
---

### jQueryイベントの書き方、登録方法
jQでは、**jsのイベントタイプ（クリックやキー押下）に対応するメソッド**が用意されている

イベント発生時に実行したい処理をメソッドの引数に指定する

```js
// clickメソッドでクリックイベントを登録

// id属性がbuttonの要素をクリックしたとき「ボタンを押しました」と表示
$('#button').click(function () {
  alert('ボタンを押しました');
});

```

#### 主なイベント用メソッド
メソッド名　/ .....イベントタイプ
.click() .....クリック
.dbclick() .....ダブルクリック
.hober() ..... マウスポインタが乗った
.keydown()、.keypress()、 .keyup() .....キーボード関連のイベント
.mousedown()、.mouseenter()、.mouseseleave()※切り取り、.mousemove()、.mouseout、.mouseup() .....マウス関連のイベント
.resize() .....リサイズ
.scroll .....スクロール
### 複数のイベントに同じ処理を登録できる
より複雑なイベントを登録するためにonメソッドが用意されている
複数のイベントに対して同じ処理を登録できる

「マウスが乗った、マウスが離れた」という2つのイベントに同一の処理を登録したい場合
スペースで区切り、例文のように記述する。
また、offメソッドを使用するとイベントに登録した処理を取り消すことができる
```js
// onメソッドでイベントを登録する

// id属性がareaの要素の上にマウスが乗ったり離れたりするたびに文字を表示
$('#area').on('mouseover mouseout' , function () {
  console.log('マウスが要素の境界を移動しました')
});
```

```js
// offメソッドでイベントを解除する

// id属性がbuttonの要素から、イベントに登録された処理すべてを取り除く
$('#button').off();

// id属性がbuttonの要素から、clickイベントに登録された処理すべてを取り除く
$('#button').off('click');

```
---

### ドロップダウンメニューを作成

##### ドロップダウンメニューの外観を作る
HTMLファイルを編集
 - 定義メニュー「dl」でddメニューの大枠を作る
 - dl要素のid属性に「menu」を指定しておく
 - 続いて「dt」にドリンクメニュー、「dd」にdtに対応する各ドリンク名を入力していく

**dl > dt > dd**
```html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <title>インプレス いちばんやさしいJavaScriptの教本</title>
    <link rel="stylesheet" href="css/style.css" />
  </head>
  <body>
    <dl id="menu">
      <dt>ドリンクメニュー</dt>
      <dd>ウーロン茶</dd>
      <dd>コーラ</dd>
      <dd>オレンジジュース</dd>
      <dd>ミネラルウォーター</dd>
    </dl>
    <script src="js/jquery-3.3.1.min.js"></script>
    <script src="js/app.js"></script>
  </body>
</html>
```

```js
js

'use strict'

$(function () {　// HTML要素を読み込み完了後に{}内の処理を実行

  // dt要素を選択。clickメソッドの引数として無名関数を書く
  $('#menu dt').click(function () {
    // クリックイベント発生時にこの処理を行う
    $('#menu dd').slideToggle(); //slideToggleメソッド...HTML要素の表示/非表示をスライドするように切り替える
  });
});
```
##### slideToggleメソッド
jQが提供するメソッド
指定したHTML要素の高さを操作して、slideDown/slideDownの動作を交互に行う。引数は1/1000秒単位で、変化にかかる時間を指定できる

---

### Topに戻るボタンを作る

animateメソッド ...スムーズにアニメーションさせる
scrollメソッド ...スクロールイベントを検出する

```html
html
<a href="#"> ...ページ内リンク。ページの一番上に移動する。a要素で指定している。
```

スクロール処理が起きるたびに処理を行うため、
1.windowオブジェクトのスクロールイベントに対して処理を登録する
　$(window).scroll(function(){);

2.「$this.scrollTop()」でwindowのスクロール位置を取得する

- もしスクロール位置が200以上まで動いたらボタンをフェードインで表示する。
  それ以外はフェードアウトで非表示にさせる。
```js
$(function () { //読み込み完了後に実行

  // 上に戻るボタンの初期化
  let topBtn = $('#scrollTop'); //要素を選択。後で使うので変数に格納
  // 最初はボタンを消しておく
  topBtn.hide(); //hideメソッドで非表示にする

  // ある程度スクロールされたら、上に戻るボタンを表示する
  // ハマった所：windowオブジェクト指定時は’’いらない。オブジェクトだから？documentも同じく''いらない。
  $(window).scroll(function () { //スクロールイベントに登録

    // 位置に応じてボタンを表示
    if ($(this).scrollTop() > 300) { //引数が多いほどスクロール距離が長い
      topBtn.fadeIn(); //フェードインで表示  
    } else {
      topBtn.fadeOut(); //フェードアウトで非表示
    }
  });
});
```

#### 表示/非表示を切り替えるメソッド
 - 一瞬で非表示にする ...hide()
 - 徐々に透明度を変えながら表示/非表示を切り替える...fadeOut()/fadeIn()
 表示/非表示系のメソッドは、いずれも表示/非表示にかかる時間(ミリ秒)を引数に指定できる
```js
$('#button').fadeOut(); //id属性がbuttonの要素をフェードアウトする

$('#button').fadeIn(1000); //1秒かけてフェードインする
```

##### その他の表示/非表示に関するメソッド
メソッド　　/　　用途
.show() .....非表示状態にある要素を表示する
.hide() .....表示状態にある要素を非表示にする
.toggle() .....要素の透明度を操作して表示/非表示を切り替える
.slideToggle() .....要素の高さを操作して表示/非表示を切り替える

---

#### 先頭までスムーズに戻るアニメーションを付ける

preventDefault() ...Webブラウザが標準で十個する動作を無効化する。prevent※防ぐ
 - 「どのイベントの後続処理を無効化するか」を指定する必要がある。jsのイベントでは、引数にイベントに関する情報が詰まった「eventオブジェクト」が格納されるため、今回はそれを使う。
```js
  // クリックで上に戻るボタン
  topBtn.click(function (event) {
event.preventDefault(); //prevent※防ぐ。ページ内リンクによる移動を無効化。
```
```js
 // クリックで上に戻るボタン
  topBtn.click(function (event) {
    event.preventDefault(); //prevent※防ぐ。ページ内リンクによる移動を無効化。
    $('body,html').animate({
      scrollTop: 0
    }, 500); //(ボタンをクリックすると)先頭まで徐々にスクロール。引数はアニメーションの時間。
    // scrollTop: 0は戻った際の先頭行からの距離。この場合は0なので先頭まで戻る。500なら先頭から500下まで戻る
  });
```
#### セレクタにbodyとhtmlの両方を指定する理由
ブラウザによって、html要素のscrollTopを指定すべき場合と、body要素のscrollTopを指定すべき場合があるため。
両方の要素を指定しておけば、どのブラウザでも問題なく動作させることができる。
#### animateメソッド
animate( { }, 500);
 - animateメソッドはスクロール以外にもCSSのスタイルを徐々に変化させるために使える

#### animateメソッドの使い方
指定した時間をかけて徐々にスタイルを変化させる。CSSならたいていのものを変化させられる。
 - 引数には、スタイルのプロパティの名前と値をまとめたオブジェクトを渡す。
 - 使用できるプロパティ名は基本的にCSSと同じものが用意されているが「-」の代わりに大文字表記にする。
 ちなみに、**scrollTopは例外で、CSSのプロパティではなくHTMLのプロパティ。**
##### animateメソッドの構文
```js
  $(セレクタ).animate({
  プロパティ名: プロパティ値,
  プロパティ名: プロパティ値,
  ...
  }, 変化時間);
});
```

---

## jQueryプラグインでスライドショーを作成
プラグイン.....機能を簡単に追加できるプログラム。
jQueryプラグイン.....**jQueryを使って作られた機能を拡張するプログラム**
 - スライドショーやグラフを簡単に作れる

 プラグインは玉石混在。動作不良やほかのPGに悪影響を及ぼすことも。公式サイトで紹介されているものがおすすめ。
 - 利用方法はプラグインごとに異なる。マニュアルやサンプルコードを参考にする。
 利用条件あるものもある。**利用時は必ず利用規約やライセンス規約を確認すること**

[jQueryプラグイン公式サイト](https://plugins.jquery.com/)

---

[jQueryプラグイン「slick」公式サイト](http://kenwheeler.github.io/slick/)
 - get it nowをクリック＞Download Now をクリック
「slick-1.8.1zip」がダウンロードされる
 - ダウンロードしたファイルを展開し、「slick」フォルダをコピー。
 利用したいフォルダへ貼り付ける。（例：レッスンのpracticeフォルダ直下。jsやimgフォルダと同じ階層。） 
---
### HTMLファイルでslickを読み込む
```html

//headにlink要素を2つ追加
//slickのスタイルを適用させる為に、slickのcssを読み込む
<head>
  <meta charset="UTF-8">
  <title>インプレス いちばんやさしいJavaScriptの教本</title>
  <link rel="stylesheet" href="slick/slick.css">  //CSSを読み込む
  <link rel="stylesheet" href="slick/slick-theme.css">  //CSSを読み込む
  <link rel="stylesheet" href="css/style.css">
</head>

// body要素内では、slickで使用するjsファイルを読み込む
// slick.min.jsはjQueryを使用するので、必ず「jQの後に」読み込むこと
<body>
  <script src="js/jquery-3.3.1.min.js"></script>
  <script src="slick/slick.min.js"></script>  //slickを読み込む
  <script src="js/app.js"></script>
</body>
```
#### 表示する画像を指定する
```html
 <body>

 //slickでは、スライドショー全体を表示する領域を任意のclassで指定する。

    <div class="slideshow">  //全体のdiv要素を追加

    //class="slideshow"要素に含まれるdiv要素の1つひとつが、スライドの1ﾍﾟｰｼﾞとして認識される。ので、img要素をdiv要素で囲んでスライド表示させる画像を指定していく。
      <div><img src="img/1.jpg" alt="" /></div> //表示する画像を追加
      <div><img src="img/2.jpg" alt="" /></div>
      <div><img src="img/3.jpg" alt="" /></div>
      <div><img src="img/4.jpg" alt="" /></div>
    </div>
```
---
#### スライドショーのスタイルを整える
```css
/* 背景色を設定する */
body {
  background: #444;
}

/* スライドを中央に配置する */
/* サイズを設定して中央に配置 */
.slideshow{
  width: 500px;
  margin: auto;
}

/* 画像の幅を親の100%に */
.slideshow img{
  width: 100%;
}
```
#### slickを有効にして、スライドショーを完成させる
```js
$(function () { //読み込み完了後に実行

  //スライドに使用する要素を指定するため、セレクタに「.slideshow」クラスを指定
  $('.slideshow').slick({ //スライドショーの要素を選択してslickメソッドを実行

    //プラグインで提供されるslickメソッドと使って、スライドショーの各設定を記述
    autoplay: true,  //自動再生オン
    autoplaySpeed: 3000,
    dots: true  /* 枚数を示すdots。画像下の〇アイコン */
  });
});
```
#### ※引数にオブジェクトを指定する
関数の引数としてオブジェクトを渡すことはよくある。
引数が20個ある関数だと順番通り()に引数を書くのは大変、順番を間違うと動かなくなることも。
1つのオブジェクト型の引数にまとめてしまえばスッキリしたコードになる。
「プロパティ：値」の形で名前が付けられるので引数の区別がしやすくなる。
 
 slickのより詳細な設定方法は[公式サイト](http://kenwheeler.github.io/slick/)の「setting」で確認

 ---
 ### jQueryを利用しない場合もある
 jQは多機能で汎用的。ただ、意図的に利用しない場面もある。
 例えば、高速処理が必要な場合。より軽量なライブラリを利用する。
 またはライブラリを利用せずにjsを記述したりする。
 その他、jQと併用できないほかのライブラリやフレームワークを採用することもある。
 jQは広く利用されているが、jsそのものの知識も重要。
 両方の書き方を覚えておくこと。
### プラグイン/ライブラリの活用にも基本が大切
プラグイン/ライブラリ利用時には、変数や関数の名前の重複に注意。
プラグインやライブラリもPGなので、jsの変数や関数を使っている。
気づかないうちに変数名などが被るとうまく動作しない。
こういったトラブル時の解決にもjsの基礎知識は欠かせない。

