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
**元の配列は、各要素で実行された比較関数の戻り値に従って並び変わる。**
**比較関数の引数が(a,b)だとすると、比較関数の戻り値が0未満なら、aを持つ要素はbを持つ要素よりも後ろに並ぶ。**
  
例えば次のコードを実行すると、配列要素の数値が小さい順に並び変わる
##### リスト3-2-3　sort()関数の使用例
```js
js

// リスト3-2-3　sort()関数の使用例

// 金額の配列
let array_price = [1280, 1980, 1580, 980, 1680, 1780];

// 値が小さい順に並び変える比較関数
function desc_order(a, b) { //aとbに配列のすべての数値を代入していき、自動的に比較してくれる
  document.write(a + "　←a  b→　" + b);
  document.write("　　　　");

  if (a < b) { return -1; } //aを持つ要素はbを持つ要素より手前
  if (a == b) { return 1; } //aを持つ要素はbを持つ要素より後ろ
  return 0; //順番は同じ
}

// 安い順にソート
array_price.sort(desc_order);

// 並び変えた結果を表示
console.log(array_price); // =>[980, 1280,～1980の安い順に並ぶ]
// document.write(array_price);HTMLに表示できる
```

```html
<body>

  <script src="main3_2_3.js"></script>
</body>
</html>
```
  
##### リスト3-2-4　シンプルな比較関数
```js
// リスト3-2-4　シンプルな比較関数
// 単純に数値の大小関係を比較するだけなら、比較関数はもっとシンプルに記述できる

let array_price = [1280, 1980, 1580, 980, 1680, 1780];

function desc_order(a, b) {
  return a - b;
}

array_price.sort(desc_order);

console.log(array_price);
// alert(desc_order);
```
  
##### リスト3-2-5　シンプルな記述
```js
// リスト3-2-5　シンプルな記述

// さらに、このような特定の処理だけで使う局所的な関数は、関数定義をsort()内に直接記述すると、グローバルスコープに関数名を増やすことなく、sort()内に隠蔽することができる

let array_price = [1280, 1980, 1580, 980, 1680, 1780];

// 並び替え
array_price.sort(function (a, b) {
  return a - b;
});

// 並び変えた結果を確認
console.log(array_price); // => [980, 1280,～1980の安い順に並ぶ]
```
  
##### リスト3-2-6　オブジェクトの並び替え
```js
// リスト3-2-6　オブジェクトの並び替え

// 配列要素が単純な数値ではなくオブジェクトの場合、比較関数のa,bにはオブジェクトが渡される。そのため、商品番号や商品価格などといった1つの商品に関するデータはオブジェクトにまとめ、オブジェクトを配列にすると、価格順にオブジェクトを並び変えることができる

// 商品オブジェクトの配列
let products = [
  { ID: 1, price: 1280 },
  { ID: 2, price: 1980 },
  { ID: 3, price: 1580 },
  { ID: 4, price: 980 },
  { ID: 5, price: 1680 },
  { ID: 6, price: 1780 }
];

// 安い順にソート
products.sort(function (a, b) {
  return a.price - b.price;
})

// 並び変えた結果を確認
console.log(products);

// F12のconsole.log結果
// 0: {ID: 4, price: 980}
// 1: {ID: 1, price: 1280}
// 2: {ID: 3, price: 1580}
// 3: {ID: 5, price: 1680}
// 4: {ID: 6, price: 1780}
// 5: {ID: 2, price: 1980}
// length: 6

alert(products[0].price); // =>980
alert(products[0].ID); // =>4
```
  
##### リスト3-2-7　（応用）商品一覧の並び替え

<details><summary>サンプルコードjs</summary><div>

```js
js

// リスト3-2-7　（応用）商品一覧の並び替え
// コンポーネントのルートノード
let nodeApp = document.querySelector('#app');

/////////////////// チェックボックスのイベントハンドラを登録 ///////////////////
let nodeCheckbox = nodeApp.querySelectorAll('input[type="checkbox"]');
nodeCheckbox[0].addEventListener('change', onCheckChanged, false);
nodeCheckbox[1].addEventListener('change', onCheckChanged, false);

// セレクトボックスのイベントハンドラを登録
let nodeSelect = nodeApp.querySelector('.sorting');
nodeSelect.addEventListener('change', onOrderChanged, false);

// 初期表示時の商品ノードリスト（保存用）
let nodeItemsOrg = nodeApp.querySelectorAll('.item');
// チェック状態イベントハンドラ
function onCheckChanged(event) {
  let nodeItems = nodeApp.querySelectorAll('.item'); //商品ノードのリスト
  let nodeCount = nodeApp.querySelector('.count'); //表示件数のノード
  let count = nodeItems.length; //表示件数

  // 全ての商品ノードをいったん表示する
  for (let i = 0; i < nodeItems.length; i++) {
    showNode(nodeItems[i]);
  }

  // セール対象のチェックがついている場合
  if (nodeCheckbox[0].checked) {
    // 全ての商品ノードを捜査
    for (let i = 0; i < nodeItems.length; i++) {
      // セール対象の商品ではない場合
      if (!isSaleItem(nodeItems[i])) {
        // この商品を非表示にする
        hideNode(nodeItems[i]);
        // 件数のカウント減らす
        count--;
      }
    }
  }
  // 送料無料のチェックがついている場合
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

/////////////////// 並び順変更のイベントハンドラ ///////////////////
function onOrderChanged(event) {

  let nodeList = nodeApp.querySelector('.list'); // 商品一覧ノード
  let nodeItems = nodeApp.querySelectorAll('.item'); // 商品ノードのリスト

  // 商品ノードのリストを新しい配列に詰め替える(退避しておく)
  // 商品ノードリスト（初期表示用ではないノードリスト）
  let products = [];
  for (let i = 0; i < nodeItems.length; i++) {
    products.push(nodeItems[i]);
  }

  // DOMから全ての商品ノードを削除する
  while (nodeList.firstChild) {
    nodeList.removeChild(nodeList.firstChild);
  }
  //e.target はclass=sortingの<option value="1">標準かvalue="2"の要素を参照します
  if (event.target.value == '1') { // 「標準」が選択されている場合
    // 初期表示時の商品ノードを復元する
    for (let i = 0; i < products.length; i++) {
      nodeList.appendChild(nodeItemsOrg[i]);
    }
  }
  // 「価格が安い順」が選択されている場合
  else if (event.target.value == '2') {
    // 配列を並び替え
    products.sort(function (a, b) {
      // 商品価格のノードからカンマを除去した数値を読み取る
      let prevPrice = parseInt(a.querySelector('.price span').textContent.replace(',', ''));
      let currentPrice = parseInt(b.querySelector('.price span').textContent.replace(',', ''));
      return prevPrice - currentPrice;
    });
    // 並び替え後の商品ノードをDOMに追加する
    for (let i = 0; i < products.length; i++) {
      nodeList.appendChild(products[i]);
    }
  }
}

// セール商品かどうかを判定する関数
function isSaleItem(nodeItem) {
  let node = nodeItem.querySelector('.status'); //Document の querySelector() メソッドは、指定されたセレクターまたはセレクターのグループに一致する、文書内の最初の Element を返します。
  return (node && node.textContent == 'SALE');
}

// 送料無料かどうかを判定する関数
function isDelvFreeItem(nodeItem) {
  let node = nodeItem.querySelector('.shipping-fee');
  return (node && node.textContent == '送料無料');
}

// ノードを非表示にする関数
function hideNode(node) {
  node.setAttribute('style', 'display:none;');
}

// ノードを表示する関数
function showNode(node) {
  node.removeAttribute('style');
}

```

