 # Outline
本ガイドラインは、迷っている時間を少なくし、品質とスピードを一定に保つためのものです。   

## Definition
+ 予測しやすい
+ 再利用しやすい
+ 保守しやすい
+ 拡張しやすい

これらが保たれているかを念頭においてコーディングしてください。



 <br>
 
# Directory
```
root/
	├ include/
	│	├ functions.php
	│	├ variable.php
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
	│	│	├ page-ページ名.min.css
	│	│	├ wp-admin.min.css
	│	│	├ wp-editor.min.css
	│	│	└ wp-login.min.css
	│	├ js/
	│	│	├ library.js
	│	│	├ module.min.js
	│	│	├ common.min.js
	│	│	├ page-ページ名.min.js
	│	│	├ component-コンポーネント名.min.js
	│	│	└ wp-admin.min.js 
	│	├ font/
	│	└ pdf/
	├ wp/
	├ ページ名/
	└ index.php
```

## Include
各ページで読み込ませる共通パーツを格納するディレクトリです。
- functions.php -- 関数を記述するファイルです。また、変数やサイト全体の設定も合わせて記述しています。変数と別々にするか悩んでます。
- meta.php -- headタグ内のファイルです。headはheader.phpと名前が似ているため、meta.phpにしています。
- js.php -- body閉じタグの手前に配置するjsを記述するファイルです。headタグ内が都合が良い場合は、meta.phpに直書きしてください。


## Assets
- img -- imgタグで出力する画像を格納。common,meta以外は、ページ名でディレクトリを作る。
- svg -- インラインで仕様するsvgを格納
- font -- フォントをディレクトリ単位で格納
- pdf -- PDFを格納


## CSS
- common.min.css -- ページ共通のcssファイル
- page-ページ名.min.css --  ページ固有のcssファイル
- wp-admin.min.css --  WordPressの全ユーザの管理画面用cssファイル
- wp-editor.min.css --  WordPressの編集者の管理画面用cssファイル
- wp-login.min.css --  WordPressのログイン画面用cssファイル

※themeが少ない場合は、commonと合わせても問題ない  
※style.cssは、どこのスタイルか解らず抽象的なため廃止し、common（共通）にしています。


## JavaScript
- library.js -- 外部ライブラリを集めたJavaScriptファイル（圧縮なし）
- module.min.js -- 自作プラグインを集めたJavaScriptファイル
- common.min.js -- ページ共通のJavaScriptファイル
- page-ページ名.min.js -- ページ固有のJavaScriptファイル
- component-コンポーネント名.min.js -- フォームなど部品のJavaScriptファイル
- wp-admin.min.js  -- WordPressの全ユーザの管理画面用JavaScriptファイル

※pageが少ない場合は、commonと合わせても問題ない  
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
 
### 関数名 [JavaScript,PHP]
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


## Template

共通部分はincludeディレクトリで管理し、各ファイルでrequireかincludeで読み込んでください。

### index.php
ファイルの最上部で、titleやdescriptionを変数に代入してください。　　
- $directory -- パンクズリストやjson-ldなどで使用する変数です。配列で ('ページ名','ディレクトリ') を指定してください。<br>ディレクトリは $home_url 以下を指定してください。
- $preload -- rel="preload" as="image" で先読みした画像を配列で指定してください。
- $style -- common.min.cssなどの共通ファイル以外に、ページ固有のcssなど読み込ませたい場合、配列でcssのhrefを指定してください。
- $script -- common.min.jsなどの共通ファイル以外に、ページ固有のcssなど読み込ませたい場合、配列でscriptのsrcを指定してください。


```
<?php require_once( dirname( __FILE__ ) . '/include/functions.php' ); ?>
<?php
	$title       = $top_title;
	$description = $top_description;
	$keywords    = $top_keywords;
	$directory   = array(
		array('ホーム','')
	);
	$preload = array(
		$home_url . 'assets/img/top/visual_01.jpg',
	);
	$style = array(
	);
	$script = array(
		$home_url . 'assets/js/page-top.min.js',
	);
 ?>
<!DOCTYPE html>
<html lang="ja">
<head>
<?php require_once($web_root.$home_url.'include/meta.php'); ?>
</head>
<body data-root="<?= $home_url; ?>">
<?php require_once($web_root.$home_url.'include/preload-svg.php'); ?>
<?php require_once($web_root.$home_url.'include/loading.php'); ?>
<?php require_once($web_root.$home_url.'include/header.php'); ?>
	<main>
		<!-- comment -->
		<!-- /comment -->
	</main>
<?php require_once($web_root.$home_url.'include/aside.php'); ?>
<?php require_once($web_root.$home_url.'include/footer.php'); ?>
<?php require_once($web_root.$home_url.'include/js.php'); ?>
</body>
</html>
```


