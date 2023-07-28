---
theme: "simple"
customTheme : "dc-theme"
transition: "convex"
slideNumber: false
title: "コーディング専攻 - HTMLとCSS"
---

# コーディング専攻<br>ライブ授業
<h2 class="firstPage">4週目「HTMLとCSS」</h2>
<img src="./img/logo_bg_none.png" style="width: 16%;">
---

1. 課題
1. 座学
1. 実習
1. 講師FB
1. まとめ
1. 受講生MTG

---

### 課題

--

「人工知能(？)」

---

座学の時間
## HTMLとCSS

---

### ところで

--

#### Can I use  
https://caniuse.com/

#### MDN  
https://developer.mozilla.org/ja/docs/Web

---

### HTMLの便利な要素

--

#### details要素とsummary要素

--

```html
<details>
    <summary>徒然草</summary>
    つれづれなるまゝに、日暮らし、硯にむかひて、心にうつりゆくよしなし事を、そこはかとなく書きつくれば、あやしうこそものぐるほしけれ
</details>
```

--

#### dialog要素

--

```html
<dialog>
    ダイアログだよ
</dialog>
```

--

#### template要素

--

```html
<template>
    <div>
        テンプレート
    </div>
</template>
```


---

### WAI-ARIA

--

Web Accessibility Initiative  
\-  
Accessible Rich Internet Applications

--

通常のHTMLタグを補完して、より正確な意味付けを行うもの

--

**利点**

- コンピューターの理解が向上する
- スクリーンリーダーなどで適切に情報が伝えられるようになる

--

絶対必要なものではなく、必要だと思ったときにつかおう

--

判断基準は、このままだとタグの意味としておかしいぞ、ってとき

--

#### role

要素の役割を定義する

```html
<div role="navigation">これはナビゲーション</ｄ>
```

<a class="notes">https://developer.mozilla.org/ja/docs/Web/Accessibility/ARIA/Roles</a>

--

#### tabindex

```html
<div tabindex="0">タブキーでフォーカス</div>
```

--

#### aria-label

```html

<button aria-label="閉じる"></button>

```

--

#### aria-hidden

```html
<span aria-hidden="true"></span>
```

--

#### aria-controls
```html
<button aria-controls="nav"></button>

<nav id="nav"></nav>
```

--

#### aria-expanded

```html
<button aria-controls="gnav" aria-expanded="true"></button>

<nav id="nav" aria-hidden="false"></nav>
```

---

他にも構造化データなども調べてみて

---

### SASS（SCSS）について

--

"Dart Sass"と"Lib Sass"

--

SASS記法とSCSS記法がある  
※ファイルの拡張子も.sassと.scssでわける
--

Node.jsやらNPMやらをコマンドラインで
<p><img src="./img/3w/cli_ss.png" style="width: 75%;"><p/>

--

設定ファイルものいろいろだし、書き方の変化も早い

--

つらい人にはつらい

---

### Preprosの使い方

--

基本はフォルダをアプリの画面にドラッグ&ドロップ
<p><img src="./img/3w/prepros.png" style="width: 75%;"><p/>

--

ソースとなるファイルと変換先の確認は忘れずに

---

#### まずはHTMLを

--

```html

<div class="demo01">
    <p>Sass</p>
    <span>Scss</span>
</div>
<div class="demo02">
    <p class="demo02_pra">demo</p>
</div>


```

---

#### Sassって便利、その１
入れ子（ネスト）

--

```scss
.demo01 {
    p {color: red;}
    span {color: blue;}
}
.demo02 {
    &_pra {background: green;}
}
```
↓
```css
.demo01 p {color: red;}
.demo01 span {color: blue;}
.demo02_pra {background: green;}
```

--

参考：SASS記法

```sass

.demo01
    p
        color: red
    span
        color: blue

.demo02
    &_pra
        background: green


```

--

```scss
.demo01 {
    p {color: red;}
    @media only screen and (max-width: 640px) {
        p {color: yellow;}
    }
}

```
↓
```css
.demo01 p {color: red;}
@media only screen and (max-width: 640px) {
    .demo01 p {color: yellow;}
}


```

---

#### Sassって便利、その2
@extend(継承)

--

```scss
.demo01 {
    padding: 1rem;
    background: gray;
}
.demo02 {
    @extend .demo01;
    border: 1px solid black;
}
```
↓
```css
.demo01 {
    padding: 1rem;
    background: gray;
}
.demo02 {
    padding: 1rem;
    background: gray;
    border: 1px solid black;
}
```

---

#### Sassって便利、その3
@mixin

--

```scss
@mixin borderRadius {
    border-radius: 8px;
}

.demo01 {
    @include borderRadius;
}
.demo02 {
    @include borderRadius;
}
```
↓
```css
.demo01 {
    border-radius: 8px;
}
.demo02 {
    border-radius: 8px;
}
```

--

引数も使える

```scss
@mixin borderRadius($radius: 8px) {
    border-radius: $radius;
}

.demo01 {
    @include borderRadius();
}
.demo02 {
    @include borderRadius(16px);
}
```
↓
```css
.demo01 {
    border-radius: 8px;
}
.demo02 {
    border-radius: 16px;
}
```

---

#### Sassって便利、その4
いろんな色

--

```scss
$baseColor: #3FC9CA;

.demo01 {
    background: $baseColor;
}
.demo02 {
    background: lighten($baseColor, 10);
    // background: darken($baseColor, 100);
    // background: saturate($baseColor, 50);
    // background: invert($baseColor);
    // background: mix($baseColor, red, 50);
}

```
↓
```css
.demo01 {
    background: #3FC9CA;
}
.demo02 {
    border-radius: #67d4d5;
}
```

---

#### Sassって便利、その5
別のファイルを読み込んでひとつのファイルに

--

```scss
//Lib Sass
@import 'ファイル名1';
@import 'ファイル名2';

//Dart Sass
@use 'ファイル名1';
@use 'ファイル名2';

```

---

#### Sassって便利、その6
他にもいろいろ便利な機能があるから、調べてみて

--

```scss
@function pxToRem($px, $baseSize: 16) {
    @return $px / $baseSize * 1rem;
}

.demo02 {
    font-size: pxToRem(24);
}


```
↓
```css
.demo02 {
    font-size: 1.5rem;
}
```
--

```scss
$breakpoint: (
    tab: 'screen and (min-width: 600px)',
    pc: 'screen and (min-width: 1000px)'
);
@mixin mq($bp) {
    @media #{map-get($breakpoint, $bp)} {
        @content;
    }
}
.demo02 {
    @include mq(pc) {
        background: white;
    }
}
```

---

最新のCSSでは・・・

--

ネストはできます

--

```css
.demo01 {
    .child {color: red;}
}
.demo02 {
    & h1 {background: green;}
}
```

--

別のファイルの読み込みもできます

--

```css
@layer a, b, c;

@import url(a.css) layer(a);
@import url(b.css) layer(b);
@import url(c.css) layer(c);
```

カスケードレイヤーについて  
https://developer.mozilla.org/ja/docs/Web/CSS/@layer

---

## 座学の最後に

--

HTMLはセマンティックを心がける

--

CSSでできることはCSSでやってしまうのがいい

けれども・・・

JSとのすみわけもきちんと考えよう

--

JSを書くときは・・・  
<ruby>Vanilla<rt>バニラ</rt><ruby>なJavaScriptで書くのがいいと思います

---

## 実習

--

14:10-14:50まで  
※休憩等は自由に

---

## 来週に向けて

--

クライアントのコーディングをやる！
<p class="notes">※卒業制作もすすめないとつらいよ</p>

--

それではまた来週を楽しみにしています！
