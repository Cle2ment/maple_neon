# Maple Neon：Cherry Studio テーマ

![Free Palestine](https://freepalestinemovement.org/wp-content/uploads/2013/06/banner.jpg)
![Cherry Studio](https://www.cherry-ai.com/assets/cherry-logo-CtmH594q.svg)
![Static Badge](https://img.shields.io/badge/Tailored_for-Cherry_Studio_v2.0%2B-red?logo=Github)
![Static Badge](https://img.shields.io/badge/License-AGPL--3.0-blue)
![Static Badge](https://img.shields.io/badge/Language-CSS-pink?logo=css)
![Static Badge](https://img.shields.io/badge/Release-v2.0.0-green)
<div style="text-align: center">
<a href="https://github.com/Cle2ment/maple_neon/blob/master/docs/README.zh.md">中文</a> |
<a href="https://github.com/Cle2ment/maple_neon/blob/master/README.md">English</a> |
<a href="https://github.com/Cle2ment/maple_neon/blob/master/docs/README.fr.md">Français</a> |
日本語
</div>

## 紹介

これはCherry Studioに特化したテーマです。Cherry Studioは複数の大規模言語モデルプロバイダをサポートするデスクトップクライアントで、Windows、Mac、Linuxシステムで使用可能です。本テーマは **Cherry Studio v2.0+** を対象とし、v2 テーマ API（セマンティック CSS 変数と `data-ui` フック）に基づいて構築されています。\
Cherry Studioに関する詳細情報は、[こちら](https://github.com/CherryHQ/cherry-studio)を参照してください。

## 使用方法

1. （任意）フォントをダウンロードします：[Maple Font](https://github.com/subframe7536/maple-font/releases/download/v7.3/MapleMono-NF-CN-unhinted.zip)からMaple Mono NF CNを、[DreamHan Font](https://github.com/Pal3love/dream-han-cjk/releases)からDreamHan SansとDreamHan Serifを入手します。未インストールの場合は代替フォント（`Fira Code` / Microsoft YaHei）が適用されます。Cherry Studio内蔵の**フォント設定**（グローバルフォント / コードフォント）で、インストール済みのフォントを選ぶこともできます。
2. [maple-neon.css](../themes/maple-neon.css) の全文をコピーします — フルバージョン（フォント + ネオン走馬灯アニメーション + 公式トークンマッピング）。軽量な変体も2つ用意されています：[maple-neon-font-minimal.css](../themes/maple-neon-font-minimal.css)（フォントのみ）と [just-flowing-border.css](../themes/just-flowing-border.css)（流れるボーダーアニメーションのみ）。
3. Cherry Studioで**設定 → 表示設定 → カスタムCSS**を開き、CSSを貼り付けます。
4. **v1からのアップグレードユーザーの方へ**：v2では旧カスタムCSSは自動的に無効化され、先頭に `/* cherry-studio:custom-css:v1 */` というマーカー行が追加されます。旧内容は本テーマのv2版全文で置き換え、マーカー行は残さないでください。
5. 保存するとすぐに反映され、リアルタイムでプレビュー・微調整できます。

<details>
<summary>または、変更したくない場合は、ここから直接CSSをコピーしてください！</summary>

```css
/* Maple Neon Minimal Theme for Cherry Studio
   专注于输入框AI智能体运行时的跑马灯效果 */

/* === 字体配置 === */
:root {
    /* UI字体：使用微软雅黑作为主要UI字体 */
    --font-family:
        var(--user-font-family), "Microsoft YaHei", "Microsoft YaHei UI",
        "微软雅黑", Ubuntu, -apple-system, BlinkMacSystemFont, "Segoe UI",
        system-ui, Roboto, Oxygen, Cantarell, "Open Sans", "Helvetica Neue",
        Arial, "Noto Sans", sans-serif, "Apple Color Emoji", "Segoe UI Emoji",
        "Segoe UI Symbol", "Noto Color Emoji";

    /* 代码字体：使用Maple Mono作为代码字体 */
    --code-font-family:
        var(--user-code-font-family), "Maple Mono", "Maple Mono NF",
        "Cascadia Code", "Fira Code", "Consolas", Menlo, Courier, monospace;
}

/* Windows系统专用字体配置 */
body[os="windows"] {
    --font-family:
        var(--user-font-family), "Microsoft YaHei", "Microsoft YaHei UI",
        "微软雅黑", "Twemoji Country Flags", Ubuntu, -apple-system,
        BlinkMacSystemFont, "Segoe UI", system-ui, Roboto, Oxygen, Cantarell,
        "Open Sans", "Helvetica Neue", Arial, "Noto Sans", sans-serif,
        "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol",
        "Noto Color Emoji";

    --code-font-family:
        var(--user-code-font-family), "Maple Mono", "Maple Mono NF",
        "Cascadia Code", "Fira Code", "Consolas", "Sarasa Mono SC",
        "Microsoft YaHei UI", Courier, monospace;
}

/* 应用字体到具体元素 */
body {
    font-family: var(--font-family);
}

/* 代码相关元素使用Maple Mono字体 */
code,
pre,
.markdown code,
.markdown pre,
.shiki,
.cm-editor .cm-scroller,
kbd,
samp,
tt,
var {
    font-family: var(--code-font-family) !important;
}

/* === AI智能体跑马灯动画 === */
@keyframes ai-running-gradient {
    0% {
        background-position: 0% 50%;
    }
    25% {
        background-position: 100% 50%;
    }
    50% {
        background-position: 200% 50%;
    }
    75% {
        background-position: 300% 50%;
    }
    100% {
        background-position: 400% 50%;
    }
}

/* AI思考状态脉冲 */
@keyframes ai-thinking-pulse {
    0%,
    100% {
        box-shadow: 0 0 5px rgba(255, 106, 1, 0.2);
    }
    50% {
        box-shadow: 0 0 20px rgba(138, 43, 226, 0.6);
    }
}

/* 数据流动效果 */
@keyframes ai-data-flow {
    0% {
        transform: translateX(-100%);
        opacity: 0;
    }
    50% {
        opacity: 1;
    }
    100% {
        transform: translateX(100%);
        opacity: 0;
    }
}

/* === 输入框跑马灯效果 === */
#inputbar {
    position: relative;
    border-radius: 12px;
}

/* AI运行时的跑马灯边框 */
#inputbar::before {
    content: "";
    position: absolute;
    inset: -2px;
    border-radius: inherit;
    padding: 2px;
    background: linear-gradient(
        90deg,
        #ff6a01,
        /* 爱马仕橙 */ #f8c91c,
        /* 那不勒斯黄 */ #8a2be2,
        /* 紫罗兰 */ #00d4ff,
        /* 青色 */ #f8c91c,
        /* 那不勒斯黄 */ #ff6a01 /* 爱马仕橙 */
    );
    background-size: 300% 100%;
    mask:
        linear-gradient(#fff 0 0) content-box,
        linear-gradient(#fff 0 0);
    -webkit-mask:
        linear-gradient(#fff 0 0) content-box,
        linear-gradient(#fff 0 0);
    -webkit-mask-composite: destination-out;
    mask-composite: exclude;
    animation: ai-running-gradient 7s linear infinite;
    opacity: 0;
    transition: opacity 0.4s ease-in-out;
    pointer-events: none;
    z-index: -1;
}

/* 激活跑马灯效果的条件 */
#inputbar:focus-within::before,
#inputbar.ai-active::before,
#inputbar[data-ai-status="running"]::before {
    opacity: 1;
}

/* AI思考状态的额外效果 */
#inputbar.ai-thinking {
    animation: ai-thinking-pulse 4s ease-in-out infinite;
}

/* 数据流动覆盖层 */
#inputbar.ai-thinking::after {
    content: "";
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(
        90deg,
        transparent,
        rgba(0, 212, 255, 0.1),
        transparent
    );
    animation: ai-data-flow 3.5s ease-in-out infinite;
    border-radius: inherit;
    pointer-events: none;
    z-index: 1;
}

/* === 输入框内部样式优化 === */
#inputbar input,
#inputbar textarea {
    position: relative;
    z-index: 2;
    transition: all 0.3s ease;
}

/* === 状态指示器 === */
.ai-status-dot {
    position: absolute;
    top: 8px;
    right: 8px;
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: #8a2be2;
    opacity: 0;
    transition: opacity 0.3s ease;
    z-index: 3;
}

#inputbar.ai-thinking .ai-status-dot,
#inputbar[data-ai-status="running"] .ai-status-dot {
    opacity: 1;
    animation: ai-thinking-pulse 3s ease-in-out infinite;
}

/* === 辅助类 === */
/* 手动触发AI运行效果 */
.ai-mode-active #inputbar::before {
    opacity: 1 !important;
}

/* 禁用AI效果 */
.ai-mode-disabled #inputbar::before,
.ai-mode-disabled #inputbar::after {
    opacity: 0 !important;
    animation: none !important;
}

/* === 响应式设计 === */
@media (max-width: 768px) {
    #inputbar::before {
        inset: -1px;
        padding: 1px;
    }

    #inputbar::before {
        background-size: 200% 100%;
        animation-duration: 5.5s;
    }
}

/* === 无障碍支持 === */
@media (prefers-reduced-motion: reduce) {
    #inputbar::before,
    #inputbar::after,
    #inputbar,
    .ai-status-dot {
        animation: none !important;
    }

    #inputbar::before {
        background: linear-gradient(90deg, #ff6a01, #8a2be2);
        background-size: 100% 100%;
    }
}

/* === 高对比度模式 === */
@media (prefers-contrast: high) {
    #inputbar::before {
        background: linear-gradient(
            90deg,
            #ff8c00,
            #ffd700,
            #9370db,
            #00bfff,
            #ffd700,
            #ff8c00
        );
    }
}

/* === 浏览器兼容性修复 === */
/* Firefox支持 */
@supports not (-webkit-mask-composite: destination-out) {
    #inputbar::before {
        mask-composite: exclude;
    }
}

/* Safari支持 */
@supports (-webkit-mask-composite: destination-out) {
    #inputbar::before {
        -webkit-mask-composite: destination-out;
    }
}
```

</details>

## 特徴

- Cherry Studio v2.0+ にモダンで美しいユーザーインターフェイスを提供します。v2 テーマ API（セマンティック CSS 変数と `data-ui` フック）に基づいて構築されています。
- Mapleフォントとネオンスタイルの入力欄を組み合わせ、ユニークで視覚的に印象的な使用体験を提供します。
- DreamHanフォントシリーズとMicrosoft YaHeiを使用して、優れた中国語フォント表示効果を提供します。
- 3つの変体を用意しています：`maple-neon.css`（フル：フォント + ネオン走馬灯アニメーション + 公式トークンマッピング）、`maple-neon-font-minimal.css`（フォントのみ）、`just-flowing-border.css`（流れるボーダーアニメーションのみ）。

## デモンストレーション

Cherry Studio v2.x をベースに
![明るいページ](../examples/main-page-light.png)

![暗いページ](../examples/main-page-dark.png)

## カスタマイズ

テーマの配色は、CSS冒頭の `:root` で定義された小さなパレット変数から取得します。色を変えるには、ハードコードされた色を探すのではなく、これらの変数を編集してください：

- `--mn-orange`：`#ff6a01`
- `--mn-yellow`：`#f8c91c`
- `--mn-violet`：`#8a2be2`
- `--mn-cyan`：`#00d4ff`

このプロジェクトをフォークして独自のCherry Studioテーマを変更することもできます。詳細な説明は、[Cherry Studio ドキュメント](https://docs.cherry-ai.com/personalization-settings/css)を参照してください。

## 他のテーマを見る

他のテーマを表示するには、[もう1つ見る](../OneMoreGlance.md)を参照してください。

## インスピレーションの源泉

### テーマ

- Dracula Theme: <https://cherrycss.com>
- Neon Theme: <https://cherry-ai.com/css>

### フォント

- Maple Font: <https://github.com/subframe7536/maple-font>
- DreamHan Sans: <https://github.com/Pal3love/dream-han-cjk/releases>

### ツール

- テーマ部分はDeepSeek-0324とClaude-3.7の助けを借りて構築されました。

## LICENSE

本プロジェクトは [AGPL-3.0 LICENSE](../LICENSE)に準拠しています。
