# WordPress

## Directory
```
└ root/
	└ wp/
```

### サブディレクトリ 
WordPressは、サブディレクトリ上階層で表示する形を採用しています。  

### 方法
https://zenlogic.jp/support/knowledge/wordpress/install_directory.html


<br>

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


<br>

## 投稿の表示

### 基本
```php
<?php if ( have_posts() ) : while ( have_posts()) : the_post(); ?>
	<?php the_time('Y.m.d'); ?> <!-- 時間 -->
	<?php the_title(); ?>       <!-- タイトル -->
	<?php the_content(); ?>     <!-- 投稿内容 -->
	<?php the_permalink(); ?>   <!-- リンク -->
<?php endwhile ; endif ;?>
```

### トップページ、固定ページなど
```php
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
		echo '<p>現在投稿がありません。</p>';
	endif;
	wp_reset_postdata();
?>
```

### 複数の条件（タクソノミーやタグ）を満たす投稿
```php
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

### WebP
webpは、WordPressのプラグイン「EWWW Image Optimizer」などで生成されるように設定します。  
しかし、webpが生成される場合とされない場合があり、php側でファイルが存在するか否かを判定する必要がある。  
  
ファイルの存在するか否かの判定には、2種類方法があります。  
- themeファイルのみがある場合
- themeのファイルとディレクトリの二つが存在する場合
  
themeファイルのみの場合は、wpからの相対パスに変換して判定します。  
themeファイルとディレクトリの二つが存在する場合は、さらに相対パスに変換して判定します。  

#### variable.php
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

#### themeファイルのみがある場合
```php
/* ---------- thumbanil ---------- */
if( has_post_thumbnail() ){
	$image_id  = get_post_thumbnail_id();
	$image_url = wp_get_attachment_image_src($image_id,'564-348_thumbnail');
	$image_url = $image_url[0];

	// wpからのパスに変換
	$replace_url = str_replace( $wp_site_url , '', $image_url . '.webp' );

	// webpがあればsourceタグを入れる
	if( file_exists( $replace_url ) ){
		$static_image_url = str_replace( $domain_url , '', $image_url );
		$sourse = '<source type="image/webp" srcset="'. $static_image_url .'.webp">';
	} else{
		$sourse = '';
	}

	$image = '<img src="'. $image_url .'" alt="" class="c-objectfit -cover">';
} else{
	$sourse = '<source type="image/webp" srcset="'. $noimg_url_webp .'">';
	$image  = '<img src="'. $noimg_url_png .'" alt="" class="c-objectfit -cover">';
}
```

#### themeのファイルとディレクトリの二つが存在する場合
```php
/* ---------- thumbanil ---------- */
if( has_post_thumbnail() ){
	$image_id  = get_post_thumbnail_id();
	$image_url = wp_get_attachment_image_src($image_id,'544-336_thumbnail');
	$image_url = $image_url[0];

	// 現在のディレクトリからの相対パスに変換
	$replace_url_towp = str_replace( $wp_site_url , '', $image_url . '.webp' );
	$replace_url = $back_dir_towp . $replace_url_towp;

	// webpがあればsourceタグを入れる
	if( file_exists( $replace_url ) ){
		$static_image_url = str_replace( $domain_url , '', $image_url );
		$sourse = '<source type="image/webp" srcset="'. $static_image_url .'.webp">';
	} else{
		$sourse = '';
	}

	$image = '<img src="'. $image_url .'" alt="" class="c-objectfit -cover">';
} else{
	$sourse = '<source type="image/webp" srcset="'. $noimg_url_webp .'">';
	$image  = '<img src="'. $noimg_url_png .'" alt="" class="c-objectfit -cover">';
}
```


### snsシェア
```php
<ul class="p-article__share__list">
	<li class="p-article__share__facebook">
		<a href="http://www.facebook.com/share.php?u=<?php urlencode( the_permalink() );?>" target="_blank">
			<span>facebookでシェアする</span>
		</a>
	</li>
	<li class="p-article__share__twitter">
		<a href="http://twitter.com/share?url=<?php urlencode( the_permalink() );?>&amp;text=<?php the_title(); ?>" onclick="window.open(this.href, 'tweetwindow', 'width=550, height=450,personalbar=0,toolbar=0,scrollbars=1,resizable=1'); return false;" target="_blank">
			<span>ツイッターでシェアする</span>
		</a>
	</li>
	<li class="p-article__share__line">
		<a href="http://line.me/R/msg/text/?<?php the_title(); ?>%0D%0A<?php urlencode( the_permalink() );?>" target="_blank">
			<span>LINEに送る</span>
		</a>
	</li>
