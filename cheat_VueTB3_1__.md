# Vue.js
## Vue.jsのツボとコツ　第3章～
### vue.jsで商品一覧を描画する
  
 - 絞り込み検索機能を備えたECサイトの商品一覧ページをvueで作る
 - まずは、HTMLとCSSだけでモックアップ(大雑把な模型)を作り、段階的にVue.jsを適用していく

**何をデータ化して、どこをテンプレート化するか、の発想の仕方に慣れていく** 

---  
### 初期表示
 - ECサイトの商品データは、本来は専用の管理画面を通してデータベースに登録されているが、今回はまだサーバを使わないので、HTMLやjsに直接記述する
 - 最初はすべての商品が表示される。
 - 表示された商品の件数が「検索結果　●件」と表示される
 - 商品には送料無料のもの、セール対象のものがあり、絞り込みのチェックボックスがある
 - 初期表示では「すべての商品」にチェックがついていない状態とする
 - 並び替えのセレクトボックスには「標準」と「価格が安い順」を表示し、ユーザーが選択を切り替えると、指定の順番に商品が並び変わる

---

### 機能詳細
#### 商品部分の表示
 - 各商品はタイル状のボックスで表示
 - ボックス内に表示する項目は
 ・「商品画像」
 ・「商品名」
 ・「価格」
 ・「送料」
 ただし、送料無料の商品は「送料無料」と表示
 セール対象の商品は左上に「SALE」マークを表示

---

#### 商品の絞り込み
 - チェックボックスのチェック状態を切り替えると、条件に該当する商品だけを表示
 - 「セール対象」にチェックをつけると、セール対象の商品だけを表示
 - 「送料無料」にチェックをつけると、送料無料の商品だけを表示
 - 2つともチェックをつけた場合は、両方の条件に該当する商品だけを表示
 - チェック状態を切り替えても、商品の並び順は変わらない

---

#### 商品の並び替え
 - ユーザーが商品を比較しやすいように、セレクトボックスで商品一覧の並び替えができる
 - 「標準」を選択すると、初期表示の並び順と同じ順番で表示
 - 「価格が安い順」を選択すると、安い順に商品を並び変える。
   - ただし、チェックボックスで絞り込んだ結果には影響を与えない
   - たとえば、「セール対象」にチェックをつけている場合、絞り込まれた商品の中で価格が安い順番に並び変わる

  
## モックアップの作成
### HTMLとCSSで静的なページを作成する
 - HTML,CSSだけで完成イメージと同じ見た目の静的なページを作る
 - データの持たせ方、絞り込みなどの動的な機能は一切考えず、直接HTMLに商品データを書き込んでいく
  
リスト3-2-1　表示のモックアップ(main.html,main.css)
<details><summary>サンプルコードhtml</summary><div>

