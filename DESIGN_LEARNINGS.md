# NORE Design Learnings

## 目的

bluechipペルソナは、価格を聞く前に決断できる40–60代の超富裕層コレクター。彼らに対しては「説明で売る」サイトは無効である。NOREでは、商業性をことごとく排し、美術館を訪れたときの静謐さそのものをWeb上に再現することを目指した。

このギャラリーは架空ブランドであり、実在のギャラリー・作家・作品ではない。

## 設計したこと

- 1作品ヒーロー、価格非表示、カート非搭載、モーダル禁止 — Web ECの定型を全て否定した。
- Enquire は独立ページに分離し、ボタンではなくページ遷移として扱った。
- 美術館ラベルを縦組（90°回転）でWebに翻訳し、画面の余白を最大化した。
- ナビは5項目に絞り、検索もフィルタも置かない。コレクターは目当てを持って来訪するという前提に立つ。
- スクロールに応じて作品が遠ざかる（zoom-out）演出で、画面そのものをホワイトキューブの壁面に見立てた。

## CSS

主要なCSS判断:

```css
:root {
  --bg: #ffffff;           /* pure museum white */
  --fg: #1a1a1a;           /* ink black */
  --accent: #5c1a1b;       /* deep oxblood, used <2% of area */
  --space-hero: clamp(8rem, 16vw, 14rem);
  --font-display: 'Bodoni Moda', 'Times New Roman', serif;
  --font-body: 'Inter', sans-serif;
}

/* museum label, side-rotated */
.work-caption {
  writing-mode: vertical-rl;
  letter-spacing: .25em;
  font-feature-settings: 'lnum' 1;
}

/* hero zoom-out tied to scroll */
.hero-work {
  transform: scale(calc(1 + var(--scroll-y) * -.0004));
  transform-origin: center top;
}
```

アクセント色はオックスブラッドを採用し、面積比2%以下に厳格に制限した。白の使い方が情報設計そのものになる。

## アニメーション

- ローダーなし。最初のフレームから完成形を見せる。
- 動きは最小限。reveal は使わず、スクロールに連動したzoom-outのみを許容した。
- ホバーで作品が動くなどの「インタラクションのご褒美」を一切排除し、紙の図録のような静けさを保った。

## フォント

- Display: `Bodoni Moda`（Didone系の高コントラスト・セリフ）
- Body: `Inter`（無印で読める無個性さを採用）

Bodoni Modaの細い縦画と分厚い水平セリフは、現代美術館の壁面サインに最も近い印象を作る。本文に個性を出すと美学が散らかるため、Interを選んだ。

## ボタン

NOREにはCTAボタンというものが存在しない。

「Enquire」「Visit」はすべてテキストリンク。下線さえ最小限の `text-underline-offset` で再設計し、典型的なWeb UIから遠ざけた。色も `currentColor` のみ。

## UI/UX

- ナビは5項目固定 — Works / Artists / Exhibitions / About / Enquire。
- 価格は店頭でも掲示しない、というギャラリーの実物の慣習を踏襲し、サイトでも非表示。
- Enquire はモーダル禁止。専用ページに遷移し、フォームではなく、メールアドレスを大きく1つ提示する。
- 作家紹介には「Represented since YYYY」のみ。コマーシャルな業績は書かない。

## レイアウト

縦組キャプションと作品の大きな余白で、画面そのものをホワイトキューブに見立てている。ヒーローは作品1点+作家名+制作年のみ。価格も技法も書かない。

スクロール挙動は緩く、急かさない。一度に1作品しか見えない設計で、コレクターが図録を1ページずつ繰る感覚を再現した。
