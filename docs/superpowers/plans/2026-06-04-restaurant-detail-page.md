# 飲食店予約システム 製品詳細ページ 実装計画

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** `products/restaurant-reservation.html` を新規作成し、代理店・インフルエンサーが飲食店オーナーに見せる製品詳細ページを完成させる。同時に `index.html` から全デモ・本番直リンクを削除する。

**Architecture:** 単一HTMLファイルにCSS・コンテンツをインライン記述（index.htmlと同方式）。ダーク×ライトハイブリッド構成で6セクションを縦積み。UIモックアップはHTML/CSSで実装し、外部依存なし。

**Tech Stack:** HTML5, CSS3（index.htmlのデザイントークン継承）, Google Fonts（Noto Sans JP）

---

## ファイル構成

| ファイル | 操作 | 内容 |
|---------|------|------|
| `index.html` | 修正 | デモ・本番直リンク4件を削除 / 飲食店カードに詳細ページリンク追加 |
| `products/restaurant-reservation.html` | 新規作成 | 製品詳細ページ全体（6セクション） |

---

## Task 1: index.html から直リンクを削除し詳細ページリンクを追加

**Files:**
- Modify: `index.html:498-551`

### 変更箇所と変更内容

**① 飲食店予約システム カード（line 498-500）**

変更前:
```html
<a href="https://psl-demo-restaurant.onrender.com/guest" target="_blank" class="card-link card-link-featured" style="margin-top:16px;display:inline-flex;">
  デモを触ってみる <svg ...></svg>
</a>
```

変更後:
```html
<a href="products/restaurant-reservation.html" class="card-link card-link-featured" style="margin-top:16px;display:inline-flex;">
  詳細を見る <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M18 13v6a2 2 0 01-2 2H5a2 2 0 01-2-2V8a2 2 0 012-2h6"/><polyline points="15,3 21,3 21,9"/><line x1="10" y1="14" x2="21" y2="3"/></svg>
</a>
```

**② 売上集計ツール カード（line 508）**

変更前:
```html
<a href="https://pumpstack-lab.github.io/sales-tool/" target="_blank" class="card-link">デモを見る <svg ...></svg></a>
```

変更後:
```html
<p class="card-link-muted">詳細はご相談時にご案内します</p>
```

**③ グループホーム日報ツール カード（line 545）**

変更前:
```html
<a href="https://pumpstack-lab.github.io/gh-report-tool/" target="_blank" class="card-link">デモを見る <svg ...></svg></a>
```

変更後:
```html
<p class="card-link-muted">詳細はご相談時にご案内します</p>
```

**④ 在庫管理ツール カード（line 551）**

変更前:
```html
<a href="https://inventory-tool-zbuj.onrender.com" target="_blank" class="card-link">デモを見る <svg ...></svg></a>
```

変更後:
```html
<p class="card-link-muted">詳細はご相談時にご案内します</p>
```

### 実装ステップ

- [ ] **Step 1: 飲食店予約システムカードのリンクを変更**

  `index.html` の498行目付近を編集（Editツール使用）：
  - `href="https://psl-demo-restaurant.onrender.com/guest"` → `href="products/restaurant-reservation.html"`
  - `target="_blank"` 属性を削除
  - ボタンテキスト `デモを触ってみる` → `詳細を見る`

- [ ] **Step 2: 売上集計ツールのデモリンクを削除**

  line 508のアンカータグを `<p class="card-link-muted">詳細はご相談時にご案内します</p>` に置換

- [ ] **Step 3: グループホーム日報ツールのデモリンクを削除**

  line 545のアンカータグを `<p class="card-link-muted">詳細はご相談時にご案内します</p>` に置換

- [ ] **Step 4: 在庫管理ツールのデモリンクを削除**

  line 551のアンカータグを `<p class="card-link-muted">詳細はご相談時にご案内します</p>` に置換

- [ ] **Step 5: ブラウザで動作確認**

  index.html をブラウザで開き：
  - 飲食店予約システムのカードに「詳細を見る」リンクがある
  - 売上集計・日報ツール・在庫管理カードに「詳細はご相談時にご案内します」テキストがある
  - 外部URLへのリンクが一切ない（ブラウザのリンク検査で確認）

- [ ] **Step 6: grep で直リンクが残っていないことを確認**

  ```bash
  grep -n "inventory-tool\|gh-report-tool\|psl-demo-restaurant\|onrender.com" index.html
  ```
  Expected: 出力なし（0件）

---

## Task 2: products/ ディレクトリと詳細ページのHTML骨格を作成

**Files:**
- Create: `products/restaurant-reservation.html`

- [ ] **Step 1: products ディレクトリ作成確認**

  ```bash
  mkdir -p products
  ls products/
  ```

