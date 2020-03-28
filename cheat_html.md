# Emmet記法 
## HTML
コード入力後、tabキーで省略して記述できる

id名を直接記載
```html
<!-- div#target -->
<div id="target"></div>
```
---
#### Emmetの基本ルール

|記号  |意味  |
|:-------|:-------------|
|要素>要素|直下の階層を指定|
|要素+要素|隣接する要素|
|要素*数字|要素を複製する|
|^|一つ上の階層を指定|
|()|グループ化|
|$|連番にする|
|#id名|divタグにid属性を設定|
|.クラス名|divタグにクラスを設定|
|[]|属性を設定|
|{}|テキストを設定|
---
#### formに関するタグを展開してみよう
```html
<!-- form:post -->
<form action="" method="post"></form>

<!-- input:t -->
<input type="text" name="" id="">

<!-- input:r -->
<input type="radio" name="" id="">

<!-- input:c -->
<input type="checkbox" name="" id="">

<!-- select>[value="item$"]*5 -->
<select name="" id="">
  <option value="item1"></option>
  <option value="item2"></option>
  <option value="item3"></option>
  <option value="item4"></option>
  <option value="item5"></option>
</select>
```
#### []を使用して連続して書く
```html
<!-- p>input[type=submit id=submit value=送信] -->

<p><input type="submit" id="submit" value="送信"></p>


<!-- form#form1>ul.radioList>li*5>label[for=r-$]>input[type=radio name=r id=r-$]+{内容$} -->

<form id="form1" action="">
 <ul class="radioList">
 <li><label for="r-1"><input name="r" id="r-1" type="radio"/>内容1</label></li>
 <li><label for="r-2"><input name="r" id="r-2" type="radio"/>内容2</label></li>
 <li><label for="r-3"><input name="r" id="r-3" type="radio"/>内容3</label></li>
 <li><label for="r-4"><input name="r" id="r-4" type="radio"/>内容4</label></li>
 <li><label for="r-5"><input name="r" id="r-5" type="radio"/>内容5</label></li>
 </ul>
</form>
```
---
\<textarea name="textarea" id="textarea" cols="50" rows="30"></textarea>

cols="50" rows="30" //50文字幅 30行のテキストエリア

---


