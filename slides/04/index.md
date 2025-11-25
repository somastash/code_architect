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

## 時刻と日付
JS で時刻と日付を扱うには、**`Date` オブジェクト**を利用する。

```js
let date = new Date(); // Date オブジェクトを取得
let year = date.getFullYear();
```

[MDN のリファレンス](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)

