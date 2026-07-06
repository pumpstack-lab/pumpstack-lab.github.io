# TableStack 1枚紙＋LPライト改修 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 外販予約サービス「TableStack」の店舗配布用A4両面1枚紙（PDF）を作り、LPをライト改修（CTA2段階化・成果コピー・FAQ・差別化カード・TableStack名称反映）して1回のpushで公開する。

**Architecture:** 静的サイト（GitHub Pages・シングルファイルHTML群）。1枚紙は印刷CSS付きHTML→Chrome headlessでPDF化し、`assets/` に置いてヒーローCTAからリンク。テストは pytest なし＝ローカルサーバー目視＋PDF実寸確認＋オーナーOKゲートで代替。

**Tech Stack:** HTML/CSS（既存デザイントークン踏襲）・segno（QR生成・作業用単発）・Chrome headless（PDF化）

**Spec:** `docs/superpowers/specs/2026-07-04-tablestack-onepager-lp-light-update-design.md`

---

### Task 1: LINE QRコード生成

**Files:**
- Create: `assets/line-qr.svg`

- [ ] **Step 1: segnoを導入しQR生成**

```bash
cd /Users/Yutalow420/Desktop/pumpstack-lab.github.io && mkdir -p assets
pip3 install --user --quiet segno
python3 -c "
import segno
qr = segno.make('https://line.me/R/ti/p/@425ukgwa', error='m')
qr.save('assets/line-qr.svg', scale=10, dark='#0a0f1e', border=2)
print('OK:', qr.designator)
"
```
Expected: `OK: <バージョン>-M` が出力され `assets/line-qr.svg` が生成される。

- [ ] **Step 2: QRをスマホ実機で読み取り確認（オーナー確認時にまとめて実施でも可・PDF内で最終確認するためここでは生成のみ）**

---

### Task 2: 1枚紙HTML作成（A4両面・全文コピー確定版）

**Files:**
- Create: `assets/tablestack-onepager.html`

- [ ] **Step 1: 以下の完全な内容でファイルを作成**

コピーの原則：状態変化で書く／実態ベースの数字のみ／税抜表記。全文は以下（実装時はこのまま使用。微調整はネイト精査の指摘があった場合のみ）。

**表面（Page 1）の内容:**
- ヘッダー: PSLロゴ＋「by PumpStack Lab.」
- 商品名: TableStack（テーブルスタック）／キッカー「飲食店向け 予約システム」
- キャッチ: **予約の電話、鳴らなくなります。**
- リード: 営業中に鳴り続ける予約電話、手書き台帳のダブルブッキング、大手サイトの手数料。TableStackは、小さなお店のための「自分の店専用」予約システムです。
- こんなお困りごと、ありませんか？（3点）
  1. ピークタイムに予約電話が鳴って、調理・接客の手が止まる
  2. 手書き台帳で、ダブルブッキングや記入漏れが起きたことがある
  3. 大手グルメサイトの送客手数料・掲載料が重い
- TableStackを入れると、こう変わります（4点）
  1. 予約はお客様がスマホから24時間自分で入れる——電話対応が減ります
  2. 新しい予約はお店のLINEに自動で届く——スマホを見るだけ
  3. 重複や営業時間外の予約は、システムが自動でブロック
  4. 送客手数料ゼロ。月額固定だから、予約が増えても費用は同じ
- 下部帯: 福岡県内の飲食店で本番稼働中。現場の声から生まれたシステムです。

**裏面（Page 2）の内容:**
- できること（主要機能6点・実機能のみ）: Web予約フォーム（店の席数・営業時間・定休日に完全対応）／LINE自動通知／人数に応じた自動席確保／席移動・時間変更・キャンセル対応（重複・営業時間外チェック付き）／顧客リストでリピーターがわかる／月間カレンダー・貸切・イベント設定
- 料金: 初期費用 ¥30,000 ＋ 月額 ¥6,000〜（税抜）／送客手数料なし／相談・見積もり無料
- PSLが選ばれる理由（2点）: **担当者は、開発者本人です**（営業・サポート・開発が分かれていないので、話が早い）／**ヒアリングから最短3日で導入**（設定は全部PSLがやります）
- よくある質問（3問）:
  - Q. 料金は？ → A. TableStackは初期¥30,000＋月額¥6,000〜（税抜）。テイクアウト受付・売上集計などその他のツールは、ヒアリング後に無料でお見積りします。
  - Q. 契約の縛りや、しつこい営業はありませんか？ → A. ありません。最低契約期間なし。「話を聞くだけ」も歓迎です。
  - Q. 機械が苦手でも大丈夫？ → A. 席数・営業時間・メニューの設定はすべてPSLが行います。導入後もLINEでいつでもサポートします。