- [ ] **Step 2: restaurant-reservation.html の骨格を作成**

  以下の完全なHTMLを `products/restaurant-reservation.html` として作成する：

  ```html
  <!DOCTYPE html>
  <html lang="ja" translate="no">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>飲食店予約システム｜PumpStack Lab.</title>
    <meta name="description" content="あなたの店専用のネット予約システムを最短3日で作ります。席数・営業時間・ルールをフルカスタム。月額¥6,000〜。">
    <meta name="google" content="notranslate">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;500;700;900&display=swap" rel="stylesheet">
    <style>
      /* === RESET & TOKENS === */
      *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
      :root {
        --blue: #2563eb;
        --blue-dark: #1d4ed8;
        --blue-light: #eff6ff;
        --violet: #7c3aed;
        --violet-light: #a78bfa;
        --dark: #0a0f1e;
        --dark-2: #0f172a;
        --dark-3: #1e293b;
        --gray: #64748b;
        --gray-light: #94a3b8;
        --light: #f8fafc;
        --white: #ffffff;
        --green: #16a34a;
        --green-line: #06c755;
        --amber: #d97706;
        --radius: 12px;
        --font: 'Noto Sans JP', 'Hiragino Sans', sans-serif;
      }
      html { scroll-behavior: smooth; }
      body { font-family: var(--font); color: var(--dark-2); background: var(--white); line-height: 1.75; -webkit-font-smoothing: antialiased; }
      a { text-decoration: none; color: inherit; }
      img { max-width: 100%; height: auto; display: block; }
      .container { max-width: 960px; margin: 0 auto; padding: 0 24px; }

      /* === HEADER === */
      header {
        position: fixed; top: 0; left: 0; right: 0; z-index: 100;
        background: rgba(255,255,255,0.95); backdrop-filter: blur(12px);
        border-bottom: 1px solid #e2e8f0;
        padding: 10px 28px; display: flex; justify-content: space-between; align-items: center;
      }
      .logo-link { font-size: 15px; font-weight: 900; color: var(--dark); letter-spacing: -.02em; }
      .logo-link span { color: var(--blue); }
      .header-cta {
        background: var(--green-line); color: white; border: none; border-radius: 8px;
        padding: 10px 20px; font-size: 13px; font-weight: 700; cursor: pointer;
        text-decoration: none; display: flex; align-items: center; gap: 6px;
        font-family: var(--font); transition: opacity 0.15s;
      }
      .header-cta:hover { opacity: 0.85; }

      /* === SECTION BASE === */
      section { padding: 80px 0; }
      .section-kicker {
        font-size: 11px; font-weight: 700; letter-spacing: .14em;
        color: var(--violet-light); text-transform: uppercase; margin-bottom: 12px;
      }
      .section-title { font-size: clamp(24px, 4vw, 36px); font-weight: 900; line-height: 1.25; margin-bottom: 16px; }
      .section-sub { font-size: 15px; color: var(--gray); line-height: 1.8; }

      /* placeholder: sections will be added in subsequent tasks */
    </style>
  </head>
  <body>

    <!-- HEADER -->
    <header>
      <a href="../index.html" class="logo-link">Pump<span>Stack</span> Lab.</a>
      <a href="https://lin.ee/XXXXXXX" class="header-cta">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M19.365 9.863c.349 0 .63.285.63.631 0 .345-.281.63-.63.63H17.61v1.125h1.755c.349 0 .63.283.63.63 0 .344-.281.629-.63.629h-2.386c-.345 0-.627-.285-.627-.629V8.108c0-.345.282-.63.63-.63h2.386c.346 0 .627.285.627.63 0 .349-.281.63-.63.63H17.61v1.125h1.755zm-3.855 3.016c0 .27-.174.51-.432.596-.064.021-.133.031-.199.031-.211 0-.391-.09-.51-.25l-2.443-3.317v2.94c0 .344-.279.629-.631.629-.346 0-.626-.285-.626-.629V8.108c0-.27.173-.51.43-.595.06-.023.136-.033.194-.033.195 0 .375.104.495.254l2.462 3.33V8.108c0-.345.282-.63.63-.63.345 0 .63.285.63.63v4.771zm-5.741 0c0 .344-.282.629-.631.629-.345 0-.627-.285-.627-.629V8.108c0-.345.282-.63.63-.63.346 0 .628.285.628.63v4.771zm-2.466.629H4.917c-.345 0-.63-.285-.63-.629V8.108c0-.345.285-.63.63-.63.348 0 .63.285.63.63v4.141h1.756c.348 0 .629.283.629.63 0 .344-.282.629-.629.629M24 10.314C24 4.943 18.615.572 12 .572S0 4.943 0 10.314c0 4.811 4.27 8.842 10.035 9.608.391.082.923.258 1.058.59.12.301.079.766.038 1.08l-.164 1.02c-.045.301-.24 1.186 1.049.645 1.291-.539 6.916-4.078 9.436-6.975C23.176 14.393 24 12.458 24 10.314"/></svg>
        LINEで無料相談
      </a>
    </header>

    <main style="padding-top: 64px;">
      <!-- sections inserted in Tasks 3-8 -->
    </main>

    <!-- FOOTER -->
    <footer style="background: var(--dark); color: var(--gray-light); text-align: center; padding: 40px 24px; font-size: 13px;">
      <p style="margin-bottom: 8px; font-weight: 700; color: white;">PumpStack Lab.</p>
      <p>© 2026 PumpStack Lab. All rights reserved.</p>
      <p style="margin-top: 12px;"><a href="../index.html" style="color: var(--gray-light); text-decoration: underline;">← サービス一覧に戻る</a></p>
    </footer>

  </body>
  </html>
  ```

