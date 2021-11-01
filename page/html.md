# HTML

## Comment
コメントアウトは、sectionなど大区分か ループする記述の可視性を上げる為、始めと終わりに記述してください。
```html
<!-- t-top-visual -->
<section class="t-top-visual">
</section>
<!-- /t-top-visual -->
```

<br>

## Template

共通部分はincludeディレクトリで管理し、各ファイルでrequireかincludeで読み込んでください。

<br>

## headタグ
headタグは、include/meta.php で共通管理しています。  
header.phpと名前がややこしくなるので、meta.phpという名前にしています。

```php
<?php
	$title       = removeUseless( $meta['title'] );
	$description = removeUseless( $meta['description'] );
	$keywords    = removeUseless( $meta['keywords'] );
 ?>
	<meta charset="UTF-8">
	<title><?= $title; ?></title>
	<meta http-equiv="x-ua-compatible" content="ie=edge">
	<meta name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=no">
	<meta name="format-detection" content="telephone=no">
	<meta name="robots" content="<?= $robots; ?>">
<?php if( $description ): ?>
	<meta name="description" content="<?= $description; ?>">
<?php endif; ?>
<?php if( $keywords ): ?>
	<meta name="keywords" content="<?= $keywords; ?>">
<?php endif; ?>
	<meta name="copyright" content="© <?= $author; ?>">
	<meta name="author" content="<?= $author; ?>">
	<meta name="theme-color" content="<?= $theme_color; ?>">
	<meta name="msapplication-TileColor" content="<?= $theme_color; ?>">
	<meta name="application-name" content="<?= $site_name; ?>">
	<meta name="apple-mobile-web-app-title" content="<?= $site_name; ?>">
	<meta name="thumbnail" content="<?= $ogp_url; ?>">
	<meta name="twitter:card" content="summary_large_image">
	<meta name="twitter:title" content="<?= $title;?>">
<?php if( $description ): ?>
	<meta name="twitter:description" content="<?= $description; ?>">
<?php endif; ?>
	<meta name="twitter:image:src" content="<?= $ogp_url; ?>">
<?php if( $web_url == $home_url ): ?>
	<meta property="og:type" content="website">
<?php else: ?>
	<meta property="og:type" content="article">
<?php endif; ?>
	<meta property="og:site_name" content="<?= $site_name; ?>">
	<meta property="og:title" content="<?= $title;?>">
<?php if( $description ): ?>
	<meta property="og:description" content="<?= $description; ?>">
<?php endif; ?>
	<meta property="og:url" content="<?= $url; ?>">
	<meta property="og:image" content="<?= $ogp_url; ?>">
	<meta property="og:locale" content="ja_JP">
	<link rel="dns-prefetch" href="//typesquare.com">
	<link rel="dns-prefetch" href="//webfont.fontplus.jp">
	<link rel="dns-prefetch" href="//fonts.googleapis.com">
	<link rel="dns-prefetch" href="//www.google-analytics.com">
	<link rel="preload" href="<?= $home_url; ?>assets/css/common.min.css<?= $cashDate; ?>" as="style">
	<link rel="preload" href="<?= $home_url; ?>assets/js/library.js<?= $cashDate; ?>" as="script">
	<link rel="preload" href="<?= $home_url; ?>assets/js/module.min.js<?= $cashDate; ?>" as="script">
	<link rel="preload" href="<?= $home_url; ?>assets/img/common/loading.svg" as="image">
<?php outputPreload( $preload ); ?>
	<link rel="index" href="<?= $top_url; ?>">
<?php if( !is_404() ): ?>
	<link rel="canonical" href="<?= $url; ?>">
<?php endif; ?>
	<link rel="contents" href="<?= $top_url; ?>sitemap.xml" title="サイトマップ">
	<link rel="icon" type="image/svg+xml" href="<?= $home_url; ?>assets/img/meta/favicon.svg">
	<link rel="icon" type="image/png" href="<?= $home_url; ?>assets/img/meta/icon-512x512.png">
	<link rel="apple-touch-icon" href="<?= $home_url; ?>assets/img/meta/apple-touch-icon.png">
	<!-- googlefont -->
	<link rel="stylesheet" href="<?= $home_url; ?>assets/css/common.min.css<?= $cashDate; ?>">
<?php outputStyle( $style ); ?>
	<!-- fontplus -->
	<!-- typesquare -->
	<script src="<?= $home_url; ?>assets/js/jquery.min.js"></script>
	<script src="<?= $home_url; ?>assets/js/library.js<?= $cashDate; ?>" defer></script>
	<script src="<?= $home_url; ?>assets/js/module.min.js<?= $cashDate; ?>" defer></script>
	<script src="<?= $home_url; ?>assets/js/common.min.js<?= $cashDate; ?>" defer></script>
<?php outputScript( $script ); ?>
<?php outputJsonld( $directory , $title , $description , $pageJsonld ); ?>
	<!-- Google Analytics -->
<?php if( $test_mode == true ): ?>
	<meta name="robots" content="noindex,nofollow">
<?php endif; ?>
```
<br>

## favicon
faviconはfavicon.ico,favicon.svg,apple-touch-icon.pngの3種類のみの準備とする。  
サイズは180×180とする

<br>

## headerタグ
headerタグは、ページのヘッダー以外にも、  
ページタイトル部分や各セクションのヘッダー、シングルページの記事(article)のヘッダーにも使えそうな時は使用してください。  
各セクションでは、main直下レベルのセクションは有りとし、かなり潜った子要素では使わない。

<br>

## navタグ
https://developer.mozilla.org/ja/docs/Web/HTML/Element/nav

<br>

## addressタグ
https://developer.mozilla.org/ja/docs/Web/HTML/Element/address

<br>

## aタグ
https://edge.sincar.jp/web/target_blank-security/
```html
<a href="" target="_blank" rel="noopener"></a>
```

<br>

## WebP
https://rendan.jp/note/2020-10-24-17/

### 例） PCとスマホで振り分け
```html
<picture>
	<source type="image/webp" srcset="./assets/img/top/visual_1-pc.webp" media="(min-width:769px)">
	<source type="image/webp" srcset="./assets/img/top/visual_1-sp.webp" media="(max-width:768px)">
	<source srcset="./assets/img/top/visual_1-pc.jpg" media="(min-width:769px)">
	<source srcset="./assets/img/top/visual_1-sp.jpg" media="(max-width:768px)">
	<img src="./assets/img/top/visual_1-pc.jpg" alt="" class="c-objectfit -cover">
</picture>
```


## WAI-ARIA
https://accessible-usable.net/2015/07/entry_150701.html
