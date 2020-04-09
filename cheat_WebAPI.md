# Web API
Application Programing Interface
 - Webを通じて利用できるサービス
 - そのサービスを利用するためのルール

ログイン、決済、配達など自分で作ることが大変なサービスを既存のサービスと連携でき、簡単に目的のサービスを提供できる。
  
ログインAPI...会員サービス事業者
決済API...決済サービス事業者
配達サービスAPI...配達サービス事業者

#### 「Web API」で検索
---
#### 代表的なAPI（無料）
API名　　/　　公式ドキュメント
政府統計の総合窓口...https://www.e-stat.go.jp/api/
図書館検索 カーリル...https://calil.jp/doc/api.html
天気情報(livedoor)...http://weather.livedoor.com/weather_hacks/
郵便番号検索API...http://zip.cgis.biz/
Twitter...https://developer.twitter.com/en/docs
Google...https://console.cloud.google.com/apis/library?hl=ja
Yahoo...https://developer.yahoo.co.jp/sitemap/
Wikipedia...https://www.mediawiki.org/wiki/API:Main_page/ja
※利用料や機能によっては一部有料

---

### Web APIの基本は「リクエスト」「レスポンス」
Webの世界では、**URLを使ってほしい情報を「リクエスト」して、その「レスポンス」として結果を受け取る**
##### Web APIも基本的には同じ仕組み
 API使用時は
 - 「どのようなURLでリクエストすればいいか」
 - 「レスポンスをどのようなデータ形式で受け取ることができるのか」
 - 「受け取ったデータをどのように活用すればいいのか」
 といったことが大切
 
 ---
 #### リクエストとレスポンスの流れ
**クライアント（ブラウザなど）**>>(ﾘｸｴｽﾄ)>>｢https://xxx.com/index.htmlのファイルをください｣>>>>**サーバー**
  
   **クライアント**（ブラウザなど）<<<<｢OK!データを送ります｣<<(レスポンス)<<**サーバー**
### 郵便番号から住所を自動入力する仕組み
1.jsでリクエスト「555-1234の住所をください」
2.住所情報のAPIのレスポンス「○○府中央区です」
3.jsでレスポンスのデータを画面(テキストボックスなど)に反映
 - jsを使うことでWebページを遷移せずにサーバーと通信できる

 ---

# Ajax
Asynchronous javascript + XML
※Asynchronous(非同期)

Ajaxを使うと、ページを再読み込みせずにWeb APIを利用したり、その結果をWebページに羽根井させることができる
 - GoogleMapsや住所自動入力でAjaxが使われている

 ---

### Ajaxを実装する
jsだけで記述できるが、ブラウザ間の細かい動作の違いがある。ので、ブラウザ間の違いを吸収してくれるjQを使って利用するのがおすすめ。
#### jQueryを利用したAjaxの基本構文
 - $.ajax()メソッドの引数には、オブジェクトの形式でパラメータを指定する
 - urlにはリクエスト先のURL(Web APIなど)を指定する
 - dataTypeは、レスポンスとして受け取るデータの形式を指定する

```js
js ajax

$.ajax({
    url: リクエスト先のURL,
    dataType: レスポンスのデータ形式,
    ...
  }).done(function(data) {
    //通信が成功したときの処理
  }).fail(function(data) {
    //通信が失敗したときの処理
  });
  ...
  ...
```
### 通信後の処理を記述する
#### 通信に成功した場合の処理
**$.ajaxに続けてdone()メソッドを使って記述する**
 - メソッドの引数に実行したい処理を関数で指定する。
  - このとき、関数の引数(data)にはレスポンスで得られたデータが自動的に格納される

#### 通信に成功した場合の処理
**fail()メソッドを使用する**
書き方はdoneと同じ

---
# JSON
JavaScript Object Notation
※Notation(表記)
JSONというデータ形式
  
  Web APIの多くは「XML」や「JSON」と呼ばれる通信に適した形式でデータを提供している。JSONは近年の主流。
  
   - クライアントとサーバー間で情報をやりとりするためには、お互いに理解できるデータ形式が必要
   - JSONは、Web APIはもちろん、それ以外のPGでも広く利用されている