- [ ] **Step 3: ブラウザで骨格を確認**

  `products/restaurant-reservation.html` をブラウザで開いてヘッダー・フッターが表示されることを確認

---

## Task 3: ヒーローセクションを実装

**Files:**
- Modify: `products/restaurant-reservation.html`（`<main>` 内に追加）

- [ ] **Step 1: ヒーロー用CSSを `<style>` ブロックに追加**

  `/* placeholder: sections will be added in subsequent tasks */` の直前に挿入：

  ```css
  /* === HERO === */
  .hero {
    background: linear-gradient(160deg, var(--dark) 0%, #0d1b3e 100%);
    color: white; padding: 100px 0 80px; position: relative; overflow: hidden;
  }
  .hero::before {
    content: ''; position: absolute; inset: 0;
    background-image:
      linear-gradient(rgba(37,99,235,0.06) 1px, transparent 1px),
      linear-gradient(90deg, rgba(37,99,235,0.06) 1px, transparent 1px);
    background-size: 56px 56px; pointer-events: none;
  }
  .hero-inner { position: relative; z-index: 1; max-width: 720px; }
  .hero-kicker {
    display: inline-block; font-size: 11px; font-weight: 700;
    letter-spacing: .14em; color: var(--violet-light);
    border: 1px solid rgba(167,139,250,.3); border-radius: 20px;
    padding: 4px 14px; margin-bottom: 24px;
  }
  .hero h1 {
    font-size: clamp(28px, 5vw, 48px); font-weight: 900; line-height: 1.2;
    letter-spacing: -.03em; margin-bottom: 20px;
  }
  .hero h1 em { font-style: normal; color: var(--violet-light); }
  .hero-sub { font-size: 16px; color: #94a3b8; line-height: 1.8; margin-bottom: 32px; max-width: 560px; }
  .hero-badges { display: flex; flex-wrap: wrap; gap: 10px; margin-bottom: 36px; }
  .hero-badge {
    font-size: 12px; font-weight: 700; color: rgba(255,255,255,.7);
    background: rgba(255,255,255,.07); border: 1px solid rgba(255,255,255,.12);
    border-radius: 20px; padding: 5px 14px;
  }
  .btn-line {
    display: inline-flex; align-items: center; gap: 8px;
    background: var(--green-line); color: white; font-weight: 700; font-size: 16px;
    padding: 16px 32px; border-radius: 10px; transition: opacity 0.15s;
  }
  .btn-line:hover { opacity: 0.85; }
  .btn-sub { font-size: 12px; color: var(--gray-light); margin-top: 12px; }
  ```

- [ ] **Step 2: ヒーローHTMLを `<main>` 内に追加**

  `<!-- sections inserted in Tasks 3-8 -->` を以下で置換：

  ```html
  <!-- HERO -->
  <section class="hero">
    <div class="container">
      <div class="hero-inner">
        <span class="hero-kicker">飲食店向け 予約システム</span>
        <h1>ネット予約を、<br><em>あなたの店専用に</em><br>最短3日で作ります。</h1>
        <p class="hero-sub">既存の大手SaaSと違い、席・時間・ルールをすべて御社に合わせてカスタム設定します。テンプレートではなく、あなたの店のためだけに作るシステムです。</p>
        <div class="hero-badges">
          <span class="hero-badge">💰 月¥6,000〜</span>
          <span class="hero-badge">⚡ 最短3日稼働</span>
          <span class="hero-badge">✅ 強引な営業なし</span>
          <span class="hero-badge">🔧 フルカスタム対応</span>
        </div>
        <a href="https://lin.ee/XXXXXXX" class="btn-line">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M19.365 9.863c.349 0 .63.285.63.631 0 .345-.281.63-.63.63H17.61v1.125h1.755c.349 0 .63.283.63.63 0 .344-.281.629-.63.629h-2.386c-.345 0-.627-.285-.627-.629V8.108c0-.345.282-.63.63-.63h2.386c.346 0 .627.285.627.63 0 .349-.281.63-.63.63H17.61v1.125h1.755zm-3.855 3.016c0 .27-.174.51-.432.596-.064.021-.133.031-.199.031-.211 0-.391-.09-.51-.25l-2.443-3.317v2.94c0 .344-.279.629-.631.629-.346 0-.626-.285-.626-.629V8.108c0-.27.173-.51.43-.595.06-.023.136-.033.194-.033.195 0 .375.104.495.254l2.462 3.33V8.108c0-.345.282-.63.63-.63.345 0 .63.285.63.63v4.771zm-5.741 0c0 .344-.282.629-.631.629-.345 0-.627-.285-.627-.629V8.108c0-.345.282-.63.63-.63.346 0 .628.285.628.63v4.771zm-2.466.629H4.917c-.345 0-.63-.285-.63-.629V8.108c0-.345.285-.63.63-.63.348 0 .63.285.63.63v4.141h1.756c.348 0 .629.283.629.63 0 .344-.282.629-.629.629M24 10.314C24 4.943 18.615.572 12 .572S0 4.943 0 10.314c0 4.811 4.27 8.842 10.035 9.608.391.082.923.258 1.058.59.12.301.079.766.038 1.08l-.164 1.02c-.045.301-.24 1.186 1.049.645 1.291-.539 6.916-4.078 9.436-6.975C23.176 14.393 24 12.458 24 10.314"/></svg>
          LINEで無料相談（0円）
        </a>
        <p class="btn-sub">相談だけでも大丈夫です。しつこい営業は一切しません。</p>
      </div>
    </div>
  </section>

  <!-- sections: pain, features, proof, pricing, cta inserted in Tasks 4-8 -->
  ```