</ul>
```


<br>

## カスタム投稿、タクソノミー

```php
/* fuga（hoge）
---------------------------------------------------- */
add_action('init','register_custom_post_hoge');
function register_custom_post_hoge(){
	register_post_type(
		'hoge',
		array(
			'label'           => 'ホゲ',
			'public'          => true,
			'capability_type' => 'post',
			'menu_position'   => 5,
			'has_archive'     => true,
			'supports'        => array(
				'title',
				'author',
				'editor',
				'thumbnail',
				// 'custom-fields',
			),
			'rewrite' => array(
				'with_front' => false,
				// 'slug'       => 'works',
			)
		)
	);
	register_taxonomy(
		'hoge-category',
		'hoge',
		array(
			'hierarchical' => true,
			'label'        => 'カテゴリー',
			'query_var'    => true,
			'rewrite'      => true
		)
	);
}

```


<br>

## オプションページ
```php
/* ------------------------------------------------------------------------------
 Smart Custom Fields オプションページ
------------------------------------------------------------------------------ */
SCF::add_options_page('採用情報','採用情報','edit_posts','recruit-post');
```



<br>

## 管理画面カスタマイズ

### タグの読み込み

#### functions.php
```php
/* ------------------------------------------------------------------------------
 管理画面カスタマイズ
------------------------------------------------------------------------------ */
/* ---------------------------------------------------
 管理画面 タグ追加
-------------------------------------------------- */
function my_admin_tag() {
	echo '<link rel="stylesheet" type="text/css" href="'.get_home_url().'/assets/css/wp-admin.min.css">';
	echo '<script src="'.get_home_url().'/assets/js/wp-admin.min.js"></script>';
}
add_action('admin_print_scripts', 'my_admin_tag');
```


### 共通設定

#### wp-admin.js
```javascript
///////////////////////////////////////////////////////////////
// load
///////////////////////////////////////////////////////////////
window.addEventListener('load' , function(){
	document.body.classList.add('is-load');
});
```

#### wp-admin.scss
```scss
/* ------------------------------------------------------------
 is-load
------------------------------------------------------------ */
/*
 * 公開・更新ボタン、プレビューボタン、カテゴリーをloadするまでオフ
 */