## Headタグ
headタグは、include/meta.php で共通管理しています。  
header.phpと名前がややこしくなるので、meta.phpという名前にしています。

```
<meta charset="UTF-8">
<title><?= $title; ?></title>
<meta http-equiv="x-ua-compatible" content="ie=edge">
<meta name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=no">
<meta name="format-detection" content="telephone=no">
<meta name="robots" content="all">
<meta name="description" content="<?= $description; ?>">
<meta name="keywords" content="<?= $keywords; ?>">
<meta name="copyright" content="© <?= $author; ?>">
<meta name="author" content="<?= $author; ?>">
<meta name="theme-color" content="<?= $theme_color; ?>">
<meta name="msapplication-TileColor" content="<?= $theme_color; ?>">
<meta name="application-name" content="<?= $site_name; ?>">
<meta name="apple-mobile-web-app-title" content="<?= $site_name; ?>">
<meta name="thumbnail" content="<?= $ogp_url; ?>">
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="<?= $title;?>">
<meta name="twitter:description" content="<?= $description; ?>">
<meta name="twitter:image:src" content="<?= $ogp_url; ?>">
<meta property="og:type" content="website">
<meta property="og:site_name" content="<?= $site_name; ?>">
<meta property="og:title" content="<?= $title;?>">
<meta property="og:description" content="<?= $description; ?>">
<meta property="og:url" content="<?= $url; ?>">
<meta property="og:image" content="<?= $ogp_url; ?>">
<meta property="og:locale" content="ja_JP">
<link rel="dns-prefetch" href="//webfont.fontplus.jp">
<link rel="dns-prefetch" href="//fonts.googleapis.com">
<link rel="dns-prefetch" href="//www.google-analytics.com">
<link rel="preload" as="style" href="<?= $home_url; ?>assets/css/common.min.css<?= $cashDate; ?>">
<link rel="preload" as="script" href="<?= $home_url; ?>assets/js/library.js<?= $cashDate; ?>">
<link rel="preload" as="script" href="<?= $home_url; ?>assets/js/module.min.js<?= $cashDate; ?>">
<link rel="index" href="<?= $top_url; ?>">
<link rel="canonical" href="<?= $url; ?>">
<link rel="contents" href="<?= $top_url; ?>sitemap.xml" title="サイトマップ">
<link rel="icon" type="image/png" href="<?= $home_url; ?>assets/img/meta/icon-512x512.png">
<link rel="apple-touch-icon" href="<?= $home_url; ?>assets/img/meta/apple-touch-icon.png">
<!-- googlefont -->
<link rel="stylesheet" href="<?= $home_url; ?>assets/css/common.min.css<?= $cashDate; ?>">
<!-- fontplus -->
<script type="application/ld+json"></script>
<!-- Google Analytics -->
```





<br> 

# CSS

## 命名規則
cssファイルでコーディングをする場合、命名規則はBEMにしています。  
class名を見ただけで種類（レイアウト・共通・ページ）が理解できるように、頭には commonやlayout,ページ名を入れてください。  
flocssとほぼ同じなので、詳しくは<a href="#flocss">flocss</a>を参照ください。


### Sample
```
<div class="common-card common-card--new">
	<figure class="common-card__figure">
		<img src="" alt="">
	</figure>
	<div class="common-card__content">
		<h2 class="common-card__title">タイトルが入ります。</h2>
		<p class="common-card__time"><time>0000.00.00</time></p>
		<p class="common-card__paragraph">テキストテキストテキストテキスト</p>
		<p class="common-card__more">
			<a href="">MORE</a>
		</p>
	</div>
</div>
```


## よく使うCSS

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
	├ page/
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
- page -- objectには属さない、ページ固有のスタイルを定義します。
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
// Page
------------------------------------------------------------ */
@import './page/**/*.scss';


/* ------------------------------------------------------------
 ua
------------------------------------------------------------ */
@import './ua/**/*.scss';
```


## flocss



### Prefix

| name | description |
----|---- 
| .l- | layout |
| .c- | Component |
| .p- | Project |
| .u- | Utility |
| .t- | Theme |
| .pg- | Page |
| .ua- | UserAgent |
| .js- | JavaScript |
| .wp- | WordPress |
| .is- | Status |


### Sample
```
<div class="c-card c-card--new">
	<figure class="c-card__figure">
		<img src="" alt="">
	</figure>
	<div class="c-card__content">
		<h2 class="c-card__title">タイトルが入ります。</h2>
		<p class="c-card__time"><time>0000.00.00</time></p>
		<p class="c-card__paragraph">テキストテキストテキストテキスト</p>
		<p class="c-card__more">
			<a href="">MORE</a>
		</p>
	</div>