- [ ] **Step 3: ブラウザ確認**

  ページをリロードしてヒーローセクションが正しく表示されること（ダーク背景、グリッドパターン、コピー・バッジ・LINEボタン）を確認

---

## Task 4: 課題共感セクションを実装

**Files:**
- Modify: `products/restaurant-reservation.html`

- [ ] **Step 1: 課題共感セクション用CSSを追加**

  ```css
  /* === PAIN SECTION === */
  .pain { background: var(--light); }
  .pain-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 20px; margin-top: 40px; }
  .pain-card {
    background: white; border-radius: var(--radius); padding: 28px 24px;
    border: 1px solid #e2e8f0; box-shadow: 0 2px 8px rgba(0,0,0,.04);
  }
  .pain-icon { font-size: 32px; margin-bottom: 12px; }
  .pain-card h3 { font-size: 16px; font-weight: 700; margin-bottom: 8px; color: var(--dark-2); }
  .pain-card p { font-size: 14px; color: var(--gray); line-height: 1.7; }
  .pain-bridge {
    margin-top: 48px; text-align: center;
    font-size: clamp(18px, 3vw, 24px); font-weight: 900; color: var(--dark-2);
  }
  .pain-bridge em { font-style: normal; color: var(--blue); }
  ```

- [ ] **Step 2: 課題共感セクションHTMLを追加**

  `<!-- sections: pain, features, proof, pricing, cta inserted in Tasks 4-8 -->` を以下で置換：

  ```html
  <!-- PAIN -->
  <section class="pain">
    <div class="container">
      <p class="section-kicker">こんな悩みありませんか</p>
      <h2 class="section-title">予約業務で<br>消えていく時間と機会</h2>
      <div class="pain-grid">
        <div class="pain-card">
          <div class="pain-icon">📞</div>
          <h3>電話が来るたびに手が止まる</h3>
          <p>ランチのピーク時間に予約電話。厨房から抜けて対応するたびに、料理のクオリティが落ちる。</p>
        </div>
        <div class="pain-card">
          <div class="pain-icon">📋</div>
          <h3>手書き台帳でダブルブッキング</h3>
          <p>紙の予約ノートを複数人で管理するうちに記入ミス。お客様にご迷惑をかけてしまう。</p>
        </div>
        <div class="pain-card">
          <div class="pain-icon">😰</div>
          <h3>定休日・貸切の管理が追いつかない</h3>
          <p>イベントや忘年会シーズンの貸切設定を電話で受け、カレンダーとの照合に毎回時間がかかる。</p>
        </div>
      </div>
      <p class="pain-bridge">PSLなら、<em>これをすべて解決できます。</em></p>
    </div>
  </section>

  <!-- sections: features, proof, pricing, cta inserted in Tasks 5-8 -->
  ```

- [ ] **Step 3: ブラウザ確認**

  課題共感セクションが白背景で3カードグリッド表示されること、「PSLなら、これをすべて解決できます。」の橋渡しコピーが表示されることを確認

---

## Task 5: 機能カード×ミニUIセクションを実装

**Files:**
- Modify: `products/restaurant-reservation.html`

- [ ] **Step 1: 機能カードセクション用CSSを追加**

  ```css
  /* === FEATURES === */
  .features { background: white; }
  .features-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 24px; margin-top: 48px; }
  .feature-card {
    background: var(--light); border-radius: var(--radius); padding: 24px;
    border: 1px solid #e2e8f0;
  }
  .feature-top { display: flex; align-items: center; gap: 10px; margin-bottom: 8px; }
  .feature-icon { font-size: 24px; }
  .feature-card h3 { font-size: 15px; font-weight: 700; color: var(--dark-2); }
  .feature-card > p { font-size: 13px; color: var(--gray); margin-bottom: 14px; line-height: 1.6; }

  /* mini UI previews */
  .mini-ui { border-radius: 8px; padding: 12px; font-size: 11px; }
  .mini-ui--blue { background: var(--blue-light); }
  .mini-ui--green { background: #f0fdf4; }
  .mini-ui--amber { background: #fffbeb; }
  .mini-ui--violet { background: #f5f3ff; }
  .mini-ui-title { font-size: 10px; font-weight: 700; color: #1e40af; margin-bottom: 6px; }
  .mini-ui-title--green { color: #166534; }
  .mini-ui-title--amber { color: #92400e; }
  .mini-ui-title--violet { color: #5b21b6; }
  .mini-ui-row { color: #475569; margin-bottom: 2px; }
  .mini-cal { display: grid; grid-template-columns: repeat(7, 1fr); gap: 2px; text-align: center; }
  .mini-cal-head { font-size: 9px; color: #94a3b8; padding: 2px 0; }
  .mini-cal-day { font-size: 10px; color: #334155; padding: 2px; border-radius: 3px; }
  .mini-cal-day--today { background: var(--blue); color: white; font-weight: 700; }
  .mini-cal-day--near { background: #dbeafe; color: #1e40af; font-weight: 700; }
  ```

