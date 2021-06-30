# コメントアウト
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

<br>

# 命名規則
## 基本
- 半角英数字のみを使用
- 全角スペース、半角スペースは使用しない

### 参考
- [CSSのクラス名を決めるときに使うリストをつくりました](https://qiita.com/manabuyasuda/items/dbb76ed36970bec95470)
- [【クラス命名に迷わない】HTML、CSSのクラス名を決めるための自分用メモ](https://qiita.com/kei_1011/items/8f5c6393dbb652280d2d)
- [プログラミングでよく使う英単語のまとめ](https://qiita.com/Ted-HM/items/7dde25dcffae4cdc7923#%E5%8D%98%E4%BD%8D)

## 略語
検索で、「英単語 略」で検索して存在する場合は使用して良いものとする。  
自分しか分からないような略後は使用しない。  

```
// 例
Attention → attn
Reservation → rsv
```
 
## 画像名
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

## ディレクトリ名
単語間はハイフンを使用してください。  
```
// 例
/about/
/portfolio-item/
```

## jsファイル名
キャメルケースを使用してください。  
```
// 例
objectFit.js
isCurrent.js
smoothScroll.js
``` 
 
## 変数名 [JavaScript,php]
キャメルケースまたはスネークケースを使用してください。 
```
// 例
const snakeRoad  = 'hoge';
const snake_road = 'hoge';
```
 
## 関数名 [JavaScript,PHP]
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
| is | 期待する状態になっているか |

https://murashun.jp/blog/20181109-01.html

## [WordPress](./wordpress.md)
WordPressの投稿タイプ名にハイフンを使用すると問題を引き起こす可能性があるので、アンダースコアを使用してください。  
ただ、ディレクトリ名はGoogleがハイフンを推奨しているため、rewriteでスラッグをハイフンに変更してください。  
  
タクソノミー、タームはハイフンを使用してください。  

<br>


## HTML
タグ込みのサンプルです。参考程度に。

### basic
```html
<div class="l-wrapper">
	<header class="l-header -type1">
		<div class="l-header__inner">
			<h1 class="l-header__logo"></h1>
			<nav class="l-nav">
				<ul class="l-nav__main">
					<li class="l-nav__main__parent">
						<a href="">私たちについて</a>
					</li>
					<li class="l-nav__toggle">
						<div class="l-nav__main__parent">
							<a href="">会社概要</a>
							<div class="l-nav__toggle__icon"></div>
						</div>
						<div class="l-nav__main__children">
							<ul>
								<li></li>
							</ul>
						</div>
					</li>
				</ul>
			</nav>
		</div>
		<nav class="l-sitemap">
			<div class="l-sitemap__inner">
				<ul class="l-sitemap__main"></ul>
				<ul class="l-sitemap__sub"></ul>
			</div>
		</nav>
		<button class="l-button" aria-label="メインメニューの切替">
			<span></span>
			<span></span>
		</button>
	</header>
	<main class="l-main">
		<!-- p-hero -->
		<header class="p-hero">
			<div class="p-hero__title">
				<h1 class="p-hero__title__ja"></h1>
				<p class="p-hero__title__en"></p>
			</div>
			<ol class="c-breadcrumb">
				<li></li>
			</ol>
			<div class="p-hero__bg">
				<picture>
					<source type="image/webp" srcset="/assets/img/hoge/hero.webp">
					<img src="/assets/img/hoge/hero.jpg" alt="" class="c-objectfit -cover">
				</picture>
			</div>
		</header>
		<!-- /p-hero -->
		<!-- p-hero -->
		<header class="p-hero">
			<div class="p-hero__contents">
				<div class="p-hero__title">
					<h1 class="p-hero__title__ja"></h1>
					<p class="p-hero__title__en"></p>
				</div>
				<ol class="c-breadcrumb">
					<li></li>
				</ol>
			</div>
			<div class="p-hero__visual">
				<picture>
					<source type="image/webp" srcset="/assets/img/hoge/hero.webp">
					<img src="/assets/img/hoge/hero.jpg" alt="" class="c-objectfit -cover">
				</picture>
			</div>
		</header>
		<!-- /p-hero -->
		<!-- l-container -->
		<div class="l-container">
			<!-- p-localnav -->
			<nav class="p-localnav">
				<h2 class="p-localnav__title"></h2>
				<ul class="p-localnav__list"></ul>
			</nav>
			<!-- /p-localnav -->
		</div>
		<!-- /l-container -->
	</main>
	<aside class="l-aside"></aside>
	<footer class="l-footer">
		<div class="l-footer__inner">
			<div class="l-footer__top">
				<div class="l-footer__profile">
					<address class="l-footer__profile__info">
						<p class="l-footer__profile__logo"></p>
						<ul class="l-footer__profile__address"></ul>
					</address>
				</div>
				<nav class="l-footer__nav">
					<ul class="l-footer__nav__main">
						<li class="l-footer__nav__main__parent">
							<a href=""></a>
						</li>
						<li class="l-footer__nav__main__toggle js-toggle">
							<p class="l-footer__nav__main__parent">
								<a href="">会社概要</a>
								<div class="l-footer__nav__main__toggle__icon"></div>
							</p>
							<div class="js-toggle__content">
								<ul class="l-footer__nav__main__children"></ul>
							</div>
						</li>
					</ul>
					<ul class="l-footer__nav__sub">
						<li></li>
					</ul>
				</nav>
				<div class="l-footer__sns"></div>
				<div class="l-footer__detail"></div>
			</div>
			<div class="l-footer__bottom">
				<div class="l-footer__other"></div>
				<p class="k-footer__copyright">
					<small>&copy;</small>
				</p>
				<div class="l-footer__gotop">
					<a href="#document-top"></a>
				</div>
			</div>
		</div>
	</footer>
</div>
```

### derivation
```html
<!-- l-container -->
<div class="l-container">
	<!-- pg-hoge-intro -->
	<section class="pg-hoge-intro">
		<div class="pg-hoge-intro__inner c-inner">
			<h2 class="pg-hoge-intro__slogan"></h2>
			<h3 class="pg-hoge-intro__catch"></h3>
			<p class="c-txt -crop"></p>
			<div class="pg-hoge-intro__flex">
				<div class="pg-hoge-intro__contents"></div>
				<figure class="pg-hoge-intro__figure"></figure>
			</div>
		</div>
	</section>
	<!-- /pg-hoge-intro -->
	<!-- pg-hoge-fuga -->
	<section class="pg-hoge-fuga">
		<div class="pg-hoge-fuga__inner c-inner">
			<header class="pg-hoge-fuga__header">
				<h2></h2>
			</header>
			<section class="pg-hoge-fuga__item">
				<header>
					<h3></h3>
				</header>
			</section>
			<section class="pg-hoge-fuga__item"></section>
			<section class="pg-hoge-fuga__item"></section>
		</div>
	</section>
	<!-- /pg-hoge-fuga -->
	<!-- pg-hoge-piyo -->
	<section class="pg-hoge-piyo">
		<div class="pg-hoge-piyo__inner c-inner">
			<header class="pg-hoge-piyo__header">
				<h2></h2>
			</header>
			<div class="c-column">
				<div class="pg-hoge-piyo__cell" data-category="hoge"></div>
			</div>
		</div>
	</section>
	<!-- /pg-hoge-piyo -->
	<!-- pg-hoge-outro -->
	<section class="pg-hoge-outro">
	</section>
	<!-- /pg-hoge-outro -->
</div>
<!-- /l-container -->
```

### archive
```html
<aside class="p-sidebar">
	<div class="p-sidebar__cell">
		<header class="p-sidebar__title">
			<h2 class="p-sidebar__title__ja"></h2>
		</header>
		<nav class="p-sidebar__nav">
			<ul>
				<li></li>
			</ul>
		</nav>
	</div>
</aside>
<div class="c-inner">
	<!-- c-column -->
	<ul class="c-column-gap-nn -col-n -row-g-nn">
		<li class="p-card">
			<a href="">
				<p class="p-card__new"></p>
				<figure class="p-card__figure"></figure>
				<p class="p-card__category" data-category="hoge"></p>
				<h2 class="p-card__title"></h2>
			</a>
		</li>
	</ul>
	<!-- /c-column -->
</div>
<!-- p-pagination -->
<footer class="p-pagination">
	<ul class="p-pagination__number">
		<li></li>
		<li></li>
	</ul>
</footer>
<!-- /p-pagination -->
```

### single
```html
<!-- p-article -->
<article class="p-article">
	<header class="p-article__header">
		<div class="p-article__header__meta">
			<p class="p-article__header__time">
				<time></time>
			</p>
			<p class="p-article__header__category"></p>
		</div>
		<h1 class="p-article__header__title"></h1>
	</header>
	<div class="p-article__body">
		<div class="p-article__contents">
		</div>
		<footer class="p-article__footer">
			<div class="p-article__footer__info">
				<p class="p-article__footer__title"></p>
			</div>
			<div class="p-article__footer__share">
				<h2 class="p-article__footer__share__title"></h2>
				<ul class="p-article__footer__share__list"></ul>
			</div>
		</footer>
	</div>
</article>
<!-- /p-article -->
<!-- p-article-relate -->
<aside class="p-article-relate">
</aside>
<!-- /p-article-relate -->
```
