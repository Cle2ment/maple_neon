# Maple Neon: A Theme for Cherry Studio

![Cherry Studio](assets/cherry-logo.svg)
![Static Badge](https://img.shields.io/badge/Tailored_for-Cherry_Studio_v2.0%2B-red?logo=Github)
![Static Badge](https://img.shields.io/badge/License-AGPL--3.0-blue)
![Static Badge](https://img.shields.io/badge/Language-CSS-pink?logo=css)
![Static Badge](https://img.shields.io/badge/Release-v2.0.0-green)

<div style="text-align: center">
English |
<a href="https://github.com/Cle2ment/maple_neon/blob/master/docs/README.zh.md">中文</a> |
<a href="https://github.com/Cle2ment/maple_neon/blob/master/docs/README.fr.md">Français</a> |
<a href="https://github.com/Cle2ment/maple_neon/blob/master/docs/README.ja.md">日本語</a>
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
/* =========================================================================
 * Maple Neon — 完整主题（枫叶霓虹）
 * 面向 Cherry Studio v2.0+ 自定义 CSS（ui.custom_css）
 * 变体定位：完整超集 —— 字体配置 + 调色板 + 官方语义 token 映射 + 跑马灯动画
 * 许可证：AGPL-3.0
 * =========================================================================
 * v2 说明：自定义 CSS 以无 cascade layer 的 <style> 注入，普通声明即可胜过
 * 内置分层样式，因此本文件不做任何强制覆盖（.dark = 暗色，:root/.light = 亮色）。
 * ========================================================================= */

/* === 字体配置 === */
:root {
    /* UI 字体栈：v2 内置字体设置写 --app-user-font-family，v1 时代为 --user-font-family，双兜底。
       Windows 专有字体（"Twemoji Country Flags"）已并入主栈，缺失时浏览器自动跳过。 */
    --font-family: var(
        --app-user-font-family,
        var(
            --user-font-family,
            "Microsoft YaHei", "Microsoft YaHei UI", "微软雅黑",
            "Twemoji Country Flags", Ubuntu, -apple-system, BlinkMacSystemFont,
            "Segoe UI", system-ui, Roboto, Oxygen, Cantarell, "Open Sans",
            "Helvetica Neue", Arial, "Noto Sans", sans-serif,
            "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol",
            "Noto Color Emoji"
        )
    );

    /* 代码字体栈：Maple Mono 系优先，Windows 专有字体已并入主栈 */
    --code-font-family: var(
        --app-user-code-font-family,
        var(
            --user-code-font-family,
            "Maple Mono", "Maple Mono NF", "Cascadia Code", "Fira Code",
            Consolas, "Sarasa Mono SC", "Microsoft YaHei UI", Menlo, Courier,
            monospace
        )
    );
}

/* 应用 UI 字体 */
body {
    font-family: var(--font-family);
}

/* 代码相关元素使用 Maple Mono 字体（v1 类名与 v2 语义钩子并存，后者优先生效） */
code,
pre,
kbd,
samp,
tt,
var,
.markdown code,
.markdown pre,
.shiki,
.cm-editor .cm-scroller,
[data-ui~="part:code-block"],
[data-ui~="part:message-content"] code,
[data-ui~="part:message-content"] pre {
    font-family: var(--code-font-family);
}

/* === 调色板 === */
:root {
    /* 枫叶霓虹四主色 —— 全文件唯一硬编码处，其余一律经 var() 引用 */
    --mn-orange: #ff6a01; /* 爱马仕橙 */
    --mn-yellow: #f8c91c; /* 那不勒斯黄 */
    --mn-violet: #8a2be2; /* 紫罗兰 */
    --mn-cyan: #00d4ff; /* 青色 */

    /* 高对比度模式四主色 */
    --mn-hc-orange: #ff8c00;
    --mn-hc-yellow: #ffd700;
    --mn-hc-violet: #9370db;
    --mn-hc-cyan: #00bfff;
}
/* 半透明衍生色统一由 color-mix() 从上面的变量推导，不再硬编码 rgba 字面量 */

/* === 官方语义 token 映射（仅本文件） === */
/* 克制原则：只映射「强调 / 交互 / 代码」类 token，
   不触碰 --background / --card / --popover / --sidebar 等大面积表面色，
   避免整个窗口被染色、与宿主亮暗色体系打架。 */
:root {
    /* 主色 → 紫罗兰，用于按钮与选中态等强调元素 */
    --primary: var(--mn-violet);
    /* 主色前景 → 纯白，保证紫底上的文字对比度 */
    --primary-foreground: #ffffff;
    /* 焦点环 → 橙色，与输入框跑马灯首色呼应 */
    --ring: var(--mn-orange);
    /* 链接色 → 青色压暗（亮色背景上纯青可读性不足） */
    --link: color-mix(in srgb, var(--mn-cyan) 70%, black);
    /* 图表四色直接取调色板，形成数据可视化的一致性 */
    --chart-1: var(--mn-orange);
    --chart-2: var(--mn-yellow);
    --chart-3: var(--mn-violet);
    --chart-4: var(--mn-cyan);
    /* 行内代码 → 淡紫底 + 深紫字 */
    --inline-code: color-mix(in srgb, var(--mn-violet) 10%, transparent);
    --inline-code-foreground: color-mix(in srgb, var(--mn-violet) 75%, black);
    /* 代码块底色 → 极淡紫，仅做微调而非覆盖宿主 */
    --code-block: color-mix(in srgb, var(--mn-violet) 4%, transparent);
}

/* 暗色模式（根元素 .dark）下按需提亮，保证深底可读性 */
.dark {
    --primary: var(--mn-violet);
    --primary-foreground: #ffffff;
    --ring: var(--mn-cyan);
    /* 深底上纯青对比度充足，无需压暗 */
    --link: var(--mn-cyan);
    --inline-code: color-mix(in srgb, var(--mn-violet) 22%, transparent);
    --inline-code-foreground: color-mix(in srgb, var(--mn-violet) 40%, white);
    --code-block: color-mix(in srgb, var(--mn-violet) 8%, transparent);
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
        box-shadow: 0 0 5px color-mix(in srgb, var(--mn-orange) 20%, transparent);
    }
    50% {
        box-shadow: 0 0 20px color-mix(in srgb, var(--mn-violet) 60%, transparent);
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
/* 锚点双写：v2 语义钩子优先，v1 的 #inputbar 兜底 */
[data-ui~="chat.composer"],
#inputbar {
    position: relative;
    border-radius: var(--radius, 12px);
}

/* AI运行时的跑马灯边框 */
[data-ui~="chat.composer"]::before,
#inputbar::before {
    content: "";
    position: absolute;
    inset: -2px;
    border-radius: inherit;
    padding: 2px;
    background: linear-gradient(
        90deg,
        var(--mn-orange),
        /* 爱马仕橙 */ var(--mn-yellow),
        /* 那不勒斯黄 */ var(--mn-violet),
        /* 紫罗兰 */ var(--mn-cyan),
        /* 青色 */ var(--mn-yellow),
        /* 那不勒斯黄 */ var(--mn-orange) /* 爱马仕橙 */
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

/* 激活跑马灯效果的条件：:focus-within 为主触发；
   .ai-active / [data-ai-status="running"] / .ai-thinking 为渐进增强（best-effort，
   v2 未必提供这些钩子，存在时即生效，缺失时无副作用）。 */
[data-ui~="chat.composer"]:focus-within::before,
[data-ui~="chat.composer"].ai-active::before,
[data-ui~="chat.composer"][data-ai-status="running"]::before,
#inputbar:focus-within::before,
#inputbar.ai-active::before,
#inputbar[data-ai-status="running"]::before {
    opacity: 1;
}

/* AI思考状态的额外效果（渐进增强，best-effort） */
[data-ui~="chat.composer"].ai-thinking,
#inputbar.ai-thinking {
    animation: ai-thinking-pulse 4s ease-in-out infinite;
}

/* 数据流动覆盖层（渐进增强，best-effort） */
[data-ui~="chat.composer"].ai-thinking::after,
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
        color-mix(in srgb, var(--mn-cyan) 10%, transparent),
        transparent
    );
    animation: ai-data-flow 3.5s ease-in-out infinite;
    border-radius: inherit;
    pointer-events: none;
    z-index: 1;
}

/* === 输入框内部样式优化 === */
/* v2 输入区本体保持在跑马灯之上 */
[data-ui~="part:composer-input"] {
    position: relative;
    z-index: 2;
}

[data-ui~="chat.composer"] input,
[data-ui~="chat.composer"] textarea,
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
    background: var(--mn-violet);
    opacity: 0;
    transition: opacity 0.3s ease;
    z-index: 3;
}

