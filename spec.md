# NORE — design-art-gallery-bluechip Spec

**Status:** Approved
**Author:** torifo
**Created:** 2026-05-22
**Updated:** 2026-05-22

---

## 1. Overview

### Problem Statement
ブルーチップ・ギャラリー（Gagosian / Pace / Hauser & Wirth 級）のWebサイトは「美術館的な静謐さ」を要件としつつ、コレクターを次のアクション（展覧会訪問・カタログ請求・プライベートビューイング予約）へ導く必要がある。多くのサイトは前者に振り切るあまり「閲覧体験は美しいが何も起こさせない」状態に陥っているか、後者を優先して「商業的すぎて作品の格が落ちる」状態に陥っている。

### Goal
"NORE"（北極星のような響きを持つ造語）という架空のブルーチップ・ギャラリーのランディングページを実装し、**美術館級の静謐さ × 1作品=1スクロールの没入** × **抑制されたコレクター動線** が両立可能であることを検証する。

### Non-Goals
- EC機能・カート・即時購入
- ユーザー認証・マイページ
- リアルタイム入札（オークション機能）
- 多言語切替（英語のみ）

### Background
- NORE は本デザイン研究のために作成した架空ブランドであり、実在のギャラリー・アーティスト・作品ではない
- `design-art-gallery-bluechip` リポジトリ予定
- art-gallery シリーズ4部作の第1作（市場ハイエンド軸）
- 姉妹シリーズ: apparel (LUEUR/ARCH/FRAY/FORM), furniture (HVILE/VELA/BURL/BLOC)

---

## 2. Persona

| 属性 | 詳細 |
|------|------|
| 年齢 | 40–60代 |
| 職業 | エグゼクティブ・実業家・相続層・美術ファンドマネージャー |
| 資産 | 投資可能資産 $5M+、年間アート購入予算 $100K–$2M |
| 行動 | Art Basel / Frieze / FIAC を年4–6回巡回、TEFAF会員、Sotheby's/Christie's プレビュー常連 |
| 共鳴する価値 | プロヴェナンス（来歴）、学芸員のキュレーション、寡黙な権威、museum-quality |
| 嫌うもの | ポップアップ、過剰な動き、カート、価格の前面表示、「今すぐ」「在庫残り◯点」的訴求 |
| 情報源 | Art Newspaper, Artforum, Frieze, ARTnews 印刷版 |

---

## 3. User Stories

| ID | Persona | Want to | So that |
|----|---------|---------|---------|
| US-01 | コレクター | 開いた瞬間にギャラリーの格と取扱作家の重みを感じたい | 「ここは本物だ」と確信し、フェアで足を運ぶ判断材料にしたい |
| US-02 | 同上 | 現在の展覧会の中心作品を、美術館鑑賞のような余白の中で見たい | 自宅・自室に置いた時の存在感を想像できる |
| US-03 | 同上 | アーティストの来歴と所蔵歴を読みたい | 投資判断、コレクション全体との整合性を検討できる |
| US-04 | ギャラリー学芸員（情報共有相手） | 展覧会プレスリリースを参照させたい | 短時間で情報を共有できる |
| US-05 | プライベートクライアント | 公開されていない作品の問い合わせ動線を見つけたい | 直接コンタクトを取れる |

---

## 4. Functional Requirements

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-01 | ページロードアニメーション（純白背景、ブランド名のみ、垂直線スライドイン） | P0 |
| FR-02 | 極限まで余白を取った1作品ヒーロー（縦横どちらかが90vh以上） | P0 |
| FR-03 | 作品メタ情報サイドキャプション（作家名・タイトル・年・素材・寸法、左下固定） | P0 |
| FR-04 | スクロール駆動の作品ズームアウト（hero 100% → 60% へ縮小しながら背景余白へ） | P0 |
| FR-05 | Current Exhibition セクション（1展覧会=1スクリーン、フルブリード写真+チャプターナンバリング） | P0 |
| FR-06 | Artists 一覧（縦組リスト、アルファベット順、ホバーで作品サムネ） | P0 |
| FR-07 | Press / Catalogue リンクストリップ（PDFアイコン+発行年） | P1 |
| FR-08 | Locations セクション（NY / London / Paris / Hong Kong、住所と現在開廊時間） | P1 |
| FR-09 | Enquire フォーム動線（モーダルでなく独立ページへの遷移） | P0 |
| FR-10 | フッター（ニュースレター登録、SNS控えめ、Copyright） | P1 |
| FR-11 | スクロール時のナビ背景半透明化（pure white → rgba blur） | P0 |
| FR-12 | モバイル対応（375px基準、ヒーローは縦組に切替） | P0 |
| FR-13 | カスタムカーソル（極小ドットのみ、リング無し） | P2 |

