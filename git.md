---------------------------------------------------------
GitHub Pagesでサイトを公開する記事
https://www.tam-tam.co.jp/tipsnote/html_css/post11245.html

カンペ
https://******-s.github.io/*********/

カフェ
https://******-s.github.io/*********_cafe/

いちやさgit
https://*********-s.github.io/*********Sample1/
---------------------------------------------------------

1.ローカルリポジトリを作成する

ディレクトリ内までcd
cd *****PJ
cd js_ichiyasa

「js_ichiyasa」にローカルリポジトリを作成する（まだ器だけの状態）
git init　　//ローカルリポジトリ作成コマンド
ディレクトリ内を確認
ls -a　　　//リストオール

2.ステージングエリアに登録

・カレントディレクトリ配下のすべてのファイルを追加
 git add .　　//追加コマンド

・サブディレクトリ（janken）配下のすべてのファイルを追加
 git add janken

・サブディレクトリ（janken）配下の指定のファイルを追加
 git add janken/index.html

※コマンド入力後、以下の警告が出る
warning: LF will be replaced by CRLF in janken/index.html.
The file will have its original line endings in your working directory

警告：LFはjanken / index.htmlでCRLFに置き換えられます。
ファイルの元の行末は作業ディレクトリになります

git statusで確認
new file:追加成功
Untracked files:追跡できないファイル（追加していないので）

・ファイルの差分確認
git diff 


・ステージングエリアとGitディレクトリの差分を確認する
git diff --cached
長文の縦の...内で↓キーでスクロール
qで抜ける
※エクセルなどのバイナリファイルは差分を確認できない。変更されたことのみ確認できる
　メモ帳などのテキストファイルは確認できる

3.（まだ器だけの状態の）ローカルリポジトリにコミット
git status
git commit　 //コミットを実行

hint: Waiting for your editor to close the file...（vscodeにコメントを書いてエディタを閉じて）

vscodeが開く
vscodeの#で囲まれた行はコメント行。コミットメッセージには反映されない

・コミットメッセージを書く
ルール
・1行目に要約
・2行目は空白
・3行目以降に詳細を書く
※複数行で書いた場合は1行目の内容がコミットタイトルとして扱われる

```
1 学習用のプロジェクトをコミット
2 
3 「javascriptいちやさ」のファイル7章まで
```
・書き終わったら**ファイルを保存**し、vscodeを閉じる
###### コミットメッセージが1行の時に素早くコミットする
git commit -m "ここにコミットメッセージを書く"

すべてコミットすると以下が表示される
$ git status
On branch master
nothing to commit, working tree clean
（コミットするものは何もない。ワークツリーはクリーンだ）
##### コミットされる情報は、ステージングエリアに登録した時点のファイル
登録後にワークツリーで行った変更は含まれない。新しい変更があったファイルをコミットしたければ、再度addコマンドを実行する

