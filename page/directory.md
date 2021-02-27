# ディレクトリ構成

```
root/
	├ include/
	│	├ functions.php
	│	├ variable.php
	│	├ meta.php
	│	├ loading.php
	│	├ preload-svg.php
	│	├ header.php
	│	├ footer.php
	│	└ aside.php
	├ assets/
	│	├ img/
	│	│	├ common/
	│	│	│	├ banner/
	│	│	│	├ icon/
	│	│	│	├ object/
	│	│	│	└ title/
	│	│	├ meta/
	│	│	│	├ favicon.ico
	│	│	│	├ favicon.png
	│	│	│	├ favicon.svg
	│	│	│	├ apple-touch-icon.png
	│	│	│	└ ogp.png
	│	│	└ ページ名/
	│	├ svg/
	│	├ css/
	│	│	├ common.css
	│	│	├ page-ページ名.css
	│	│	├ wp-admin.css
	│	│	├ wp-editor.css
	│	│	└ wp-login.css
	│	├ js/
	│	│	├ library.js
	│	│	├ module.js
	│	│	├ common.js
	│	│	├ page-ページ名.js
	│	│	├ component-コンポーネント名.js
	│	│	└ wp-admin.js 
	│	├ font/
	│	│	└ フォント名/
	│	├ video/
	│	└ pdf/
	├ wp/
	├ ページ名/
	├ 401.php
	├ 404.php
	├ favicon.ico
	└ index.php
```


## Include
各ページで読み込ませる共通パーツを格納するディレクトリです。
- variable.php -- 変数を記述するファイル。wp-loadもここでこなっています。
- functions.php -- 関数を記述するファイル
- meta.php -- headタグ内のファイル。headはheader.phpと名前が似ているため、meta.phpにしています。

※上記以外は、パーツごとにファイルを作成。


## Assets
- img -- imgタグで出力する画像を格納。common,meta以外は、ページ名でディレクトリを作る。
- svg -- インラインで仕様するsvgを格納
- css -- CSSを格納
- js -- JavaScriptを格納
- font -- フォントをディレクトリ単位で格納
- video -- videoを格納。ページ単体のものはディレクトリ名で分ける。そうでなければ全て直下に配置する。
- pdf -- PDFを格納


## Img
- common -- 共通ファイルを格納。「object」「icon」などある一定数以上のパーツがある場合は、ディレクトリを作っても良いものとする。  
- meta -- （meta.phpと連動して）meta.phpファイル内で使用する画像は、metaディレクトリに格納。

※common,meta以外は、ページ名でディレクトリを作る。　　


## CSS
- common.css -- ページ共通のcssファイル
- page-ページ名.css --  ページ固有のcssファイル
- wp-admin.css --  WordPressの全ユーザの管理画面用cssファイル
- wp-editor.css --  WordPressの編集者の管理画面用cssファイル
- wp-login.css --  WordPressのログイン画面用cssファイル

※ファイルに圧縮をかけている場合は、「.min」の形にする。　　
※pageが少ない場合は、commonと合わせても問題ない。　　
※style.cssは、どこのスタイルか解らず抽象的なため廃止し、common（共通）にしています。


## JavaScript
- library.js -- 外部ライブラリを集めたJavaScriptファイル（圧縮なし）
- module.js -- RENDANプラグインを集めたJavaScriptファイル
- common.js -- ページ共通のJavaScriptファイル
- page-ページ名.js -- ページ固有のJavaScriptファイル
- component-コンポーネント名.js -- フォームなど部品のJavaScriptファイル
- wp-admin.js  -- WordPressの全ユーザの管理画面用JavaScriptファイル

※ファイルに圧縮をかけている場合は、「.min」の形にする。　
※pageが少ない場合は、commonと合わせても問題ない  
※script.jsは、どこのscriptか解らず抽象的なため廃止し、common（共通）にしています。