</div>
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


## page(旧名:theme)
objectは、繰り返し使用できるスタイルで、ページ固有のスタイルを定義する場所がないです。  
そのため、sassディレクトリ直下にpageディレクトリを追加し、そこをページ固有のスタイルを定義するディレクトリにします。  
プレフィックスは、pg です。


## class名
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

jQueryは基本的に使用していません。  
プラグインなどで仕方がない場合のみ使用してください。　　

又、今までscript.jsにまとめていましたが、読み込み速度や今後の管理を考慮して 意味合い・種類別に分割することにしました。  

## Directory
```
└ dev/dev_html/assets/js/
	├ library/
	├ module/
	├ common.js
	├ page-ページ名.min.js
	├ component-コンポーネント名.min.js
	└ wp-admin.min.js 
```

- library -- 外部ライブラリーを格納するディレクトリ。Gulpで結合してlibrary.jsとして圧縮せず出力します。
- module -- 独自プラグインを格納するディレクトリ。今まではscript.min.jsとしていましたが、区別するために分けました。Gulpで結合してmodule.min.jsとして圧縮して出力します
- common.js -- 全ページ共通のScriptなどを記述します。sassのobjectディレクトリに関するものは、処理が少なければcommon.jsに記述しても良いです。
- page-ページ名.min.js -- ページ固有のScriptを記述します。
- component-コンポーネント名.min.js -- 複数のページで使用するが、処理が多いものなどを記述するファイルです。フォームやスライダーなどが該当します。

themeやcomponentを分けた理由は、ページ数が多いサイトだとscript.min.jsがどうしても多くなるところが気になっていたからです。  
小規模のサイトやJavaScriptが少ないサイトでは、themeやcomponentはcommon.jsに記述して良いです。


## Plugin
- gsap --  <a href="https://greensock.com/" target="_blank">https://greensock.com/</a>
- imagesLoaded  --  <a href="https://imagesloaded.desandro.com/" target="_blank">https://imagesloaded.desandro.com/</a>
- Polyfill sticky  --  <a href="https://github.com/wilddeer/stickyfill" target="_blank">https://github.com/wilddeer/stickyfill</a>


## Module
module.min.jsでは、独自プラグインを圧縮して出力しています。  
また、独自プラグイン以外にも base.js（jsの諸々設定）もmodule.min.jsに含めています。

### よく使用する独自プラグイン
- js-useragent -- <a href="https://github.com/taichaaan/js-useragent/" target="_blank">https://github.com/taichaaan/js-useragent/</a>
- js-smoothScroll -- <a href="https://github.com/taichaaan/js-smoothScroll/" target="_blank">https://github.com/taichaaan/js-smoothScroll/</a>
- js-popup -- <a href="https://github.com/taichaaan/js-popup/" target="_blank">https://github.com/taichaaan/js-popup/</a>
- js-objectFit- -- <a href="https://github.com/taichaaan/js-objectFit/" target="_blank">https://github.com/taichaaan/js-objectFit/</a>
- js-lazyload -- <a href="https://github.com/taichaaan/js-lazyload/" target="_blank">https://github.com/taichaaan/js-lazyload/</a>


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




## Plugin 

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
```
<?php if ( have_posts() ) : while ( have_posts()) : the_post(); ?>
	<?php the_time('Y.m.d'); ?> <!-- 時間 -->
	<?php the_title(); ?>       <!-- タイトル -->
	<?php the_content(); ?>     <!-- 投稿内容 -->
	<?php the_permalink(); ?>   <!-- リンク -->
<?php endwhile ; endif ;?>
```

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

## 複数の条件（タクソノミーやタグ）を満たす投稿
```
<?php
	$args = array(
		'post_type'      => 'post',   
		'post_status'    => 'publish',
		'posts_per_page' => 4,
		'tax_query' => array(
			array(
				'taxonomy' => 'category',
				'field' => 'slug',
				'terms' => array(
					'news',
				),
			),
			array(
				'taxonomy' => 'post_tag',
				'field' => 'slug',
				'terms' => array(
					'development-camp',
				),
			),
			'relation' => 'AND'
		),
	);
	$the_query = new WP_Query( $args );
?>
```





<br> 

# 開発環境


## Directory
```
└ project/
	├ dev/
	│	├ dev_html/
	│	│	├ assets/
	│	│	├ _include
	│	│	│	├ functions.pug
	│	│	│	└ variable.pug
	│	│	└ hoge.pug
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


