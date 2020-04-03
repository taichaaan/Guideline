 # Outline
本ガイドラインは、迷っている時間を少なくし、品質とスピードを一定に保つためのものです。   

## Definition
+ 予測しやすい
+ 再利用しやすい
+ 保守しやすい
+ 拡張しやすい

 以上4つが CSS Architecture で提唱された「良いcss」 の定義です。  
 これらが保たれているかを念頭においてコーディングしてください。



 <br>
 
# Directory
```
root/
	├ include/
	│	├ functions.php
	│	├ meta.php
	│	├ js.php
	│	├ loading.php
	│	├ preload-svg.php
	│	├ header.php
	│	├ footer.php
	│	└ aside.php
	├ assets/
	│	├ img/
	│	│	├ common/
	│	│	├ meta/
	│	│	└ ページ名/
	│	├ svg/
	│	├ css/
	│	│	├ common.min.css
	│	│	├ theme-ページ名.min.css
	│	│	├ wp-admin.min.css
	│	│	├ wp-editor.min.css
	│	│	└ wp-login.min.css
	│	├ js/
	│	│	├ library.js
	│	│	├ module.min.js
	│	│	├ common.min.js
	│	│	├ theme-ページ名.min.js
	│	│	├ component-コンポーネント名.min.js
	│	│	└ wp-admin.min.js 
	│	├ font/
	│	└ pdf/
	├ wp/
	├ ページ名/
	└ index.php
```

## include
各ページで読み込ませる共通パーツを格納するディレクトリです。
- functions.php -- 関数を記述するファイルです。また、変数やサイト全体の設定も合わせて記述しています。
- meta.php -- headタグ内のファイルです。headはheader.phpと名前が似ているため、meta.phpにしています。
- js.php -- body閉じタグの手前に配置するjsを記述するファイルです。headタグ内が都合が良い場合は、meta.phpに直書きしてください。


## assets
- img -- imgタグで出力する画像を格納。common,meta以外は、ページ名でディレクトリを作る。
- svg -- インラインで仕様するsvgを格納
- font -- フォントをディレクトリ単位で格納
- pdf -- PDFを格納


## css
- common.min.css -- ページ共通のcssファイル
- theme-ページ名.min.css --  ページ固有のcssファイル
- wp-admin.min.css --  WordPressの全ユーザの管理画面用cssファイル
- wp-editor.min.css --  WordPressの編集者の管理画面用cssファイル
- wp-login.min.css --  WordPressのログイン画面用cssファイル

※themeが少ない場合は、commonと合わせても問題ない  
※style.cssは、どこのスタイルか解らず抽象的なため廃止し、common（共通）にしています。


## JavaScript
- library.js -- 外部ライブラリを集めたJavaScriptファイル（圧縮なし）
- module.min.js -- 自作プラグインを集めたJavaScriptファイル
- common.min.js -- ページ共通のJavaScriptファイル
- theme-ページ名.min.js -- ページ固有のJavaScriptファイル
- component-コンポーネント名.min.js -- フォームなど部品のJavaScriptファイル
- wp-admin.min.js  -- WordPressの全ユーザの管理画面用JavaScriptファイル

※themeが少ない場合は、commonと合わせても問題ない  
※script.jsは、どこのscriptか解らず抽象的なため廃止し、common（共通）にしています。

 <br>
 
 
# Breakpoint

| type | range |
----|---- 
| pc | 1024px ~ |
| tablet | 561px ~ 1023px |
| smartphone | ~ 560px |

メディアクエリは、sassのmixinで管理しています。  
上記の範囲はあくまで基礎で、768pxや1000pxなど 状況に応じて可変してください。