---

## 5. Design System

### Color Palette
```css
--bg:        #FFFFFF;   /* 純白（museum white） */
--bg-sub:    #F7F6F4;   /* かすかに温かい白 */
--bg-deep:   #0A0A0A;   /* 黒に近いチャコール（ダークセクション） */
--fg:        #1A1A1A;   /* 印刷インク的な黒 */
--fg-muted:  #6F6F6F;   /* グラフィックグレー */
--fg-light:  #B8B8B8;   /* 罫線・キャプション */
--border:    #E8E8E6;   /* 極薄ホワイトキューブ罫線 */
--accent:    #5C1A1B;   /* ディープ・オックスブラッド（リンクホバー・強調） */
```

### Typography
```css
--font-display: 'Bodoni Moda', 'Didot', Georgia, serif;  /* Display, brand, hero */
--font-sans:    'Inter', 'Söhne', -apple-system, sans-serif;  /* Body, captions, nav */
```
- Google Fonts CDN: Bodoni Moda (wght 400, 500, 700, opsz 6..96), Inter (wght 300, 400, 500)
- Display サイズ: clamp(4rem, 11vw, 13rem), letter-spacing -0.02em
- Body サイズ: 16px / line-height 1.55
- キャプション: 11px / letter-spacing 0.12em / uppercase

### Spacing
```css
--space-museum:  clamp(6rem, 14vw, 14rem);  /* セクション間、museum余白 */
--space-frame:   clamp(2rem, 6vw, 5rem);    /* 画像の四辺フレーム */
--space-caption: 1.2rem;                    /* キャプションのインナー余白 */
```

### Motion
```css
--ease:     cubic-bezier(0.22, 1, 0.36, 1);
--ease-slow: cubic-bezier(0.16, 1, 0.3, 1);
/* loader: brand 1.6s fade-in, vertical line 1.2s scale-y */
/* hero artwork: scroll-driven scale(1→0.6) over 100vh */
/* reveal: opacity 1.2s + translateY 36px → 0 */
/* nav: bg fade 0.4s on scroll */
/* cursor: none (default), optional dot 4×4px */
```

### Imagery
- ヒーロー作品画像: 5000px幅以上、高解像度、必ず中央のみ配置
- Exhibition view: 美術館のインスタレーション風広角写真、人物入れず
- 作家ポートレート: モノクロのみ、引きの構図
- カラー画像と白黒画像を意図的に混在させない（各セクション統一）

---

## 6. Architecture

```
index.html
├── .loader              # 純白×ブランド名×垂直線
├── nav                  # 左ロゴ "NORE"、右リンク (Exhibitions / Artists / Locations / Enquire)
├── .hero                # 1作品全画面、左下キャプション固定
│   ├── .artwork-frame   # 中央に絵画、四辺に museum 余白
│   └── .caption-side    # 縦組キャプション (作家|タイトル|年|素材|寸法)
├── .section#current     # Current Exhibition
│   ├── .chapter-num     # "01" 大型ナンバー
│   ├── .exhibition-img  # フルブリード installation view
│   └── .exhibition-meta # 展覧会名・期間・キュレーター名
├── .section#artists     # 縦組アーティストリスト
│   └── .artist-row      # 名前 + (ホバー時) サムネイル
├── .section#press       # プレス・カタログPDFストリップ
├── .section#locations   # NY/London/Paris/Hong Kong グリッド
└── footer               # ニュースレター + SNS + © + Imprint
```

---

## 7. Key Design Decisions

