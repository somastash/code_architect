---
marp: true
paginate: true
theme: press
---

<!-- _class: cover -->

<h1 class="logo"><b>CODE</b>_ARCHITECT #3</h1>
<p class="title">コード・アーキテクト :: アプリ設計・開発手法 #3</p>
<p class="author">&copy; 2025 Satoshi Soma</p>

---

# 始めよう。Git でバージョン管理

---

## Git とは
Git は CLI アプリの一つで、「**バージョン管理ソフト**」と呼ばれるものの一つだ。
バージョン管理ソフトとは端的に言うと、**ファイルの編集履歴**を記録・管理するシステムの総称だ。

<small class="note">「バージョン」とは「*版*」のことを意味する。
バージョン管理ソフトには他にも SVN や Mercurial などが存在するが、2025 年現在 Git が最も広く使われている。
</small>

---

Git を利用することで、例えば以下のようなことが可能になる。

- プロジェクト内のある時点でのファイルの状態を **記録（コミット）** する。
  - 記録した状態はいつでも確認することができるし、必要とあればその時点に*戻す*ことも可能。
  - 前後の状態と比較した *差分（追記, 変更, 削除等）* も確認できる。
- [GitHub](https://github.com/) や [Bitbucket](https://bitbucket.org/) などのホスティングサービスとの連携。
  - プロジェクトを「**リモート・リポジトリ**」として保存・共有することができる。
  - 他者のリポジトリを自分のマシン上に **複製（クローン）** できる。
    - 複製後に複製元の版が更新されても、最新版にいつでも*同期*することができる。

---

## 「リポジトリ」を作成する
1. VSCode でプロジェクトルートを開く。
2. コマンドパレットを開く ( <kbd>⌘</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> ) 。
3. "git init" と検索し、`Git: Initialize Repository (Git: リポジトリの初期化)` を選択・実行。

<table>
<thead>
<tr><td>Before</td><td>After</td></tr>
</thead>
<tbody>
<tr>
<td>

```
📁 プロジェクトルート
├── index.html
├── style.css
└── sketch.jsaaa
```

</td>
<td>

```
📁 プロジェクトルート
├── 📁 .git
├── index.html
├── style.css
└── sketch.jsaaa
```

</td>
</tr>
</tbody>
</table>

---