</div></details>
  
上記の補足
商品ノードの親ノード(.list)に対して、商品ノード(.item)の追加や削除を行う。
ただし、いったん「価格が安い順」にノードを並び変えてしまうと、次に「標準」に戻したとき、元の順番がわからなくなる。
そのため、**グローバルスコープの`nodeItemsOrg`変数に初期表示のノードを保持しておき、「標準」が選択されたときはここから復元する**ようにしている。
  
やや微妙な実装となっている。「標準」の並び順を復元するために、**グロ－バルスコープにデータを保持するのは避けたい。**
上記の大部分はDOMを操作するコードであるが、Vue.jsのデータバインディングを使うと、ここまで煩雑なコードを書かなくて済む。
  

### 商品データをアプリケーションに結びつける
上記のモックアップは、商品データを直接HTMLに記述していた。
そのため、jsから参照するたびにDOMにアクセスしなければならなかった。
Vueを適用すると、必然的にアプリケーションはデータを中心とした構造(データ駆動)になり、
なおかつ、強力なデータバインディングのおかげで、DOMへのアクセスをほとんど意識しなく済むようになる。
  
#### Vue.jsを組み込む準備
リスト3-3-1　Vue.jsを読み込む

```html

・・・省略
    <script src="https://jp.vuejs.org/js/vue.js"></script>
    <script src="main3_3_1.js"></script>
  </body>
```

```js
let app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
});
```

main.htmlの
**`<div id="#app">`～`</div>`で囲んだ部分が、商品一覧コンポーネントの描画領域になる**

main.jsの
**`new Vue({・・・})`がコンポーネントのデータや動作を制御するプログラムを記述する部分になる**
  
### dataオプションにデータを定義する
コンポーネントのdataオプションに、どのデータをどの形式で持たせる必要があるか？を考える
データには2種類ある
・画面などを通して直接目に見えるデータ
・目に見えないが、制御に必要なデータ
  
---
#### 目に見えるデータ
・ブラウザの画面や、htmlの中から、目に見えるデータを探す
・ユーザーの操作や商品の登録内容によって表示が変わる部分は、**全てデータ化する必要があると考える**
  
 - SALEマーク：セール対象の場合に表示
「セール対象かどうかを表す値」をデータ化する必要がある

- 商品画像：`<img src="画像のパス" alt="">`の形式でhtmlに埋め込む
「画像のパス」をデータ化すればよい。今回はhtmlと同じディレクトリのimagesフォルダ内に画像を置くので、main.htmlからの相対パスを使う
- 価格：「1,580円」のカンマや円を含んだ文字列全体ではなく、数値1580だけをデータ化したほうがPGで加工しやすい
- 送料：数値部分だけをデータ化
送料無料なら「0」をデータ化する
- 表示中の件数：絞り込みの条件によって表示が変わるため、件数の数字をデータ化する
---

#### 目に見えないデータ
商品一覧に表示される商品数や並び順は、チェックボックスの入力値やセレクトボックスの選択値によって変わる。
そのため、**チェック状態や選択値をデータ化して、コンポーネントに保持させておく**必要がある

  
- セール対象、送料無料：チェックボックスの有無をデータ化
- 並び替え：セレクトボックスでどれが選択されているかをデータ化
---

#### POINT! データを洗い出すコツ
・外部データを表示する部分やユーザの操作で表示が変わる部分はデータ化の対象と考える
・動作の情けにゃ切り替えの判断基準となる情報もデータ化の対象と考える

---
  
#### データの持たせ方を決める
データが洗い出せたので、具体的な変数をdataオプションに記述していく
ここで、データ型や変数名をどうするのが適切かを考える
  
 - 表示中の商品数、チェックボックス、セレクトボックスの入力値
→互いに独立したデータなので単独の変数にする

- 商品名、かかっく、商品画像のパスなど、1つ1つの商品移管するデータ
→オブジェクト形式にまとめたものを配列に詰め込むと管理がしやすい
  
