# Pug

## Comment
コメントアウトは、sectionなど大区分か ループする記述の可視性を上げる為、始めと終わりに記述してください。
```pug
//- ----------------------------------------
//- t-top-visual
//- ----------------------------------------
section.t-top-visual
```


<br>

## Template

共通部分は_includeディレクトリで管理し、各ファイルでrequireかincludeで読み込んでください。
