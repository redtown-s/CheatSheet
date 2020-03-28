# CSS
  ### Emmet記法
```css
  /* ds:none tab */
  #form{
    display: none;
  }

CSS　#08 margin､paddingを展開してみよう
body {
  /* m */
  margin: 10px;
  /* p */
  padding: 10px;
  /* m10 */
  margin: 10px;
  /* m10p */
  margin: 10%;
  /* m10r */
  margin: 10rem;
  /* m10p20p */
  margin: 10% 20%;
  /* m10-20-30 */
  margin: 10px 20px 30px;
  /* mb10 */
  margin-bottom: 10px;
}

#09 CSSのプロパティを展開してみよう
body {
  /* fsz */

  font-size: 20px;
  cursor: pointer;
  /* fw */
  font-weight: normal;
  /* psr */
  position: relative;
  /* psab */
  position: absolute;
}

  ```

  ---
###  全体のスタイル
|プロパティ|値|効果|
|-|-|-|
|box-sizing|border-box|要素のサイズ指定にボーダーの太さを含まれるようにする|
|text-align|center|画像やテキストの中央揃え|
||||
||||
||||



---
#### いちやさjs　レイアウトサンプル

```css
/* 全体のスタイルを調整 */
body {
  background-color: #444444;
  box-sizing: border-box;　要素のサイズ指定にボーダーの太さを含まれるようにする
  text-align: center;　中央寄せ
}

/* 余白調整 */
/*id名#がgalleryのxx要素に対して */
#gallery {
  margin: auto;
  padding-top: 40px;
  width: 500px;
}

/* 写真に枠を付ける */
/* #gallery .main img */
.main img {
  border: 4px solid #fff; 周囲の枠
  box-shadow: 0 0 14px #000;
  width: 100%; 
}

/* キャプションを目立たせる */
/* #gallery .main p */
.main p {
  color: #bbb;　フォントカラー
  font-size: 20px;
  font-weight: bold;　太字
}

/* 画像を小さく、丸くする */
.thumb img{
  border: 4px solid #fff; 白枠
  border-radius:400px;　角丸
  box-shadow: 0 0 10px #000;　シャドー
  height:60px;　hとwを揃えると正円になる
  margin: 10px;　画像間の上下左右の余白
  width: 60px;  
}



```

