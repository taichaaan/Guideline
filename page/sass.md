# Sass

[flocss](https://github.com/hiloki/flocss)をベースにカスタマイズしています。  


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
	│	├ library/
	│	└ variable/
	├ layout/
	├ object/
	│	├ component/
	│	│	├ form/
	│	│	├ icon/
	│	│	└ txt/	
	│	├ js/
	│	│	├ effect/
	│	│	└ ui/	
	│	├ scope/
	│	├ project/
	│	└ utility/
	├ page/
	│	└ _page-name.scss
	├ wp-admin.scss
	├ wp-editor.scss
	├ wp-login.scss
	├ page-ページ名.scss
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
	- vaiable -- CSS変数をファイル別で定義します。
- layout -- ページを構成するスタイルを定義します。
- object -- 繰り返し使用できるスタイルを定義します
	- component -- 再利用できるパターンとして、小さな単位のモジュールを定義します
	- scope -- classセレクタと要素セレクタの子孫セレクタでスタイルを格納するディレクトリ。ブログのエディターなどが該当します。
	- project -- 複数のcomponentからなる、もしくはsection単位などの大きな単位のモジュールを定義します。
	- utility -- わずかなスタイルの調整のための便利クラスなどを定義します。
- page -- objectには属さない、ページ固有のスタイルを定義します。


<br>

## common.scss
[gulp-sass-bulk-import](https://www.npmjs.com/package/gulp-sass-bulk-import)でディレクトリをインポートできるようにしています。  
ただ、ファイルの順番は指定できないので、`/foundation/base` のみ個別で指定しています。

```scss
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
 Object
------------------------------------------------------------ */
@import './object/component/**/*.scss';
@import './object/js/**/*.scss';
@import './object/wp/**/*.scss';
@import './object/project/**/*.scss';

/* ------------------------------------------------------------
 Layout
------------------------------------------------------------ */
@import './layout/**/*.scss';

/* ------------------------------------------------------------
 Page
------------------------------------------------------------ */
@import './page/**/*.scss';

/* ------------------------------------------------------------
 Object - utility
------------------------------------------------------------ */
@import './object/utility/**/*.scss';
```


<br>

## gulpの補完
ベンダープレフィックスや`@charset "UTF-8";`はgulpが補完してくれるため不要。  
なお、[autoprefixer](https://www.npmjs.com/package/gulp-autoprefixer)の基本設定は以下のようになっています。

```
.pipe( autoprefixer({
	grid: true,
	cascade: false,
	remove: true,
	overrideBrowserslist: [
		'> 1% in JP',
		'last 1 version',
		'Firefox ESR'
	]
}) )
```

[指定方法の参考](https://qiita.com/takeshisakuma/items/0bc1c39ee976bd1f52d7)



<br>

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
| .lp- | LP |
| .ua- | UserAgent |
| .js- | JavaScript |
| .wp- | WordPress |
| .is- | Status |


### Sample
```html
<div class="c-card c-card--new">
	<figure class="c-card__figure">
		<img src="" alt="">
	</figure>
	<div class="c-card__content">
		<h2 class="c-card__title">タイトルが入ります。</h2>
		<p class="c-card__time"><time>0000.00.00</time></p>
		<p class="c-card__txt">テキストテキストテキストテキスト</p>
		<p class="c-card__more">
			<a href="">MORE</a>
		</p>
	</div>
</div>
```


<br>

## シリーズを形成する場合
類似しているものは基本意味のある命名を推奨しますが、ときに名前の付け分けが難しい場合もあります。  
その場合は連番を付けて管理することも許容します。  
  
※1つ目のものには連番を付けません。

```scss
.c-txt-small{}
.c-txt-small2{}
```



<br>

## モジュールの省略
モジュールはクラスが長くなるので、ハイフンから始めて良いものとしています。

```html
<p class="c-button c-button--black">
	<!-- 通常 -->
</p>

<p class="c-button -black">
	<!-- これもOK -->
</p>
```
```scss
.c-button{
	&.-black{
		/* style */
	}
}
```

### -type-n
モジュールクラスは、`-black`や`-large`など  
基本意味のある命名を推奨しますが、ときに名前の付け分けが難しい場合もあります。  
その場合は連番を付けて管理することも許容します。  
その場合、`-type-`の後に連番を付けます。  
typeの場合シリーズとは違い、1つ目のタイプにも連番を付けます。  

```scss
.c-button{
	/* ---------- -type1 ---------- */
	&.-type1{
		/* style */
	}

	/* ---------- -type2 ---------- */
	&.-type2{
		/* style */
	}
}
```


<br>

## margin-top,bottomどちらを採用するか
余白を取るとき、marign-top,bottomどちらを使用するかは昔から議論されている課題です。  
本ガイドラインでは、基本的にtopを使用し、場合によってはbottomを使用するやり方を推奨しています。  
  
要素は基本的に上から詰まっていくため、margin-topを使用し、  
隣接する要素に関わらず余白が統一のものはmargin-bottomを使用します。  
例）ページタイトルやヘッダー、タイトルなど  
  
  
ここで問題なのが、フッターのmargin-topです。  
フッターのmargin-topが統一なら問題のないのですが、ページごとで余白が違う場合があります。  
その場合は、mainタグに「pg-ページ名」をつけ、mainタグのmargin-bottomで余白をつけます。  
  
メインタグ内の最後の要素で余白をつけても良いのですが、  
最後の要素がなくなった場合、再度余白をせっている必要があるため、  
メインタグで設定します。

  
※projectのページを構成するものは例外とします。
例）p-contactなど







<br>

## component、projectの判別について
https://qiita.com/uggds/items/d904b2f9a103c37a25fa


### component
componentでは、使い回しができるパーツを定義します。  
各サイトで あまり変わることはないです。  
例）ボタンやタイトル、段落、リスト、テーブル、ページャー、column、flex、gird、inner、content  など

```scss
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
```scss
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
```scss
.c-txts{
	> * {
		&:not(:last-of-type){
			margin-bottom: 30 / 16 + em;
		}
	}
}
.c-txt-small{
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


### project
projectでは、複数のcomponentからなる大きなブロックを定義します。  
複数のcomponentがなくても、フォームやブログの詳細記事など今後増える可能性があるものもprojectに含めます。  
また、大きすぎるパーツもprojectに含んで良いものとしています。  
各サイト固有のprojectが定義されます。  
例）form、article、サイト固有project


### utility
utilityでは、単一スタイルを定義します。  
余白に関するスタイルは、space.scssでmargin,paddingそれぞれで管理してください
省略する場合は、Emmentの記述などを参考にしてください。  
例）display、margin、padding、text-align  など

```scss
.u-bg-none  { background-color: rgba(0,0,0,0); }
.u-bg-white { background-color: #fff; }
```
```scss
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
```scss
.u-t-right   { text-align: right; }
.u-t-left    { text-align: left; }
.u-t-center  { text-align: center; }
.u-t-justify { text-align: justify; }
```
```scss
.u-font-normal  { font-weight: normal; }
.u-font-bold    { font-weight: bold; }
.u-font-lighter { font-weight: lighter; }
.u-font-bolder  { font-weight: bolder; }
.u-font-700     { font-weight: 700; }
```
```scss
.u-p-relative{ position: relative; }
.u-p-absolute{ position: absolute; }

.u-p-relative-0{ position: relative; z-index: 0; }
.u-p-relative-1{ position: relative; z-index: 1; }
.u-p-relative-2{ position: relative; z-index: 2; }
```


### page(旧名:theme)
objectは、繰り返し使用できるスタイルで、ページ固有のスタイルを定義する場所がないです。  
そのため、sassディレクトリ直下にpageディレクトリを追加し、そこをページ固有のスタイルを定義するディレクトリにします。  
CSSを分ける場合は、直下に`page-ページ名.scss`で定義します。  
プレフィックスは、`pg` です。  