- CTA（右下にQR）: まずはLINEで無料相談（QR＝`line-qr.svg`）／メール pumpstack.lab.2026@gmail.com／強引な営業は一切しません。

**実装仕様:**
- `@page { size: A4; margin: 0; }`、`.page { width: 210mm; height: 296mm; padding: 13mm 14mm; page-break-after: always; overflow: hidden; }`
- 配色: 白基調・見出し `#0a0f1e`・アクセント `#2563eb`／`#7c3aed`・ボックス背景 `#eff6ff`。本文グレーは印刷で薄くならないよう `#475569` 以上の濃度
- フォント: `'Noto Sans JP','Hiragino Sans',sans-serif`（Google Fonts link付き・オフライン時はヒラギノにフォールバック）
- ロゴ参照: `../logo.png`（assets/からの相対）

- [ ] **Step 2: ブラウザで開いてレイアウト崩れがないか確認**

```bash
open /Users/Yutalow420/Desktop/pumpstack-lab.github.io/assets/tablestack-onepager.html
```

---

### Task 3: PDF生成

**Files:**
- Create: `assets/tablestack-onepager.pdf`

- [ ] **Step 1: Chrome headlessでPDF化**

```bash
cd /Users/Yutalow420/Desktop/pumpstack-lab.github.io
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless --disable-gpu \
  --no-pdf-header-footer \
  --print-to-pdf="assets/tablestack-onepager.pdf" \
  "file://$PWD/assets/tablestack-onepager.html"
```
Expected: `assets/tablestack-onepager.pdf`（2ページ）が生成される。

- [ ] **Step 2: PDFを開いて2ページ・文字切れなしを確認**

```bash
open assets/tablestack-onepager.pdf
```

- [ ] **Step 3: Commit**

```bash
git add assets/ && git commit -m "feat: TableStack店舗配布用1枚紙（A4両面PDF＋ソースHTML・LINE QR）"
```

---

### Task 4: index.html ライト改修（6編集）

**Files:**
- Modify: `index.html`

- [ ] **Step 1: meta description更新（7行目）**

`予約システム・業務ツール・HP制作` → `予約システム「TableStack」・業務ツール・HP制作`

- [ ] **Step 2: ヒーローCTA差し替え＋実績リンク退避（453-458行付近・477行付近）**

置換前:
```html
      <a href="#gallery" class="btn-outline" style="font-size:14px;padding:14px 28px;opacity:0.7;">稼働実績を見る ↓</a>
```
置換後:
```html
      <a href="assets/tablestack-onepager.pdf" class="btn-outline" target="_blank">サービス資料を見る（PDF）</a>
```
hero-note置換前:
```html
    <p class="hero-note">強引な営業は一切しません</p>
```
置換後:
```html
    <p class="hero-note">強引な営業は一切しません&nbsp;／&nbsp;<a href="#gallery" style="color:#475569;text-decoration:underline;">稼働実績を見る ↓</a></p>
```

- [ ] **Step 3: ヒーローサブコピーを状態変化型に（449-451行付近）**

置換前:
```html
      予約管理・業務効率化——<br>現場の声をそのままツールにしてきました。
```
置換後:
```html
      予約の電話を減らす。紙の記録をなくす。<br>現場の声を、そのままツールにしてきました。
```

- [ ] **Step 4: 業種ブロックに成果1行追加（CSS＋HTML2箇所）**

CSSに追加（`.industry-icon` ルールの直後）:
```css
    .industry-lead { font-size: 13px; color: var(--gray); margin: 12px 0 16px; }
```
飲食ラベル直後に挿入:
```html
      <p class="industry-lead">予約の電話とダブルブッキングを、システムが肩代わりします。</p>
```
サロン・消防・福祉ラベル直後に挿入:
```html
      <p class="industry-lead">点検票・日報・在庫管理——紙とExcelの手間を、現場から減らします。</p>
```

- [ ] **Step 5: TableStack名称反映（featuredカード・ロードマップ）**

置換前: `<h3>飲食店予約システム</h3>`
置換後: `<h3>TableStack<span style="font-size:13px;font-weight:500;color:#94a3b8;">（テーブルスタック）</span>｜飲食店予約システム</h3>`

ロードマップ置換前: `<strong>飲食店予約システム</strong>`
置換後: `<strong>TableStack（飲食店予約システム）</strong>`

- [ ] **Step 6: FAQセクション新設（CSSと、`<!-- CTA -->` 直前にHTML）**

