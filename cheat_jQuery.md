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



