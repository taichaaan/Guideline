# JavaScript

jQueryは基本的に使用していません。  
プラグインなどで仕方がない場合のみ使用してください。  

また、今までscript.jsにまとめていましたが、  
読み込み速度や今後の管理を考慮して、意味合い・種類別に分割することにしました。  

<br>

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
- module -- RENDAN独自プラグインを格納するディレクトリ。今まではscript.min.jsとしていましたが、区別するために分けました。Gulpで結合してmodule.min.jsとして圧縮して出力します
- common.js -- 全ページ共通のScriptなどを記述します。sassのobjectディレクトリに関するものは、処理が少なければcommon.jsに記述しても良いです。
- page-ページ名.min.js -- ページ固有のScriptを記述します。
- component-コンポーネント名.min.js -- 複数のページで使用するが、処理が多いものなどを記述するファイルです。フォームやスライダーなどが該当します。

themeやcomponentを分けた理由は、ページ数が多いサイトだとscript.min.jsがどうしても多くなるところが気になっていたからです。  
LPや小規模のサイトでは、pageやtheme、componentはcommon.jsに記述して良いです。

<br>

## Plugin
### よく使用する外部プラグイン
- [gsap](https://greensock.com/)
- [imagesLoaded](https://imagesloaded.desandro.com/)
- [Polyfill sticky](https://github.com/wilddeer/stickyfill)

<br>

## Module
module.min.jsでは、RENDAN独自プラグインを圧縮して出力しています。  
また、独自プラグイン以外にも base.js（jsの諸々設定）もmodule.min.jsに含めています。

### よく使用する独自プラグイン
- [js-useragent](https://github.com/taichaaan/js-useragent/)
- [js-smoothScroll](https://github.com/taichaaan/js-smoothScroll/)
- [js-popup](https://github.com/taichaaan/js-popup/)
- [js-objectFit](https://github.com/taichaaan/js-objectFit/)
- [js-lazyload](https://github.com/taichaaan/js-lazyload/)

<br>

## 未対応ブラウザへの配慮

- [webp](https://caniuse.com/?search=webp)と[picture](https://caniuse.com/?search=picture)タグ、[object-fit](https://caniuse.com/?search=object-fit)
- [object-fit](https://caniuse.com/?search=object-fit)とlazyload

上記のような未対応ブラウザがあるプロパティやタグを掛け合わせる時が多々あり、JavaScriptで対応します。  
有名どころで、[ofi.js](https://github.com/fregante/object-fit-images)や[picturefill.js](http://scottjehl.github.io/picturefill/)などがありますが、  
先程のような掛け合わせの場合、JS同士がバッティングしてしまい、崩れてします。  
  
なので、RENDANオリジナルプラグインを作りました。  
それぞれ、object-fitやpictureタグ、未対応ブラウザか否かを考慮した作りになっています。  

- [object-fit](https://github.com/taichaaan/js-objectFit)
- [picture](https://github.com/taichaaan/js-picture)
- [lazyload](https://github.com/taichaaan/js-lazyload)



<br>

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