#### JSONは、js由来のデータ形式
jsでデータをまとめて扱える「オブジェクト」のデータ型があった。
**JSONは、このjsのオブジェクトを、保存や通信に適した形式に変換したもの**

---

### Web APIでよく利用されるデータ形式
JSON.....軽量でjsとの相性が非常に良い
XML.....マークアップで汎用的なデータ構造を作れるが、データ量はJSONより重くなる
 - jsでAPIを利用する際は、JSONで通信することが多くなっている

 ---

## JSONの書き方
jsの配列やオブジェクトと同じだが、**プロパティ名はダブルクォーテーション「"」で囲んだ文字列にしなければならない**というルールがある

##### JSON形式で郵便番号と住所情報をまとめたデータ
```json
json

{
  "results": [
    {
      //1件目の住所情報
      "address1": "東京都", 
      "address2": "中央区",
      "address3": "八重集",
      "address4": "1030028"
    },
    {
      //2件目の住所情報
      "address1": "東京都",
      "address2": "渋谷区",
      "address3": "渋谷",
      "address4": "1500022"
    },
    ...
    ...
  ]
}
```
### ドメインをまたぐ技術「JSONP」
Webページは通常、そのWebページが設置されているドメイン以外のサーバーと通信することができない。
そのため、この問題に対策をしていないWebAPIは、jsから直接利用できない。
この問題を解決する技術に**JSONP(ジェイソンピー:JSON with padding)**(※余白)がある。
JSONPに対応したWebAPIなら、データもJSONで提供され、ドメインをまたいでスムーズに利用できる。
  mysite○○.com
  api○○.com
   - 上記の場合、ドメインが異なるので、ドメインをまたいだ通信は禁止
   - JSONPを使えば別ドメインと通信できる

---

### Web APIで郵便番号から住所を取得する
#### zipcloud
郵便番号から住所を提供してくれるWeb API

##### 検索ボタンを押すと自動で住所が入力されるフォームを作成する

プログラムの流れ
1.郵便番号を入れ、検索ボタン押下
2.Web API (zipcloud)に住所情報がリクエストされる
3.Web API (zipcloud)からレスポンスを受け取る
4.レスポンスをHTMLに反映する

