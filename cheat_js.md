##### vscode拡張機能
 * JS-CSS-HTML Formatter ...カーソルが強制的に戻るから使わない
---
##### エラーチェック
'use strict'

### jsの動きの基本
要素を取得→加工→処理を行う

#### 変数の種類
|変数の種類|有効範囲|値の変更|
|----|----|----|
|let|狭い(ブロックスコープ)|〇|
|const|狭い(ブロックスコープ)|×|
|var|普通(関数のみスコープ)|〇|
|宣言なし変数|すべてのPGから(グローバル)|〇|
 * constant; 常数
※定数は慣習的に大文字で記述する
 　const GU = 1; 
 * var; variable(変数)
 　{}ブロック外でも有効。自身の関数内でのみ有効
 * let; ～とする
　プログラムのどこからでも参照可能
---
#### ダイアログボックス
 * alert(' *** ') ....戻り値はundifined（未定義） 
 * confirm(' *** ') ...YES/NO  Y=true, N=false  (※確認)
 * prompt(' ***') ...文字列入力ボックスを表示。戻り値は入力された文字列。(※促す)
---
#### 文字列を数値に変換
##### parseFloat(budget) ...小数点も計算
```javascript:hello.javascript
let budget = prompt('所持金を数字で数字で入力してください');
budget = parseFloat(budget); //文字列budgetを数値に変換
if(budget >= 1500){
  alert('ピザを注文しました');
}
```

##### parseInt(budget) ...整数表示される(1.5は1と表示)。pは大文字だとエラーになる
```
parseInt("1000", 2);　2進数で表示した1000を10進数に変換します。
parseInt("010", 8);　8進数で表示した010を10進数に変換します。
parseInt("8", 10);　10進数で表示した8を10進数に変換します。
parseInt("0x8", 16);　16進数で表示した0x8を10進数に変換します。
```
第2引数が10なら10進数

---
##### Math.***()
 * Math.ramdom() ...0以上～1未満の数字を生成
 * Math.floor() ...()に指定された数値以下の最大の整数を作る
 　Math.floor(2.9)　→　2となる
 　Math.floor(3)　→　3となる
* 組み合わせ例：`Math.floor(Math.random() * 3) + 1;`
　0-2を生成し、1を足す（結果は1-3のランダムな数字となる）
---
## 関数
##### function ※機能
 ```javascript
 functuin 関数名 (引数1, 引数2) { 
   行いたい処理；
   return 戻り値;
 } 
 ```
※returnがない(戻り値がない)場合は、処理を最後まで実行し、戻り値は「undefined ※未定義」となって終了する

#### 引数
##### デフォルト引数
```javascript
function greet ( 引数1 = 'デフォルト値1' , 引数2 = 'デフォルト値2'){
  行いたい処理
}
```
引数の値が指定されていない場合に「代わりの名前」が値として使用される。引数を指定せずに実行してもエラーを起こさない。
```javascript
function greet(name = '名無しさん') {
  let message = 'こんにちは';
  alert(message + name);
  return;
}
greet();  //こんにちは名無しさん と表示される
greet('たろうさん');  //こんにちはたろうさん  が表示される
```
#### 無名関数
```
let 変数名 = function (引数1, 2, ...){
  行いたい処理;
  return 戻り値;
}
```
functionの後ろの関数名を省略できる。
変数名に代入しておき、「変数名()」の形式でこのメソッドを呼び出せる 

