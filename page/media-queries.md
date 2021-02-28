# 可変



# ブレイクポイント
## Breakpoint

| type | range |
----|---- 
| pc | 1024px ~ |
| tablet | 561px ~ 1023px |
| smartphone | ~ 560px |

ブレイクポイントは、sassのmixinで管理しています。  
上記の範囲はあくまで参考程度で、768pxや1000pxなど 状況に応じて変更してください。

```
$breakpoint-up-width: (
	'xxxs': '(min-width: 321px)',
	'xxs' : '(min-width: 376px)',
	'xs'  : '(min-width: 415px)',
	'sm'  : '(min-width: 561px)',
	'md'  : '(min-width: 769px)',
	'lg'  : '(min-width: 1024px)',
	'xl'  : '(min-width: 1281px)',
	'xxl' : '(min-width: 1361px)',
	'xxxl': '(min-width: 1681px)',
	'fhd' : '(min-width: 1921px)',
	'2K'  : '(min-width: 2048px)',
	'wqhd': '(min-width: 2561px)',
) !default;
```
```
$breakpoint-down-width: (
	'xxxs': '(max-width: 320px)',
	'xxs' : '(max-width: 375px)',
	'xs'  : '(max-width: 414px)',
	'sm'  : '(max-width: 560px)',
	'md'  : '(max-width: 768px)',
	'lg'  : '(max-width: 1023px)',
	'xl'  : '(max-width: 1280px)',
	'xxl' : '(max-width: 1360px)',
	'xxxl': '(max-width: 1680px)',
	'fhd' : '(max-width: 1920px)',
	'2K'  : '(max-width: 2048px)',
	'wqhd': '(max-width: 2560px)',
) !default;
```
```sass
//
//
// mediaquery.scss
//
//

//
// overview : メディアクエリの管理
//            引数にはvariableディレクトリのbreakpointから選び、freeの場合は自由に入れる。
// reference: https://www.tam-tam.co.jp/tipsnote/html_css/post10708.html
//


///////////////////////////////////////////////////////////////
// min-width
///////////////////////////////////////////////////////////////
@mixin mq-up( $breakpoint: lg ) {
	@media screen and #{map-get($breakpoint-up-width, $breakpoint)} {
		@content;
	}
}

@mixin mq-up-free( $breakpoint ) {
	@media screen and ( min-width: $breakpoint ) {
		@content;
	}
}


///////////////////////////////////////////////////////////////
// max-width
///////////////////////////////////////////////////////////////
@mixin mq-down( $breakpoint: lg ) {
	@media screen and #{map-get($breakpoint-down-width, $breakpoint)} {
		@content;
	}
}

@mixin mq-down-free( $breakpoint ) {
	@media screen and ( max-width: $breakpoint ){
		@content;
	}
}


///////////////////////////////////////////////////////////////
// min-width and max-width
///////////////////////////////////////////////////////////////
@mixin mq-updown( $breakpoint-up: lg , $breakpoint-down: sm ) {
	@media screen and #{map-get($breakpoint-down-width, $breakpoint-up)} and #{map-get($breakpoint-up-width, $breakpoint-down)} {
		@content;
	}
}

@mixin mq-updown-free( $breakpoint-up:1023px, $breakpoint-down:561px) {
	@media screen and ( max-width: $breakpoint-up ) and ( min-width: $breakpoint-down ) {
		@content;
	}
}
```

