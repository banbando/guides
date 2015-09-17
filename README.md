
# CSSスタイルガイド

なるべくこうした方が良いよ、というルールなので厳格に守る必要はありません。  
念頭において状況に応じてCSSを書きましょう。


## 記述ルール

*基本ルール*
+ [SCSSで記述する](#scssで記述する)
+ [文字コードはUTF-8](#文字コードはutf-8)
+ [インデントはスペース2つ分](#インデントはスペース2つ分)
+ [ネストは3～5階層まで](#ネストは35階層まで)
+ [用途がわかるようにコメントをつける](#用途がわかるようにコメントをつける)
+ [クラスセレクタでスタイルをつくる](#クラスセレクタでスタイルをつくる)
+ [スタイルのまとまりごとに5行あける](#スタイルのまとまりごとに5行あける)

*名称ルール*
+ [クラス名に接頭辞をつける](#クラス名に接頭辞をつける)
+ [継承はアンダースコア、複合語をつなぐのはキャメルケース](#継承はアンダースコア複合語をつなぐのはキャメルケース)
+ [クラス名はわかりやすい名前にする](#クラス名はわかりやすい名前にする)
+ [IDセレクタは使用しない（JSは例外とするが、可能な限り使わない）](#idセレクタは使用しないjsは例外とするが可能な限り使わない)

*記述ルール*
+ [プロパティはなるべく短くまとめる](#プロパティはなるべく短くまとめる)
+ [カラーコードは可能であれば3桁で書く](#カラーコードは可能であれば3桁で書く)
+ [タグに依存したセレクタを書かない](#タグに依存したセレクタを書かない)
+ [プロパティの記述順序を統一する](#プロパティの記述順序を統一する)
+ [プロパティ名のコロンの後（バリュー）にスペースをいれる](#プロパティ名のコロンの後バリューにスペースをいれる)
+ [セレクタと{のあいだに半角スペースをひとつ空ける](#セレクタとのあいだに半角スペースをひとつ空ける)
+ [0のあとに単位は書かない](#0のあとに単位は書かない)
+ [extendは先頭に記述する](#extendは先頭に記述する)
+ [複数セレクタを指定する場合は、１つのセレクタに１行ずつ書く](#複数セレクタを指定する場合は１つのセレクタに１行ずつ書く)
+ [3回同じスタイルを使用した場合、コンポーネント化](#3回同じスタイルを使用した場合コンポーネント化)
+ [まとまったスタイルごとにコメントタイトルをつけて5行あける](#まとまったスタイルごとにコメントタイトルをつけて5行あける)
+ [数値はremを使用する](#数値はremを使用する)


## 参考
+ [Web制作者のためのCSS設計の教科書](http://book.impress.co.jp/books/1113101128)
+ [メンテナブルCSS](https://www.cyberagent.co.jp/techinfo/techreport/report/id=7926)
+ [airbnbのCSSスタイルガイドを読んで一部訳してみた](http://nerd.hatenadiary.jp/entry/2015/08/31/204820)
+ [Airbnb CSS / Sass Styleguide](https://github.com/airbnb/css)
+ [thoughtbotのsassスタイルガイドを和訳してみた](http://nerd.hatenadiary.jp/entry/2015/08/28/205801)
+ [thoughtbot/guides Sass](https://github.com/thoughtbot/guides/tree/master/style/sass)
+ [CSS Nite LP32の「コピペで使える！変数とmixin！」](https://github.com/geckotang/cssnite-lp32)


### SCSSで記述する
こちらはもともと導入していた経緯で、SCSSで記述しています。  
CSSさえ書いたことがあれば参入しやすいのがメリットです。  
ちなみにCompassも導入されています。

### 文字コードはUTF-8
こちらも仕様に沿っています。  
かならずCSSファイルの最初に記述してください。
```css
@charset "UTF-8";
```

### インデントはスペース2つ分
こちらも仕様に沿っています。  
可読性を考慮すると4つくらいが見やすいかなと思いますが、すみませんが仕様です！

### ネストは3～5階層まで
便利なネスト（入れ子）ですが、階層が深くなるとコードの可読性が下がります。  
3～5階層程度に留めておくようにしましょう。
```css
.sample {
  width: 100%;
  background: #f8f8f8;
  .text {
    font-size: 14px;
    line-height: 1.5;
    .link {
      color: #069;
      text-decoration: none;
    }
  }
}
```

### 用途がわかるようにコメントをつける
コメントはコンパイル時に圧縮されるため削除されます。  
用途や使い方がわかるように記述しましょう。  
もし削除したくない・できないコメントの場合は下記のとおりに記述してください。
```css
/*! 残したいコメントの場合 */
```

### クラスセレクタでスタイルをつくる
タグやIDではなく、クラスでセレクタをつくってください。
```css
/* 悪い例 */
#badId {}
p {}

/* 良い例 */
.goodClass {}
```

### スタイルのまとまりごとに5行あける
可読性向上のため、スタイルのまとまりごとに5行分あけてください。  
SCSSファイルはCSSファイルにコンパイルする際に、改行は削除されるためファイル容量が増える心配はありません。
```css
/*
# `sample1`  サンプルスタイル1
*/

.sample1 {
  width: 100%;
  background: #f8f8f8;
}





/*
# `sample2`  サンプルスタイル2
*/

.sample2 {
  padding: 10px;
  color: #0098de;
}
```


### クラス名に接頭辞をつける
CSSの肝はネーミングにかかっています。  
また既存のクラス名との衝突を避けるために接頭辞をつけて差別化を図っています。  
接頭辞の種類は3つあります  
`u_`,`l_`,`is_`  
それぞれカテゴライズしています。

#### u_
汎用性が高く、再利用するもの  
基本はこの接頭辞  
ex. ボタン、タイトルなど

#### l_
固有性のあるもの 
イレギュラーな場合など  
ex. フォーマット外のもの

#### is_
部分的な変更やバリエーションを増やすとき  
単独で使わず、他のクラスと併用して使う  
ex. ボタンの色違い、サイズ違いなど


### 継承はアンダースコア、複合語をつなぐのはキャメルケース
例をお見せしたほうがわかりやすいので下記の通りです。
```css
.header {
  display: block;
}
/* 継承の場合 */
.header_navigation {
  background: #fff;
}
/* 複合語の場合 */
.linkText {
  color: #0098de;
}
```

### クラス名はわかりやすい名前にする
名前から用途がわかるようにつけてください。  
若干長くなってもかまいません。
```css
/*
# `u_dynamicPackageModule`  ダイナミックパッケージモジュール
*/
.u_dynamicPackageModule {
  
}
```

### IDセレクタは使用しない（JSは例外とするが、可能な限り使わない）
下記の利用から非推奨です。

+ 詳細度が上がる（予期しない上書きが起こる）
+ ページに対して１つしか利用できない
+ 再利用性が損なわれる

以上の理由から、クラスセレクタを使いましょう。

### プロパティはなるべく短くまとめる
特に理由がない限り、ショートハンドでまとめて記述してください。
```css
.sample {
  padding: 10px;
  border: 1px solid #ddd;
}
```

### カラーコードは可能であれば3桁で書く
可読性向上と同じ数字を6桁も打つと間違えることもあるため  
省略できるものはまとめてください。
```css
/* 悪い例 */
.bad {
  color: #006699;
}

/* 良い例 */
.good {
  color: #069;
}
```

### タグに依存したセレクタを書かない
タグに依存してしまうと再利用性が損なわれ、余分なセレクタを増やしてしまう原因になります。
```css
/* 悪い例 */
a {
  color: #069;
}

/* 良い例 */
.link {
  color: #069;
}
```

### プロパティの記述順序を統一する

1. 位置情報系(position, top, right, z-index, display, float など)
1. サイズ(width, height, margin, padding)
1. その他（border, border-radius）

以降はアルファベット順に記述してください。


### プロパティ名のコロンの後（バリュー）にスペースをいれる
下記のとおりに記述を統一してください。
```css
color: #069;
```

### セレクタと{のあいだに半角スペースをひとつ空ける
下記のとおりに記述を統一してください。
```css
.sample {}
```

### 0のあとに単位は書かない
プロパティなどの数値で「0」を記述する場合、単位は書かないでください。
```css
.sample {
  padding: 10px 0;
}
```

### extendは先頭に記述する
extend を記述する場合は、どのプロパティよりも先頭に記述してください。
```css
.sample {
  @extend %test;
  width: 100%;
  padding: 10px 20px;
}
```

### 複数セレクタを指定する場合は、１つのセレクタに１行ずつ書く
１行にまとめてセレクタを記述しないこと。  
可読性を優先して１行につき１セレクタずつ記述してください。
```css
.sample01,
.sample02,
.sample03 {
  padding: 10px;
}
```

### 3回同じスタイルを使用した場合、コンポーネント化
Rule of three に則って、3回同じスタイルを使用した場合はコンポーネント化します。  
ですが、はじめから再利用を目的に書く必要はありません。  

### まとまったスタイルごとにコメントタイトルをつけて5行あける
コードを見やすくするため、まとまったスタイルごとに5行あけて記述してください。  
コンパイル時に改行も削除されるのでファイル容量増加にはなりません。
```css
/*
# .sample  スタイルのタイトル
*/

.sample {
  width: 100%;
}





/*
# .sample  スタイルのタイトル
*/

.sample {
  width: 100%;
}
```


### 数値はremを使用する
将来的にpxという単位が良いのか悩ましいところで、実験的にremを採用しています。  
そこでSassの便利機能でpxで記述できるようにしています。  
書き方は下記のとおりです。  

正直むずかしいところで、フォントサイズだけrem採用するのが良いのかなとも思います。  
pxのが慣れているし、デザインを作るときはそちらの数値で作りますし  
レスポンシブのメディアクエリとか限定的に使ったほうがいいかもしれません。

参考：
https://github.com/geckotang/cssnite-lp32/blob/master/scss/_rem.scss

```css
/*
# `pxToRem`  pxをremに変換するmixin

@include rem();()内にプロパティを設定する
ex1: @include rem(margin, 10 15);
ex2: @include rem(border, 1 solid #bcbcbc);
*/

//基準となるフォントサイズ
$basePx: 16;
$rem-root-font-size:$basePx !default;
//レガシーブラウザ用にpxを出力するかしないか
$rem-legacy-support: false !default;

//@function parseInt
//@param $n {String} 数値に変換したい文字列
@function parseInt($n) {
  @return $n / ($n * 0 + 1);
}

//@function rem
//@description 単位なしの数値・もしくはpxならremに変換、
//remの場合はpxに変換(remに対応してないブラウザ向け)
//@param $value {Number} 数値

@function rem($value) {
  $root: $rem-root-font-size;
  $val: parseInt($value);
  $unit: unit($value);
  $result: "";

  @if $unit == "px" or unitless($value) {
    $result: ($val / $root + 0rem);
  }
  @if $unit == "rem" {
    $result: ($val * $root + 0px);
  }

  @return $result;
}

//@mixin rem
//@description 単位なしの数値・もしくはpxならremに変換、
//remの場合はpxに変換(remに対応してないブラウザ向け)
//@param $property {String} プロパティ名
//@param $values {Number} 数値（複数可）
//@usage:
//.list{
//  =rem('font-size', 16px); //*font-size:1.6rem; font-size: 16px;
//  =rem('margin', 10px auto 10px);
//margin: 1rem auto 1rem; margin: 10px auto 10px;
//}
@mixin rem($property, $values) {
  $px : ();
  $rem: ();

  @each $value in $values {
    @if $value == 0 or $value == auto {
      $px : append($px , $value);
      $rem: append($rem, $value);
    }

    @else if type-of($value) == number {
      $unit: unit($value);
      $val: parseInt($value);

      @if unitless($value) {
        $unit: "px";
        $value: $value * 1px;
      }

      @if $unit == "px" {
        $px : append($px,  $value);
        $rem: append($rem, rem($value));
      }

      @if $unit == "rem" {
        $px : append($px,  rem($value));
        $rem: append($rem, $value);
      }
    }

    @else {
      $px : append($px,  $value);
      $rem: append($rem, $value);
    }
  }

  @if $px == $rem {
    #{$property}: $px;
  } @else {
    @if $rem-legacy-support == true {
      #{$property}: $px;
    }
    #{$property}: $rem;
  }
}
```