#### アロー関数
[基本構文 記事中段](https://it-biz.online/web-design/arrow-function/)

```javascript
let name = prompt('名前を入力してください');
// greet(name);
// function greet(name) {
//   let message = 'こんにちは';
//   alert(message + name);
//   return;
// }
```
アロー式に置き換え
```javascript
let name = prompt('名前を入力してください');
let greet = () => {
  let message = 'こんにちは';
  alert(message + name);
  return;
}
greet();
```
return省略
```javascript
let greet = () => {
  let message = 'こんにちは';
  alert(message + name);
}
greet();
```

#### 即時関数
```javascript
( function () {
  この中に記述した処理はすぐに実行される
  この中で宣言した変数は、ローカル変数となる
}) ();
```
関数全体を()で囲み、最後に();を付ける

---
#### 繰り返し処理
##### while
```
let year = 2000;
while (year <= 2100) {
  if (year % 4) {
    console.log(year + ':冬季オリンピック');
  } else {
    console.log(year + ':夏季オリンピック');
  }
  year = year + 2;
}
```
 * continue ...繰り返しをスキップし、whileの先頭にジャンプ
 * break 繰り返し処理を途中で中断して処理を抜ける
##### do while
```
do {
  行いたい処理
} while (year <= 2000);
```
##### for文
```
for (let i = 1; i <= 100; i++) {
  console.log(i + '回目のこんにちは');
}
```
---
### オブジェクト
 * windowオブジェクト
```
window.console.log('hello'); //windowは省略可能
window.alert('hello'); //windowは省略可能
```
#### window < document < element
 * window オブジェクト
 * document オブジェクト
 * element オブジェクト
---
## DOM
##### Document Object Model
```
documnt
       --head
             --html
                   --body
                         --h1
                         --p
```

### DOM操作：内容の書き換え

##### HTML要素を取得(ID属性)
`HTML要素が持つid属性の値を手掛かりに`、HTML要素を取得する
・let `element` = document.getElementById(`'sample'`);
・let `変数` = document.getElementById(`'id属性の値'`);
id="sample"の要素を取得して変数elementに代入

##### HTML要素の内容を書き換える
・`element`.innnerHTML = '`サンプル`';
・`HTML要素`.innnerHTML = '`書き換えたい内容`';
id="sample"の要素の内容を「\<p>こんにちは\</p>」に書き換える場合
```
let element = document.getElementById('sample')
element.innnerHTML = '<p>こんにちは</p>';
```
##### innerHTMLにHTMLタグを代入すると要素になる
```html:pr.html
  <body>
    <div id="practice">練習</div>
    <script src="js/app.js"></script>
  </body>
```
```javascript:pr.javascript
let practice = document.getElementById('practice');
practice.innerHTML = '<h1>れんしゅう</h1>';
```
##### \<h1>のようなHTMLタグを含む文字列の場合
##### InnerText
`innerHTML`では、ブラウザが\<h1>タグを解釈して新しいHTML要素が作られる。文章そのままのテキストで「\<h1>」と表示させたい場合は、`InnerText`プロパティを使う。
##### オブジェクトの参照返し
※要素の操作について
 データ型が「オブジェクト」のデータを変数に代入したときだけは、データがコピーされるのではなく、元のデータを参照するための情報が変数に記憶される。変数を使用して操作すると、元のオブジェクトが変更される。
```
. jsで変数を操作　→　HTMLのelementオブジェクト("代入元")が書き変わる
```
---
### DOM操作：要素へのアクセス
#### querySelectorメソッド
document.querySelector('`.about`');
document.querySelector('`CSSセレクタ`');
 * HTML文書の先頭から順に探し始めて、`引数に指定したセレクタに最初にマッチ`した要素が取得される。

```html
<section class="about">
  <h2>このサイトについて</h2>
  <p>このサイトは...です</p>
</section>
```

```javascript
let element = document.querySelector('.about h2');
//「.aboutセレクタ」の「h2」要素を取得
```
---
### 複数の要素を取得・操作する

#### querySelectorAll(' *** ')
 * 引数に指定したCSSセレクタにマッチするすべての要素を取得できる
戻り値はマッチした要素をまとめた`「NodeListオブジェクト」`になる。
要素を操作する際は**事前にNodeListオブジェクトから取り出す**必要がある。
##### NodeListオブジェクトから取り出し
 * オブジェクト名[0]
* for文ですべての要素を取り出し、lengthの値未満となるように記述することで、すべての要素に処理が可能。
```javascript
// CSSセレクタが="a.button"の要素をすべて取得
let nodeList = document.querySelectorAll('a.button');

// 最初にマッチした要素を取得
let firstElement = nodeList[0];

// 取得したすべての要素をコンソールに表示
for (let i = 0; i < nodeList.length; i++) {
  console.log('nodeList');
}
```
#### 要素の取得に用いられるメソッド
|メソッド|引数|戻り値|
| ---- | ---- | ---- |
|getElementById()|id属性値|Elementオブジェクト|
|querySelector()|CSSセレクタ|Elementオブジェクト|
|querySelectorAll()|CSSセレクタ|NodeListオブジェクト|
|getElementsByClassName()|クラス属性値|NodeListオブジェクト|
|getElementsByName()|name属性値|NodeListオブジェクト|
|getElementsByTagName()|タグ名|NodeListオブジェクト|
----
### DOM操作：CSSの変更
#### jsから要素のスタイルを変更
 *  styleプロパティ
`element`.style.`color` = '`#FF0000`';
`要素`.style.`CSSプロパティ名` = '`プロパティ値`';

```javascript
// id="sample"のHTML要素の文字色を「#FF0000」に変更
let element = document.getElementById('sample');
element.style.color = '#FF0000';
```
※CSSのハイフン「-」の書き換え
background-color
backgroundColor
font-size
fontSize
##### サンプル
```html
  <body>
    <div id="practice">練習</div>
    <script src="js/app.js"></script>
  </body>
```
```javascript
let practice = document.getElementById('practice');
practice.innerHTML = '<h1>れんしゅう</h1>';
practice.style.backgroundColor = '#999999'; //濃いグレー
practice.style.fontSize = '30px';
practice.style.color = '#FFFFFF'; //白
```
---
### DOM操作：要素の追加
##### 要素を作り属性と内容を設定する
##### createElement
 * タグだけを指定した要素を作る
##### setAttribute
 * 属性を指定する

 let `element` = document.createElement('`h1`');
`element`.setAttribute('`id`','`first`');

 let `変数` = document.createElement('`タグ名`');
`変数`.setAttribute('`属性名`','`属性値`');

##### insertBefore
 * 新しい要素をHTML文書に追加する

`element`.insertBefore(`newelement`, `targetelement`)
`親要素`.insertBefore(`追加する要素`, `ターゲット要素`)
  
※`追加したい要素`は親要素(element)の`子要素`である。
第2引数で指定した**ターゲット要素の前**に、追加したい要素が追加される。
`追加したい要素`を**最後の子要素にしたい場合**は`第2引数`を「`null`」にする。

---

##### DOMの観点ではWebページはNodeという単位で構成されている
* Nodeは基本的なオブジェクト
  * 要素、属性、テキストもノード
  * 要素はノードの一種という認識でOK
---
##### サンプル
 * 要素を追加
 
```html
  <body>
    <div id="practice">練習</div>
    <script src="js/app.js"></script>
  </body>
```

```javascript
let practice = document.getElementById('practice');
practice.innerHTML = '<h1>れんしゅう</h1>';
practice.style.backgroundColor = '#999999';
practice.style.fontSize = '30px'; //濃いグレー
practice.style.color = '#FFFFFF'; //白

// 要素を追加
let first = document.createElement('div'); //新しいdiv要素を作成
//属性と内容を設定
first.setAttribute('id','first'); 
first.innerHTML = '<p>要素を追加</p>';
practice.insertBefore(first, null); //要素をHTMLに追加

// さらに要素を追加
let second = document.createElement('div'); //要素を作成
second.setAttribute('id', 'second');
second.innerHTML = '<p>さらに要素を追加</p>';
practice.insertBefore(second, first); //要素を追加
```
---
### DOM操作：要素の削除
 * まず削除したい要素の**親要素を探す**
#### parentElement
 * 親要素のオブジェクトを取得するプロパティ
   * ###### 取得後に子要素を削除する
#### removeChild
 * 子要素を削除するメソッド
##### parentElement プロパティ
let `parent` = `targetelement`.parentElement
let `親要素を代入する変数` = `子要素`.parentElement
##### removeChild メソッド
`parent`.removeChile(`targetelement`);
`親要素`.removeChile(`削除したい要素`);
 
 ※削除したい要素の親要素がわからない場合は、`parentElement`プロパティから取得できる。
```js
// 要素を削除
let parent = first.parentElement; //親要素を取得
parent.removeChild(first); //要素を削除
```
---
##### jQuery
ライブラリ。ブラウザ間の違いを修正。\
##### [Can I Use...](https://caniuse.com/)
jsのメソッドやCSSプロパティのブラウザごとの対応状況を確認できるサイト

---
### イベントの設定 ３つの方法
 * 主流はイベントリスナーで指定する(**複数の設定が行える**)
   * 要素のプロパティで指定（イベントハンドラ）
   * HTMLファイルで要素の属性に指定する（イベントハンドラ）
イベントリスナーでの指定以外の方法は**1要素・1イベントにつき1つの設定**しか行うことができない
#### イベントリスナー
 * イベントの聞き手
 イベントが発生したときにそれを聞きつけて、あらかじめ指定しておいた関数を実行する

##### addEventListener
 * addEventListenerメソッドで名前のある関数を指定
`element`.addEventListener('`click`', `func`);
`対象の要素`.addEventListener('`イベントタイプ名`', `実行したい関数名`);
　※上記funcのように名前のある関数を使う場合は、引数を渡せない
--
 * addEventListenerメソッドで無名関数を指定
`element`.addEventListener('`click`', `function(*****)` { 行いたい処理 });
`element`.addEventListener('`click`', `無名関数` { 行いたい処理 });
　※引数を渡したい場合は無名関数を使い、その中で関数に引数を渡す
---
### イベントの種類
##### マウス操作
|イベントタイプ名|発生タイミング|
|----|----|
|click|要素をクリックしたとき|
|dblclick|ダブルクリック|
|mouseout|マウスカーソルが要素上から外に出た時|
|mouseover|マウスカーソルが要素上に乗った時|
|mouseup|マウスボタンを話したとき|
|mousedown|マウスボタンを押下したとき|
|mousemove|マウスを動かしているとき|
※click(= mousedown + mouseup)と同じ動き
##### キーボード操作
|イベントタイプ名|発生タイミング|
|----|----|
|keyup|キーを放したとき|
|keydown|キー押下時|
|keypress|キーを押し続けているとき|
##### その他
|イベントタイプ名|発生タイミング|
|----|----|
|blur|フォーカスが外れたとき|
|focus|フォーカスが当たった時|
|change|内容が変更されたとき|
|select|テキストが選択されたとき|
|submit|フォームを送信しようとしたとき|
|reset|フォームがリセットされたとき|
|abort(※中断)|画像の読み込みを中断したとき|
|error|画像の読み込み中にエラーが発生したとき|
|load|ページや画像の読み込みが完了したとき|
|unload|アンロード時（ページ遷移時など）|
----
#### イベントハンドラ
##### 要素のプロパティを利用して指定する方法
`element`.`onclick` = `elementclick`;
`要素`.`イベントハンドラ名` = `実行したい関数名`;
##### HTMLファイルで要素の属性に指定する直接記述する方法
\<button id ="test" `onclick`="`elementclick();`">○○○○\</button>
\<button id ="test" `イベントハンドラ名`="`関数の呼び出し();`">○○○○\</button>
 * HTMLに書く場合は、関数名だけでなく行末に();を付ける
 * イベントハンドラ名は基本的にイベントタイプ名の先頭に**on**を付ける
---
#### イベントオブジェクト
イベントリスナーで指定した関数の第1引数に自動で受け渡される
 * 使用する場合は、その代入先となる引数※例では（event）を指定するだけでOK
 押されたキーの情報はkeyプロパティに格納されている
 ```js
//  押されたキーを取得する
document.addEventListener('keydown', function (event) { //eventオブジェクトが引数に渡される
  console.log(event.key); //コンソールにキーを表示
});
 ```

#### Event.target プロパティ
##### イベントを発生させたオブジェクトへの参照です。 
theTarget = event.target
```js
// リストを作ります
var ul = document.createElement('ul');
document.body.appendChild(ul);

var li1 = document.createElement('li');
var li2 = document.createElement('li');
ul.appendChild(li1);
ul.appendChild(li2);

function hide(e){
  // e.target はクリックされた <li> 要素を参照します
  // これはコンテキスト内の親 <ul> を参照する e.currentTarget とは異なります
  e.target.style.visibility = 'hidden';
}

// リストにリスナーを接続します
// <li> がクリックされた時に発火します
ul.addEventListener('click', hide, false);
```

 ---
#### getAttributeメソッド
その要素のに任意の**属性値を取得**する
`element`.getAttribute('`maxlength`');
`要素`.getAttribute('`属性名`');
```html
<textarea name="textarea"         <textarea name="textarea" id="textarea" cols="50" rows="30" maxlength="500"></textarea>
//maxlength="500"の属性値500を取得

````
##### textarea.value.length
文字数を調べる
valueプロパティ... テキストエリアに入力された文字列を取得する働きを持つ
lengthプロパティ... さらにその後、長さを調べる 
```js
// フォームの要素を取得
let button = document.getElementById('button');
let form = document.getElementById('form');
let textarea = document.getElementById('textarea'); //textarea要素を取得

// 文字数制限
let maxTextNum = textarea.getAttribute('maxlength'); //属性値を調べる

/* 要素の追加 *********************************/
// 残り文字数を表示する要素の追加
let textMessage = document.createElement('div');
let parent = textarea.parentElement;
parent.insertBefore(textMessage, textarea);

// テキストエリアでキーをタイプしたとき
textarea.addEventListener('keyup', function () {
  let currentTextNum = textarea.value.length; //文字数を調べる
  textMessage.innerHTML = '<p>あと' + (maxTextNum - currentTextNum) + '文字入力できます</p>';  //残り文字数を表示
});
```
---
#### Stringオブジェクトを使用する
`length`は`Stringオブジェクト`のプロパティ
その他、Stringオブジェクトには
**trim**... 前後の空白を消す
**raplace**... 検索置換
などがある
 * lengthプロパティは以下のように文字列を確認することができる
 `あいうえお`.length; &nbsp;&nbsp;&nbsp;//5
 ##### jsでは文字列型でもStringオブジェクトがもつプロパティを直接利用できる
 ---
 ### setIntervalメソッド
 #### タイマー処理
一定間隔で処理を繰り返す
 * **戻り値には、セットしたタイマーを解除するためのIDが発行される**ので、通常は使用開始と同時に「タイマー識別用の変数」に記録しておく
 * 第1引数には実行したい処理
 * 第2引数には実行したい間隔をミリ秒で指定する
 * **タイマーを解除する際はclearIntervalメソッドの変数**に、記憶しておいた「タイマー識別用の変数」を指定すればOK
#### setIntervalメソッド
let `timer` = setInterval(`timefunc`, `200`);
let `タイマー識別用の変数` = setInterval(`実行したい関数`, `間隔`);

#### clearIntervalメソッド
clearInterval(`timer`);
clearInterval(`タイマー識別用の変数`);
#### setTimeout()メソッド
 * 基本的にはsetIntervalと同じ
こちらは**一定時間後に一度だけ処理を実行する**
 * 第1引数に実行したい処理を記述した関数を指定
 * 第2引数に実行までの待ち時間（ミリ秒）を指定
##### setIntervalの注意点
1回の処理が**繰り返しの時間内に終わりきらなかった場合、前の処理が終了する前に次の処理を開始**してしまう
 * それを回避するためにsetTimeoutメソッドを使用することもできる。
 * setIntervalと違い、必ず「**処理が終了してから」間隔を空けて次の処理を実行**してくれるので、実行時間がわからないときは、setTimeoutを使うほうが安全
#### setTimeoutメソッド
let `timer` = setTimeout(`timerfunc`, `1000`);
let `タイマー識別用の変数` = setTimeout(`実行したい関数`, `待ち時間`);
#### clearTimeoutメソッド
`clearTimeout`(timer);
`タイマー識別用の変数`(timer);
```js
setTimeoutメソッドによる繰り返し処理の例

function foo() {
  // setTimeoutメソッドで1秒後に関数fooを呼び出す
  setTimeout(foo, 1000);
  console.log('繰り返し');
}
foo();
```
---
### 配列
```js
// おみくじの結果データを作成
results = ['大吉', '吉', '中吉', '小吉','凶'];

// 配列をコンソールに表示
console.log(results);

// インデックスが0の要素をコンソールに表示
console.log(results[0]);

// 配列に所属するすべてのデータをfor文ですべて表示
for (let i = 0; i < results.length; i++) {
  console.log('index：' + i + 'データ：' + results[i]);
}
```
#### オブジェクトを作成し、データをまとめる
let `human` = {  //{はオブジェクトの始まり
  `name`: '`山田一郎`',
  `age`: `31`,
  height: 170,
  weight: 70
}     //}はオブジェクトの終わり
  
let `変数名` = {  //{はオブジェクトの始まり
  `プロパティ1`: '`データ1`',
  `プロパティ2`: `データ2`,
  height: 170,
  weight: 70
}     //}はオブジェクトの終わり
```js
console.log(human)  //{name: "山田一郎", age: 31, height: 170, weight: 70}
console.log(human.name)  //山田一郎
```

#### 独自のメソッドを作る
独自メソッドを定義したい場合、オブジェクト定義{}の中で、**「メソッド名:」の後に無名関数function(,)を記述**する。
メソッドのプロパティの一種なので、書き方はプロパティの書き換えと一緒。（P名→M名に、データの部分→無名関数に置き換えればOK）

##### メソッドの定義
```js
let 変数名 = {
  メソッド名1: function (引数1, 引数2... ) {
    // 実行したい処理
  },
  ...
}
```

##### メソッドのイメージ
```js
let おみくじ = {  //おみくじオブジェクトを定義
  くじを引く: function () {
    // くじを引くメソッドの定義として、結果を繰り返す処理を書く
  }
}
// くじを引くメソッドの結果をコンソールに表示
console.log(おみくじ.くじを引く());  //「くじを引く」メソッドを呼び出す
```
おみくじプログラム
```js
// おみくじオブジェクトの定義
// omikuji.results  ...imokujiオブジェクトの、resultsプロパティ。プロパティは後で呼び出せる
let omikuji = {
  results: ["大吉", "吉", "中吉", "小吉", "凶"],  //omikujiのオブジェクト1(プロパティ):[データ]
  getResult: function () {  //omikujiオブジェクトのオブジェクト2(getresultメソッド)」: [データは無名関数]
    let results = this.results; //無形関数内では、omikuji(this)のプロパティ(オブジェクト1)である[results配列]を呼び出し変数に格納


    return results[Math.floor(Math.random() * results.length)];  //results[配列]のインデックスに0-4を入れて処理を返す。
    // 0-1未満 * 5(配列の長さ)。その計算の数値以下の最大の整数にする(結果は0-4)
  } //getResultメソッドの処理結果(omikujiオブジェクトのメソッド:が処理したデータ)としてresults[0-4]のインデックス番号となる。
} //この時点でomikujiオブジェクトは{results配列プロパティ, results[0-4](メソッド処理の戻り値)}のデータを持つオブジェクトを保有している

//呼び出しはc.log(omikuji.getResult());  
// c.log(omikuji.getResult); ではない
console.log(omikuji.getResult());  //omikujiのgetResultメソッドを呼び出して結果を表示。getResult()の戻り値はresults[0-4]なので、インデックス番号に割り当てられた、results配列プロパティの: ["大吉", "吉", "中吉", "小吉", "凶"] のデータが表示される
```

サンプル
```html
<body>
  <h1>おみくじ</h1>
  <p><input type="button" id="getResult" value="おみくじを引く"></p>
  <div id="result"></div>
  <script src="js/app.js"></script>
</body>
```

```js
// おみくじオブジェクトの定義
let omikuji = {
  results: ["大吉", "吉", "中吉", "小吉", "凶"],  //omikujiのオブジェクト1(プロパティ):[データ]
  getResult: function () {  //omikujiオブジェクトのオブジェクト2(getresultメソッド)」: [データは無名関数]
    let results = this.results; //無形関数内では、omikuji(this)のプロパティ(オブジェクト1)である[results配列]を呼び出し変数に格納

    return results[Math.floor(Math.random() * results.length)];  //results[配列]のインデックスに[0-4]を入れて処理を返す。
    // 0-1未満 * 5(配列の長さ)。その計算の数値以下の最大の整数にする(結果は0-4)
  }
} //{results配列プロパティ, results[0-4]}のオブジェクトを保有

// 要素オブジェクトの取得
let getResult = document.getElementById('getResult');
let result = document.getElementById('result');

// イベントの登録
getResult.addEventListener('click', function () {
result.innerHTML = '結果：' + omikuji.getResult() + 'でした！';  //omikuji.getResult() 行頭にomikuji(オブジェクト)がないとメソッドを呼び出せない
});
```
---
#### thisについて
 * 関数の外部で使う場合
 console.log(this === window); ...厳密に等しいので結果はtrue
**関数の定義外で使ったthisはwindowオブジェクト**を指す
 * **メソッド定義の中で使う場合はオブジェクトを指す**
  let omikuji ={
    let results = `this`.results;
  } //このthisはomikujiオブジェクトを指す

----
alt=  タイトルチップ（代替えテキスト）
#### カスタムデータ属性
##### データのやりとりに便利
 ・例えば「写真画像に関連する音楽ファイルの名前」をデータに指定する場合、「カスタムデータ属性」というオリジナル属性を作る。
・カスタムデータ属性では「`data-xxx`」 という形式で好きな属性名を付けることができ、任意のデータをHTML要素に関連付けてセットすることができる。
 * setAttribute('`data-bgm`'), 属性値); //カスタムデータ属性のセット
 * setAttribute('`data-bgm`') //属性値の参照
---

#### 写真画像を選択させる(フォトギャラリー)

<details><summary>注釈多めサンプルコード</summary><div>

```js
// オブジェクトを配列でまとめる
// 呼び出す際にプロパティ名が必要なもの...オブジェクト
// 必要無いもの...配列
// でまとめると扱いやすいデータになる

// アルバムデータの作成(写真画像とキャプションまとめたアルバム)
// src(プロパティ) , msg(キャプション)
let album = [
  { src: 'img/1.jpg', msg: '山道の緑が気持ちいい' },
  { src: 'img/2.jpg', msg: '階段がきつかった' },
  { src: 'img/3.jpg', msg: '高尾山' },
  { src: 'img/4.jpg', msg: '帰りはロープウェイでスイスイ' },
  { src: 'img/5.jpg', msg: '締めのソバ' }
];

// 最初のデータを表示しておく
// メインの写真画像を準備する
let mainImage = document.createElement('img'); //img要素を作成
mainImage.setAttribute('src', album[0].src); //album[0]から、src属性をセット(src属性に写真画像の場所を指定)
mainImage.setAttribute('alt', album[0].msg); //album[0]から、alt属性をセット(キャプションの値をセット)

// メインのキャプションを準備する
let mainMsg = document.createElement('p'); //p要素を新規作成
mainMsg.innerText = mainImage.alt; //キャプションをセット

// HTMLに反映する
let mainFlame = document.querySelector('#gallery .main'); //HTML文書の先頭から順に探し始めて、引数に指定したCSSセレクタに最初にマッチした要素を取得
mainFlame.insertBefore(mainImage, null); //要素を追加
mainFlame.insertBefore(mainMsg, null);


// サム(thumb)ネイル写真画像の表示
let thumbFlame = document.querySelector('#gallery .thumb'); //CSSセレクタ要素を取得
for (let i = 0; i < album.length; i++) {
  let thumbImage = document.createElement('img'); //img要素を作成
  thumbImage.setAttribute('src', album[i].src); //(#gallery .thumbタグ内に作成したimgタグに)src属性をセット
  thumbImage.setAttribute('msg', album[i].msg); //msg属性をセット
  thumbFlame.insertBefore(thumbImage, null); //(thumbImageの最後の要素として)img要素をHTML文書に追加
}

// サムネイルの親要素であるthumbFlameにクリックイベントを登録する
// イベントが発生したときにクリックされたのがimg要素かどうか判定する
thumbFlame.addEventListener('click', function (event) { //イベントオブジェクト。イベントリスナーで指定した関数の第1引数(今回はeventと命名)にイベントオブジェクトが自動で受け渡される

  // src属性がプロパティ値を持っているか（空ではないか）確認
  //注意：HTML要素がもつすべての属性がjsのオブジェクトにprptyとして提供されているわけではない。srcなど主要なもののみ
  // プロパティが無いものは、getAttributeやsetAttributeを使って操作する
  if (event.target.src) { //イベントオブジェクトを使用する場合は、その代入先となる引数※今回は（event）を指定するだけでOK。
    //  event.target.src はクリックされた(thumbFlame：#gallery .thumbタグ内の) <imgタグ>の<src="xxx"> 要素を参照します
  }
});
```
</div></details>



<details><summary>完成系コード</summary><div>

```html
html
<!DOCTYPE html>
<html land="ja">
  <head>
    <meta charset="UTF-8" />
    <title>インプレス いちばんやさしいJavaScriptの教本</title>
    <link rel="stylesheet" href="css/style.css" />
  </head>

  <body>
    <div id="gallery">
      <div class="main">
        <!-- javascriptの処理 が入る
         <img src="img/1.jpg" alt="山道の緑が気持ちいい">
          <p>山道の緑が気持ちいい</p> -->

</div>

      <div class="thumb">
        <!-- javascriptの処理 が入る
        <img src="img/1.jpg" alt="ここにテキスト">
        <img src="img/1.jpg" alt="ここにテキスト">
        <img src="img/1.jpg" alt="ここにテキスト">
        <img src="img/1.jpg" alt="ここにテキスト">
        <img src="img/1.jpg" alt="ここにテキスト"> -->
      </div>
    </div>

    <script src="js/app.js"></script>
  </body>
</html>
```

```js
js
// オブジェクトを配列でまとめる
// 呼び出す際にプロパティ名が必要なもの...オブジェクト
// 必要無いもの...配列
// でまとめると扱いやすいデータになる

// アルバムデータの作成(写真画像とキャプションまとめたアルバム)
// src(プロパティ) , msg(キャプション)
let album = [
  { src: 'img/1.jpg', msg: '山道の緑が気持ちいい' },
  { src: 'img/2.jpg', msg: '階段がきつかった' },
  { src: 'img/3.jpg', msg: '高尾山' },
  { src: 'img/4.jpg', msg: '帰りはロープウェイでスイスイ' },
  { src: 'img/5.jpg', msg: '締めのソバ' }
];

// 最初のデータを表示しておく
// メインの写真画像を準備する
let mainImage = document.createElement('img'); //img要素を作成
mainImage.setAttribute('src', album[0].src); //album[0]から、src属性をセット(src属性に写真画像の場所を指定)
mainImage.setAttribute('alt', album[0].msg); //album[0]から、alt属性をセット(キャプションの値をセット)

// メインのキャプションを準備する
let mainMsg = document.createElement('p'); //p要素を新規作成
mainMsg.innerText = mainImage.alt; //キャプションをセット

// HTMLに反映する
let mainFlame = document.querySelector('#gallery .main'); //HTML文書の先頭から順に探し始めて、引数に指定したCSSセレクタに最初にマッチした要素を取得
mainFlame.insertBefore(mainImage, null); //要素を追加
mainFlame.insertBefore(mainMsg, null);


// サム(thumb)ネイル写真画像の表示
let thumbFlame = document.querySelector('#gallery .thumb'); //CSSセレクタ要素を取得
for (let i = 0; i < album.length; i++) {
  let thumbImage = document.createElement('img'); //img要素を作成
  thumbImage.setAttribute('src', album[i].src); //(#gallery .thumbタグ内に作成したimgタグに)src属性をセット
  thumbImage.setAttribute('alt', album[i].msg); //msg属性をセット
  thumbFlame.insertBefore(thumbImage, null); //(thumbImageの最後の要素として)img要素をHTML文書に追加
}

// サムネイルの親要素であるthumbFlameにクリックイベントを登録する
// イベントが発生したときにクリックされたのがimg要素かどうか判定する
thumbFlame.addEventListener('click', function (event) { //イベントリスナーで指定した関数の第1引数eventにイベントオブジェクト

  // src属性がプロパティ値を持っているか（空ではないか）確認
  if (event.target.src) { //  クリックされたthumbFlame(#gallery>.thumb>imgタグ内>の<src="xxx"> 要素)を参照
    // 写真画像とキャプションを変更する

    // console.log(event.target.src); //値の確認
    // console.log(event.target.alt);

    mainImage.src = event.target.src; //mainImageのsrc属性に、クリックされたimg要素(thumbFlame(#gallery>.thumb>imgタグ要素内)のsrc属性値（パス）を代入
    mainMsg.innerText = event.target.alt; //mainMsgのテキストを、クリックされたimg要素のalt属性値を指定して書き換える

  }
});
```

```css
css
/* 全体のスタイルを調整 */
body {
  background-color: #444444;
  box-sizing: border-box;
  text-align: center;
}

/* 余白調整 */
/*id名#がgalleryのdin要素に対して */
#gallery {
  margin: auto;
  padding-top: 40px;
  width: 500px;
}

/* 写真に枠を付ける */
/* #gallery .main img */
.main img {
  border: 4px solid #fff;
  box-shadow: 0 0 14px #000;
  width: 100%;
}

/* キャプションを目立たせる */
/* #gallery .main p */
.main p {
  color: #bbb;
  font-size: 20px;
  font-weight: bold;
}

/* 画像を小さく、丸くする */
.thumb img{
  border: 4px solid #fff;
  border-radius:400px;
  box-shadow: 0 0 10px #000;
  height:60px;
  margin: 10px;
  width: 60px;  
}
```
</div></details>

---