- [ ] **Step 2: 機能カードセクションHTMLを追加**

  `<!-- sections: features, proof, pricing, cta inserted in Tasks 5-8 -->` を以下で置換：

  ```html
  <!-- FEATURES -->
  <section class="features">
    <div class="container">
      <p class="section-kicker">機能紹介</p>
      <h2 class="section-title">こんな画面で<br>管理できます</h2>
      <p class="section-sub">全てあなたの店のルールに合わせて設定します。テンプレートの制限はありません。</p>
      <div class="features-grid">

        <!-- 機能1 -->
        <div class="feature-card">
          <div class="feature-top">
            <span class="feature-icon">📅</span>
            <h3>ネット予約管理</h3>
          </div>
          <p>お客様がスマホから24時間予約。管理画面で全予約を一覧確認できます。</p>
          <div class="mini-ui mini-ui--blue">
            <div class="mini-ui-title">本日の予約（6/8 日）</div>
            <div class="mini-ui-row">14:00 山田 様 ／ 4名 ／ テーブル席</div>
            <div class="mini-ui-row">18:00 田中 様 ／ 2名 ／ カウンター</div>
            <div class="mini-ui-row">19:30 佐藤 様 ／ 6名 ／ 座敷</div>
          </div>
        </div>

        <!-- 機能2 -->
        <div class="feature-card">
          <div class="feature-top">
            <span class="feature-icon">🗓</span>
            <h3>月間カレンダー表示</h3>
          </div>
          <p>月単位で予約の埋まり具合を一目で把握。定休日・臨時休業も自動反映。</p>
          <div class="mini-ui mini-ui--green">
            <div class="mini-ui-title mini-ui-title--green">2026年 6月</div>
            <div class="mini-cal">
              <div class="mini-cal-head">月</div><div class="mini-cal-head">火</div><div class="mini-cal-head">水</div>
              <div class="mini-cal-head">木</div><div class="mini-cal-head">金</div><div class="mini-cal-head">土</div><div class="mini-cal-head">日</div>
              <div class="mini-cal-day">2</div><div class="mini-cal-day">3</div><div class="mini-cal-day">4</div>
              <div class="mini-cal-day">5</div><div class="mini-cal-day mini-cal-day--near">6</div>
              <div class="mini-cal-day">7</div><div class="mini-cal-day mini-cal-day--today">8</div>
              <div class="mini-cal-day">9</div><div class="mini-cal-day">10</div><div class="mini-cal-day">11</div>
              <div class="mini-cal-day">12</div><div class="mini-cal-day">13</div><div class="mini-cal-day">14</div><div class="mini-cal-day">15</div>
            </div>
          </div>
        </div>

        <!-- 機能3 -->
        <div class="feature-card">
          <div class="feature-top">
            <span class="feature-icon">🎉</span>
            <h3>貸切・イベント設定</h3>
          </div>
          <p>忘年会・歓送迎会シーズンの貸切期間と特別コースを管理画面から設定できます。</p>
          <div class="mini-ui mini-ui--amber">
            <div class="mini-ui-title mini-ui-title--amber">忘年会シーズン設定</div>
            <div class="mini-ui-row">📅 12/1〜12/28 貸切受付中</div>
            <div class="mini-ui-row">🍱 特別コース 3種設定済</div>
            <div class="mini-ui-row">👥 最大40名まで対応</div>
          </div>
        </div>

        <!-- 機能4 -->
        <div class="feature-card">
          <div class="feature-top">
            <span class="feature-icon">📱</span>
            <h3>スマホ・タブレット対応</h3>
          </div>
          <p>管理画面はスマホ・iPadに最適化。外出先からでも予約状況を確認できます。</p>
          <div class="mini-ui mini-ui--violet">
            <div class="mini-ui-title mini-ui-title--violet">どこからでも確認可能</div>
            <div class="mini-ui-row">📱 iPhone / Android 対応</div>
            <div class="mini-ui-row">🖥 iPad・PCでも快適</div>
            <div style="margin-top:8px;background:linear-gradient(90deg,#7c3aed,#4f46e5);border-radius:4px;padding:6px;text-align:center;color:white;font-size:10px;font-weight:700;">管理画面を開く</div>
          </div>
        </div>

      </div>
    </div>
  </section>

  <!-- sections: proof, pricing, cta inserted in Tasks 6-8 -->
  ```

- [ ] **Step 3: ブラウザ確認**

  4枚のカードグリッドが表示され、各カード内にミニUIプレビューが見えること

---

## Task 6: 実績・信頼セクションを実装

