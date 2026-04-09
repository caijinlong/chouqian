# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Chinese fortune-telling (抽签/灵签) web app featuring seven oracle pages:

- **index.html** — 文王六十四卦 (King Wen I Ching): Bronze/verdigris theme, coin-toss hexagram animation, 64 hexagrams (default landing page)
- **guanyin.html** — 观音灵签 (Guanyin Oracle): Temple red/gold theme, bamboo stick tube animation, 100 fortune lots
- **guandi.html** — 关帝灵签 (Guan Di Oracle): Dark bronze/gold theme, SVG 青龙偃月刀 (Green Dragon Crescent Blade) icon with shake animation, 100 fortune lots
- **lvzu.html** — 吕祖灵签 (Lv Zu Oracle): Purple/warm-gold Daoist theme, spinning ☯ bagua animation, 100 fortune lots
- **yuelao.html** — 月老灵签 (Yue Lao Oracle): Romantic red/pink theme, red thread animation, 60 fortune lots
- **caishen.html** — 财神灵签 (Caishen Oracle): Gold/red wealth theme, ingot animation, 62 fortune lots
- **huangdaxian.html** — 黄大仙灵签 (Wong Tai Sin Oracle): Yellow/amber Daoist theme, SVG gourd (葫芦) icon with shake animation, 100 fortune lots

All seven pages cross-link via fixed-position nav links (top-left and top-right corners).

## Architecture

Each page is a **single self-contained HTML file** — no build system, no bundler, no external JS/CSS frameworks. Each file contains:

1. Inline `<style>` block with all CSS (Google Fonts loaded via `@import`)
2. HTML structure: background layer, particle container, navigation links, main container (header, interactive area, result div)
3. Inline `<script>` block with:
   - Particle/smoke generation (DOM-based CSS animations)
   - Fortune data array (`lots` for 灵签 pages, `guas` for 文王卦)
   - Main interaction function (`drawLot()` for 灵签, `throwCoins()` for 文王卦)
   - `showResult()` — renders result card with fortune details and category advice grid

## Fortune Type System

- 观音: 上上, 上吉, 上平, 中吉, 中平, 中下, 下下
- 关帝: 上上, 大吉, 上吉, 中吉, 中平, 中下, 下下
- 吕祖: 大吉, 上吉, 中吉, 中平, 中下, 下下
- 黄大仙: 上上, 大吉, 上吉, 中吉, 中平, 中下, 下下
- 文王: 64 hexagrams with 卦辞, 彖曰, 象曰, 爻辞, 白话, fortune categories (财/婚/业/健/行/讼)

Each type maps to a color/glow CSS class (`.type-上上`, `.type-大吉`, etc.) and an advice lookup table. 文王卦 uses coin-toss divination (3 coins × 6 rounds) with trigram-to-hexagram lookup.

## Key Patterns

- Fonts: `Noto Serif SC` (body), `Ma Shan Zheng` (headings/poems) — loaded from Google Fonts
- All animations are CSS-based (`@keyframes`), triggered by adding/removing classes (`.shaking`, `.spinning`)
- Mobile responsive via `@media (max-width: 480px)` breakpoint
- Fortune selection is purely `Math.random()` — no backend, no persistence
- All content is in Chinese (zh-CN)

## Development

No build step. Open any HTML file directly in a browser to preview. All changes are visible on reload.
