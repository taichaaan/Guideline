# 可変

## rem
remは、「root em」の略で、ルートのフォントサイズを1として考える単位です。  
1remが10pxと同じサイズとして扱えるようにするため、`html {font-size:62.5%;} `を指定します。  
  
ただ、htmlのフォントサイズが常に62.5%だと、  
remで相対的に指定しても pxで直接指定しているのと変わりません。  
そこで、レイアウトが崩れそうになる下記ブラウザ幅では62.5%ではなくvwを使用します。  
vwにするとremの部分は相対的に変化するため、remの部分もブラウザ幅に合わせて縮小されます。  
  
<br>

- 1280px 〜 1024px  
- 375px 〜

ただ、htmlのフォントサイズにvwを使うデメリットが2つあります。  
  
## デメリット1
一つ目は、文字が極端に小さくなったりすることです。  
その場合はcssの[max関数](https://developer.mozilla.org/ja/docs/Web/CSS/max())を使用し回避します。  
  
フォントサイズが8.0remなど大きい場合はそのままでも良いですが、  
1.3remなど小さいものは、`max()`を使用し最小値を設けた方が良いです。
  
### max関数
```css
.hoge{
	font-size: 1.3rem;
	font-size: max(1.3rem ,12px);
}
```

`max()` 関数は、引数としてカンマで区切った1つ以上の式を取り、  
もっとも大きい (最も正である) 式の値をプロパティに割り当てられた値として使用します。  
最大値のrem、そして最小値のpxを指定します。  
`max()` 関数 未対応ブラウザに対しては、最初に「rem」でフォントサイズ定義し、次に「rem」で再び定義し上書きする方法をとります。  
  
### sass
sassではmixinを使用しています。  
```sass
///////////////////////////////////////////////////////////////
// font-min
///////////////////////////////////////////////////////////////
//
// overview: htmlのフォントサイズが62.5%ではなくvwの幅があった場合に使用する。
//           cssのmin関数を使用し、基本はremで可変するものの、最小値をpxで指定して それ以下にならないようにする。
//           第一引数は最大値を入れ、第二引数には最小値を入れる。
// usage   : @include font-min(13,12) // 1.3remと12pxの中で可変する
//
@mixin font-min( $max-size,$min-size ){
	// font-size: #{$max-size}px;
	font-size: #{$max-size / 10}rem;
	font-size: unquote(' max( #{$max-size / 10}rem , #{$min-size}px ) ');
}

.hoge{
	@include font-min(14,12)
}
```

## デメリット2
2つ目のデメリットは、あるブラウザでtransformと併用すると一部欠けたりする場合があります。  
その際は、transformに rotate(0.00001deg)などを適用すると解消します。  

※2020年11月ごろから行っているやり方です。



<br>

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