```html
html

<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>商品一覧</title>
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/normalize/5.0.0/normalize.min.css"
    />
    <link rel="stylesheet" href="main3_2.css" />
  </head>
  <body>
    <div id="app">
      <div class="container">
        <h1 class="pageTitle">商品一覧</h1>
        <!-- 検索欄 -->
        <div class="search">
          <div class="result">
            検索結果
            <span class="count">6件</span>
          </div>
          <div class="condition">
            <div class="target">
              <label><input type="checkbox" /> セール対象</label>
              <label><input type="checkbox" /> 送料無料</label>
            </div>
            <div class="sort">
              <label for="sort">並び替え</label>
              <select id="sort" class="sorting">
                <option value="1">標準</option>
                <option value="2">価格が安い順</option>
              </select>
            </div>
          </div>
        </div>
        <!-- 商品一覧 -->
        <div class="list">
          <div class="item">
            <figure class="image">
              <!--figure※図-->
              <div class="status">SALE</div>
              <img src="images/01.jpg" alt="" />
              <figcaption>Michael<br />スマホケース</figcaption>
            </figure>
            <div class="detail">
              <div class="price"><span>1,580</span>円（税込）</div>
              <div class="shipping-fee none">送料無料</div>
            </div>
          </div>
          <div class="item">
            <figure class="image">
              <div class="status">SALE</div>
              <img src="images/02.jpg" alt="" />
              <figcaption>Raphael<br />スマホケース</figcaption>
            </figure>
            <div class="detail">
              <div class="price"><span>1,580</span>円（税込）</div>
              <div class="shipping-fee none">送料無料</div>
            </div>
          </div>
          <div class="item">
            <figure class="image">
              <div class="status">SALE</div>
              <img src="images/03.jpg" alt="" />
              <figcaption>Gabriel<br />スマホケース</figcaption>
            </figure>
            <div class="detail">
              <div class="price"><span>1,580</span>円（税込）</div>
              <div class="shipping-fee">+送料240円</div>
            </div>
          </div>
          <div class="item">
            <figure class="image">
              <div class="status">SALE</div>
              <img src="images/04.jpg" alt="" />
              <figcaption>Uriel<br />スマホケース</figcaption>
            </figure>
            <div class="detail">
              <div class="price"><span>980</span>円（税込）</div>
              <div class="shipping-fee none">送料無料</div>
            </div>
          </div>
          <div class="item">
            <figure class="image">
              <div class="status">SALE</div>
              <img src="images/05.jpg" alt="" />
              <figcaption>Ariel<br />スマホケース</figcaption>
            </figure>
            <div class="detail">
              <div class="price"><span>980</span>円（税込）</div>
              <div class="shipping-fee none">送料無料</div>
            </div>
          </div>
          <div class="item">
            <figure class="image">
              <div class="status">SALE</div>
              <img src="images/06.jpg" alt="" />
              <figcaption>Azrael<br />スマホケース</figcaption>
            </figure>
            <div class="detail">
              <div class="price"><span>1,580</span>円（税込）</div>
              <div class="shipping-fee none">送料無料</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </body>
</html>
```

</div></details>

<details><summary>サンプルコードCSS</summary><div>