```
'ss': 'screen and (min-width: 321px)',
'xs': 'screen and (min-width: 415px)',
'sm': 'screen and (min-width: 561px)',
'md': 'screen and (min-width: 769px)',
'lg': 'screen and (min-width: 1024px)',
'xl': 'screen and (min-width: 1280px)',
'fhd': 'screen and (min-width: 1921px)',
```
```
'ss': 'screen and (max-width: 320px)',
'xs': 'screen and (max-width: 414px)',
'sm': 'screen and (max-width: 560px)',
'md': 'screen and (max-width: 768px)',
'lg': 'screen and (max-width: 1023px)',
'xl': 'screen and (max-width: 1279px)',
'fhd': 'screen and (max-width: 1920px)',
```

 
# Common

## Comment
```
///////////////////////////////////////////////////////////////
// sass,JavaScript,php comment1
///////////////////////////////////////////////////////////////

///////////////////////////////////////////
// sass,JavaScript,php comment2
///////////////////////////////////////////

/* ------------------------------------------------------------
 css comment 1
------------------------------------------------------------ */

/* ----------------------------------------
 css comment 2
---------------------------------------- */

/* ---------- all comment 3 ---------- */

/* ----- all comment 4 ----- */

/* -- all comment 5 -- */

/* - all comment 6 - */
```
 
## 命名規則

### 基本
+ 半角英数字のみを使用
+ 記号は「-」（ハイフン）を使用し、ハイフンが使えない場合は「_」（アンダースコア）を使用する
+ 全角スペース、半角スペースは使用しない

 
### 画像名
画像のファイル名は、単語間は「_」（アンダースコア）、状態を表す時は「-」（ハイフン）を使用してください。    
例えば、色が違う場合などがこれに当たります。
また、ページや種類ごとでディレクトリ名を変えているので、画像の先頭に top などの ページ名は不要としています。
```
// 例
logo_horizontal-black.svg
logo_horizontal-white.svg
logo_vertical-black.svg

[大内容]_[小内容]_..._[連番]-[状態].[拡張子]
```

### ディレクトリ名
単語間はハイフンを使用してください。  
```
// 例
/about/
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
 
### 変数名 [JavaScript,php]
スネークケースを使用してください。  
文字の単語間にアンダーバーを使用し、ひと単語が長いなど 単語を読み易くするため 大文字の使用も有りとしています。  
```
// 例
const snake_road = 'hoge';
const snakeBlack_road = 'hoge';
```
 
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
| name | description |
----|---- 
| init | 初期化 |
| base | 基礎 |
| basis | 基礎 |
| basic | 基礎 |
| set | 値を代入する場合に用いる |
| get | データの取得 |
| add | 追加 |
| remove | 削除 |



<br> 

# HTML,Pug

## Comment
コメントアウトは、sectionなど大区分か ループする記述の可視性を上げる為、始めと終わりに記述してください。
```
<!-- t-top-visual -->
<section class="t-top-visual">
</section>
<!-- /t-top-visual -->
```
```
//- ----------------------------------------
//- t-top-visual
//- ----------------------------------------
section.t-top-visual
```


<br> 

# css

よく使うcss

```
:nth-of-type(X)  /* X番目 */
:nth-of-type(n+X)  /* X番目以降 */
:not(:first-of-type)  /* 最初以外 */
:not(:last-of-type)  /* 最後以外 */
:nth-last-of-type(n+X)  /* 最後からX番目以前 */
```
|  |  |
----|---- 
| object-fit | <img> や <video> などの中身を、コンテナーにどのようにはめ込むかを設定できる。 |
| text-transform | テキストを大文字表記、小文字表記を指定できる。 |
| will-change | 要素の変更が予測されているかブラウザに助言できる。最終解決手段で使用する。 |

1万人に聞いた、2019年の最新CSS使用状況  
https://qiita.com/rana_kualu/items/6d967b4d4cd4fc59d7e2



<br> 

# Sass
flocssをベースにカスタマイズしています。  
https://github.com/hiloki/flocss


## Directory
```
└ dev/dev_html/assets/sass/
	├ foundation/
	│	├ animation/
	│	├ genetal/
	│	│	├ function/
	│	│	├ mixin/
	│	│	└ variable/
	│	├ base/
	│	│	├ _reset.scss
	│	│	└ _base.scss
	│	├ font/
	│	└ library/
	├ layout/
	├ object/
	│	├ component/
	│	├ project/
	│	├ utility/
	│	├ js/
	│	└ wp/
	├ theme/
	│	└ _pagename.scss
	├ ua/
	├ wp-admin.scss
	├ wp-editor.scss
	├ wp-login.scss
	└ common.scss