### リモートリポジトリ
4.Githubでリポジトリを新規作成する方法
[Github](https://github.com/)
右上+アイコン＞New repository
Repository nameを入力、ディスクリプションを入力
Public　か　Private　を選択　　※Privateはクレジット決済などあるケース有り
Create repositoryクリック

・githubページ内にヒント明記あるので参考に
[参考記事：ローカルでgitを使用した後、gitHubに登録する方法](https://qiita.com/koshihikari/items/dcf126fa9c0de2b6fa7e)

新規リポジトリ作成後に表示される画面の文書アイコンをクリックし内容をコピー、
以下の内容をターミナルに入力する。
git remote add origin git@github.com: ******-s/js_ichiyasa.git
上記コマンドによってoriginという名前(識別子)で
git@github.com: ******-s/js_ichiyasa.gitのリモートリポジトリを指すようになります。

下記のコマンドを入力してローカルの内容をリモートリポジトリに送信します。
git push -u origin master　　//リモートにプッシュ。originはリモートリポジトリを表している（クローン元のリポジトリ）
　
・ローカルの内容をリモートリポジトリに送信する
git checkout master
ローカルのmasterブランチの内容を上記で登録したリモートリポジトリに送信します。
ローカルのブランチがmasterでない場合は下記のコマンドでmasterブランチに移動しておいてください。


vscodeで編集する
code /C:/*****s/****/****PJ/js_ichiyasa



---
・ワークツリーの変更を取り消す場合
git status
modified：ファイル名の赤文字（ステージングエリアに登録されていない変更を表示している）
git checkout -- ファイル名.拡張子
git statusでクリーンなっていれば変更取り消しに成功。
ファイルは最後にコミットした時の状態へ戻っている。
※ **厳密には、最後にコミットした状態ではなく、ステージングエリアの状態に戻す**コマンド。
ステージングエリアにファイルの状態が残ったままになっていると想定通りの動作にならない。
その場合は、**git reset**コマンドを使う

git checkoutで取り消せないケース
・ファイルを新規作成したとき（作成したファイルがそのまま残る）
・ファイル名を変更したとき（ファイル名変更前と変更後のファイルが残ってしまう）
いずれの場合も不要なファイルは自分で削除する

・ステージングエリアへの変更を取り消す
間違ってファイルの状態をステージングエリアに登録してしまった。。。
git reset コマンドを使って取り消す
・git checkoutと違い、ワークツリー内のファイル変更は取り消されない
git reset HEAD ファイル名.拡張子（ディレクトリパス）
resetの後ろのHEADは、このローカルリポジトリで**最後にコミットした状態を意味している**
ステージングエリアの状態を最後のコミットと同じ状態にするという意味。
・git resetコメンドには、コミットをなかったことにする機能もあるが、コミット自体に手を加えると様々な問題を引き起こすことがある。コミットした内容を取り消したいときはファイルを以前の状態に修正して新しく「取り消すためのコミット」を追加するようにする。


#### Gitの管理下にあるファイルを削除する
・ディレクトリを削除する場合
git rm -r   //rmの後ろに「-rオプション（recursive:再帰的※）」を指定する
※指定したディレクトリの中にあるファイルやディレクトリに対して、削除の処理を繰り返し実行するいう意味
-rオプションを付けないと中身があるディレクトリを削除できない

##### ファイルやディレクトリを削除するコマンド
git rm ファイルパス（ファイル名）　　//**ファイル**を削除するコマンド
git rm -r ディレクトリパス　　//**ディレクトリ**を削除するコマンド


#### Gitで管理しない（無視する）ファイルを設定する
##### .gitignore　（ignore:Gitが無視(ignoreイグノア)する）
「.git」ディレクトリがある（同列の階層に）.gitignoreを配置する
※基本ローカルリポジトリ配下であればどこでも良いが、**.gitignoreファイルが配置されたディレクトリ配下のパスにしか効果がない**
ローカルリポジトリ内のすべてのディレクトリに設定を反映するには「.git」ディレクトリと同じ階層に置くこと
・一度設定すればgit status コマンドでディレクトリをを指定しても、そのファイルを無視してくれる
・.gitignoreの書き方
```
vscodeで.gitignoreファイルを新規作成
ディレクトリパス（名）/ファイル名.拡張子　//ファイル名を直接指定
target/　　　　//ディレクトリ名を指定する（ディレクトリ全体が対象））
* .log　　//*を使えば、ファイルの拡張子で指定できる

subDirectory/file.md
target/
* .log　

sample.txt    //これでも無視される

```

##### .gitignoreを作成する
注意：Windowsの場合
.gitignoreのように、.で始まるファイルを作成する場合は必ずvscodeからファイルを作成すること。それ以外の方法だと面倒な手間が発生してしまう

・vscodeで.gitignoreファイルを作成
・.gitignoreファイル内に無視したいファイル名を書く
git status
Untracked 赤字表示される
git add .gitignore
git commit -m ".gitignoreファイルを追加する"
※無視推奨ファイル 
以下のファイルがフォルダに作成されることがあるので、.gitignoreに追加しておく（Gitで管理する必要がない）
Windows... Thumbs.db
MacOS... .DS_Store

[.gitignore(無視ファイル)の書き方に迷ったらここ(PG言語やツールごとのテンプレート集)](https://github.com/github/gitignore) 

#### カレントディレクトリ配下のコミット履歴を確認する
git log
差分付きでコミット履歴を確認する場合
git log -p   //git diff的な使い方