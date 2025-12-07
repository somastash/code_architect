---
marp: true
paginate: true
theme: press
---

<!-- _class: cover -->

<h1 class="logo"><b>CODE</b>_ARCHITECT #4</h1>
<p class="title">コード・アーキテクト :: アプリ設計・開発手法 #4</p>
<p class="author">&copy; 2025 Satoshi Soma</p>

---

# ウェブ API
外部サイトからデータを取得する

---

**API** <small>(Application Programming Interface)</small> とは、広義では異なるアプリ同士が情報 <small>(データ)</small> をやりとりするためのインターフェースのことをいう。
特にウェブアプリやウェブサービスが外部のアプリとの連携のために公開している API のことをウェブ API と呼ぶ。

---

## 様々なウェブ API
https://dog.ceo/
http://thecatapi.com/
https://randomfox.ca/

Open-Meteo (天気情報)
https://open-meteo.com/

Art Institute of Chicago (シカゴ美術館)
http://api.artic.edu/

https://github.com/public-apis/public-apis?tab=readme-ov-file

---

## JSON
**JSON** <small>(JavaScript Object Notation)</small> とはデータ記述のためのフォーマットおよびファイル形式の一つ。
ファイルの拡張子は `.json` だ。構文は JS におけるオブジェクトの記述方法と似ている。

```json
{
  "キー名A": 値,
  "キー名B": 値,
  "キー名C": 値
}
```

このように、`{ }` 内に `"キー名"` と `値` のペアを `, (カンマ)` 区切りで列挙していく。
最後の値には `,` を付けてはならない。
`"キー名"` はオブジェクトのプロパティにあたるものだが、**`"` で括る**必要がある点に注意。

---

<div class="cols c32 gap">
<div>

```json
{
  "name": "味噌汁",
  "calories": 35,
  "vegan": true,
  "ingredients": ["味噌", "豆腐", "わかめ"],
  "howto": {
    "time": 20,
    "text": "豆腐とわかめを加えて軽く煮たら火を止め味噌を溶き入れて完成です。"
  }
}
```

料理のレシピを JSON データで表した一例。

</div>
<div>

値の型<small>（タイプ）</small> は

- 文字列
- 数値
- 真偽値<small>（ブーリアン）</small>
- 配列
- オブジェクト

が使用可能だ。

</div>
</div>

---

## JSON の取得と非同期処理
API を介して JSON データを取得するには複数の方法が存在するが、
p5.js においては [`loadJSON()`](https://p5js-ja.pages.dev/reference/p5/loadJSON/) 関数を利用するのがお手軽だろう。

第 1 引数に URL を渡すと API リクエストが発行され、承認されればデータが返ってくる。

```js
loadJSON("https://dog.ceo/api/breeds/image/random");
```

ここで少し厄介なのが、データの**受け取り方**だ。

---

`loadJSON()` を実行し、こちらがリクエストを投げてからデータが返ってくるまで、
多かれ少なかれ*時間差*が発生する。

問題は、アプリケーションはその間も*停止することなく動き続ける*ということだ。
具体的には、**`loadJSON()` の結果を待たずに次の行に処理が進んでしまう**のだ。

```js
console.log("リクエスト開始。");
loadJSON("https://dog.ceo/api/breeds/image/random");
console.log("まだ取得できてないよ。");
```

`loadJSON()` のように結果が即座に返ってこず、プログラムがそれを待たずに次の行に進んでしまうような処理のことを「**非同期 <small>(Asynchronous)</small> 処理**」と呼ぶ。

---

非同期処理を行う関数から結果を受け取る方法の一つとして、
「*コールバック <small>(Callback)</small>* 」という仕組みが存在する。

```js
let dog; // 犬
console.log("リクエスト開始。");
loadJSON("https://dog.ceo/api/breeds/image/random", function(data) { // コールバック関数
  console.log("データ取得完了:", data);
  dog = data; // 取得データを明け渡す
});
console.log("データ取得中...");
```

`loadJSON()` の第 2 引数に関数を渡すと、
**データの取得が完了した瞬間にその関数が呼び出<small>（コールバック）</small>される**。
コールバック関数には**取得したデータが引数として渡される**ので、
後はそれを外部の変数に明け渡すことで自由にデータを利用することができるようになる。

---

コールバックを利用すれば、`loadJSON()` を含む `load*` 系の関数を
`preload()` 関数内に留まらず、いつでも好きなタイミングで呼び出すことができる。

<div class="cols gap">
<div>
コールバック無し:

```js
let img;
function preload() {
  img = loadImage("photo.jpg");
}
function setup() {
  createCanvas(400, 400);
}
```

<small class="note">画像の読み込みが終わるまで `setup()` が開始されず、その間画面は空白になってしまう。</small>

</div>
<div>
コールバック有り:

```js
let img;
function setup() {
  createCanvas(400, 400);
  loadImage("photo.jpg", function(data) {
    // 読み込み完了
    img = data;
  });
}
function draw() {
  if (!img) { // まだ読み込まれていない場合
    text("画像を読み込んでいます...", 100, 100);
  }
}
```

</div>
</div>

---

## 無名関数とアロー関数
先程からコールバック関数として使用しているのは*名前を持たない関数*で、
「**無名関数 <small>(Anonymous Function)</small>** 」と呼ばれるものだ。書き方の違いに注意しよう。

<div class="cols gap">
<div>
通常の関数<small>（名前有り）</small>:

```js
function hello() {

}

// 引数有り
function hello(x) {

}
```

</div>
<div>
無名関数:

```js
function() {
  
}

// 引数有り
function(x) {
  
}
```

</div>
</div>

---

無名関数にはもう一つの記法が存在する。「**アロー <small>(Arrow)</small> 関数**」と呼ばれる記法だ。

<div class="cols gap">
<div>

```js
function() {
  
}

// 引数有り
function(x) {
  
}
```

</div>
<div>

```js
() => {
  
}

// 引数有り
(x) => {
  
}

// 引数が一つの場合は () を省略可
x => {
  
}
```

</div>
</div>

左が通常の無名関数。右がアロー関数だ。`=>` を矢印に見立ててそう呼ばれている。
アロー関数の方がタイプ数が少なくて済むため好まれる。

---

`loadImage()` 関数の第 2 引数に渡すコールバックにアロー関数を指定すると、右のようになる。

<div class="cols gap">
<div>

```js
loadImage("photo.jpg", function(data) {
  // 読み込み完了
  img = data;
});
```

</div>
<div>

```js
loadImage("photo.jpg", data => {
  // 読み込み完了
  img = data;
});
```

</div>
</div>

結果はどちらも同じだが、アロー関数を使用したほうが短く記述できるため好ましい。

---

## 時刻と日付
JS で時刻と日付を扱うには、**`Date` オブジェクト**を利用する。

```js
let date = new Date(); // Date オブジェクトを取得
```

`Date` オブジェクトの**メソッド**<rb>*</rb>を呼び出すことで、
年, 月, 日, 時, 分, 秒などの数値を個別に取り出すことができる。
例えば年は `getFullYear()` メソッドで取得できる。

```js
let year = date.getFullYear();
```

その他のメソッドについては [MDN のリファレンス](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Date) を参照してほしい。

<small class="note">* メソッド (Method) とはオブジェクトが所有する関数のこと。</small>

