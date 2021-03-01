# 開発環境


## Directory
```
└ project/
	├ dev/
	│	├ dev_html/
	│	│	├ assets/
	│	│	│	├ img/
	│	│	│	├ svg/
	│	│	│	├ sass/
	│	│	│	├ js/
	│	│	│	│	├ library/
	│	│	│	│	├ module/
	│	│	│	│	├ common.js
	│	│	│	│	├ page-ページ名.js
	│	│	│	│	├ component-コンポーネント名.js
	│	│	│	│	└ wp-admin.js 
	│	│	│	├ font/
	│	│	│	│	└ フォント名/
	│	│	│	├ video/
	│	│	│	└ pdf/	
	│	│	├ _include
	│	│	│	├ functions.pug
	│	│	│	└ variable.pug
	│	│	└ hoge.pug
	│	└ gulp/
	│		├ gulpfile.js
	│		├ package.json
	│		├ package-lock.json
	│		└ node_modules/
	└ public_html/
```

- dev -- 開発ディレクトリ。ここにpugやsass、圧縮前の画像を入れます。
- public_html -- 出力ディレクトリ。sassやpugなどdevディレクトリの内容がコンパイルされる仕組み。このディレクトリごとサーバーにアップする。


<br>

## Gulp
[Gulp](https://gulpjs.com/)を使用してコンパイルや画像の圧縮を行っています。  
詳しくはgulpfile.jsを見てください。  

- pugのコンパイル、圧縮
- sassのコンパイル、結合、圧縮
- JavaScriptの結合、圧縮
- 画像、svgの圧縮
- webp生成
- 上記以外のファイルの移動


### バージョン
gulpのバージョンは適宜アップしています。  

#### node
v14.14.0

#### gulp
v4.0.2

※2021年2月28日現在 


### 汎用コマンド
#### ターミナルで特定フォルダに移動するコマンド
cdスペースフィンダーからフォルダをドラッグアンドドロップ
```
例：cd /Users/hogehoge/Desktop/project/dev/gulp
```

#### インストールしているプラグイン一覧表示コマンド
```
npm list --depth=0
```

#### プラグインインストールコマンド
```
npm install --save-dev プラグイン名
```

#### プラグインアンインストールコマンド
```
npm uninstall --save-dev プラグイン名
```

#### gulpモジュールインストールコマンド
```
npm install
```

#### gulp実効コマンド
```
gulp
```





### gulpfile.js 2021年2月28日現在
```javascript
/**
 * gulpfile.js
 * @creation: 20018.??.??
 * @update  : 2020.12.02
 * @version : 2.1.4
 *
 * @license Copyright (C) 2020 Taichi Matsutaka
 */
///////////////////////////////////////////////////////////////
// variable
///////////////////////////////////////////////////////////////

/* Project path.
------------------ */
const devRoot   = '../dev_html/'; // Path to dev webroot.
const devAssets = devRoot + 'assets' + '/';
const devImg    = devAssets + 'img' + '/';
const devSvg    = devAssets + 'svg' + '/';
const devSass   = devAssets + 'sass' + '/';
const devScript = devAssets + 'js' + '/';
const devHtml   = devRoot;
const devWp     = devRoot + 'wp' + '/';

const projectRoot   = '../../public_html/'; // Path to project webroot.
const projectAssets = projectRoot + 'assets' + '/';
const projectImg    = projectAssets + 'img' + '/';
const projectSvg    = projectAssets + 'svg' + '/';
const projectCss    = projectAssets + 'css' + '/';
const projectScript     = projectAssets + 'js' + '/';
const projectHtml   = projectRoot;
const projectWp     = projectRoot + 'wp' + '/';


/* gulp
------------------ */
// Gulp.
const gulp = require('gulp');

// common
const sourcemaps = require('gulp-sourcemaps');
const plumber    = require('gulp-plumber');
const notify     = require('gulp-notify');
const rename     = require('gulp-rename');
const concat     = require('gulp-concat');
const del        = require('del');
const header     = require('gulp-header');


// Sass plugin.
const sass         = require('gulp-sass');
const autoprefixer = require('gulp-autoprefixer');
const bulkSass     = require('gulp-sass-bulk-import');
const gcmq         = require('gulp-group-css-media-queries');
const cleanCSS     = require("gulp-clean-css");

// Minify Images plugin.
const changed     = require('gulp-changed');
const imagemin    = require('gulp-imagemin');
const imageminJpg = require('imagemin-jpeg-recompress');
const imageminPng = require('imagemin-pngquant');
const imageminGif = require('imagemin-gifsicle');
const svgmin      = require('gulp-svgmin');
const webp        = require('gulp-webp');

// Pug min
const pug         = require('gulp-pug');
const htmlComp    = require('gulp-phtml-simple-comp');
const PugBeautify = require('gulp-pug-beautify');

// Minify javaScript plugin.
const uglify = require('gulp-uglify-es').default;




///////////////////////////////////////////////////////////////
// Pug
///////////////////////////////////////////////////////////////
const pugTask = () => {
	return gulp
		.src( devHtml + '**/!(_|#)*.pug' )
		.pipe( plumber({ errorHandler: notify.onError("Error: <%= error.message %>") }) )
		.pipe( PugBeautify({
			fill_tab: true,
			tab_size: 4,
			separator_space: true
		}) )
		.pipe( pug({
			pretty: true
		}) )
		.pipe( htmlComp() )
		.pipe( rename({
			extname: '.php'
		}) )
		.pipe( gulp.dest( projectHtml ) );
}
exports.pug = pugTask;




///////////////////////////////////////////////////////////////
// sass
///////////////////////////////////////////////////////////////
const sassTask = () => {
	return gulp
		.src( devSass + '**/*.scss')
		.pipe( plumber({ errorHandler: notify.onError("Error: <%= error.message %>") }) )
		.pipe( bulkSass() )
		.pipe( sass({
			// outputStyle: 'expanded',
			// indentWidth: 1,
			// indentType : 'tab',
		}) )
		.pipe( cleanCSS() )
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
		.pipe( rename({suffix: '.min'}) )
		.pipe( gulp.dest(projectCss) );
}
exports.sass = sassTask;




///////////////////////////////////////////////////////////////
// imageMin
///////////////////////////////////////////////////////////////
const devImgFile    = devImg + '**/!(_|#|apng)*.+(jpg|jpeg|png|gif)';
const devWebpFile   = devImg + '!(meta)**/**/!(_|#|apng)*.+(jpg|jpeg|png|gif)';
const devImgSvgFile = devImg + '**/!(_|#)*.svg';
const devSvgFile    = devSvg + '**/!(_|#)*.svg';


const imgTask = ( done ) => {
	/* ----- jpg,png,gif ----- */
	gulp
		.src( devImgFile )
		.pipe( changed( projectImg ) )
		.pipe( imagemin([
			imageminPng(),
			imageminJpg(),
			imageminGif({
				interlaced: false,
				optimizationLevel: 3,
				colors:180
			})
		],{
			verbose: true
		}) )
		.pipe( gulp.dest( projectImg ) );


	/* ----- img/*.svg ----- */
	gulp
		.src( devImgSvgFile )
		.pipe( changed( projectImg ) )
		.pipe( svgmin() )
		.pipe( gulp.dest( projectImg ) );


	/* ----- svg/*.svg ----- */
	gulp
		.src( devSvgFile )
		.pipe( changed( projectSvg ) )
		.pipe( svgmin() )
		.pipe( gulp.dest( projectSvg ) );


	/* ----- webp ----- */
	gulp
		.src( devWebpFile )
		.pipe( changed( projectImg , {extension: '.webp'} ) )
		.pipe( webp() )
		.pipe( gulp.dest( projectImg ) );


	done();
}
exports.img = imgTask;




///////////////////////////////////////////////////////////////
// javascriptMin
///////////////////////////////////////////////////////////////
const jsTask = ( done ) => {
	/* ----- basic ----- */
	gulp
		.src( devScript + '!(_|#|*.min)*.js' )
		.pipe( plumber({ errorHandler: notify.onError("Error: <%= error.message %>") }) )
		.pipe( uglify({ output: {comments: 'some'} }) )
		.pipe( rename({extname: '.min.js'}) )
		.pipe( gulp.dest( projectScript ));


	/* ----- move ----- */
	gulp
		.src( devScript + '**.min.js' )
		.pipe( changed( projectScript ) )
		.pipe( plumber({ errorHandler: notify.onError("Error: <%= error.message %>") }) )
		.pipe( gulp.dest( projectScript ));


	/* ----- library ----- */
	gulp
		.src( devScript + 'library/*.js' )
		.pipe( plumber({ errorHandler: notify.onError("Error: <%= error.message %>") }) )
		.pipe( concat('library.js') )
		.pipe( gulp.dest( projectScript ));


	/* ----- module ----- */
	gulp
		.src( devScript + 'module/*.js' )
		.pipe( plumber({ errorHandler: notify.onError("Error: <%= error.message %>") }) )
		.pipe( concat('module.js') )
		.pipe( uglify({ output: {comments: 'some'} }) )
		.pipe( rename({extname: '.min.js'}) )
		.pipe( gulp.dest( projectScript ));

	done();
}
exports.js = gulp.series(
	gulp.parallel( jsTask )
);




///////////////////////////////////////////////////////////////
// move
///////////////////////////////////////////////////////////////
const devMove = [
	devHtml + '**/*.+(mp4|mp3|mov|m4a|txt|pdf|ttf|eot|woff|woff2|ico|webp)',
	devHtml + '**/apng*.+(png)',
	devHtml + '**/*.css',
];

const moveTask = () => {
	return gulp
		.src( devMove )
		.pipe( changed( projectHtml ) )
		.pipe( plumber({ errorHandler: notify.onError("Error: <%= error.message %>") }) )
		.pipe( gulp.dest( projectHtml ) );
}
exports.move = moveTask;




///////////////////////////////////////////////////////////////
// watch
///////////////////////////////////////////////////////////////
const watchTask = () => {
	console.log(
		''
		+ "\n" + '-- Now Watching ------------------------------------------------'
		+ "\n"
		+ "\n" + '   @name    : gulp watch'
		+ "\n" + '   @task    : pug,sass,js,img,move'
		+ "\n" + '   @version : 2.1.3'
		+ "\n" + '   @gulp    : 4.0.2'
		+ "\n" + '   @node    : 14.14.0'
		+ "\n"
		+ "\n" + '   Copyright (C) 2020 Taichi Matsutaka'
		+ "\n"
		+ "\n" + '------------------------------------------------- Now Watching --'
		+ "\n"
	);

	gulp.watch( devRoot + '**/*.pug' , gulp.parallel( pugTask ) );
	gulp.watch( devSass + '**/*.scss' , gulp.parallel( sassTask ) );
	gulp.watch( devScript + '**/*.js' , gulp.parallel( jsTask ) );
	gulp.watch( devImg + '**/*.+(jpg|jpeg|png|gif|svg)' , gulp.parallel( imgTask ) );
	gulp.watch( devMove , gulp.parallel( moveTask ) );
}
exports.watch = watchTask;




///////////////////////////////////////////////////////////////
// default
///////////////////////////////////////////////////////////////
exports.default = gulp.series(
	gulp.series(
		pugTask,
		sassTask,
		jsTask,
		imgTask,
		moveTask,
		watchTask,
	)
);
````


<br>

## Template
各テンプレートは、それぞれ管理しています。  
プロジェクト開始のたびに適切なものをダウンロードして始めてください。

- [tpl-gulpfile](https://github.com/taichaaan/tpl-gulpfile/)
- [tpl-assets](https://github.com/taichaaan/tpl-assets/)
- [tpl-php](https://github.com/taichaaan/tpl-php/)
- [tpl-pug](https://github.com/taichaaan/tpl-pug/)
- [wp-php](https://github.com/taichaaan/wp-php/)
- [wp-pug](https://github.com/taichaaan/wp-pug/)