[zipcloud(郵便番号検索API)](http://zipcloud.ibsnet.co.jp/doc/api)
利用規約を必ず確認すること
Google検索で同名のマルウェアも記事も出るが、これとは関連なし

##### リクエストの構文
```js
// 郵便番号の-ハイフンはあってもなくてもOK
http://zipcloud.ibsnet.co.jp/api/search?zipcode=郵便番号
```
--- 
#### レスポンスパラメータ
|フィールド名|項目名|備考|
|----|----|----|
|status|ステータス|正常時は200、エラー発生時にはエラーコードが返される|
|message|メッセージ|エラー発生時にエラーの内容が返される|
|results|-| --- 検索結果が複数存在する場合は、以下の項目が配列として返される ---|
|zipcode|郵便番号|7桁の郵便番号、ハイフンなし|
|prefcode|都道府県コード|JIS X 0401に定められた2桁の都道府県コード|
|adress1|都道府県名||
|adress2|市区町村名||
|adress3|町域名||
|kana1|都道府県名カナ||
|kana2|市区町村名カナ||
|kana3|町域名カナ||
---
### 入力フォームを作る
<details><summary>サンプルコード</summary><div>

```html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <title>インプレス いちばんやさしいJavaScriptの教本</title>
    <link rel="stylesheet" href="css/style.css" />
  </head>
  <body>
    <!-- 各入力項目(input要素)には、後でjsから操作しやすいようにid属性を付与している -->

    <h3>住所検索</h3>
    <div>
      <p>
        <label
          >郵便番号<input id="zipcode" type="text" size="10" maxlength="8"
        /></label>
        <button id="btn">検索</button>
      </p>
      <p>
        <label>都道府県<input id="prefecture" type="text" size="10" /></label>
      </p>
      <p>
        <label>市区町村<input id="city" type="text" size="10" /></label>
      </p>
      <p>
        <label>住所<input id="address" type="text" size="10" /></label>
      </p>
    </div>

    <script src="js/jquery-3.3.1.min.js"></script>
    <script src="js/app.js"></script>
  </body>
</html>
```

</div></details>

##### 動作とレスポンスの確認
以下をブラウザのアドレスバーに打ち込んでアクセス。WebAPIが仕様通りに利用できることを確認しておく

リクエストの例
`http://zipcloud.ibsnet.co.jp/api/search?zipcode=1030028`

成功するとレスポンスのJSONが以下のようにブラウザの画面に表示される。
```api
search?zipcode=1030028(※郵便番号)に対する
レスポンスのJSON

{
	"message": null,
	"results": [
		{
			"address1": "東京都",
			"address2": "中央区",
			"address3": "八重洲",
			"kana1": "ﾄｳｷｮｳﾄ",
			"kana2": "ﾁｭｳｵｳｸ",
			"kana3": "ﾔｴｽ",
			"prefcode": "13",
			"zipcode": "1030028"
		}
	],
	"status": 200
}

※WebAPIを利用した通信といっても、ブラウザでWebページを見るのとそう変わりはないことがわかる。
　これにさらにAjaxを組み合わせると、Webページ全体を更新することなく、一部だけを更新することができる。
```
---
#### 1. 検索ボタンに処理を関連付ける
検索ボタンをクリックしたときに処理が実行されるように、検索ボタンのクリックイベントに処理を関連付ける。
```js
$(function () { //読み込み完了後に実行

  $('#btn').on('click', function () {  // クリックイベントに登録
   
    // 今後、ここにクリックされたときの処理を記述する

  });
});

// id="btn"は、 $('#btn') で取得できる。
// これにonメソッドを使用してクリックイベントが発生したときの処理を書いていく
// onメソッドは複数処理の登録ができる

```

#### 2. 住所情報をリクエストする(Ajax処理)
続いて、Ajaxを使用してWebAPIに住所情報をリクエストする処理を記述していく。
まずは$.ajaxメソッドに、必要なパラメータを設定していく。
 - **$('zipcode').val()** で、フォームに入力されている郵便番号を取得し、結合する。
`.val()`は[要素のvalue値を取得](http://js.studio-kingdom.com/jquery/attributes/val)する。戻り値:`String, Number, Array`  

 - 「dataType」はJSONでデータを所得できるように「jsonp」を指定する

```js
$(function () {
  $('#btn').on('click', function () {

    // 入力された郵便番号でWebAPIに住所情報をリクエスト
    $.ajax({ //ajaxを追加
      url: "http://zipcloud.ibsnet.co.jp/api/search?zipcode=" + $('#zipcode').val(), //urlを指定
      dataType: 'jsonp', //dataTypeを指定

    });
  });
});
```
#### 3. 通信に成功した場合の処理を書く(Ajax処理)
doneメソッドを使い、通信に成功した場合の処理を書いていく。
**doneメソッドを利用する際に引数を指定すると、その引数から取得したデータにアクセスできる。**
引数の名前は自由、今回はdataとする。
これで取得したデータに、引数で指定した`変数「data」`からアクセスできるようになる。

```js
$(function () { //読み込み完了後に実行
  $('#btn').on('click', function () {
    $.ajax({
      url: "http://zipcloud.ibsnet.co.jp/api/search?zipcode=" + $('#zipcode').val(),
      dataType: 'jsonp',

    }).done(function (data) {
      console.log(data); //取得できているかの確認用。ChromeでF12でコンソール確認後に消す
    });

  });
});
```
#### 4. エラーが起きた際の処理を書く(Ajax処理)
通信に成功(200)しても、郵便番号が正しくなければ住所を取得できない
そのため、問題が起きた場合の処理も書いておく

 - data.resultsが所得できなかった場合の条件分岐を追記する
 - ネットワーク経路の障害などで通信に失敗した場合も住所を取得できない。ので、failメソッドも書いておく。
```js
$(function () { //読み込み完了後に実行
  $('#btn').on('click', function () {
    $.ajax({
      url: "http://zipcloud.ibsnet.co.jp/api/search?zipcode=" + $('#zipcode').val(),
      dataType: 'jsonp',
    }).done(function (data) {

      //dataの検索結果(results)が取得できなかった場合の条件分岐
      if (data.results) {
        // データが取得できた時の処理を書く
      } else { //検索結果が無い(ifがfalse)のとき
        alert('該当するデータが見つかりませんでした');
      }
    }).fail(function (data) { //通信自体に失敗したときの為のfailメソッド
      alert('通信に失敗しました');
    });
  });
});
```
---
### 住所情報をHTMLに反映する
#### 1. JSONからデータを取り出す関数を作る
最後に、WebAPIから取得した情報をHTMLに反映する処理を書く
 - **所得したJSONから住所情報を取り出して、HTMLに反映する`setData()`関数を作成する**
引数として取得したJSONの「results(複数の検索結果)」のフィールドにある住所情報を受け取ると、HTMLの各input要素の値として設定るようにする

`.val( value )`
文字列、または配列で要素に設定したいvalue値を指定します。
戻り値:`jQuery`


```JS
  // データ取得が成功したときの処理
  function setData(data) { //関数を定義
    // 取得したデータを各HTMLに代入
    // input要素に設定
    $('#prefecture').val(data.address1); //都道府県名
    $('#city').val(data.address2); //市区町村名
    $('#address').val(data.address3); //町域名
  }
});
```
#### 2. 関数を呼び出す
1.で関数が出来上がったら、doneメソッド内のデータの取得処理が完了した部分でsetData関数を呼び出すようにする。
 - setDataの引数には住所の情報を指定する必要がある。
 レスポンスされたJSON※を確認すると、**resultsフィールドの配列に入っている**ことがわかる。
<details><summary>※レスポンスされたJSONを開く</summary><div>

```api
search?zipcode=1030028(※郵便番号)に対する
レスポンスのJSON

{
	"message": null,
	"results": [
		{　　//「data.results[0]」の住所情報群
			"address1": "東京都",
			"address2": "中央区",
			"address3": "八重洲",
			"kana1": "ﾄｳｷｮｳﾄ",
			"kana2": "ﾁｭｳｵｳｸ",
			"kana3": "ﾔｴｽ",
			"prefcode": "13",
			"zipcode": "1030028"
		}
	],
	"status": 200
}
```
</div></details><br>
  
  - そこで引数に「`data.results[0]`」を指定して、住所情報だけが渡るようにしている。
 

```js
 }).done(function (data) {
      if (data.results) {
 
        setData(data.results[0]); //関数を呼び出す

      } else {
        alert('該当するデータが見つかりませんでした');
      }
    }).fail(function (data) {
      alert('通信に失敗しました');
    });
  });

  // データ取得が成功したときの処理
  function setData(data) { //関数を定義
    // 取得したデータを各HTMLに代入
    // input要素に設定
    $('#prefecture').val(data.address1); //都道府県名
    $('#city').val(data.address2); //市区町村名
    $('#address').val(data.address3); //町域名
  }
});
```
<details><summary>完成系サンプルコード</summary><div>

```html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <title>インプレス いちばんやさしいJavaScriptの教本</title>
    <link rel="stylesheet" href="css/style.css" />
  </head>
  <body>
    <!-- 各入力項目(input要素)には、後でjsから操作しやすいようにid属性を付与している -->

    <h3>住所検索</h3>
    <div>
      <p>
        <label
          >郵便番号<input id="zipcode" type="text" size="10" maxlength="8"
        /></label>
        <button id="btn">検索</button>
      </p>
      <p>
        <label>都道府県<input id="prefecture" type="text" size="10" /></label>
      </p>
      <p>
        <label>市区町村<input id="city" type="text" size="10" /></label>
      </p>
      <p>
        <label>住所<input id="address" type="text" size="10" /></label>
      </p>
      <p>
        <label>カナ1<input id="kana1" type="text" size="10" /></label>
      </p>
    </div>
    <script src="js/jquery-3.3.1.min.js"></script>
    <script src="js/app.js"></script>
  </body>
</html>
```

```js
js
'use strict'

$(function () { //読み込み完了後に実行
  $('#btn').on('click', function () {
    $.ajax({
      url: "http://zipcloud.ibsnet.co.jp/api/search?zipcode=" + $('#zipcode').val(),
      dataType: 'jsonp',
    }).done(function (data) {
      if (data.results) {
 
        setData(data.results[0]); //関数を呼び出す

      } else {
        alert('該当するデータが見つかりませんでした');
      }
    }).fail(function (data) {
      alert('通信に失敗しました');
    });
  });

  // データ取得が成功したときの処理
  function setData(data) { //関数を定義
    // 取得したデータを各HTMLに代入
    // input要素に設定
    $('#prefecture').val(data.address1); //都道府県名
    $('#city').val(data.address2); //市区町村名
    $('#address').val(data.address3); //町域名
    $('#kana1').val(data.kana1); //町域名
  }
});
```

</div></details>

---

## YouTube動画ギャラリー
### YouTube Data API(v3)
Google提供のWebAPIの中の一つ
#### 制作の手順
1.toutubedataAPI(v3)の利用準備 APIキーの取得
2.v3の利用方法の確認
3.ビデオギャラリー制作：jsの記述
4.　〃　：スタイルの記述
5.完成

---

APIキー.....APIの悪用や規約違反して利用されないように、誰が利用しているか特定するための「利用証明書」の役割を担う

---

  APIキーを利用するにはGoogle Cloud Platformにログインして、APIキーを発行する


 - [Google Cloud Platform](https://console.cloud.google.com/getting-started)にGoogleアカウントでログイン

##### プロジェクトを作成する
[Google Cloud Platform](https://console.cloud.google.com/getting-started)にて
1.上部メニュー：プロジェクトの選択＞新しいプロジェクトをクリック
2.PJ名を入力＞作成
3.プロジェクトの選択＞作成したPJをクリック
##### YouTubeData APIを有効にする
1.左上メニュー＞APIとサービス＞ダッシュボード
2.APIとサービスを有効化をクリック
3.YouTube Data API v3を選択＞有効にするをクリック
##### APIキーを発行する
認証情報を作成＞
使用するAPI：YouTube Data API(v3)を選択
API を呼び出す場所：ウェブブラウザ(js)
一般公開データ
必要な認証情報をクリック
認証情報が発行されるので完了をクリック

---

#### APIの利用方法
YouTube Data API(v3)を了するには
「https://googleapis.com/youtube/v3/search」のURLの後に ? を付け、そのあとに「パラメーター名=値」の形式で検索条件のパラメータを指定していく。
パラメータは&記号を使って複数指定でき、先ほど取得したAPIキーも「Key=APIキー」の形式で指定できる。

##### 「music」をキーワードとした検索を行う
```
https://www.googleapis.com/youtube/v3/search?type=video&part=snippet&q=music&key=APIキー
```
パラメータを理解するには以下サイトを確認
[公式Webサイト YouTube >DataAPI](https://developers.google.com/youtube/v3/docs/search/list?hl=ja)

#### 動画検索に利用するパラメータとレスポンス
動画検索で指定するパラメータは下表を参照
ビデオギャラリーを作成するため、
 - musicという検索キーワード
 - APIキー
 - 「videoEmbeddable(Webページに埋め込み可能な動画のみ取得する)」などのパラメータ

を追加する。
また、レスポンスからは様々なデータを取得できるが、今回はYouTubeのビデオにアクセスするために必要となる「**videold**」を取得する

#### 今回のサンプルで使用するパラメータ

|パラメータ|意味|備考|
|-|-|-|
|part|取得するリソースのプロパティを指定|必須項目。idかsnippetを指定。snippetにするとすべてのプロパティを取得できる。(※snippet〔切り取られた〕小片、切れ端)|
|type|検索対象を特定のリソースに限定|video、channel、playlist|
|q|検索に用いる文字列を指定|「音楽」「動物」「ニュース」などの検索文字列を指定|
|videoEmbeddable|検索対象をWebページに埋め込み可能な動画のみに限定|trueまたはfalse|
|videoSyndicated|検索対象をyoutube.com以外で再生できる動画のみに指定|trueまたはfalse|
|maxResults|一度に取得する検索数を指定|10、100....などの数字で指定|
|key|APIの利用に必要なAPIキーを指定|自分で取得したAPIキーが必要|

##### レスポンスの例
```js
{
  "items": [ // 検索結果を格納した配列
  {
    /* 中略 */
    "id": {       // 検索結果のID
      "kind":     // リソースの種類,
      "videold":  // 動画ID ... /* 今回の動画表示に必要 */
      ...
      ...
      ...      
    }
  }  
  ]
}

// https://www.googleapis.com/youtube/v3/search?type=video&part=snippet&q=music&key=APIキーの例
 "items": [
  {
   "kind": "youtube#searchResult",
   "etag": "\"xwzn9fn**********************\"",
   "id": {
    "kind": "youtube#video",
    "videoId": "SC-Llu1u_aE"
   },
```

---

### ビデオギャラリーを作成する
#### プログラムの流れ
1. APIへのリクエスト準備
2. APIへのリクエスト(Ajax通信)
3. レスポンスに応じた条件分岐
4. 取得したデータを元にビデオを表示
  
 - HTMLでビデオギャラリーの表示領域を作る
 - jsファイルで、リクエストパラメータを準備
 - API(v3)にリクエスト(Ajax通信)を行い、動画の検索データを取得する
 - レスポンスの成否に応じた条件分岐を行い、取得してデータを元にビデオを表示
 - CSSをでスタイルを整えて完成

 ---

 ### HTMLに記述
APIで得られたデータはjsでHTMLを記述するため、HTMLにはほとんどコードを記述しない。
**後からjsでギャラリーを表示する場所を指定するため、div要素を追加してid属性に「videoList」を指定**しておく。
この時点でブラウザには何も表示されない。
```html
  <body>
    <!--要素を追加する-->
    <h3>Video Gallery</h3>
    <div id="videoList"></div> <!--後からjsでギャラリーを表示する場所"videoList"-->

    <script src="js/jquery-3.3.1.min.js"></script>
    <script src="js/app.js"></script>
  </body>
```

---

### jsに記述
#### 1. リクエストURLを準備する
 - リクエスト先のURLに含める情報を記述する
 - まず、APIを使用する為のAPIキーの指定が必要
 - APIキーは長いので変数「KEY」に値として代入しておく
 - 今回利用するAPIのURLが必要。長いので変数「url」に代入しておく

```js
// リクエストパラメータのセット
const KEY = 'さっき取得したAPIキー'; //APIキーを貼り付け変数に代入
let url = 'https://www.googleapis.com/youtube/v3/search?'; //API URLを変数に代入
```

#### 2. リクエストパラメータを指定する
このサンプルでは'&q=music'と指定しているが、
「music」の部分を好きな言葉に変えれば、検索結果を変えることができる。
```js
// リクエストパラメータのセット
const KEY = 'さっき取得したAPIキー'; //APIキーを貼り付け変数に代入
let url = 'https://www.googleapis.com/youtube/v3/search?'; //API URLを変数に代入
// パラメータを連結
url += 'type=video';  // 動画を検索する
url += '&part=snippet';  // 検索結果にすべてのプロパティを含む
url += '&q=music';  // 検索ワード このサンプルでは music に指定
url += '&videoEmbeddable=true';  // Webページに埋め込み可能な動画のみを検索
url += '&videoSyndicated=true';  // YouTube.com以外で再生できる動画のみに限定
url += '&maxResults=6';  // 動画の最大取得件数
url += '&key=' + KEY;  // API KEY
```
#### 3. リクエストURLが正常に動作するか確認する
```js
// リクエストパラメータのセット
const KEY = 'さっき取得したAPIキー'; //APIキーを貼り付け変数に代入
let url = 'https://www.googleapis.com/youtube/v3/search?'; //API URLを変数に代入
// パラメータを連結
url += 'type=video';  // 動画を検索する
url += '&part=snippet';  // 検索結果にすべてのプロパティを含む
url += '&q=music';  // 検索ワード このサンプルでは music に指定
url += '&videoEmbeddable=true';  // Webページに埋め込み可能な動画のみを検索
url += '&videoSyndicated=true';  // YouTube.com以外で再生できる動画のみに限定
url += '&maxResults=6';  // 動画の最大取得件数
url += '&key=' + KEY;  // API KEY

// 動作確認したら消す
console.log(url); //F12でコンソールにリクエストURLが表示される
```
確認したURLをブラウザでリクエストしてみる
 - うまく通信できればブラウザの画面にレスポンスのJSONが表示される
 - APIからレスポンスが得られる
 ---
 ### AjaxでAPIを利用する
 #### 1. Ajaxでリクエストする
 リクエストURLとパラメータの準備ができたら実際にAPIを利用する「リクエスト」の処理を記述していく
  - jsでリクエストを行う
  - jQueryを用いたAjaxでリクエストを行う

ajaxメソッドの引数に先ほど準備したurlを指定してリクエストを実行する

```js
// HTMLが読み込まれてから実行する処理
$(function () {  //読み込み完了後に実行
  // youtubeの動画を検索して取得
  $.ajax({    // リクエストを実行
    url: url,
    dataType: 'jsonp'
  })
});
```

 #### 2. doneメソッドとfailメソッドを追加する
 ```js
 // HTMLが読み込まれてから実行する処理
$(function () {  //読み込み完了後に実行
  // youtubeの動画を検索して取得
  $.ajax({    // リクエストを実行
    url: url,
    dataType: 'jsonp'
  }).done(function (data) {  //doneメソッドを追加 ※$ jQueryはメソッドチェイン可能
      // データ取得が成功したときの処理。doneメソッドの引数(data)にはレスポンスで得られたデータが自動的に格納される
  }).fail(function (data) {  //failメソッドを追加
    alert('通信に失敗しました');
  });
});
```

 #### 3. レスポンスごとの処理を記述する
通信に成功しても別の問題でデータが取得できないこともある。
その場合は、data.itemsという値が無くなるので、値があるかどうかをifでチェック。
  
見つからない場合は警告メッセージを出す。
また、取得できなかったとき際のレスポンスの内容を後で確認できるようにdataの値をコンソールに表示させるようにする
 ```js
 // HTMLが読み込まれてから実行する処理
$(function () {  //読み込み完了後に実行
  // youtubeの動画を検索して取得
  $.ajax({    // リクエストを実行
    url: url,
    dataType: 'jsonp'
  }).done(function (data) {
    if (data.items) {  // データをチェック
      // データ取得が成功したときの処理
    } else {
      console.log(data);  // 警告メッセージを表示
      alert('該当するデータが見つかりませんでした');
    }
  }).fail(function (data) {
    alert('通信に失敗しました');
  });
});
```

 #### 4. 取得したデータをHTMLに反映する関数を作る
取得したJSONをHTMLに反映する処理は長くなるので、わかりやすくするためにsetData関数として記述する。
引数として取得したJSONを丸ごと受け取ることにする。
  
JSONのitemsプロパティには、動画の情報が配列としてまとめられている。
 - これをfor文で1データずつ取り出す。
 - そこからビデオIDを取り出し、動画を表示するiframe要素のタグを作成する

最後に作成したHTMLを、videoListというIDを持つHTML要素の子にする

 ```js
 // データ取得が成功したときの処理
function setData(data) {  // 関数を定義
  let result = '';
  let video = '';
  // 動画を表示するHTMLを作る
  // iframe要素のタグを作る
  for (let i = 0; i < data.items.length; i++) { //.itemsはJSONのレスポンスの値
    video = '<iframe src="https://www.youtube.com/embed/';
    video += data.items[i].id.videoId;
    video += '" allowfullscreen></iframe>';
    result += '<div class="video">' + video + '</div>'
  }
  // HTMLに反映する
  $('#videoList').html(result);  //  要素を作成
}
 ```

 #### ※iframe要素を使って動画を表示する
 Youtubeの動画をWebページに埋め込んで再生する場合、iframe要素を利用して
 「https://www.youtube.com/embed/ビデオID」
 というURLを取り込む。
 今回のサンプルではiframe要素をdiv要素の子として追加している。
```js
js

<div class="video">
<iframe src="https://www.youtube.com/embed/ビデオID"allowfullscreen></iframe>
</div>
```

#### 5. 関数を呼び出す
関数ができたら、doneメソッド内のデータ取得処理が完了した部分で、setData関数を呼び出す

```js
  $.ajax({
    url: url,
    dataType: 'jsonp'
  }).done(function (data) {
    if (data.items) {  // データをチェック

      setData(data);  // データ取得が成功したときの関数setDataを呼び出す

    } else {
      console.log(data);
      alert('該当するデータが見つかりませんでした');
    }
  }).fail(function (data) {
    alert('通信に失敗しました');
  });
});
```

---
### スタイルを整える
#### ビデオギャラリーのHTML構造を確認する
##### jsで作り変えたHTMLに対してCSSを適用する
HTMLファイルの内容でなく、**jsが実行された後に、実際にブラウザに表示されているHTMLの構造を想定する必要がある**
  
Chromeで表示しているWebページのHTMLを確認するには、デベロッパーツールを表示して「**Elements**」パネルを選択する

---

### 全体のスタイルを整える

#### 1. 全体のスタイルとタイトルを整える

```css
/* 背景色を指定して中央揃え */
body {
  background-color: #444;
  box-sizing: border-box;
  text-align: center;
}

/* タイトルを整える */
h3 {
  color: #bbb;
  font-size: 20px;
  font-weight: bold;
}
```

#### 2. ビデオリストの幅と余白を調整する

```css
/* ビデオリストの幅と余白を調整 */
#videoList{
  margin: auto;
  padding-top: 40px;
  width: 1216px;
}
```

#### 3. 動画に枠を付ける
```css
/* 動画に枠を付ける */
#videoList .video {
  border: 4px solid #fff;
  box-shadow: 0px 0px 14px #000;
  float: left;
  height: 315px;
  margin: 20px;
  width: 560px;
}
```

#### 4. iframe要素を整える
```css
/* iframe要素を整える */
#videoList .video iframe {
  border: none;
  height: 315px;
  width: 560px;
}
```
#### iframe
\<iframe>(アイフレーム)タグはHTMLの文書の中に、もうひとつ別のHTMLファイルを組み込みます（インラインフレームといいます）。HTML内に別のHTMLを入れ子にするタグと考えるといいでしょう。

iframeは、埋め込みコンテンツとしての意味しかないけど、だからこそ汎用的に使われているのかも。
```
・iframeタグ  inline frame  <iframe>〜</iframe>
特定のファイルをページの一部に表示させます。

・src属性
画像や文書など、表示させるファイルの出処を指定します。

・width属性：幅の指定
書いてある通りですが、iframeの幅を指定できます

・height属性：高さの指定
書いてある通りですが、iframeの高さを指定できます
```
<iframe>

---