```
- foundation -- プロジェクトにおける基本的なスタイルを定義します
	- animation -- アニメーションを定義します
	- general -- mixinや変数など、プロジェクト全体で使用するスタイルを定義します
		- function -- 関数をファイル別で定義します。
		- mixin -- mixinをファイル別で定義します。
		- variable -- 変数をファイル別で定義します。
	- font -- アニメーションを定義します
	- base -- フォントの読み込みがある場合、定義します。
	- library -- jsの外部プラグインでcssがある場合は、拡張子をscssに変えて定義します。
- layout -- ページを構成するスタイルを定義します。
- object -- 繰り返し使用できるスタイルを定義します
	- component -- 再利用できるパターンとして、小さな単位のモジュールを定義します。
	- project -- 複数のcomponentからなる、もしくはsection単位などの大きな単位のモジュールを定義します。
	- utility -- わずかなスタイルの調整のための便利クラスなどを定義します。
- theme -- objectには属さない、ページ固有のスタイルを定義します。
- ua -- UserAgentを使用し、ブラウザや端末などでスタイルを時に定義します。


## common.scss
```
@charset "UTF-8";
/*
 *
 * common.scss
 *
 */

//
// This file just imports sass.
//

///////////////////////////////////////////////////////////////
// general
///////////////////////////////////////////////////////////////
@import './foundation/general/**/*.scss';


/* ------------------------------------------------------------
 Foundation
------------------------------------------------------------ */
@import './foundation/font/**/*.scss';
@import './foundation/base/reset.scss';
@import './foundation/base/base.scss';
@import './foundation/animation/**/*.scss';
@import './foundation/library/**/*.scss';


/* ------------------------------------------------------------
 Layout
------------------------------------------------------------ */
@import './layout/**/*.scss';


/* ------------------------------------------------------------
 Object
------------------------------------------------------------ */
@import './object/component/**/*.scss';
@import './object/project/**/*.scss';
@import './object/utility/**/*.scss';
@import './object/js/**/*.scss';
@import './object/wp/**/*.scss';


/* ------------------------------------------------------------
// Theme
------------------------------------------------------------ */
@import './theme/**/*.scss';