[data-ui~="chat.composer"].ai-thinking .ai-status-dot,
[data-ui~="chat.composer"][data-ai-status="running"] .ai-status-dot,
#inputbar.ai-thinking .ai-status-dot,
#inputbar[data-ai-status="running"] .ai-status-dot {
    opacity: 1;
    animation: ai-thinking-pulse 3s ease-in-out infinite;
}

/* === 辅助类 === */
/* 手动触发AI运行效果（选择器比基础态多一级，无需强制覆盖即可胜出） */
.ai-mode-active [data-ui~="chat.composer"]::before,
.ai-mode-active #inputbar::before {
    opacity: 1;
}

/* 禁用AI效果（本节位于激活态之后，同权重时靠后声明胜出） */
.ai-mode-disabled [data-ui~="chat.composer"]::before,
.ai-mode-disabled [data-ui~="chat.composer"]::after,
.ai-mode-disabled #inputbar::before,
.ai-mode-disabled #inputbar::after {
    opacity: 0;
    animation: none;
}

/* === 响应式设计 === */
@media (max-width: 768px) {
    [data-ui~="chat.composer"]::before,
    #inputbar::before {
        inset: -1px;
        padding: 1px;
        background-size: 200% 100%;
        animation-duration: 5.5s;
    }
}

/* === 无障碍支持 === */
@media (prefers-reduced-motion: reduce) {
    /* 关闭跑马灯与脉冲。为了让这些声明胜过动效声明而不动用强制覆盖，
       选择器权重与其一一对齐，并靠后出现。 */
    [data-ui~="chat.composer"],
    [data-ui~="chat.composer"]::before,
    #inputbar,
    #inputbar::before,
    .ai-status-dot {
        animation: none;
    }

    [data-ui~="chat.composer"].ai-thinking,
    [data-ui~="chat.composer"].ai-thinking::after,
    [data-ui~="chat.composer"].ai-thinking .ai-status-dot,
    [data-ui~="chat.composer"][data-ai-status="running"] .ai-status-dot,
    #inputbar.ai-thinking,
    #inputbar.ai-thinking::after,
    #inputbar.ai-thinking .ai-status-dot,
    #inputbar[data-ai-status="running"] .ai-status-dot {
        animation: none;
    }

    /* 静态双色渐变替代流动渐变 */
    [data-ui~="chat.composer"]::before,
    #inputbar::before {
        background: linear-gradient(90deg, var(--mn-orange), var(--mn-violet));
        background-size: 100% 100%;
    }
}

/* === 高对比度模式 === */
/* 注：媒体特性合法取值为 no-preference / less / more / custom，
   历史版本写的 `prefers-contrast: high` 并非合法值，整块从未生效，故改为 more。 */
@media (prefers-contrast: more) {
    [data-ui~="chat.composer"]::before,
    #inputbar::before {
        background: linear-gradient(
            90deg,
            var(--mn-hc-orange),
            var(--mn-hc-yellow),
            var(--mn-hc-violet),
            var(--mn-hc-cyan),
            var(--mn-hc-yellow),
            var(--mn-hc-orange)
        );
    }
}

/* === 浏览器兼容性修复 === */
/* Firefox支持 */
@supports not (-webkit-mask-composite: destination-out) {
    [data-ui~="chat.composer"]::before,
    #inputbar::before {
        mask-composite: exclude;
    }
}

/* Safari支持 */
@supports (-webkit-mask-composite: destination-out) {
    [data-ui~="chat.composer"]::before,
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

The Project follows [AGPL-3.0 LICENSE](./LICENSE).
