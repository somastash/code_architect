---
marp: true
paginate: true
theme: press
---

<!-- _class: cover -->

<h1 class="logo"><b>CODE</b>_ARCHITECT #2</h1>
<p class="title">コード・アーキテクト :: アプリ設計・開発手法 #2</p>
<p class="author">&copy; 2025 Satoshi Soma</p>

---

# ローカルでスケッチを動かす

---

まずは前回デスクトップに作成した `📁 HelloP5` にターミナルで移動しよう。

```sh
% cd ~/Desktop/HelloP5
```

この記号 *`~`* は「*ティルダ<small>（またはチルダ）</small>*」と呼び、ターミナルにおいては特別な意味がある。
**`~` で始まるファイルパスは必ず自分のホームディレクトリを基準としたパスとして解釈される**のだ。
つまり、上記のコマンドは以下のコマンドと同じ意味を持つ。<small>（macOS の場合）</small>

```sh
% cd /Users/自分のユーザー名/Desktop/HelloP5
```

<small class="note"><kbd>Tab</kbd> キーでパスの補完が出来ることも忘れずに。</small>

---

次に CODE_ARCHITECT に付属している `📁 files/p5_template` フォルダ内の*全ファイル*を、
`📁 HelloP5` フォルダ内にコピーしてほしい。

ファイルのコピーは *`cp コピー元 コピー先`* というコマンドで行える。 
また、**フォルダ内の全ファイルをまとめてコピー**したい場合は、

```sh
% cp コピー元ディレクトリ/* コピー先ディレクトリ/
```

このように *`*` 記号*を用いる。

---