**Files:**
- Modify: `products/restaurant-reservation.html`

- [ ] **Step 1: 実績セクション用CSSを追加**

  ```css
  /* === PROOF === */
  .proof { background: var(--dark-2); color: white; }
  .proof .section-kicker { color: var(--violet-light); }
  .proof .section-title { color: white; }
  .proof .section-sub { color: var(--gray-light); }
  .proof-badge {
    display: inline-flex; align-items: center; gap: 8px;
    background: rgba(74,222,128,.1); border: 1px solid rgba(74,222,128,.3);
    border-radius: 8px; padding: 10px 20px; margin: 24px 0 32px;
    font-size: 14px; font-weight: 700; color: #4ade80;
  }
  .proof-list { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 16px; }
  .proof-item {
    display: flex; align-items: flex-start; gap: 12px;
    background: rgba(255,255,255,.05); border-radius: 10px; padding: 18px 20px;
  }
  .proof-check { font-size: 18px; flex-shrink: 0; }
  .proof-item-text h4 { font-size: 14px; font-weight: 700; margin-bottom: 4px; }
  .proof-item-text p { font-size: 13px; color: var(--gray-light); line-height: 1.6; }
  .proof-callout {
    margin-top: 40px; padding: 24px 28px;
    background: rgba(37,99,235,.12); border: 1px solid rgba(37,99,235,.3);
    border-radius: var(--radius);
    font-size: 15px; font-weight: 700; color: #93c5fd; line-height: 1.7;
  }
  ```

- [ ] **Step 2: 実績・信頼セクションHTMLを追加**

  `<!-- sections: proof, pricing, cta inserted in Tasks 6-8 -->` を以下で置換：

  ```html
  <!-- PROOF -->
  <section class="proof">
    <div class="container">
      <p class="section-kicker">実績・信頼</p>
      <h2 class="section-title">実際に<br>稼働しています</h2>
      <div class="proof-badge">
        <span>✅</span> 実店舗テスト稼働中 2026年〜
      </div>
      <div class="proof-list">
        <div class="proof-item">
          <span class="proof-check">🪑</span>
          <div class="proof-item-text">
            <h4>席種別管理</h4>
            <p>テーブル・カウンター・座敷・個室など、店舗独自の席区分をそのまま設定</p>
          </div>
        </div>
        <div class="proof-item">
          <span class="proof-check">🐾</span>
          <div class="proof-item-text">
            <h4>ペット同伴可/不可の区分設定</h4>
            <p>ペット可エリアと一般エリアを分けて予約受付できます</p>
          </div>
        </div>
        <div class="proof-item">
          <span class="proof-check">📆</span>
          <div class="proof-item-text">
            <h4>定休日・臨時休業の自動反映</h4>
            <p>管理画面で設定するだけ。ゲスト側には予約不可日として自動表示</p>
          </div>
        </div>
        <div class="proof-item">
          <span class="proof-check">🎉</span>
          <div class="proof-item-text">
            <h4>貸切・イベントコース設定</h4>
            <p>通常予約と貸切予約を切り替え。特別コースの価格設定も可能</p>
          </div>
        </div>
        <div class="proof-item">
          <span class="proof-check">👥</span>
          <div class="proof-item-text">
            <h4>人数制限・最大予約枠</h4>
            <p>1テーブルの最大人数や、1日の予約上限を店舗独自のルールで設定</p>
          </div>
        </div>
        <div class="proof-item">
          <span class="proof-check">⏰</span>
          <div class="proof-item-text">
            <h4>時間帯ごとの営業設定</h4>
            <p>ランチ・ディナーの時間帯を分けた予約受付、曜日ごとの営業時間変更に対応</p>
          </div>
        </div>
      </div>
      <div class="proof-callout">
        大手SaaSでは「設定できない」と言われることを、<br>PSLは全てカスタムで対応します。
      </div>
    </div>
  </section>

  <!-- sections: pricing, cta inserted in Tasks 7-8 -->
  ```

- [ ] **Step 3: ブラウザ確認**

  ダーク背景に稼働バッジ・6項目グリッド・青い吹き出しが表示されること

---

## Task 7: 料金・導入フローセクションを実装

**Files:**
- Modify: `products/restaurant-reservation.html`