##### データの持たせ方
|No.|変数名|データ型|説明|
|-|-|-|-|
|1|count|数値|表示中の商品数|
|2|showSaleItem|真偽値|true:セール対象品のみ表示,　false:セール対象外品も表示|
|3|showDelvFree|真偽値|true:送料無料品のみ表示,　false:送料有り品も表示|
|4|sortOrder|数値|1:初期表示の順に並べて表示,　2:商品価格が安い順に表示|
|5|products|配列|商品リスト(NO.6-No.10を持つオブジェクトの配列)|
|6|name|文字列|商品名|
|7|price|数値|商品価格(税込)|
|8|image|文字列|商品画像のパス|
|9|delv|数値|送料(商品の配送にかかる料金)|
|10|isSale|真偽値|true:セール対象,　false:セール対象外|
  
### dataオプションの中身を書き換える
上記の表を見ながら進める

リスト3-3-3　dataオプションの中身を書き換える
```js
// リスト3-3-1　Vue.jsを読み込む
let app = new Vue({
  el: '#app',
  data: {

    // 商品リスト以外のデータには初期値を設定しておく 
    // 表示中の商品数
    count: 0,
    // セール対象のチェック状態(true:チェック有、f:無し)
    showSaleItem: false,
    // 送料無料のチェック状態(true:チェック有、f:無し)
    showDelvFree: false,
    // 「並び替え」の選択値(1:標準, 2:価格が安い順)
    sortOrder: 1,

    // 商品リスト
    products: [
      { name: 'Michael<br />スマホケース', price: 1580, image: 'images/01.jpg', delv: 0, isSale: true },
      { name: 'Raphael<br />スマホケース', price: 1580, image: 'images/02.jpg', delv: 0, isSale: true },
      { name: 'Gabriel<br />スマホケース', price: 1580, image: 'images/03.jpg', delv: 240, isSale: true },
      { name: 'Uriel<br />スマホケース', price: 980, image: 'images/04.jpg', delv: 0, isSale: true },
      { name: 'Ariel<br />スマホケース', price: 980, image: 'images/05.jpg', delv: 0, isSale: false },
      { name: 'Azrael<br />スマホケース', price: 1580, image: 'images/06.jpg', delv: 0, isSale: false }
    ]
  }
});
```
商品リスト以外のデータには初期値を設定しておく 
あとでhtmlとデータバインドするので、あらかじめ初期表示状態と同じ値を設定しておく
例：sortorder:1　の「1:標準」を初期値とする
**ただし、countを「6」ではなく「0」とする。**
理由：**本章の段階では商品データをコンポート内に定義しているが、実際のアプリケーションではサーバから商品データを動的に読みこむので、ページを表示するまで商品は確定しない。**
**そのため、countには、一般に数値型の初期値として使われる「0」を設定しておく**
  
###### コメントの癖をつける
中規模以上の開発では、データの定義を開発メンバーで共有するが、
設計書の作らない小規模開発ではコメントが重要になってくる
  
