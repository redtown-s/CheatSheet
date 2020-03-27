#### qiita 参考記事
[マークダウン一覧](https://qiita.com/shizuma/items/8616bbe3ebe8ab0b6ca1)
[Markdown記法チートシート](http://qiita.com/Qiita/items/c686397e4a0f4f11683d)

##### 補足:ページをMarkdownで見る
Qiitaを見ていると「これはどんな記法で書いてあるんだろう」ときになることがあるかもしれません。
そんな時はMarkdown記法で見たいURLの最後に.mdをつければ見ることが出来ます。

#### リスト
* 書き方

>
```
* テキスト
    * テキスト
    * テキスト
```

* **結果**

>
* テキスト
    * テキスト
    * テキスト

* 補足
    * 「-」でも可。

#### Markdown 表Tableの基本記法
\|  TH  |  TH  |
\| ---- | ---- |
\|  TD  |  TD  |
\|  TD  |  TD  |

|  TH  |  TH  |
| ---- | ---- |
|  TD  |  TD  |
|  TD  |  TD  |

#### セル内で改行する方法
\<br>タグを挿入するとセル内で改行します。
\|  TH  |  TH  |
\| ---- | ---- |
\|  TD  |  セル内で<br>改行  |

|  TH  |  TH  |
| ---- | ---- |
|  TD  |  セル内で<br>改行  |

#### 右寄せ・中央寄せ・左寄せ
 * 左寄せの場合 :---
 * 中央寄せの場合 :---:
 * 右寄せの場合 ---:
\| TH 左寄せ | TH 中央寄せ | TH 右寄せ |
\| :--- | :---: | ---: |
\| TD | TD | TD |
\| TD | TD | TD |

| TH 左寄せ | TH 中央寄せ | TH 右寄せ |
| :--- | :---: | ---: |
| TD | TD | TD |
| TD | TD | TD |

#### マークダウンのエスケープ
[vscodeで先頭行をまとめてエスケープ](https://qiita.com/takahiro_itazuri/items/8e2999907e5c9b367090)
Ctrl + ALt + カーソル（上 or 下）

「\」をMarkdownの前につけることでMarkdownを無効化出来ます。
この記事ではこれを多用しました。
>
\\#見出しh1
とすると
\#見出しh1
となります。

#### インライン
コードをインライン表示することも可能です。
\` puts 'Qiita'`
> \` puts 'Qiita'` はプログラマのための技術情報共有サービスです。

**結果**
` puts 'Qiita'` はプログラマのための技術情報共有サービスです。

インラインコードがn個連続するバッククオートを含む場合、n+1連続のバッククオートで囲みます。

> \`\` \`バッククオート\` \`\` や \`\`\` \`\`2連続バッククオート\`\` \`\`\` も記述できます。

**結果**

`` `バッククオート` `` や ``` ``2連続バッククオート`` ``` も記述できます。 
` puts 'Qiita'` はプログラマのための技術情報共有サービスです。

#### 引用
\>を書くだけです。
ただし、改行するときはその度に\>を書く必要があるので注意です。
>
\>ここに引用文を書きます。
>>ここに引用文を書きます。

引用の中で別のMarkdown記法を使うことが出来ます。

ちなみに、引用をネストするときは\>を複数書くとネストされます。
>
\>引用文です
\>\>ネストです
>>引用文です
>>>ネストです

#### 文字の修飾(イタリック、太字)
* イタリック
「_」または「*」で文字をくくります。

>
\_イタリック\_
_イタリック_
>
\*イタリック\*
*イタリック*

* 太字
「__」または「**」で文字をくくります。

>
\_\_太字\_\_
__太字__
>
\*\*太字\*\*
**太字**

#### リスト
リストの上下に空白を入れないと正しく表示されないので注意。
また、記号と文の間に半角スペースを入れること。

* 順序なしリスト

文頭に「*」「+」「-」のいずれかを入れる。
>
\* 順序なしリスト
>
* 順序なしリスト


* 順序つきリスト

文頭に「数字.」を入れる。
見た目はほぼ変わりません。

>
1. リスト1
2. リスト2

#### 水平線
「*」か「-」を3つ以上一行に書く。
以下は全て水平線となる。
>
\*\*\*
\* \* \*
\-\-\-
\- \- \-
>
全部以下の水平線
***

#### コードの挿入
コードの挿入の基本は\`\`\`(バッククオート3つ)でコードをくくることです。
\` はバッククオートです。クォーテーション '　ではありません。ご注意を。
>
\`\`\`
function hello(){
　return "hello world!";
}
\`\`\`
のように書くと
>
```
function hello(){
  return "hello world!";
}
```
のように記載出来ます。


また、コードにシンタックスハイライトをつけることが出来ます。
各言語にシンタックスハイライトが付けられます。
例えば、phpを例にとると
>
\`\`\`php
function hello(){
　return "hello world!";
}
\`\`\`
のように書くと
>
```php
function hello(){
  return "hello world!";
}
```
シンタックスハイライトを使えるのは以下の言語
Bash, C#(cs), C++(cpp), CSS, Diff, HTML, XML, Ini, Java, Javascript, PHP, Perl, Python, Ruby, SQL, 1C, AVR Assembler(avrasm), Apache, Axapta, CMake, DOS .bat(dos), Delphi, Django, Erlang, Erlang, REPL, Go, Haskell, Lisp, Lua, MEL, Nginx, Objective C(objectivec), Parser3, Python, profile, Scala, Smalltalk, TeX, VBScript, VHDL, Vala

さらに、コードにファイル名を入れることも出来ます。\`\`\`php:(ファイル名)とするだけです。
>
\`\`\`php:hello.php
function hello(){
　return "hello world!";
}
\`\`\`
のように書くと
>
```php:hello.php
function hello(){
  return "hello world!";
}
```

#### リンクの挿入、画像の埋め込み
リンクの挿入は、\[リンクテキスト](URL)と書きます。
>
\[Qiita](http://qiita.com/)
のように書くと
[Qiita](http://qiita.com/)

タイトル付きリンク（タグにtitleがつきます）は\[リンクテキスト](URL "タイトル")と書きます。
>
\[Qiita](http://qiita.com/　"キータ")
のように書くと
[Qiita](http://qiita.com/ "キータ")

画像の挿入は、\!\[代替テキスト](画像URL)と書きます。
>
\!\[Qiita](http://cdn.qiita.com/assets/siteid-reverse-6044901aace6435306ebd1fac6b7858c.png)
のように書くと
>
![Qiita](http://cdn.qiita.com/assets/siteid-reverse-6044901aace6435306ebd1fac6b7858c.png)

タイトル付きにするにはリンクと同様に\!\[リンクテキスト](URL "タイトル")と書きます。
>
\!\[Qiita](http://cdn.qiita.com/assets/siteid-reverse-6044901aace6435306ebd1fac6b7858c.png　"キータ")
のように書くと
>
![Qiita](http://cdn.qiita.com/assets/siteid-reverse-6044901aace6435306ebd1fac6b7858c.png "キータ")

ただし、Qiitaでの編集の場合はドラック&ドロップで画像が挿入されるので、画像の挿入を手動で入力する必要はありません。