- [ ] **Step 1: 料金・フローセクション用CSSを追加**

  ```css
  /* === PRICING === */
  .pricing { background: var(--light); }
  .pricing-cards { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 20px; margin-top: 40px; }
  .pricing-card {
    background: white; border-radius: var(--radius); padding: 28px 24px;
    border: 1px solid #e2e8f0; box-shadow: 0 2px 8px rgba(0,0,0,.04);
    text-align: center;
  }
  .pricing-card.featured { border-color: var(--blue); box-shadow: 0 0 0 3px rgba(37,99,235,.1); }
  .pricing-label { font-size: 12px; font-weight: 700; color: var(--gray); margin-bottom: 8px; }
  .pricing-amount { font-size: 36px; font-weight: 900; color: var(--dark-2); letter-spacing: -.03em; }
  .pricing-amount span { font-size: 14px; font-weight: 400; color: var(--gray); }
  .pricing-desc { font-size: 13px; color: var(--gray); margin-top: 8px; line-height: 1.6; }
  .pricing-note { margin-top: 20px; font-size: 13px; color: var(--gray); text-align: center; }

  /* flow steps */
  .flow { margin-top: 60px; }
  .flow-title { font-size: 18px; font-weight: 700; margin-bottom: 28px; }
  .flow-steps { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 0; position: relative; }
  .flow-steps::before {
    content: ''; position: absolute; top: 28px; left: 0; right: 0; height: 2px;
    background: linear-gradient(90deg, var(--blue), var(--violet));
  }
  .flow-step { text-align: center; padding: 0 16px; position: relative; }
  .flow-num {
    width: 56px; height: 56px; border-radius: 50%;
    background: linear-gradient(135deg, var(--blue), var(--violet));
    color: white; font-size: 18px; font-weight: 900;
    display: flex; align-items: center; justify-content: center;
    margin: 0 auto 16px; position: relative; z-index: 1;
    box-shadow: 0 4px 12px rgba(37,99,235,.3);
  }
  .flow-step h4 { font-size: 14px; font-weight: 700; margin-bottom: 4px; }
  .flow-step p { font-size: 12px; color: var(--gray); line-height: 1.6; }
  ```

- [ ] **Step 2: 料金・フローセクションHTMLを追加**

  `<!-- sections: pricing, cta inserted in Tasks 7-8 -->` を以下で置換：

  ```html
  <!-- PRICING -->
  <section class="pricing">
    <div class="container">
      <p class="section-kicker">料金・導入の流れ</p>
      <h2 class="section-title">シンプルな料金体系、<br>最短3日で稼働</h2>
      <div class="pricing-cards">
        <div class="pricing-card">
          <div class="pricing-label">初期費用（一回限り）</div>
          <div class="pricing-amount">¥30,000<span>（税込¥33,000）</span></div>
          <div class="pricing-desc">システム構築・カスタム設定・初回サポートを含みます</div>
        </div>
        <div class="pricing-card featured">
          <div class="pricing-label">月額費用</div>
          <div class="pricing-amount">¥6,000<span>〜 / 月</span></div>
          <div class="pricing-desc">ホスティング・保守・小規模な変更対応を含みます</div>
        </div>
      </div>
      <p class="pricing-note">複数店舗・機能追加のご相談は別途お見積もりいたします。</p>

      <div class="flow">
        <div class="flow-title">申し込みから稼働まで</div>
        <div class="flow-steps">
          <div class="flow-step">
            <div class="flow-num">1</div>
            <h4>LINEで無料相談</h4>
            <p>店舗のルール・希望をヒアリング</p>
          </div>
          <div class="flow-step">
            <div class="flow-num">2</div>
            <h4>お見積もり・確認</h4>
            <p>3営業日以内にご連絡</p>
          </div>
          <div class="flow-step">
            <div class="flow-num">3</div>
            <h4>開発・設定</h4>
            <p>最短3日でシステム構築</p>
          </div>
          <div class="flow-step">
            <div class="flow-num">4</div>
            <h4>稼働開始</h4>
            <p>テスト確認後、本番リリース</p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- section: cta inserted in Task 8 -->
  ```

- [ ] **Step 3: ブラウザ確認**

  料金カード2枚（初期・月額）と4ステップのフロー図が正しく表示されること

---

## Task 8: CTAセクションを実装・全体レスポンシブ調整

**Files:**
- Modify: `products/restaurant-reservation.html`

- [ ] **Step 1: CTAセクション用CSSとレスポンシブを追加**

  ```css
  /* === CTA === */
  .cta-section {
    background: linear-gradient(160deg, var(--dark) 0%, #0d1b3e 100%);
    color: white; text-align: center; padding: 100px 24px;
  }
  .cta-section .section-kicker { color: var(--violet-light); }
  .cta-title { font-size: clamp(24px, 4vw, 40px); font-weight: 900; line-height: 1.25; margin-bottom: 16px; }
  .cta-sub { font-size: 15px; color: var(--gray-light); line-height: 1.8; margin-bottom: 40px; max-width: 520px; margin-left: auto; margin-right: auto; }
  .cta-note { font-size: 13px; color: var(--gray); margin-top: 16px; }

  /* === RESPONSIVE === */
  @media (max-width: 600px) {
    section { padding: 60px 0; }
    .hero { padding: 80px 0 60px; }
    .flow-steps::before { display: none; }
    .flow-steps { gap: 24px; }
  }
  ```