### 構文エラーがないか確認する
まだhtmlとは連動していないが、main.jsの構文に間違いがあれば、この時点でブラウザのコンソールにエラーが出る。
少しでもjsを更新したら、こまめにコンソールを確認する癖をつけておく
　例えば商品リストの配列を以下のように書き間違えたとする
リスト3-3-4
```js
・・・
// 商品リスト
products:{  // []と書けていない→F12コンソールにUncaught SyntaxError:  ... main.js:14 が表示される
  {商品オブジェクト}
}
・・・
```
**初めて見るメッセージはすぐにネットで調べる**
Syntax：構文
Unexpected:予期しない　＝Un(打消し)expected(期待通り)
token(トークン):「[」「｛」などの記号の総称
`Uncaught SyntaxError: Unexpected token{　　　main.js:14`
「main.jsの14行目に構文間違いがあります。
　ここに{　があるのはおかしい（予期していない）ですよ。見直してください。」

**些細な場違いでも、エラーの意味を調べ、解決しながら進んでいけるようになることが大切**

---

## 3-4 商品データを描画する
jsのデータ準備ができたので、htmlを書き換えてデータバインドしていく。
まずは商品データの部分をVue.jsで置き変えてみる
  
### 出力するHTMLのパターン
商品データは`v-forディレクティブ`を使って繰り返す
 - そのため、htmlのどこからどこまでのは範囲に1件分の商品データが入るのかを確認しておく
 `<div class="item">`を6回繰り返しているので、ここが商品データを繰り返す範囲となる
```js
        <!-- 商品一覧 -->
        <div class="list">
          
          以下のitemを6回繰り返しているので、ここが商品データを繰り返す範囲となる
          <div class="item">・・・</div> 
          <div class="item">・・・</div> 
          ・・・

        </div>//class="list"
```
##### ただし、**SALEのマークと送料の表記は、商品によって異なる
　`v-for`で繰り返すときも、商品によってhtmlの出力内容を切り替えなければならない箇所である。
  
上記を踏まえてhtmlを注意深く見ていくと、最終的に出力しなければならないhtmlは以下のようになる
リスト3-4-1　商品データの出力部分
```html
          <div class="item">
            <figure class="image">

              <!--▼セール対象の場合▼-->
              <div class="status">SALE</div>
              <!--▲セール対象の場合▲-->
              
              <img src="images/01.jpg" alt="" />
              <figcaption>Michael<br />スマホケース</figcaption>
            </figure>

            <div class="detail">
              <div class="price"><span>1,580</span>円（税込）</div>

              <!--▼送料無料の場合▼-->
              <div class="shipping-fee none">送料無料</div>
              <!--▲送料無料の場合▲-->
              <!--▼送料ありの場合▼-->
              <div class="shipping-fee">+送料280円</div>
              <!--▲送料ありの場合▲-->

            </div>
          </div>
```

`<div class="status">SALE</div>`の部分は、セール対象品の場合だけ出力し、
送料の部分は送料が0か、それ以外化でhtmlの出力内容を替えなければならないことが整理できた
**いきなりVue.jsのテンプレート構文で置き換えるのが難しい場合は、このように日本語のコメントで出力条件を書き込んでおくと、ロジックが視覚化できてわかりやすくなる**

---

### テンプレート構文で置き換える
繰り返す商品データは、dataオプションに「products」という配列で定義したので、
htmlの`<div class="item">~~</div>`に`v-for`を使ってバインドする
  
リスト3-4-2　商品データの出力部分
```html
        <div class="list">
          <div class="item" v-for="product in products">
            <!-- この範囲がproductsの配列要素の数だけ繰り返される -->
          </div>
        </div>
```
#### Point!　v-forを記述する場所に注意
- v-forディレクティブは**繰り返したい要素自身**に記述することに気を付ける。
- **繰り返したい部分を囲む要素に記述するのは間違い**
もし上記リスト2で`<div class="list" v-for="product in products>`と記述すると、
**1つ1つの商品が`<div class="list">~~</div>`で囲まれてしまい、タイル状の配置にならない**
  
　
- v-forで宣言したproductには、productsの配列要素（商品オブジェクト）が繰り返しのたびに代入される
 - **繰り返しの範囲では、productから商品名や価格などのプロパティを参照し、マスタッシュ{{・・・}}やv-ifなどの条件式で使うことができる**
  
　
##### リスト3の回答を見ないで、第2章を振り返りながらリスト1を書き換えてみる
リスト3-4-3　(自己コード)商品データの出力部分
```html
        <!-- 商品一覧 -->
        <div class="list">
          <div class="item" v-for="product in products">
            <figure class="image">
              <template v-if="product.isSale ">
                <div class="status">SALE</div>
              </template>
              <img v-bind:src="product.image" alt="" />
              <figcaption>{{product.name}}</figcaption>
            </figure>

            <div class="detail">
              <div class="price"><span>{{product.price}}</span>円（税込）</div>
              <template v-if="product.delv==0">
                <div class="shipping-fee none">送料無料</div>
              </template>
              <template v-else>
                <div class="shipping-fee">+送料{{product.delv}}円</div>
              </template>

            </div>
          </div>
        </div>
```

v-if、v-elseディレクティブは何らかの要素に対して指定する必要があるが、
**`<div>`や`<span>`などを使うと、そのタグまで出力されてしまうので、ここでは`<template>`を使った**
**`<template>`はDOMに出力されない特殊なタグだから。**
  
#### うまくいかない場合
・コンソールを調べる
・ElementsタブでDOMを調べる
**・もしデータバインドに成功した場合：`v-*`で始まるディレクティブは最終的なHTMLからは取り除かれるはず**
・templateのタグの閉じ忘れや、兄弟要素、親子要素の関係にも注意する

### 金閣の書式と商品名の改行
・1,580のように3桁ごとにカンマで区切られていない
・商品名にbrタグがそのままテキストとして表示されている
  
#### 金額の書式変換
2-5節のフィルターを使う
金額のデータを更新することなく、DOMの出力結果だけを「#,###,###」の書式に変換できる
**汎用的に使えるフィルターなので、グローバルスコープに登録することにする**
#### 注意：filterは、そのフィルターを利用するコンポーネントよりも先に定義すること
  
リスト3-4-5　フィルターを定義する
```js
// リスト3-4-5　フィルターを定義する
// 数値を通貨書式「#,###,###」に変換するフィルター
Vue.filter('number_format', function (val) {
  return val.toLocaleString();
});

// 商品一覧コンポーネント
let app = new Vue({
```

```html
// リスト3-4-6　フィルターを適用する
       <!-- 商品一覧 -->
        <div class="list">
          <div class="item" v-for="product in products">
            <figure class="image">
              <template v-if="product.isSale ">
                <div class="status">SALE</div>
              </template>
              <img v-bind:src="product.image" alt="" />
              <figcaption>{{product.name}}</figcaption>
            </figure>

            <div class="detail">
              <div class="price"><span>{{product.price | number_format}}</span>円（税込）</div> <!--Vue.filterでカンマ区切りの価格を受け取るー-->
              <template v-if="product.delv==0">
                <div class="shipping-fee none">送料無料</div>
              </template>
              <template v-else>
                <div class="shipping-fee">+送料{{product.delv | number_format}}円</div>
              </template>
            </div>
          </div>
        </div>
```
  
#### 商品名の改行
商品名には。ページ上で表示させたい場所に`<br>`タグが含まれているので、
**普通にバインドすると` < や > `はエスケープ処理されるので、htmlには「`$It;br&gt`」が出力されてしまう**
**マスタッシュ{{}}で埋め込んだデータはVue.jsが必ずエスケープ処理を行うから**
  
どうすれば良いのか？？
**実は、`v-html`をいうディレクティブがあり、これを使ってバインドしたデータはそのままHTMLとして出力できる**
  
リスト3-4-7　HTMLタグをそのまま出力する
```html
<!-- <figcaption>{{product.name}}</figcaption> -->
<figcaption v-html="product.name"></figcaption>
```
初期表示が完成した
  
## 3-5　ユーザーの入力に応じて表示を切り替える
絞り込み、並び替え機能の実装方法を考える
まずは、チェックボックス、セレクトボックスにデータをバインドすることから始める
  
### フォームコントロールにデータバインドする
コンポーネント側のdataオプションに用意した3つの変数
showSaleItem
showDelvFree
sortOrder
をフォームコントロールにバインドする
  
**この3つはユーザー入力によって更新されるデータ**なので、`v-bind`による**一方通行のンバインドではなく、**
**`v-model`による双方向のバインドを使う**
  
リスト3-5-1・2　フォームコントロールのバインド
```html
          <div class="condition">
            <div class="target">
              <label><input type="checkbox" v-model="showSaleItem"/> セール対象{{showSaleItem}}</label>
              <label><input type="checkbox" v-model="showDelvFree"/> 送料無料{{showDelvFree}}</label>
            </div>
            <div class="sort">
              <label for="sort">並び替え{{sortOrder}}</label>
              <select id="sort" class="sorting" v-model.number="sortOrder">
                <option value="1">標準</option>
                <option value="2">価格が安い順</option>
              </select>
            </div>
          </div>
```
フォームコントロールの際はバインドするデータの**型**に注意
**チェックボックスにv-modelでバインド**した場合：フォーム側からの入力値は**真偽値**になる。
　そのため以前作成したコードでは、showSaleItem,showDelvFreeを真偽値にした
  
**セレクトボックスの入力値は文字列型**になる
たとえ、`<option>`タグのvalueを"1"や"2"といった数値にしていても、**これらは「数値」型ではなく「数字（文字列型）」となる**
**そのため`.number`修飾子を使って、入力値を数値に変換**する
この段階で{{}}で正しくバインド出来ているか確認しておく
（フォームコントロールの近くに直接{{}}でデータをバインドすると簡単にデバッグできる）
実際にWebページから入力を行って、表示が変わることを確認しておく
  
### 絞り込み機能を実装する
絞り込みを行うのは、ユーザがチェックボックスの状態を変更したタイミング
`v-onディレクティブ`を使ってチェックボックスのchangeイベントをハンドリングすればよさそう
　あるいは、データ駆動の立場で言い換えると、バインドしたデータが更新されたタイミングなので、ウォッチャを使ってもよい
changeイベント(要素に変更があった場合)が発生すると、バインドしたデータが更新されるので、ウォッチャで監視していれば検知できる
  
どちらの方法も間違いではない
ウォッチャを使えばテンプレート側に`v-on`でイベントハンドラを割り当てなくて済むので、HTMLをクリーンな状態に保つことができる
ここではウォッチャを使うことを考えてみる
  
リスト3-5-3　チェックボックスを監視するウォッチャ
```js
// リスト3-5-3　チェックボックスを監視するウォッチャ

'use strict'
// リスト3-5-3　チェックボックスを監視するウォッチャ
// 数値を通貨書式「#,###,###」に変換するフィルター
// 注意：filterは、そのフィルターを利用するコンポーネントよりも先に定義すること
Vue.filter('number_format', function (val) {
  return val.toLocaleString();
});


// Vue.jsを読み込む
// 商品一覧コンポーネント
let app = new Vue({
  el: '#app',
  data: {
    // 商品リスト以外のデータには初期値を設定しておく 
    // 表示中の商品数
    count: 0,
    // セール対象のチェック状態(true:チェック有、f:無し)
    showSaleItem: false,
    // 送料無料のチェック状態(true:チェック有、f:無し)
    showDelvFree: false,
    // 「並び替え」の選択値(1:標準, 2:価格が安い順)
    sortOrder: 1,

    // 商品リスト
    products: [
      { name: 'Michael<br>スマホケース', price: 1580, image: 'images/01.jpg', delv: 0, isSale: true },
      { name: 'Raphael<br>スマホケース', price: 1580, image: 'images/02.jpg', delv: 0, isSale: true },
      { name: 'Gabriel<br>スマホケース', price: 1580, image: 'images/03.jpg', delv: 240, isSale: true },
      { name: 'Uriel<br>スマホケース', price: 980, image: 'images/04.jpg', delv: 0, isSale: true },
      { name: 'Ariel<br>スマホケース', price: 980, image: 'images/05.jpg', delv: 0, isSale: false },
      { name: 'Azrael<br>スマホケース', price: 1580, image: 'images/06.jpg', delv: 0, isSale: false }
    ]
  },  //←オプションを区切る。,忘れずに

  watch: {
    // 「セール対象」チェックボックスの状態を監視するウォッチャ
    showSaleItem: function (newVal, oldVal) { //newVal,oldValにはtrueかfalse（チェック前の状態）が入る
      // ここでproductsの配列を書き換える
      console.log('showSaleItemウォッチャが呼び出されました');
      console.log('showSaleItemウォッチャ:' + newVal + '←newの値,oldの値→' + oldVal );
    },
    // 「送料無料」チェックボックスの状態を監視するウォッチャ
    showDelvFree: function (newVal, oldVal) {
      // ここでproductsの配列を書き換える
      console.log('showDelvFreeウォッチャが呼び出されました');
      console.log('sshowDelvFreeウォッチャ:' + newVal + '←newの値,oldの値' + oldVal );
    }
  }
});

```
ウォッチャが呼び出されたとき、商品リストのproductsから表示対象外の商品オブジェクトを削除すればよさそうだが、**productsから配列要素を削除してしまうと、再びチャック状態が変更されたときに復元できなくなる**。並び替えについても同じことが言える。
**セレクトボックスの選択肢を「価格が安い順」に切り替えてから「標準」に戻したいとき、元の配列が残っていないと、元の表示に戻せなくなる。**
こんなときに役立つのが算出プロパティ。filteredListという名前で、**絞り込みを行った商品リストを返す算出プロパティを定義**してみる。
  
リスト3-5-4　絞り込みを行った商品リストを返す算出プロパティ
```js
'use strict'
// リスト3-5-4　絞り込みを行った商品リストを返す算出プロパティ
// 数値を通貨書式「#,###,###」に変換するフィルター
// 注意：filterは、そのフィルターを利用するコンポーネントよりも先に定義すること
Vue.filter('number_format', function (val) {
  return val.toLocaleString();
});


// Vue.jsを読み込む
// 商品一覧コンポーネント
let app = new Vue({
  el: '#app',
  data: {
    // 商品リスト以外のデータには初期値を設定しておく 
    // 表示中の商品数
    count: 0,
    // セール対象のチェック状態(true:チェック有、f:無し)
    showSaleItem: false,
    // 送料無料のチェック状態(true:チェック有、f:無し)
    showDelvFree: false,
    // 「並び替え」の選択値(1:標準, 2:価格が安い順)
    sortOrder: 1,

    // 商品リスト
    products: [
      { name: 'Michael<br>スマホケース', price: 1580, image: 'images/01.jpg', delv: 0, isSale: true },
      { name: 'Raphael<br>スマホケース', price: 1580, image: 'images/02.jpg', delv: 0, isSale: true },
      { name: 'Gabriel<br>スマホケース', price: 1580, image: 'images/03.jpg', delv: 240, isSale: true },
      { name: 'Uriel<br>スマホケース', price: 980, image: 'images/04.jpg', delv: 0, isSale: true },
      { name: 'Ariel<br>スマホケース', price: 980, image: 'images/05.jpg', delv: 0, isSale: false },
      { name: 'Azrael<br>スマホケース', price: 1580, image: 'images/06.jpg', delv: 0, isSale: false }
    ]
  },  //←オプションを区切る。,忘れずに

  // リスト3-5-4　絞り込みを行った商品リストを返す算出プロパティ
  computed: {
    // 絞り込み後の商品リストを返す算出プロパティ
    filteredList: function () {
      // 絞り込み後の商品リストを格納する新しい配列
      let newList = [];
      for (i = 0; i <= this.products.length; i++) {
        // 表示対象かどうかを判定するフラグ
        let isShow = true;
        // 1番目の商品が表示対象かどうかを判定する
        if (this.showSaleItem && !this.products[i].isSale) { //「セール対象」チェック有で、セール対象ではない場合
          isShow = false; // この商品は表示しない
        }
        if (this.showDelvFree && !this.products[i].delv) { //「送料無料」チェック有で、送料有の商品の場合
          isShow = false; // この商品は表示しない
        }
        //else 表示対象の商品だけを新しい配列に追加する
        if (isShow) {
          newList.push(this.products[i]);
          alert(this.products[i]);
        }
        // 絞り込み後の商品リストを返す
        return newList;
      }
    }
  },

  watch: {
    // 「セール対象」チェックボックスの状態を監視するウォッチャ
    showSaleItem: function (newVal, oldVal) { //newVal,oldValにはtrueかfalse（チェック前の状態）が入る
      // ここでproductsの配列を書き換える
      console.log('showSaleItemウォッチャが呼び出されました');
    },
    // 「送料無料」チェックボックスの状態を監視するウォッチャ
    showDelvFree: function (newVal, oldVal) {
      // ここでproductsの配列を書き換える
      console.log('showDelvFreeウォッチャが呼び出されました');
    }
  }
});
```
  
発想の仕方は人によって異なるので、この通りでなくてもOK。**同じ結果が返ればよい**
  
リスト4は**絞り込んだ結果を格納するための新しい配列`newList`を作成して、**
**元の配列`products`をループさせながら、**
**中身の商品1つ1つに対して対して「表示する条件を満たしているかどうか？」を調べる。**
そして、**条件を満たした商品だけを`push`で新しい配列に積み込んでいき、**
**全ての商品を調べ終わったら（ループが終わったら）結果をreturn**で返している。
この方法なら、絞り込みの条件が変わっても、必ず条件に当てはまる商品リストが返されることになる。
  
あとは、テンプレートにバインドするプロパティをproductsからfelteredListに変更すればOK
  
リスト3-5-5　算出プロパティをバインドする
```html

        <!-- 商品一覧 -->
        <div class="list">
          <div class="item" v-for="product in filteredList"> <!--prpductsをfilteredListに書き換え-->
```
```js
前回jsコードに修正有り再度コード記載

'use strict'
// リスト3-5-4　絞り込みを行った商品リストを返す算出プロパティ
// 数値を通貨書式「#,###,###」に変換するフィルター
// 注意：filterは、そのフィルターを利用するコンポーネントよりも先に定義すること
Vue.filter('number_format', function (val) {
  return val.toLocaleString();
});


// Vue.jsを読み込む
// 商品一覧コンポーネント
let app = new Vue({
  el: '#app',
  data: {
    // 商品リスト以外のデータには初期値を設定しておく 
    // 表示中の商品数
    count: 0,
    // セール対象のチェック状態(true:チェック有、f:無し)
    showSaleItem: false,
    // 送料無料のチェック状態(true:チェック有、f:無し)
    showDelvFree: false,
    // 「並び替え」の選択値(1:標準, 2:価格が安い順)
    sortOrder: 1,

    // 商品リスト
    products: [
      { name: 'Michael<br>スマホケース', price: 1580, image: 'images/01.jpg', delv: 0, isSale: true },
      { name: 'Raphael<br>スマホケース', price: 1580, image: 'images/02.jpg', delv: 0, isSale: true },
      { name: 'Gabriel<br>スマホケース', price: 1580, image: 'images/03.jpg', delv: 240, isSale: true },
      { name: 'Uriel<br>スマホケース', price: 980, image: 'images/04.jpg', delv: 0, isSale: true },
      { name: 'Ariel<br>スマホケース', price: 980, image: 'images/05.jpg', delv: 0, isSale: false },
      { name: 'Azrael<br>スマホケース', price: 1580, image: 'images/06.jpg', delv: 0, isSale: false }
    ]
  },  //←オプションを区切る。,忘れずに

  // リスト3-5-4　絞り込みを行った商品リストを返す算出プロパティ
  computed: {
    // 絞り込み後の商品リストを返す算出プロパティ
    filteredList: function () {
      // 絞り込み後の商品リストを格納する新しい配列
      let newList = [];
      for (let i = 0; i < this.products.length; i++) {
        // 表示対象かどうかを判定するフラグ
        let isShow = true;
        // 1番目の商品が表示対象かどうかを判定する
        if (this.showSaleItem && !this.products[i].isSale) { //「セール対象」チェック有で、セール対象ではない場合
          isShow = false; // この商品は表示しない
        }
        if (this.showDelvFree && this.products[i].delv > 0) { //「送料無料」チェック有で、送料有の商品の場合
          isShow = false; // この商品は表示しない
        }
        //else 表示対象の商品だけを新しい配列に追加する
        if (isShow) {
          newList.push(this.products[i]);
        }
      }
      // 絞り込み後の商品リストを返す
      return newList;
    }
  },
  watch: {
    // 「セール対象」チェックボックスの状態を監視するウォッチャ
    showSaleItem: function (newVal, oldVal) { //newVal,oldValにはtrueかfalse（チェック前の状態）が入る
      // ここでproductsの配列を書き換える
      console.log('showSaleItemウォッチャが呼び出されました');
    },
    // 「送料無料」チェックボックスの状態を監視するウォッチャ
    showDelvFree: function (newVal, oldVal) {
      // ここでproductsの配列を書き換える
      console.log('showDelvFreeウォッチャが呼び出されました');
    }
  }
});
```

リスト3で作成した**ウォッチャは、結果的には不要になる**が、その理由を考える。
**算出プロパティは、**
**算出の元になるリアクティブデータが更新されない限り、一度返した値はVue.jsによってキャッシュされ**、
**二回目以降はキャッシュが参照される**のだった。
  
`filteredList`の中では、showSaleItemとshowDelvFreeが使われており、
**どちらもdataオプションに定義されたリアクティブデータ**である。
そのため**ユーザが「セール対象」「送料無料」いずれかのチェック状態を切り替えるたびに**
**Vue.jsはキャッシュを破棄してfilteredListを再評価（もう一度functionを実行）する**。
そのため、**ウォッチャがなくてもページの表示と連動する。**
  　
  　
仕上げに「検索結果　6件」の部分も絞り込んだ結果と連動するようにする。
**表示中の商品数は、countという変数名でdataオプションに定義したが、実はこれも使う必要がなくなった。**
あらためて**ここに何をバインドするか考えると、先ほどの算出プロパティ`filteredList`に入っている商品オブジェクトの個数である。**
**`filteredList`はjsの配列(return newListで返ってきた配列が格納されたオブジェクトが「filteredList」)**なので、テンプレート側を次のように書き変えるだけで済む。
  
リスト3-5-6　配列の長さをバインドする
```html
  <body>
    <div id="app">
      <div class="container">
        <h1 class="pageTitle">商品一覧</h1>
        <!-- 検索欄 -->
        <div class="search">
          <div class="result">
            検索結果
            <span class="count">{{filteredList.length}}件</span> <!--6件を{{filteredList.length}}件に書き換えた-->
```
dataオプションのcountはいらなくなったので削除する
  
もし、少しでもテンプレート側にjsの式を増やしたくない場合は、filteredList.lengthを返す算出プロパティをcountという名前で追加すればよい
リスト3-5-7　表示件数を返す算出プロパティを追加する
```js
  computed: {
    // 絞り込み後の商品リストを返す算出プロパティ
    filteredList: function () {
　　　　・・・・・
    },
    // リスト3-5-7　絞り込みの後の商品リストを返す算出プロパティ
    count: function () {
      return this.filteredList.length;
    }
  },
```

リスト3-5-8　配列の長さをバインドする
```html
          <div class="result">
            検索結果
            <span class="count">{{count}}件</span> <!--{{filteredList.length}}件を{{count}}に書き換えた-->
          </div>
```
  
### 並び替え機能を実装する
並び替えは現在表示中のリストを操作すればよい
セレクトボックスにchangeイベントハンドラを仕掛けて、ハンドラ内で算出プロパティ`filteredList`の配列要素を並び替えればよさそう
しかし、**算出プロパティは基本的には読み取り専用**。書き込みを許可する構文がないわけではないが、
せっかく作ったproducts→filteredListへ変換する仕組みに逆行することになるのでお勧めできない
  
そこで、こう考える。
**filteredListの算出処理の中で、セレクトボックスにバインドしたsortOrderの値を読み取り、並び替えを済ませてしまう。**
**そして並び替えた結果を返すようにする。**
**この方法なら、filteredListは常に絞り込みと並び替えの両方を反映した配列を返すことになる。**
  
リスト3-5-9　算出プロパティ内で並び替えを行う
```js
  computed: {
    // 絞り込み後の商品リストを返す算出プロパティ
    filteredList: function () {
      // 絞り込み後の商品リストを格納する新しい配列
      let newList = [];
      for (let i = 0; i < this.products.length; i++) {
          ・・・・・・・・・・
      }
      // 新しい配列を並び変える
      if (this.sortOrder == 1) { // 並び替えのセレクトボックスで「標準：sortOrder: 1」を選んだ時
        //元の順番にpushしているので並び替え済み「newList.push(this.products[i])」
      }
      else if (this.sortOrder == 2) {
        // 価格が安い順に並び替える
        newList.sort(function (a, b) { //配列newList.をソートする
          return a.price - b.price; //a.priceは、newList.price。bも同じ。a-bのように書くと、それぞれ配列のprice要素を代入していき、安い順に自動的に並び替えをしてくれる。高い順にしたいときは、aとbの位置を入れ替える
        });
      }
      // 絞り込み後の商品リストを返す
      return newList;
    },
```
オブジェクトを含む配列の並び替えは3-2-6(P127)を参照する。
newListには、元のproductsの配列要素が順番通りにpushで格納されているので、sortOrderの値が1（標準）の場合は並び変える必要がない。
sortOrderの値が2の場合だけ並び替えを行う。
  
### 商品にキー(key)を指定する
**`v-for`で繰り返して出力する要素や`v-if`と`v-else`で表示を切り替える要素には、Vue.jsが1つ1つの要素を区別できるようにkey属性を指定する**のであった。
keyには区別したい要素間で重複のない固有の値を指定しなければならない。
通常、**ECサイトの商品には、商品番号やIDなど商品に固有の値が割り当てられる。**
JANｺｰﾄﾞ(商品のバーコード)や、AmazonにおけるASINコードやSKUなどをイメージすると良い。
そこで、商品オブジェクトにidという名前のプロパティを追加することにする。
  
リスト3-5-10　商品オブジェクトにキーを追加する
```html
<!-- `v-for`で繰り返して出力する要素や`v-if`と`v-else`で表示を切り替える要素には、Vue.jsが1つ1つの要素を区別できるようにkey属性を指定する -->
        <!-- 商品一覧 -->
        <div class="list">
          <div class="item" v-for="product in filteredList" v-bind:key="product.id">
```

```js
  data: {
    // 商品リスト以外のデータには初期値を設定しておく 

    // セール対象のチェック状態(true:チェック有、f:無し)
    showSaleItem: false,
    // 送料無料のチェック状態(true:チェック有、f:無し)
    showDelvFree: false,
    // 「並び替え」の選択値(1:標準, 2:価格が安い順)
    sortOrder: 1,

    // 商品リスト
    products: [
      { id: 1, name: 'Michael<br>スマホケース', price: 1580, image: 'images/01.jpg', delv: 0, isSale: true },
      { id: 2, name: 'Raphael<br>スマホケース', price: 1580, image: 'images/02.jpg', delv: 0, isSale: true },
      { id: 3, name: 'Gabriel<br>スマホケース', price: 1580, image: 'images/03.jpg', delv: 240, isSale: true },
      { id: 4, name: 'Uriel<br>スマホケース', price: 980, image: 'images/04.jpg', delv: 0, isSale: true },
      { id: 5, name: 'Ariel<br>スマホケース', price: 980, image: 'images/05.jpg', delv: 0, isSale: false },
      { id: 6, name: 'Azrael<br>スマホケース', price: 1580, image: 'images/06.jpg', delv: 0, isSale: false }
    ]
  },

```
これで商品一覧の描画が完成した。
  
**ただし、現時点では商品データがjsのコードに固定されているので、コンポーネントとしての独立性がない。**
**商品データの追加や変更が生じるたびに、コンポーネントを修正しなければならない。**
  
そこで次の章では、コンポーネントの外部に置いた商品データをコンポーネントに読み込む方法を実践する。

## thisについて
### thisが何を指すかはスコープによって変わる
thisは  class自身を指すキーワード
正確には、**クラスのインスタンスが生成されたときに、そのインスタンス自身を指すキーワード**

```js
let app = new Vue({
  data:{
    message: 'hello Vue'
  },
  methods:{
    logMessage:function(){
      console.log(this.message)// thisはVueインスタンスを指す
    }
  }
}),

//ここからVueのスコープ外
  console.log(app.message); // appにはVueのインスタンスが入っている
  console.log(this.message); // => undefindeエラー。スコープ外。

  console.log(this.innerWidth); // ウィンドウサイズが出力される（thisはブラウザに最初から実装されているwindowオブジェクトを指す）


/////////////////////////////////////////////////////////////////
  thisはブラウザに最初から実装されているwindowオブジェクトを指すが、
  重要な例外がある。1秒ごとにカウントダウンする例を見る
/////////////////////////////////////////////////////////////////
let app = new Vue({
  data:{
    count: 10 //カウントの初期値
  },
  methods:{
    countDown:function(){
      setInterval(function(){
       console.log(this.count--); //Vueのcount:10は減らない。Vueではなく、windowオブジェクトに干渉する。
      },1000);
    }
  }
}),

app.countDown(); // ==>NaNが繰り返し出力される
```
`setInterval`は、第一引数に指定した処理を、第二引数に指定した時間（ミリ秒）ごとに繰り返し実行するjsの関数
`setInterval(関数オブジェクト, 実行間隔)`
  
**上記リストのコードを実行すると、1秒ごとに10,9,8とは出力されない**。エラーとなる。
**名前を持たない無名関数はグローバルスコープに入るので、**
**無名関数の中でのthisはwindowオブジェクトを指してしまう**ため。
  
このような場合、**jsの`bind()`関数を使って、無名関数にローカルスコープのthisを引数で渡してあげると解決する**
  
リスト3*　bind()でコンポーネントへのインスタンスを渡す
```js
let app = new Vue({
  data:{
    count: 10 //カウントの初期値
  },
  methods:{
    countDown:function(){
      setInterval(function(){
       console.log(this.count--); //次の行のbind()の()に渡す引数に、このthisを引数として渡す。ことで、無名関数内であっても本来のthis(Vueのインスタンス)として参照してくれる 
      }.bind(this),1000); //jsの`bind()`関数を使って、無名関数にローカルスコープのthisを引数で渡してあげると解決する
    }
  }
}),

app.countDown(); // ==>10,9,8...
```

**`関数.bind(関数にthisとして渡すオブジェクト)`**
**bind()は全てのjs関数が持っているメソッドで、関数内でthisとして参照させたいオブジェクトを引数で指定する**