| Decision | Chosen | Rationale |
|----------|--------|-----------|
| テーマ | Light / pure white | ホワイトキューブの忠実なWeb化、museum white を背景に |
| ヒーロー | 1作品全画面 + サイドキャプション | カードグリッドは商業的すぎる。1作品=1スクロールでmuseum体験 |
| Display font | Bodoni Moda | Didone系の極端コントラスト。Artforum/Frieze誌的、ブルーチップの定型 |
| Body font | Inter | 中立で読みやすい。Söhneを使う案もあったが商用CDN不安 |
| アクセント | オックスブラッド #5C1A1B | 美術館の壁の絵画の額装赤、抑制された権威色 |
| キャプション位置 | 左下固定、縦組（90deg回転） | museum label のWeb翻訳。読みづらさは「格」を演出する装置 |
| カート・価格 | 表示しない | コレクター層は「価格を聞く前に決める」、表示すれば即離脱 |
| Enquire | モーダルでなく独立ページ遷移 | 「軽い問い合わせ」を許さない設計、本気の人だけが到達する |
| ナビ | 5項目以下、Hamburger不使用 | 情報構造の単純さがブランド格を反映 |
| モーション | scroll-driven scale のみ | flashy animation は museum 体験を破壊する |
| カーソル | 極小ドット or default | カスタムリングは商業的、削ぎ落とす |
| Texture | grain なし | pure であることが美徳 |

---

## 8. Layout Reference

### Hero (Desktop)
```
┌───────────────────────────────────────────────────┐
│ NORE                    Exhibitions  Artists  ... │  ← nav
├───────────────────────────────────────────────────┤
│                                                   │
│                                                   │
│         ┌─────────────────────┐                  │
│         │                     │                  │
│         │                     │                  │
│   T     │     [ ARTWORK ]     │                  │  ← museum frame
│   I     │                     │                  │
│   T     │                     │                  │
│   L     └─────────────────────┘                  │
│   E                                               │
│   ↻                                                │
│   (90° caption, left side)                       │
│                                                   │
└───────────────────────────────────────────────────┘
```

### Current Exhibition (Desktop)
```
┌───────────────────────────────────────────────────┐
│                                                   │
│  01                                               │  ← chapter number
│  ──                                               │
│                                                   │
│         [ INSTALLATION VIEW (full-bleed) ]        │
│                                                   │
│  Exhibition Title — Artist Name                   │
│  May 12 — July 8, 2026    Curated by ...          │
│                                                   │
└───────────────────────────────────────────────────┘
```

---

## 9. Accessibility

| 項目 | 実装 |
|------|------|
| コントラスト比 | fg #1A1A1A on bg #FFFFFF = 17.1:1 (AAA) |
| キーボード操作 | 全リンクtab可、focus-visible でオックスブラッド輪郭 |
| 画像 alt | 作家名・タイトル・年・素材を含む記述的 alt |
| 縦組キャプション | aria-label でフラット読み上げを補完 |
| prefers-reduced-motion | scroll-driven scale を無効化、即座に縮小状態へ |
| 言語 | `<html lang="en">` 固定 |

---

## 10. Tech & Deploy

- 単一 `index.html`、CSS Custom Properties、Vanilla JS
- ライブラリ不使用（Lenis/GSAP 不要、scroll-driven animation は CSS で）
- フォント: Google Fonts CDN（Bodoni Moda + Inter）
- 画像: Unsplash CDN または静的配置（プレースホルダー画像でOK）
- デプロイ: GitHub Pages, `design-art-gallery-bluechip` リポジトリ
- カスタムドメイン: `design.art-gallery-bluechip.riumu.net` 予定

---

## 11. Inspiration & References

- gagosian.com — 1作品ヒーロー、museum余白、Didone系見出し
- pacegallery.com — フッターまでの最小情報量、抑制動線
- hauserwirth.com — Editorial が強い、ギャラリー as publisher
- davidzwirner.com — 展覧会ページの深いストーリーテリング
- whitecube.com — minimal navigation、location リスト

NORE は上記から「**1作品ヒーロー + Bodoni系見出し + museum余白**」を抽出した架空のブランド。