- [ ] **Step 2: CTAセクションHTMLを追加**

  `<!-- section: cta inserted in Task 8 -->` を以下で置換：

  ```html
  <!-- CTA -->
  <section class="cta-section">
    <div class="container">
      <p class="section-kicker">無料相談受付中</p>
      <h2 class="cta-title">まずは、<br>話を聞くだけでも大丈夫です。</h2>
      <p class="cta-sub">強引な営業は一切しません。ご要望をお聞きし、合わなければそれで終わりです。「自分の店に合うか知りたい」だけでもお気軽にどうぞ。</p>
      <a href="https://lin.ee/XXXXXXX" class="btn-line" style="font-size:18px;padding:20px 40px;display:inline-flex;margin:0 auto;">
        <svg width="22" height="22" viewBox="0 0 24 24" fill="currentColor"><path d="M19.365 9.863c.349 0 .63.285.63.631 0 .345-.281.63-.63.63H17.61v1.125h1.755c.349 0 .63.283.63.63 0 .344-.281.629-.63.629h-2.386c-.345 0-.627-.285-.627-.629V8.108c0-.345.282-.63.63-.63h2.386c.346 0 .627.285.627.63 0 .349-.281.63-.63.63H17.61v1.125h1.755zm-3.855 3.016c0 .27-.174.51-.432.596-.064.021-.133.031-.199.031-.211 0-.391-.09-.51-.25l-2.443-3.317v2.94c0 .344-.279.629-.631.629-.346 0-.626-.285-.626-.629V8.108c0-.27.173-.51.43-.595.06-.023.136-.033.194-.033.195 0 .375.104.495.254l2.462 3.33V8.108c0-.345.282-.63.63-.63.345 0 .63.285.63.63v4.771zm-5.741 0c0 .344-.282.629-.631.629-.345 0-.627-.285-.627-.629V8.108c0-.345.282-.63.63-.63.346 0 .628.285.628.63v4.771zm-2.466.629H4.917c-.345 0-.63-.285-.63-.629V8.108c0-.345.285-.63.63-.63.348 0 .63.285.63.63v4.141h1.756c.348 0 .629.283.629.63 0 .344-.282.629-.629.629M24 10.314C24 4.943 18.615.572 12 .572S0 4.943 0 10.314c0 4.811 4.27 8.842 10.035 9.608.391.082.923.258 1.058.59.12.301.079.766.038 1.08l-.164 1.02c-.045.301-.24 1.186 1.049.645 1.291-.539 6.916-4.078 9.436-6.975C23.176 14.393 24 12.458 24 10.314"/></svg>
        LINEで無料相談を始める
      </a>
      <p class="cta-note">営業時間内に返信 ／ 秘密厳守 ／ 相談だけでも歓迎</p>
    </div>
  </section>
  ```

- [ ] **Step 3: 全体をブラウザで最終確認**

  - ヘッダー固定表示
  - ヒーロー → 課題共感 → 機能カード → 実績 → 料金・フロー → CTA の順に6セクション表示
  - スマホ幅（375px）でも崩れないこと
  - 全リンクが外部本番URLを含まないこと

- [ ] **Step 4: 外部URLが残っていないか確認**

  ```bash
  grep -n "onrender.com\|pumpstack-lab.github.io\|lin.ee" products/restaurant-reservation.html
  ```

  Expected: `lin.ee` のみ（LINE公式URL）、`onrender.com` / `pumpstack-lab.github.io` は0件

  > 注: `lin.ee/XXXXXXX` はLINE公式アカウントのURL。実際のURLをオーナーに確認して差し替えること。

---

## Task 9: Impeccable critique 実施・指摘修正

**Files:**
- Modify: `products/restaurant-reservation.html`, `index.html`（指摘に応じて）

- [ ] **Step 1: Impeccable critique を実行**

  ```
  Skill("impeccable") → critique → 対象: products/restaurant-reservation.html, index.html
  ```

- [ ] **Step 2: 重大指摘を修正**

  critiqに対して重大度「高」の指摘を全て修正する

- [ ] **Step 3: 修正後ブラウザ再確認**

---

## Task 10: PSL push前チェックリスト全実行・push

**Files:** なし（確認作業）

- [ ] **Step 1: verification-before-completion**
  ```
  Skill("superpowers:verification-before-completion")
  ```

- [ ] **Step 2: ネイト精査**
  ```
  Read("~/.claude/skills/psl-nate-review.md") → 内容通りに実行 → 結果をオーナーに報告
  ```

- [ ] **Step 3: code-review**
  ```
  Skill("superpowers:requesting-code-review")
  ```

- [ ] **Step 4: git add & commit**
  ```bash
  git add products/restaurant-reservation.html index.html
  git commit -m "feat: add restaurant reservation product detail page, remove demo direct links"
  ```

- [ ] **Step 5: finishing-a-development-branch**
  ```
  Skill("superpowers:finishing-a-development-branch")
  ```

- [ ] **Step 6: push（オーナー承認後）**
  ```bash
  git push
  ```

---

## スペックカバレッジ確認

| スペック要件 | 対応タスク |
|------------|----------|
| LP直リンク全廃止（4件） | Task 1 |
| 飲食店カードに詳細ページリンク追加 | Task 1 |
| products/restaurant-reservation.html 新規作成 | Task 2 |
| ヒーロー（コピーC・ダーク背景） | Task 3 |
| 課題共感セクション | Task 4 |
| 機能カード×ミニUIプレビュー4枚 | Task 5 |
| 実績・信頼セクション | Task 6 |
| 料金・導入フロー | Task 7 |
| CTA（ダーク背景・LINEボタン） | Task 8 |
| Impeccable critique | Task 9 |
| Nate精査・push前チェックリスト | Task 10 |
