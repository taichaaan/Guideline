# guideline

本ガイドラインは、コーディングの品質を保ったり 実装時の迷いを少なくする為のものです。 

あくまで心得の様なもので、この型に合わせる必要はなく、臨機応変にカスタマイズして良いです。  

 <br>
 
## 命名規則

### 基本
+ 半角英数字のみを使用
+ 記号は「-」（ハイフン）を使用し、ハイフンが使えない場合は「_」（アンダースコア）を使用する
+ 全角スペース、半角スペースは使用しない

### 画像名
画像のファイル名は、単語間は「_」（アンダースコア）、Modifierを表す時は「-」（ハイフン）を使用してください。    
例えば、色が違う場合などがこれに当たります。
```
// 例
assets/img/common/logo_horizontal-black.svg
assets/img/common/logo_horizontal-white.svg
assets/img/common/logo_vertical-black.svg
```

### ディレクトリ名
単語間はハイフンを使用してください。  
```
// 例
/about-us/
/portfolio-item/
```

### jsファイル名
キャメルケースを使用してください。  
```
// 例
objectFit.js
isCurrent.js
smoothScroll.js
```

### html / class
下記のflocssを参照してください。

### 変数名
スネークケースを使用してください。  
文字の単語間にアンダーバーを使用し、ひと単語が長いなど 単語を読み易くするため 大文字の使用も有りとする。  
```
// 例
const snake_road = 'hoge;
const snakeBlack_road = 'hoge;
```

### 関数名
キャメルケースを使用してください。  
最初の単語以外の文字の先頭を大文字を使用してください。  
```
// 例
const getWindowHeight = function (){
    // function ...
}
```