body:not(.is-load){
	#publish,
	#post-preview,
	.categorychecklist{
		opacity: .2;
		pointer-events: none;
	}
}
```




### カテゴリーのラジオボタン変更

#### wp-admin.js
```javascript
///////////////////////////////////////////////////////////////
// DOMContentLoaded
///////////////////////////////////////////////////////////////
window.addEventListener('DOMContentLoaded',function(){
	/**
	 *
	 *
	 * カテゴリーのラジオボタン変更
	 *
	 *
	 */
	const category_checklist      = document.querySelectorAll('#categorychecklist [type="checkbox"]');
	const news_category_checklist = document.querySelectorAll('#news-categorychecklist [type="checkbox"]');
	const editinline              = document.querySelectorAll('.editinline');

	/*
	 * 詳細画面のチェックボタンをラジオボタンに
	 */
	function radio( _this ){
		for ( let i = 0; i < _this.length; i++ ) {
			_this[i].setAttribute('type','radio');
		}
	}
	radio( category_checklist );
	radio( news_category_checklist );

	/*
	 * クイック編集は、クリックされてからエディタ画面が生成されるので、
	 * 生成後 チェックボタンをラジオボタンにする
	 */
	for (var i = 0; i < editinline.length; i++) {
		editinline[i].addEventListener('click',function(e){
			e.preventDefault();
			let _this = this;
			setTimeout(function(){
				let post    = _this.parentNode.parentNode.parentNode.parentNode;
				let id      = post.getAttribute('id');
				let edit_id = id.replace( 'post' , 'edit' );
				let edit    = document.getElementById( edit_id );
				let checkbox = edit.querySelectorAll('.category-checklist [type="checkbox"],.news-category-checklist [type="checkbox"]');

				if( checkbox.length ){
					radio( checkbox );
				}
			});
		});
	}

});
```



### エンターで公開・更新されるのを防ぐ

#### wp-admin.js
```javascript
///////////////////////////////////////////////////////////////
// DOMContentLoaded
///////////////////////////////////////////////////////////////
window.addEventListener('DOMContentLoaded',function(){
	/**
	 *
	 *
	 * エンターで公開・更新されるのを防ぐ
	 *
	 *
	 */
	/*
	 * inputでエンターキーを押した際、公開をクリックした時と同じになってしまうので、
	 * 必須項目チェックが見落とされてしまう。
	 * 以下は、タイトルとsmart-custom-fieldsが入ったinputを対象とし、enterキーを無効にしています。
	 * ※textareaは改行があるため、制御の必要なし。
	 */
	const title_input = document.querySelectorAll('[name="post_title"]');
	const scf_input   = document.querySelectorAll('input[name^="smart-custom-fields"');

	function preventEnter(target){
		for ( let i = 0; i < target.length; i++ ) {
			target[i].addEventListener('keypress',function(e){
				if( e.keyCode === 13 ){
					e.preventDefault();
				}
			});
		}
	}

	preventEnter( title_input );
	preventEnter( scf_input );
});
```



### スマートカスタムフィールドのメモ欄が、タグに対応できるように変更
スマートカスタムフィールドのメモ欄で改行したい場合、`<br>`と入れてもエンコードされるため改行できません。  
それを回避するJavaScriptです

#### wp-admin.js
```javascript
///////////////////////////////////////////////////////////////
// DOMContentLoaded
///////////////////////////////////////////////////////////////
window.addEventListener('DOMContentLoaded',function(){
	/**
	 *
	 *
	 * SCFのメモ欄が、タグに対応できるように変更
	 *
	 *
	 */
	/*
	 * forEachで一文字一文字分解し、タグを判定
	 * < と > でタグが開始する仕様になっています。
	 */
	const scf_description = document.querySelectorAll('.description');

	for ( let i = 0; i < scf_description.length; i++ ) {
		const target = scf_description[i];

		let text = target.textContent;
		text     = text.replace(/\r?\n/g, '').replace(/\r?\t/g, '');
		target.innerHTML = '';

		let tag             = '';
		let tag_flg         = true;

		text.split('').forEach(function (c) {

			/* ---------- tag start ---------- */
			if( c === '<' ){
				tag_flg = false;
				tag     = '';
			}

			/* ---------- splitText ---------- */
			if( tag_flg === true ){
				target.insertAdjacentHTML( 'beforeend' , c );
			} else {
				tag += c;
			}

			/* ---------- tag end ---------- */
			if( c === '>' ){
				target.insertAdjacentHTML( 'beforeend' , tag );
				tag     = '';
				tag_flg = true;
			}
		});

	}
});
```



### スマートカスタムフィールド 必須
スマートカスタムフィールドには、必須機能がついていません。  
なので、JavaScriptを読み込ませ必須機能を実現します。

#### wp-admin.js
```javascript
///////////////////////////////////////////////////////////////
// DOMContentLoaded
///////////////////////////////////////////////////////////////
window.addEventListener('DOMContentLoaded',function(){
	/**
	 *
	 *
	 * 必須項目
	 *
	 *
	 */
	///////////////////////////////////////////////////////////////
	// checkRequired
	///////////////////////////////////////////////////////////////
	function checkRequired( target , name ){

		const targets = document.querySelectorAll(target);
		const tag     = targets[0].tagName;
		const type    = targets[0].getAttribute('type');
		let errorMessage = '';

		if( tag ==='INPUT' ){
			if( type === 'text' || type === 'hidden' ){
				/* ---------- text --------- */
				for ( let i = 0; i < targets.length; i++ ) {
					if( targets[i].value == '' || targets[i].value == '-1' ){
						errorMessage = '・' + name + '\n';
						break;
					} else{
						errorMessage = '';
					}
				}
			} else if( type === 'checkbox' || type === 'radio' ){
				/* ---------- checkbox || radio --------- */
				for ( let i = 0; i < targets.length; i++ ) {
					if( targets[i].checked == true ){
						errorMessage = '';
						break;
					} else{
						errorMessage = '・' + name + '\n';
					}
				}
			}
		} else if( tag === 'TEXTAREA' ){
			/* ---------- text --------- */
			for ( let i = 0; i < targets.length; i++ ) {
				if( targets[i].value == '' || targets[i].value == '-1' ){
					errorMessage = '・' + name + '\n';
					break;
				} else{
					errorMessage = '';
				}
			}
		} else if( tag === 'IMG' ){
			/* ---------- img --------- */
			for ( let i = 0; i < targets.length; i++ ) {
				if( targets[i] == null ){
					errorMessage = '・' + name + '\n';
					break;
				} else{
					if( targets[i].length < 1 ){
						errorMessage = '・' + name + '\n';
					} else{
						errorMessage = '';
					}
				}
			}
		}

		return errorMessage;
	}

	function requiredsCheck( e , requireds ){
		let errorMessage = '';

		// 判定によって必須項目の切り替え
		for ( let i = 0; i < requireds.length; i++ ) {
			if( requireds[i].judgment == null ){
				/* ---------- 条件なし ---------- */
				errorMessage += checkRequired( requireds[i].selector , requireds[i].name );
			} else{
				/* ---------- 条件あり ---------- */
				const targets = document.querySelectorAll( requireds[i].judgment[0] );
				const tag     = targets[0].tagName;
				const type    = targets[0].getAttribute('type');
				let value = '';

				if( tag === 'TEXTAREA' || type === 'value' ){
					value = targets[0].value;
					if( value === requireds[i].judgment[1] ){
						errorMessage += checkRequired( requireds[i].selector , requireds[i].name );
					}
				} else if( type === 'checkbox' || type === 'radio' ){
					for (var j = 0; j < targets.length; j++) {
						if( targets[j].checked == true ){
							value += targets[j].parentNode.innerHTML;
						}
					}

					if ( value.indexOf( requireds[i].judgment[1] ) != -1) {
						errorMessage += checkRequired( requireds[i].selector , requireds[i].name );
					}
				}

			}
		}

		if( errorMessage !== '' ){
			e.preventDefault();
			let alert_text = errorMessage + 'は必須項目です。';
			alert( alert_text );
		}
	}

	// ( ボタン , 必須項目{名前 , セレクタ , [条件,条件]} )
	function clickRequiredsCheck( button , requireds ){
		if( button ){
			button.addEventListener('click',function(e){
				requiredsCheck(e,requireds);
			});
		}
	}


	///////////////////////////////////////////////////////////////
	// post publish
	///////////////////////////////////////////////////////////////
	clickRequiredsCheck( document.querySelector('.post-type-post #publish') , [
		{
			'name'    : 'タイトル',
			'selector': '#title',
			'judgment': null,
		},
		{
			'name'    : 'カテゴリー',
			'selector': '.categorychecklist [name="post_category[]"]',
			'judgment': null,
		},
	] );

});
```







