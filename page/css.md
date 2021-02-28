# CSS

## ファイル構成
cssを圧縮せず納品する場合、その後の管理がしやすいように ファイルを分割してください。  
ファイル分割の場合、flocssのuaをディレクトリで分ける概念は廃止してください。  
下記の順番でheadタグ内に記述してください。  

- base.css -- flocssのFoundationを記述するファイル
- layout.css -- flocssのLayoutを記述するファイル
- common.css -- flocssのObjectを記述するファイル
- page-pagename.css -- flocssのPageを記述するファイル
- theme-color.css -- flocssのThemeを記述するファイル

※ base,layout,commonをまとめてcommon.cssにする場合もあり。

<br>

## 命名規則
cssファイルでコーディングをする場合、命名規則は基本的にBEMにしています。  
sassをコンパイルする場合は、命名規則はflocssでも有としますが、ファイル構成は必ず守ってください。  
BEMの場合、class名を見ただけで種類（レイアウト・共通・ページ）が理解できるように、頭には commonやlayout,ページ名を入れてください。  
flocssとほぼ同じなので、詳しくは<a href="#flocss">flocss</a>を参照ください。


### Sample
```html
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

<br>

## よく使うCSS

```css
:nth-of-type(X)  /* X番目 */
:nth-of-type(n+X)  /* X番目以降 */
:not(:first-of-type)  /* 最初以外 */
:not(:last-of-type)  /* 最後以外 */
:nth-last-of-type(n+X)  /* 最後からX番目以前 */
```

- [何番目系の便利なCSSまとめ](https://qiita.com/ituki_b/items/62a752389385de7ba4a2)
- [1万人に聞いた、2019年の最新CSS使用状況](https://qiita.com/rana_kualu/items/6d967b4d4cd4fc59d7e2)
  

