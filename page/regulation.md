# レギュレーション

文字エンコーディング：UTF-8  
インデント：タブスペース１つ（半角スペース4個分） ※スペースと混在させない


<br>

## is-hover

スマートフォンやタブレット等のタッチデバイスでは、  
デバイスによってはhoverが原因で二度タップしないとリンク先に飛べなかったりするのでオフにしたいと思い、  
JavaScriptでPCのみaタグなどに `is-hover` が付与されるようにしています。  
  
そろそろ[hoverメディアクエリ](https://developer.mozilla.org/ja/docs/Web/CSS/@media/hover)に移行しようと思っていますが、  
今は一旦JavaScript判定にしています。

```
a{
	&.is-hover:hover{
		opacity: .6;
	}
}
```


<br>

## $home_url;

Webサイトの階層が変わっても、柔軟に対応できるように  
以下のように `variable.php` で `$home_url` を定義しています。  

画像やリンクなどurlを使用するものでは、基本的に `$home_url` を使用してください。  

※CSSなどは相対パスでOK.


```php
///////////////////////////////////////////////////////////////
// variable
///////////////////////////////////////////////////////////////
$domain      = $_SERVER["HTTP_HOST"];
$web_root    = $_SERVER['DOCUMENT_ROOT'];
$web_url     = $_SERVER['REQUEST_URI'];
$web_url     = preg_replace( '/\?.+$/', '', $web_url );
$url         = (empty($_SERVER["HTTPS"]) ? "http://" : "https://") . $domain . $web_url;
$url         = preg_replace( '/\?.+$/', '', $url );
$current_dir = basename(dirname($_SERVER['SCRIPT_NAME']));
$ua          = strtolower($_SERVER['HTTP_USER_AGENT']);


// $home_url = '/';
$home_url    = '/tpl-php/public_html/';
$domain_url  = (empty($_SERVER["HTTPS"]) ? "http://" : "https://") . $domain;
$root_url    = $domain_url . '/';
$top_url     = (empty($_SERVER["HTTPS"]) ? "http://" : "https://") . $domain . $home_url;
$wp_site_url = $top_url . 'wp/';


// 現在のURLからwpまでの階層を配列で取得
$static_alldir = str_replace( $wp_site_url , '' , $url );
$static_alldir = str_replace( 'index.html' ,'' , $static_alldir );
$static_alldir = str_replace( 'index.php' ,'' , $static_alldir );

$dir_list = rtrim( $static_alldir , '/' );
$dir_list = explode( '/' , $dir_list );
$dir_list = array_filter( $dir_list );

// 現在のURLからwpまでの階層を[../]の形式で取得
$back_dir_towp = '';
foreach ( $dir_list as $value ) {
	$back_dir_towp .= '../';
}
```

```php
<nav class="l-nav-main">
	<ul>
		<li>
			<a href="<?= $home_url; ?>hoge/">
				<span class="c-arrow-circle -small"></span>
				<span class="l-nav-main__text">hoge</span>
			</a>
		</li>
		<li>
			<a href="<?= $home_url; ?>fuga/">
				<span class="c-arrow-circle -small"></span>
				<span class="l-nav-main__text">fuga</span>
			</a>
		</li>
		<li>
			<a href="<?= $home_url; ?>piyo/">
				<span class="c-arrow-circle -small"></span>
				<span class="l-nav-main__text">piyo</span>
			</a>
		</li>
	</ul>
	<div>
		<img src="<?= $home_url; ?>assets/img/common/hoge.svg" alt="hoge">
	</div>
</nav>
```

```css
.hoge{
	background-image: url('../img/common/hoge.svg');
}
```