```css
CSS

/* 全体背景：黒、文字：白 */
* {
  border: 1px rgb(174, 177, 142) solid;
}

body {
  background-color: #000;
  color: #fff;
}

/* コンテンツ表示幅：960、画面両幅の余白：自動 */
.container {
  width: 960px;
  margin: 0 auto;
}

/* 画面上部 *********************************************************/

/* 上部「商品一覧」文字の太さ：普通に。ﾀｲﾄﾙに下線入れる */
.pageTitle {
  font-weight: normal;
  border-bottom: 2px solid;
}

/* 検索結果を左寄せに。セール対象～並び替えを右寄せに。検索結果の並びと並列化 */
.search {
  display: flex; /*ある要素に定義するだけで、その直下の要素が並列になる便利なスタイル。フレックスボックスを利用するためには、flexboxを利用する親要素に、display:flexを追加します。これにより、親要素がflexコンテナとなり、子要素がflexアイテムとなります。*/
  justify-content: space-between; /* 均等配置。各アイテムを均等に配置し最初のアイテムは先頭に寄せ、最後のアイテムは末尾に寄せる */
}

.search .target {
  display: inline-block;
  /* 上部のセール対象、送料無料を横並びに */
  /* インラインレベルのブロックコンテナを生成する。要素全体としてはインライン要素のような表示形式だが、内部はブロックボックスで高さ・横幅などを指定できる。 */
}

/* <LABEL>タグはフォームの構成部品（一行テキストボックス・チェックボックス・ラジオボタン等）と、 その項目名（ラベル）を明確に関連付けるための要素です。 これによりチェックボックスやラジオボタンでは、 関連付けられたテキスト部分をクリックしてもチェックを付けることができるようになります。 */
/* <LABEL>タグの使用方法は2通りあります。 1つは<LABEL>タグのfor属性の値と、フォーム部品のid属性の値を同じものにすることで両者を関連付ける方法です。 もう1つは<LABEL>～</LABEL>内にフォーム部品とテキストを含める方法です。後者の方法は、Internet Explorer5や6には対応していないようなので、できるだけ前者を用いた方が良いでしょう。 */
.search .target .label {
  margin-right: 15px;
}

.search .sort {
  display: inline-block;
  /* displayプロパティは、ブロックレベル・インライン・テーブル・ルビ・フレックスコンテナ等の、要素の表示形式を指定する際に使用します。 */
}

/* 商品一覧 ***************************************/
/************************************************/

.list {
  /* listをフレックスボックスにする */
  display: flex;
  /* フレックスアイテムの折り返しの有無、折り返す場合の折り返し行の積み上げ方向を指定できます。wrap 折り返しあり */
  flex-wrap: wrap;
  justify-content: space-between;
  /* 均等間隔で横並びになる。justify※正当化する。space-betweenアイテムの間にスペースを均等に割り付け。
justify-contentプロパティは、コンテナ内全体の主軸方向（初期値では横方向）の揃え位置を指定する際に使用します。
align-contentプロパティの主軸方向（初期値では横方向）版と考えると理解しやすいでしょう。 */
}

/* CSS において ::after は、選択した要素の最後の子要素として擬似要素を作成します。よく content プロパティを使用して、要素に装飾的な内容を追加するために用いられます。この要素は既定でインラインです。 */
.list::after {
  /* contentプロパティは、要素の直前または直後に、文字列や画像などのコンテンツを挿入する際に使用します。 contentプロパティを適用することができるのは、:before擬似要素および:after擬似要素のみです。 */
  content: "";
  display: block; /* ブロックボックスを生成する */
  width: 250px;
}

.item {
  /* flexプロパティは、フレックスコンテナ内のアイテムの幅についてまとめて指定する際に使用
  フレックスアイテムとは、フレックスコンテナ内のアイテムのことです。 具体的に言うと、display:flex; を指定したボックスがフレックスボックス、その子要素がフレックスアイテムです。 */
  flex: 0 1 250px; /*フレックスアイテムの伸び縮みとか。250pxはフレックスアイテムの幅？*/
  margin-bottom: 30px; /* 上下間のフレックスアイテムの余白 */
}

/* positionプロパティは、ボックスの配置方法（基準位置）が、相対位置か絶対位置かを指定する際に使用します。
positionプロパティで指定するのは、配置方法（基準位置）のみです。 実際の表示位置の指定には、 top、 bottom、 left、 rightを併用して、基準位置からの距離を設定する必要があります。 */
/* relative相対位置への配置となります。positionプロパティでstaticを指定した場合に表示される位置が基準位置となります。 */
.item .image {
  position: relative;
  text-align: center; /* image内のSALEや商品名を中央に */
}

.item .image img {
  width: 100%;
  height: auto;
  /* ここで商品画像が均等に並ぶ */
}

.item .status {
  /* absolute: 絶対位置への配置となります。親ボックスにpositionプロパティのstatic以外の値が指定されている場合には、親ボックスの左上が基準位置となります。親ボックスにpositionプロパティのstatic以外の値が指定されていない場合には、ウィンドウ全体の左上が基準位置となります。*/
  position: absolute;
  border-radius: 50%;
  width: 4em; /* 「em」はfont-sizeプロパティの値を1とする大きさ */
  height: 4em;
  font-size: 12px;
  display: flex;
  align-items: center; /* align-itemsプロパティは、コンテナ内のアイテムの交差軸方向（初期値では縦方向）のデフォルト揃え位置を指定する際に使用 */
  justify-content: center;
  background: #bf0000;
  color: #fff;
}

.item .detail {
  text-align: center; /* 価格、送料無料を中央に */
}

.item .price {
  display: inline-block; /* 価格と税込みを1つのインラインブロックにまとめる */
}

.item .price span {
  font-size: 180%; /* 数値価格の大きさ */
}

/* +送料240円 */
.item .shipping-fee {
  display: inline-block; /* +送料240円をインラインブロック化 */
  background-color: #f7cd12;
  color: #000;
}

/* 送料無料 */
.item .shipping-fee.none {
  background-color: #bf0000;
  color: #fff;
}
```

