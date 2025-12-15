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
% curl -LO "https://github.com/liabru/matter-js/raw/refs/heads/master/build/matter.min.js"
```

<small class="note">GitHub からファイルを `curl` で取得する際は *`Raw`* というボタンのリンク先の URL をコピーし、<br>ターミナルにペーストすればよい。</small>