/* ------------------------------------------------------------
 ua
------------------------------------------------------------ */
@import './ua/**/*.scss';
```


## component、projectの判別について
https://qiita.com/uggds/items/d904b2f9a103c37a25fa


## component
componentでは、使い回しができるパーツを定義します。  
各サイトで あまり変わることはないです。  
例）ボタンやタイトル、段落、リスト、テーブル、ページャー、column、flex、gird、inner、content、space  など

```
.c-flex{
	display: flex;
	justify-content: space-between;
}
.c-flex--2-column{
	> *{
		width: percentage( 500 / 1080 );
 	}
}
.c-flex--m30{
	margin-left: -30px;
	> * {
		margin-left: 30px;
	}
}
```
```
.c-column{
	display: flex;
	flex-wrap: wrap;
}
.c-column--2{
	> * {
		width: percentage( 500 / 1080 );
	}
}
```
```
.c-paragraphs{
	> * {
		&:not(:last-of-type){
			margin-bottom: 30 / 16 + em;
		}
	}
}
.c-paragraph-small{
	&,*{
		@include mq-up{
			@include line-height(14,28);
			@include font14;
		}
		@include mq-down{
			@include line-height(16,30);
		}
		@include mq-updown-free{
			@include font13;
		}
		@include mq-down(sm){
			@include font12;
		}
	}
}
```


## project
projectでは、複数のcomponentからなる大きなブロックを定義します。  
複数のcomponentがなくても、フォームやブログの詳細記事など今後増える可能性があるものもprojectに含めます。  
また、大きすぎるパーツもprojectに含んで良いものとしています。  
各サイト固有のprojectが定義されます。  
例）form、article、サイト固有project


## utility
utilityでは、単一スタイルを定義します。  
可変で値が変わるものは、componentで定義してください。  
省略する場合は、Emmentの記述などを参考にしてください。  
例）display、margin、padding、text-align  など

```
.u-bg-none  { background-color: rgba(0,0,0,0); }
.u-bg-white { background-color: #fff; }
```
```
.u-ib     { display: inline-block; }
.u-inline { display: inline; }
.u-block  { display: block; }
.u-n      { display: none; }

@include mq-up(lg){
	.u-n-mqUp-lg { display: none; }
}
@include mq-down(lg){
	.u-n-mqDown-lg { display: none; }
}
```
```
.u-t-right   { text-align: right; }
.u-t-left    { text-align: left; }
.u-t-center  { text-align: center; }
.u-t-justify { text-align: justify; }
```
```
.u-font-normal  { font-weight: normal; }
.u-font-bold    { font-weight: bold; }
.u-font-lighter { font-weight: lighter; }
.u-font-bolder  { font-weight: bolder; }
.u-font-700     { font-weight: 700; }
```
```
.u-p-relative{ position: relative; }
.u-p-absolute{ position: absolute; }

.u-p-relative-0{ position: relative; z-index: 0; }
.u-p-relative-1{ position: relative; z-index: 1; }
.u-p-relative-2{ position: relative; z-index: 2; }
```




## theme
objectは、繰り返し使用できるスタイルで、ページ固有のスタイルを定義する場所がないです。  
そのため、sassディレクトリ直下にthemeディレクトリを追加し、そこをページ固有のスタイルを定義するディレクトリにします。  
pageという名前が良かったのですが、projectのpとかぶっているためthemeにしています。



## クラス名
状態を表すものについては、クラスが長くなってしまうのを防ぐ為、ハイフンから始めて良いものとしています。

```
<p class="c-btn c-btn--black">
 <!-- 通常 -->
</p>

<p class="c-btn -black">
 <!-- これも有り -->
</p>
```
```
.c-btn{
 &.-black{
  /* style */
 }
}
```



<br> 

# JavaScript

今までscript.jsにまとめていましたが、読み込み速度や今後の管理を考慮して 意味合い・種類別に分割することにしました。  

## Directory
```
└ dev/dev_html/assets/js/
	├ library/
	├ module/
	├ common.js
	├ theme-ページ名.min.js
	├ component-コンポーネント名.min.js
	└ wp-admin.min.js 
```

- library -- 外部ライブラリーを格納するディレクトリ。Gulpで結合してlibrary.jsとして圧縮せず出力します。
- module -- 独自プラグインを格納するディレクトリ。今まではscript.min.jsとしていましたが、区別するために分けました。Gulpで結合してmodule.min.jsとして圧縮して出力します
- common.js -- 全ページ共通のScriptなどを記述します。sassのobjectディレクトリに関するものは、処理が少なければcommon.jsに記述しても良いです。
- theme-ページ名.min.js -- ページ固有のScriptを記述します。
- component-コンポーネント名.min.js -- 複数のページで使用するが、処理が多いものなどを記述するファイルです。フォームやスライダーなどが該当します。

themeやcomponentを分けた理由は、ページ数が多いサイトだとscript.min.jsがどうしても多くなるところが気になっていたからです。  
小規模のサイトやJavaScriptが少ないサイトでは、themeやcomponentはcommon.jsに記述して良いです。



## プラグイン
- gsap --  https://greensock.com/
- imagesLoaded  --  https://imagesloaded.desandro.com/
- Polyfill sticky  --  https://github.com/wilddeer/stickyfill



## AnimationFrame
```
///////////////////////////////////////////////////////////////
// variable
///////////////////////////////////////////////////////////////
const requestAnimationFrame = window.requestAnimationFrame || window.mozRequestAnimationFrame || window.webkitRequestAnimationFrame || window.msRequestAnimationFrame;
			const cancelAnimationFrame  = window.cancelAnimationFrame || window.mozcancelAnimationFrame || window.webkitcancelAnimationFrame || window.mscancelAnimationFrame;
			window.requestAnimationFrame = requestAnimationFrame;
			window.cancelAnimationFrame  = cancelAnimationFrame;
			
			
///////////////////////////////////////////////////////////////
// stopAnimation
///////////////////////////////////////////////////////////////	
function stopAnimation(x,y){
	if(
		mouse_clientX == Math.round( x * 100 ) / 100 &&
		mouse_clientY == Math.round( y * 100 ) / 100 &&
		start_flg == false
	){
		window.cancelAnimationFrame( requestId );
		setTimeout(function(){
			start_flg = true;
		},20);
	}
}
		
///////////////////////////////////////////////////////////////
// animation
///////////////////////////////////////////////////////////////	
function animation(){
	/* animation */
	if( 止めたい時の条件 ){
		stopAnimation(x,y);
	}
}
	
///////////////////////////////////////////////////////////////
// animationLoop
///////////////////////////////////////////////////////////////
let requestId = '';
function animationLoop(){
	requestId = window.requestAnimationFrame( animationLoop );
	animation();
}
animationLoop();
```




<br> 

# WordPress

## Directory
```
└ root/
	└ wp/
```

## サブディレクトリ 
WordPressは、サブディレクトリ上階層で表示する形を採用しています。  
ルート直下がスッキリし、可視性が上がるメリットがあります。

### 方法
https://zenlogic.jp/support/knowledge/wordpress/install_directory.html




## プラグイン 

### 必須
- Classic Editor
- Duplicate Post
- EWWW Image Optimizer
- WP Multibyte Patch

### 任意
- Category Order and Taxonomy Terms Order
- Contact Form 7
- Contact Form 7 add confirm
- Custom Post Type Permalinks
- Flamingo
- Post Types Order
- Smart Custom Fields
- Simple 301 Redirects
- User Role Editor


## 基本

## トップページ、固定ページなど
```
<?php
	$args = array(
		'post_type'      => 'event',   // カスタム投稿タイプの名称を入れる
		'post_status'    => 'publish', // 公開している投稿のみ
		'posts_per_page' => 4          // 件数
	);
	$the_query = new WP_Query( $args );
	if ( $the_query->have_posts() ) : while ( $the_query->have_posts() ) : $the_query->the_post();
?>
<?php
	endwhile;
	else:
		echo '<p>現在、投稿はありません。</p>';
	endif;
	wp_reset_postdata();
?>
```





<br> 

# 開発環境


## Directory
```
└ project/
	├ dev/
	│	├ dev_html/
	│	│	└ assets/
	│	└ gulp/
	│		├ gulpfile.js
	│		├ package.json
	│		├ package-lock.json
	│		└ node_modules/
	└ public_html/
```

devディレクトリの中に、pugやsass、結合前のJavascriptなどの元データを入れておきます。  
public_htmlにそれらがコンパイルされる仕様です。  
phpはコンパイルしないので、public_htmlにそのままファイルを作成、記述します。  




## Gulp
タスクランナーは、Gulpを使用しています。
- pugのコンパイル、圧縮
- sassのコンパイル、結合、圧縮
- JavaScriptの結合、圧縮
- 画像、svgの圧縮
- 上記以外のファイルの移動