CSSに追加（FLOWセクションのCSSの後）:
```css
    /* ===== FAQ ===== */
    .faq-section { background: white; }
    .faq-list { margin-top: 40px; display: flex; flex-direction: column; gap: 12px; max-width: 760px; }
    .faq-item { border: 1px solid #e2e8f0; border-radius: var(--radius); padding: 20px 24px; }
    .faq-item summary { font-size: 15px; font-weight: 700; cursor: pointer; list-style: none; display: flex; gap: 10px; align-items: baseline; }
    .faq-item summary::-webkit-details-marker { display: none; }
    .faq-item summary::before { content: 'Q.'; color: var(--blue); font-weight: 800; flex-shrink: 0; }
    .faq-item[open] summary { margin-bottom: 10px; }
    .faq-item p { font-size: 14px; color: var(--gray); line-height: 1.85; padding-left: 26px; }
```
HTML（`<!-- CTA -->` 直前）:
```html
<!-- FAQ -->
<section class="faq-section" id="faq">
  <div class="container">
    <div class="gallery-kicker">よくある質問</div>
    <h2 class="section-title">気になることに、先にお答えします。</h2>
    <div class="faq-list">
      <details class="faq-item" open>
        <summary>料金はいくらですか？</summary>
        <p>予約受付システム「TableStack」は初期費用¥30,000＋月額¥6,000〜（税抜）・送客手数料なしです。その他のツールは、ヒアリング後に無料でお見積りします。相談・見積もりだけでも無料です。</p>
      </details>
      <details class="faq-item">
        <summary>契約の縛りや、しつこい営業はありませんか？</summary>
        <p>ありません。最低契約期間はなく、「話を聞くだけ」も歓迎です。合わないと感じたら、そのまま断っていただいて大丈夫です。</p>
      </details>
      <details class="faq-item">
        <summary>導入後はどこまで対応してもらえますか？</summary>
        <p>席数・営業時間・メニューなどの初期設定はすべてPSLが行います。納品後の使い方相談・修正のご希望も、LINEでそのままサポートします。</p>
      </details>
    </div>
  </div>
</section>
```

- [ ] **Step 7: 「選ばれる理由」4枚目カード追加（03カードの直後）**

```html
      <div class="why-card">
        <div class="why-num">04</div>
        <h3>担当者は、開発者本人です</h3>
        <p>営業・サポート・開発が分かれていません。ご相談は作った本人にそのまま届くので、話が早く、対応が正確です。</p>
      </div>
```

---

### Task 5: products/restaurant-reservation.html 名称反映（2編集）

**Files:**
- Modify: `products/restaurant-reservation.html:6`（title）、`:427`（hero-kicker）

- [ ] **Step 1: title置換**

置換前: `<title>飲食店予約システム｜PumpStack Lab.</title>`
置換後: `<title>TableStack（テーブルスタック）｜飲食店予約システム｜PumpStack Lab.</title>`

- [ ] **Step 2: hero-kicker置換**

置換前: `<span class="hero-kicker">飲食店向け 予約システム</span>`
置換後: `<span class="hero-kicker">TableStack — 飲食店向け予約システム</span>`

- [ ] **Step 3: Commit**

```bash
git add index.html products/restaurant-reservation.html
git commit -m "feat: LPライト改修（TableStack命名・資料CTA・成果コピー・FAQ・差別化カード）"
```

---

### Task 6: ローカル検証 → オーナー確認ゲート

- [ ] **Step 1: ローカルサーバー起動・PC/スマホ幅目視（Playwright）**

```bash
cd /Users/Yutalow420/Desktop/pumpstack-lab.github.io && python3 -m http.server 8765
```
Playwrightで `http://localhost:8765` を開き、①PC幅・②375px幅でスクリーンショット。確認項目: ヒーローCTA2本の表示／資料PDFリンクが開く／FAQ開閉動作／why 4枚目カードの折返し／業種成果行の表示。

- [ ] **Step 2: オーナーにプレビュー提示（LPスクショ＋1枚紙PDF）→ OKをもらう**

**ここで停止。オーナーOKなしに次へ進まない（稼働中LPルール）。**

---

### Task 7: push前チェックリスト完走 → push（オーナーOK後）

- [ ] Skill("superpowers:verification-before-completion")
- [ ] テスト: pytest対象なし（静的サイト）→ Task 6の実動作確認結果を報告に添える
- [ ] ネイト精査（誇張チェック含む・psl-nate-review.md）
- [ ] Skill("impeccable") critique（index.html・1枚紙HTML）→ 指摘修正
- [ ] security-review: 対象外（静的コンテンツのみ・個人情報/認証/DB変更なし）を報告に明記
- [ ] Skill("superpowers:requesting-code-review")
- [ ] 全項目✅をオーナーに報告 → Skill("superpowers:finishing-a-development-branch") → push
- [ ] push後: GitHub Pages反映確認（https://pumpstack-lab.github.io で資料PDFリンク動作）
