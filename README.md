# 話せる・読める英語

英語学習をテーマにした静的HTMLサイト。文法用語を使わず、音声再生・発音練習・ゲーミフィケーションを組み合わせた学習体験を提供する。

## ページ構成

| ファイル | 内容 |
|---|---|
| `index.html` | 目次 |
| `page0.html` | 第0部 ― はじめに・サバイバル英語 |
| `page1.html` | 第1部 ― 音と文字 |
| `page2.html` | 第2部 ― 英語の骨組み |
| `page3.html` | 第3部 ― 広げる |
| `page4.html` | 第4部 ― つなぐ |
| `page5.html` | 第5部 ― 自然に話す |
| `page6-1.html` 〜 `page6-13.html` | 第6部 ― 語彙（全13章） |
| `lesson.html` | AI英会話レッスン（Practice セクション） |

## 新しいページを追加するには

### 1. ファイルを作成する

命名規則に従ってHTMLファイルを作成する。

| パターン | 例 | 用途 |
|---|---|---|
| `pageN.html` | `page7.html` | 1ページで構成される章 |
| `pageN-1.html`, `pageN-2.html`, ... | `page8-1.html` | 複数ページで構成される章 |

### 2. `<title>` タグを設定する

スクリプトが目次のタイトルを `<title>` タグから取得するため、以下の形式で記述する。

```html
<!-- 単独ページの場合 -->
<title>第7部 ― タイトル | 話せる・読める英語</title>

<!-- 複数ページの場合 -->
<title>第8部① タイトル | 話せる・読める英語</title>
```

### 3. `<div class="nextup">` を設置する

各ページ末尾に次ページの紹介セクションを置く（リンク自体はスクリプトが自動付与）。

```html
<div class="nextup">
  <div class="k">Next</div>
  <h3 class="jp">次のページタイトル</h3>
  <p class="jp">次のページの説明文。</p>
</div>
```

### 4. スクリプトを実行する

```bash
python scripts/wire_links.py
```

これだけで以下が自動更新される。

- 各ページの `.nextup` セクションに次ページへのリンクが付与される
- `index.html` の目次が再生成される（複数ページ構成の章は自動でグループ化）

## `page*.html` 以外のページを index に追加するには

`lesson.html` のように命名規則外のページは、スクリプトの管理対象外のため手動で追加する。

`index.html` の `<!-- INDEX_END -->` より下にある **Practice セクション**に直接追記する。

```html
<div class="toc">
  <div class="wrap">
    <div class="eyebrow">Practice</div>
    <ul class="toc-list">
      <li><a href="lesson.html">
        <span class="toc-num jp" style="background:var(--jade-soft);color:var(--jade)">AI会話</span>
        <span class="toc-title jp">AI英会話レッスン</span>
        <span class="toc-arrow">›</span>
      </a></li>
    </ul>
  </div>
</div>
```

このセクションはスクリプトを実行しても上書きされない。

### 5. pushする

```bash
git add .
git commit -m "Add pageN"
git push origin main
```
