# outline

本ガイドラインは、コーディングの品質を保ったり 実装時の迷いを少なくする為のものです。 

あくまで心得の様なもので、この型に合わせる必要はなく、臨機応変にカスタマイズして良いです。  

マークダウン方式についてはこちらを確認してください。  
https://gist.github.com/mignonstyle/083c9e1651d7734f84c99b8cf49d57fa

 <br>
 

# Common
 
## 命名規則

### 基本
+ 半角英数字のみを使用
+ 記号は「-」（ハイフン）を使用し、ハイフンが使えない場合は「_」（アンダースコア）を使用する
+ 全角スペース、半角スペースは使用しない
 <br>
 
### 画像名
画像のファイル名は、単語間は「_」（アンダースコア）、状態を表す時は「-」（ハイフン）を使用してください。    
例えば、色が違う場合などがこれに当たります。
また、ページや種類ごとでディレクトリ名を変えているので、画像の先頭に top などの ページ名は不要としています。
```
// 例
assets/img/common/logo_horizontal-black.svg
assets/img/common/logo_horizontal-white.svg
assets/img/common/logo_vertical-black.svg

[大内容]_[小内容]_..._[連番]-[状態].[拡張子]
```
 <br>

### ディレクトリ名
単語間はハイフンを使用してください。  
```
// 例
/about-us/
/portfolio-item/
```
 <br>

### jsファイル名
キャメルケースを使用してください。  
```
// 例
objectFit.js
isCurrent.js
smoothScroll.js
```
 <br>
 
 
### 変数名 [JavaScript,php]
スネークケースを使用してください。  
文字の単語間にアンダーバーを使用し、ひと単語が長いなど 単語を読み易くするため 大文字の使用も有りとしています。  
```
// 例
const snake_road = 'hoge';
const snakeBlack_road = 'hoge';
```
 <br>
 
### 関数名 [JavaScript,php]
キャメルケースを使用してください。  
最初の単語以外の文字の先頭を大文字を使用してください。  
```
// 例
const getWindowHeight = function (){
    // function ...
}
```

また、関数の最初は、なにをしている関数なのかを明確にするため、以下のような文字を使用してください。
| set | 値を代入する場合に用いる |
| get | データの取得 |
| add | 追加 |






# Sass
 
## flocss

### クラス名
クラスは、flocssのものをbaseに使っています。
ただ、状態を表すものについては、クラスが長くなってしまうのを防ぐ為、ハイフンから始めて良いものとしています。

```
<p class="c-btn c-btn-black">
 <!-- 通常はこれですが -->
</p>

<p class="c-btn -black">
 <!-- これも有りです -->
</p>
```
```
.c-btn{
 &.-black{
  /* style */
 }
}
```

