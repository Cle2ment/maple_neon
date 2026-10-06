# Maple Neon: A Theme for Cherry Studio

![Free Palestine](https://freepalestinemovement.org/wp-content/uploads/2013/06/banner.jpg)
![Cherry Studio](https://www.cherry-ai.com/assets/cherry-logo-CtmH594q.svg)
![Static Badge](https://img.shields.io/badge/Tailored_for-Cherry_Studio_v2.0%2B-red?logo=Github)
![Static Badge](https://img.shields.io/badge/License-MIT-blue)
![Static Badge](https://img.shields.io/badge/Language-CSS-pink?logo=css)
![Static Badge](https://img.shields.io/badge/Release-v1.2.1-green)
<div style="text-align: center">
English |
<a href="https://github.com/BoningtonChen/CherryStudio_themes/blob/master/docs/README.zh.md">中文</a> |
<a href="https://github.com/BoningtonChen/CherryStudio_themes/blob/master/docs/README.fr.md">Français</a> |
<a href="https://github.com/BoningtonChen/CherryStudio_themes/blob/master/docs/README.ja.md">日本語</a>
</div>

## Introduction

This is a theme tailored for Cherry Studio, a desktop client that supports for multiple LLM providers, available on Windows, Mac and Linux. It targets **Cherry Studio v2.0+** and is built on the v2 theme API (semantic CSS variables and `data-ui` hooks). \
For more information about Cherry Studio, check [here](https://github.com/CherryHQ/cherry-studio).

## How to USE

1. (Optional) Download the fonts: Maple Mono NF CN from [Maple Font](https://github.com/subframe7536/maple-font/releases/download/v7.3/MapleMono-NF-CN-unhinted.zip) and DreamHan Sans / DreamHan Serif from [DreamHan Font](https://github.com/Pal3love/dream-han-cjk/releases). Without them, fallbacks (`Fira Code` / Microsoft YaHei) apply. You can also pick the fonts you have installed in Cherry Studio's built-in **Font Settings** (global font / code font).
2. Copy the full content of [maple-neon.css](./themes/maple-neon.css) — the full version (fonts + neon marquee animation + official token mapping). Two lighter variants are available: [maple-neon-font-minimal.css](./themes/maple-neon-font-minimal.css) (fonts only) and [just-flowing-border.css](./themes/just-flowing-border.css) (flowing border animation only).
3. In Cherry Studio, go to **Settings → Display Settings → Custom CSS** and paste the CSS.
4. **Upgrading from v1?** In v2 your old custom CSS is automatically disabled with a `/* cherry-studio:custom-css:v1 */` marker line added at the top. Replace the whole content with this theme's v2 version, and do not keep the marker line.
5. It takes effect immediately after saving, so you can preview and fine-tune live.

<details>
<summary>Or, if you don't want to modify, directly copy CSS from here!</summary>

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

## What's special about the theme?

- It provides modernized and aesthetic UI for Cherry Studio v2.0+, built on the v2 theme API (semantic CSS variables and `data-ui` hooks).
- It mixes the Maple font with a neon-styled input-bar, creating a unique and visually appealing experience.
- Uses DreamHan font series and Microsoft YaHei to provide excellent Chinese font display effects.
- Ships in three variants: `maple-neon.css` (full: fonts + neon marquee animation + official token mapping), `maple-neon-font-minimal.css` (fonts only) and `just-flowing-border.css` (flowing border animation only).

## Demonstration

Based on Cherry Studio v2.x
![Page Light](./examples/main-page-light.png)

![Page Dark](./examples/main-page-dark.png)

## Customization

The theme derives its colors from a small palette defined at the top `:root` of the CSS. To recolor it, edit those variables instead of searching for hardcoded colors:

- `--mn-orange`: `#ff6a01`
- `--mn-yellow`: `#f8c91c`
- `--mn-violet`: `#8a2be2`
- `--mn-cyan`: `#00d4ff`

You can also fork the project and modify your own theme for Cherry Studio; for exact instructions, check [Cherry Studio Docs](https://docs.cherry-ai.com/personalization-settings/css).

## One more Glance

For other themes, check [One More Glance](./OneMoreGlance.md)

## Inspiration

### Themes

- Dracula Theme: <https://cherrycss.com>
- Neon Theme: <https://cherry-ai.com/css>

### Fonts

- Maple Font: <https://github.com/subframe7536/maple-font>
- DreamHan Sans: <https://github.com/Pal3love/dream-han-cjk/releases>

### Tools

- The Themes are constructed partly under the help of DeepSeek-0324 & Claude-3.7.

## LICENSE

The Project follows [MIT LICENSE](./LICENSE).