</div></details>

### jsで絞り込み機能を作成する
たとえば「セール商品」にチェックをつけて商品一覧を絞り込む動作を、純粋なjsで実装しようと思うと、次のような処理手順を思いつくかもしれない
##### 手順1
「セール商品」のチェックボックスにchangeイベントハンドラを追加しておく
  
##### 手順2
イベントハンドラが実行されたとき、1つ1つの商品を表す`<div class="item">`要素にアクセスし、その内側にSALEというテキストノードが存在するかどうかを順番に調べていく
  
##### 手順3
もし手順2で調べたノードが存在せず、チェックボックスにチェックがついている場合は、該当の商品を非表示にする。チェックボックスにチェックがついていない場合は、該当の商品を表示する。
  
一見、この手順でよさそうに見えるが、
 - 送料無料との兼ね合いが考慮されていないので、送料無料にチェックがついている場合に本来表示されないはずの商品が表示されてしまう
 - また、チェックを外した場合の手順がないので、一度チェックをつけて非表示になった商品はチェックを外しても表示されなくなってしまう
このような「漏れ」に気づき、正しい動作になるように修正した手順を実装すると、次のようになる
  
---

#### リスト3-2-2　絞り込み機能をjsで実装
「セール対象」「送料無料」のチェックボックスのチェック有無で絞り込みをする

<details><summary>サンプルコードHTML</summary><div>

```html
<!DOCTYPE html>
<!-- リスト3-2-2 「セール対象」「送料無料」のチェックボックスのチェック有無で絞り込みをする -->
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>商品一覧</title>
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/normalize/5.0.0/normalize.min.css"
    />
    <link rel="stylesheet" href="main3_2_2.css" />
  </head>
  <body>
    <div id="app">
      <div class="container">
        <h1 class="pageTitle">商品一覧</h1>
        <!-- 検索欄 -->
        <div class="search">
          <div class="result">
            検索結果
            <span class="count">6件</span>
          </div>
          <div class="condition">
            <div class="target">
              <label><input type="checkbox" /> セール対象</label>
              <label><input type="checkbox" /> 送料無料</label>
            </div>
            <div class="sort">
              <label for="sort">並び替え</label>
              <select id="sort" class="sorting">
                <option value="1">標準</option>
                <option value="2">価格が安い順</option>
              </select>
            </div>
          </div>
        </div>
        <!-- 商品一覧 -->
        <div class="list">
          <div class="item">
            <figure class="image">
              <!--figure※図-->
              <div class="status">SALE</div>
              <img src="images/01.jpg" alt="" />
              <figcaption>Michael<br />スマホケース</figcaption>
            </figure>
            <div class="detail">
              <div class="price"><span>1,580</span>円（税込）</div>
              <div class="shipping-fee none">送料無料</div>
            </div>
          </div>
          <div class="item">
            <figure class="image">
              <div class="status">SALE</div>
              <img src="images/02.jpg" alt="" />
              <figcaption>Raphael<br />スマホケース</figcaption>
            </figure>
            <div class="detail">
              <div class="price"><span>1,580</span>円（税込）</div>
              <!-- ひとつの class属性の値に複数のクラス名をつけて複数のスタイルを適用することもできます。 -->
              <div class="shipping-fee none">送料無料</div>
            </div>
          </div>
          <div class="item">
            <figure class="image">
              <div class="status">SALE</div>
              <img src="images/03.jpg" alt="" />
              <figcaption>Gabriel<br />スマホケース</figcaption>
            </figure>
            <div class="detail">
              <div class="price"><span>1,580</span>円（税込）</div>
              <div class="shipping-fee">+送料240円</div>
            </div>
          </div>
          <div class="item">
            <figure class="image">
              <div class="status">SALE</div>
              <img src="images/04.jpg" alt="" />
              <figcaption>Uriel<br />スマホケース</figcaption>
            </figure>
            <div class="detail">
              <div class="price"><span>980</span>円（税込）</div>
              <div class="shipping-fee none">送料無料</div>
            </div>
          </div>
          <div class="item">
            <figure class="image">
              <img src="images/05.jpg" alt="" />
              <figcaption>Ariel<br />スマホケース</figcaption>
            </figure>
            <div class="detail">
              <div class="price"><span>980</span>円（税込）</div>
              <div class="shipping-fee none">送料無料</div>
            </div>
          </div>
          <div class="item">
            <figure class="image">
              <img src="images/06.jpg" alt="" />
              <figcaption>Azrael<br />スマホケース</figcaption>
            </figure>
            <div class="detail">
              <div class="price"><span>1,580</span>円（税込）</div>
              <div class="shipping-fee none">送料無料</div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!--追加-->
    <script src="main3_2_2.js"></script>
  </body>
</html>

```

