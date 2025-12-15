---
marp: true
paginate: true
theme: press
---

<!-- _class: cover -->

<h1 class="logo"><b>CODE</b>_ARCHITECT #5</h1>
<p class="title">コード・アーキテクト :: アプリ設計・開発手法 #5</p>
<p class="author">&copy; 2025 Satoshi Soma</p>

---

# 物理シミュレーション
物理エンジンを使ってみよう

---

## 物理エンジンとは
現実世界における物体の挙動をプログラム上で再現するためのシステムの総称。
学術研究のためだけではなく、広くビデオゲームにおいても利用されることが多い。

---

## [Matter.js](https://www.brm.io/matter-js/)
Matter.js は JS で動作する物理エンジンの一つだ。
主にゲームやインタラクティブアートに利用することが想定されており、
慣性や摩擦、衝突判定などを用意にシミュレートすることができる。

---

Matter.js は p5.js 用に作られたライブラリではないため、
どのような JS アプリにも組み込むことが可能だ。

p5.js のスケッチに組み込むことも容易なので、早速試してみよう。

---

まずは Matter.js の [GitHub リポジトリ](https://github.com/liabru/matter-js) から *`build/matter.min.js`* をダウンロードしよう。
`curl` コマンドを使えば簡単だ。

```sh
% cd プロジェクトルート
% curl -LO "https://github.com/liabru/matter-js/raw/refs/heads/master/build/matter.min.js"
```

<small class="note">GitHub からファイルを `curl` で取得する際は *`Raw`* というボタンのリンク先の URL をコピーし、<br>ターミナルにペーストすればよい。</small>

---

`matter.min.js` がプロジェクトルートに配置されたことを確認したら、
`index.html` の `<head>` タグ内に `<script>` タグを書き加えよう。

```html
<head>
  ...
  <script src="matter.min.js"></script>
  ...
</head>
```

注意点は、`sketch.js` よりも `matter.min.js` が**先に読み込まれる必要がある**ということだ。
`<script>` タグは上から順番に読み込まれるのでタグの配置に気をつけよう。

---

これで準備は完了した。以降、`sketch.js` にて **`Matter`** というオブジェクトが使用可能になる。

`Matter` オブジェクトは物理演算のためのいくつかの*モジュール*をプロパティとして内包している。
アプリ開発者は自分の目的に応じたモジュールのみを取り出して使用することになる。

モジュールの一覧と各使用法は[公式のドキュメント](https://brm.io/matter-js/docs/)で確認できる。

---

使用したい各モジュールを以下のように変数に格納するとよい。

```js
let Engine    = Matter.Engine;
let Bodies    = Matter.Bodies;
let Composite = Matter.Composite;
```

また、上記のコードは次のように書き換えることもできる。

```js
let { Engine, Bodies, Composite } = Matter;
```

これは「[オブジェクトの構造分解 <small>(Object Destructuring)</small>](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Destructuring) 」と呼ばれる記法だ。
オブジェクトのプロパティを、**同名の変数に置き換える**ための短縮記法といえる。

<small class="note">プログラミングにおけるこのような利便性のための短縮記法のことを概して「*糖衣構文 (Syntax Sugar)* 」と呼ぶ。</small>

---

<!-- _class: small -->

以下のコードは Matter.js を使用し、
物理エンジンの初期化と物体の生成 & 配置を行う例だ。

```js
let {Engine, Bodies, Composite} = Matter; // モジュールを変数化
let engine; // 物理エンジン

function setup() {
  createCanvas(400, 400);

  // 物理エンジン（世界）を初期化
  engine = Engine.create();

  // 箱を生成 (X, Y, 幅, 高さ)
  let boxA   = Bodies.rectangle(150, 200, 120, 120); // 箱（大）
  let boxB   = Bodies.rectangle(200,   0,  80,  80); // 箱（小） 
  let ground = Bodies.rectangle(200, 350, 380,  50, { isStatic: true }); // 地面

  // 箱を世界に配置
  Composite.add(engine.world, [boxA, boxB, ground]);
}
```

---

<!-- _class: small -->

そして以下が、フレーム毎の物理演算と物体の描画を行う例だ。

```js
function draw() {
  background(220);

  // 世界の更新（1 フレーム時間を進める）
  Engine.update(engine, deltaTime);

  // 世界に配置された全ての物体を取得（配列） 
  let bodies = Composite.allBodies(engine.world);

  // 全ての物体を描画（配列をスキャン）
  for (let i = 0; i < bodies.length; i++) {
    drawBody(bodies[i]);
  }
}

// 自作関数: 引数で渡された物体を描画する
function drawBody(body) {
  let v = body.vertices; // 物体の頂点（配列）
  beginShape(); // 多角形描画開始
  for (let i = 0; i < v.length; i++) {
    vertex(v[i].x, v[i].y);
  }
  endShape(CLOSE); // 多角形描画終了
}
```