</div></details>


<details><summary>サンプルコードjs</summary><div>

```js
js

'use strict'
// リスト3-2-2 「セール対象」「送料無料」のチェックボックスのチェック有無で絞り込みをする 


// コンポーネントのルートノード(この部品の <div id="app">要素)
let nodeApp = document.querySelector('#app');

// チェックボックスのイベントハンドラを登録
let nodeCheckbox = nodeApp.querySelectorAll('input[type="checkbox"]');
//イベント名'change'フォーム要素の選択肢や内容が変更されたとき。addEventLisner:chrome ではデフォルトでfalse。falseがtrueになった場合、DOMの優先順位が上がる
nodeCheckbox[0].addEventListener('change', onCheckChanged, false);
nodeCheckbox[1].addEventListener('change', onCheckChanged, false);

// チェック状態変更イベントハンドラ
function onCheckChanged(event) {

  let nodeItems = nodeApp.querySelectorAll('.item'); //商品ノードのリスト
  let nodeCount = nodeApp.querySelectorAll('.count'); //表示件数のノード
  let count = nodeItems.length; //表示件数(商品ノードのlengthは6)

  // 全ての商品ノードをいったん表示する
  for (let i = 0; i < nodeItems.length; i++) {
    showNode(nodeItems[i]);
  }

  // セール対象のチェックがついている場合
  if (nodeCheckbox[0].checked) { //if(**.checked)は、チェックボックスがチェックされていればtrueを返し、チェックされていなければfalseを返す
    // チェックがついているとき、全ての商品ノードを捜査
    for (let i = 0; i < nodeItems.length; i++) {
      // セール対象の商品ではない場合。isSaleItem関数の結果がtrueが返された（セール商品だった）場合、!で反転しif文は実行されない
      // falseでreturnされた場合、!でtrueに置き換わりif文が実行される
      if (!isSaleItem(nodeItems[i])) {
        // hideNode関数でこの商品を非表示にする。
        hideNode(nodeItems[i]);
        // 商品ノードのlength６から、件数のカウントを減らす
        count--;
      }
    }
  }

  // 送料無料チェックがついている場合
  if (nodeCheckbox[1].checked) {
    // 全ての商品ノードを捜査
    for (let i = 0; i < nodeItems.length; i++) {
      // 送料無料の商品ではない場合
      if (!isDelvFreeItem(nodeItems[i])) {
        // この商品を非表示にする
        hideNode(nodeItems[i]);
        // 件数のカウントを減らす
        count--;
      }
    }
  }
  // 件数を更新
  nodeCount.textContent = count + '件';
}

// セール商品かどうかを判定する関数。trueかfalseを返す。全ての商品ノードnodeItems[i]を引数に貰う。
function isSaleItem(nodeItem) {
  let node = nodeItem.querySelector('.status');
  return (node && node.textContent == 'SALE'); //node(.status)の中身がSALEであり、node.ContextつまりnodeのテキストがSALEだった場合trueを返す。
  //textContent は Node のプロパティで、ノードおよびその子孫のテキストの内容を表します。ノードが document または Doctype 以外のノードタイプの場合、textContent は、コメントと処理命令ノードを除く、すべての子ノードの textContent 属性値を連結したものを返します。 (ノードが子を持たない場合、これは空文字列になります。)
}


// 送料無料かどうかを判定する関数
function isDelvFreeItem(nodeItem) {
  let node = nodeItem.querySelector('.shipping-fee'); //※shipping-fee　none はそれぞれ異なるクラス属性
  return (node && node.textContent == '+送料無料');
  //※.shipping-fee、+送料240円なら1件(+送料240円の商品)を表示。
  //※.shipping-fee、送料無料なら5件(送料無料商品)を表示。
  //※.none、送料無料なら5件(送料無料商品)。
  //※.none、+送料240円なら0件。
}


// ノードを非表示にする関数。呼び出された際に「node(商品ノード要素).style.display='none';」を全ての商品ノードの要素に追加する。<div class="item" style=”display:none”>
function hideNode(node) {
  node.setAttribute('style', 'display:none;');
  //***.setAttribute(name,value);指定の要素に新しい属性を追加します。または指定の要素に存在する属性の値を変更します。name は属性の名前を文字列で表現したもの。value は属性の希望する新しい値
  // 「要素.style.display = 'none';」でその要素が非表示になり、「要素.style.display = 'block';」で表示されます。
}

// ノードを表示する関数。この関数が呼び出された場合、style要素を削除する。
function showNode(node) {
  node.removeAttribute('style');//removeAttribute() メソッドは、指定された名前の属性を要素から削除します。指定された属性が存在しない場合、 removeAttribute() はエラーを発生させずに戻ります。
}
```

</div></details>

  
##### 答えは1つではない
上記はイベントハンドラの可読性を維持するために、
 - ノードの表示や非表示
 - セール対象や送料無料の判定

などを関数にしているが、最初からこのように整理したコードを思いついたのではない。
作成していく途中で「この処理は何度も使うので関数にして共通化しよう」と気づいた経緯がある
##### 別の方法があるならそれでもOK

---
  
### jsで並び替え機能を作成する
並び替えについては、
 - セレクトボックスにイベントハンドラを追加することになる
 - 商品ノードの扱い方に少し工夫が必要

絞り込みの場合は、
 - DOMノードを削除しなくてもリスト2のようにCSSの設定内容を切り替えることで実装できた

##### 並び替えは実際にDOMノードの順番を変更しなければならない
日本語の手順で示すと以下のようになる
##### 手順1
並び替えのセレクトボックスにchangeイベントハンドラを追加しておく
##### 手順2
イベントハンドラが実行されたとき、1つ1つの商品を表す`<div class="item>`要素にアクセスし、その内側にある商品価格のノードから、カンマ, を除去した数値を読み取る
##### 手順3
セレクトボックスの「価格が安い順」が選択されている場合、手運2で読み取った全ての商品の価格を数値の小さい順に並び替え、その順番にDOMの商品ノードを並び変える
手順3の並び替えが一番難しい
#### 並び替えは、配列をfor文で捜査する考え方では難しいが、実はES5で追加されたsort()関数を使うと意外とシンプルに実装できる
`配列.sort(比較関数(a,b))`
  
比較関数には自作関数の関数名か、関数オブジェクトを直接指定する。
**比較関数は2つの引数を取り、全ての配列要素に対して1回づつ実行される。**
元の配列は、各要素で実行された比較関数の戻り値に従って並び変わる。
**比較関数の引数が(a,b)だとすると、比較関数の戻り値が0未満なら、aを持つ要素はbを持つ要素よりも後ろに並ぶ。**
  
例えば次のコードを実行すると、配列要素の数値が小さい順に並び変わる
##### リスト3-2-3　sort()関数の使用例
```js
js



```

