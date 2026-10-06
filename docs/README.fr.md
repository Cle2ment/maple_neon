# Maple Neon : Un thème pour Cherry Studio

![Free Palestine](https://freepalestinemovement.org/wp-content/uploads/2013/06/banner.jpg)
![Cherry Studio](https://www.cherry-ai.com/assets/cherry-logo-CtmH594q.svg)
![Static Badge](https://img.shields.io/badge/Tailored_for-Cherry_Studio_v2.0%2B-red?logo=Github)
![Static Badge](https://img.shields.io/badge/License-AGPL--3.0-blue)
![Static Badge](https://img.shields.io/badge/Language-CSS-pink?logo=css)
![Static Badge](https://img.shields.io/badge/Release-v2.0.0-green)
<div style="text-align: center">
<a href="https://github.com/Cle2ment/maple_neon/blob/master/docs/README.zh.md">中文</a> |
<a href="https://github.com/Cle2ment/maple_neon/blob/master/README.md">English</a> |
Français |
<a href="https://github.com/Cle2ment/maple_neon/blob/master/docs/README.ja.md">日本語</a>
</div>

## Introduction

Ceci est un thème conçu pour Cherry Studio, un client de bureau qui prend en charge plusieurs fournisseurs de modèles de langage (LLM) et est disponible sur Windows, Mac et Linux. Ce thème cible **Cherry Studio v2.0+** et s'appuie sur l'API de thème v2 (variables CSS sémantiques et hooks `data-ui`). \
Pour plus d'informations sur Cherry Studio, consultez [ici](https://github.com/CherryHQ/cherry-studio).

## Comment utiliser

1. (Facultatif) Téléchargez les polices : Maple Mono NF CN depuis [Maple Font](https://github.com/subframe7536/maple-font/releases/download/v7.3/MapleMono-NF-CN-unhinted.zip) et DreamHan Sans / DreamHan Serif depuis [DreamHan Font](https://github.com/Pal3love/dream-han-cjk/releases). À défaut, les polices de secours (`Fira Code` / Microsoft YaHei) s'appliquent. Vous pouvez aussi choisir les polices déjà installées dans les **Paramètres de police** intégrés de Cherry Studio (police globale / police de code).
2. Copiez l'intégralité du fichier [maple-neon.css](../themes/maple-neon.css) — la version complète (polices + animation de bandeau néon + mappage des tokens officiels). Deux variantes allégées sont disponibles : [maple-neon-font-minimal.css](../themes/maple-neon-font-minimal.css) (polices uniquement) et [just-flowing-border.css](../themes/just-flowing-border.css) (animation de bordure fluide uniquement).
3. Dans Cherry Studio, ouvrez **Paramètres → Paramètres d'affichage → CSS personnalisé** et collez le CSS.
4. **Vous migrez depuis la v1 ?** En v2, votre ancien CSS personnalisé est automatiquement désactivé et une ligne de marqueur `/* cherry-studio:custom-css:v1 */` est ajoutée en tête. Remplacez tout le contenu par la version v2 de ce thème, sans conserver la ligne de marqueur.
5. La prise en effet est immédiate après l'enregistrement : vous pouvez prévisualiser et ajuster en direct.

<details>
<summary>Ou, si vous ne voulez pas modifier, copiez directement le CSS depuis ici !</summary>

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

## Qu'est-ce qui rend le thème spécial ?

- Il propose une interface utilisateur modernisée et esthétique pour Cherry Studio v2.0+, construite sur l'API de thème v2 (variables CSS sémantiques et hooks `data-ui`).
- Il mêle la police Maple à une zone de saisie au style néon, créant une expérience unique et visuellement attractive.
- Utilise la série de polices DreamHan et Microsoft YaHei pour fournir un excellent affichage des polices chinoises.
- Propose trois variantes : `maple-neon.css` (complète : polices + animation de bandeau néon + mappage des tokens officiels), `maple-neon-font-minimal.css` (polices uniquement) et `just-flowing-border.css` (animation de bordure fluide uniquement).

## Démonstration

Basé sur Cherry Studio v2.x
![Page claire](../examples/main-page-light.png)

![Page sombre](../examples/main-page-dark.png)

## Personnalisation

Le thème tire ses couleurs d'une petite palette définie en haut du CSS, dans `:root`. Pour le recolorer, modifiez ces variables plutôt que de chercher des couleurs codées en dur :

- `--mn-orange` : `#ff6a01`
- `--mn-yellow` : `#f8c91c`
- `--mn-violet` : `#8a2be2`
- `--mn-cyan` : `#00d4ff`

Vous pouvez aussi forker le projet et modifier votre propre thème pour Cherry Studio. Pour les instructions détaillées, consultez [Documentation Cherry Studio](https://docs.cherry-ai.com/personalization-settings/css).

## Un dernier coup d'œil

Pour d'autres thèmes, consultez [Un dernier coup d'œil](../OneMoreGlance.md)

## Inspirations

### Thèmes

- Thème Dracula : <https://cherrycss.com>
- Thème Neon : <https://cherry-ai.com/css>

### Polices

- Maple Font : <https://github.com/subframe7536/maple-font>
- DreamHan Sans : <https://github.com/Pal3love/dream-han-cjk/releases>

### Outils  

- Les Thèmes sont construits partiellement avec l'aide de DeepSeek-0324 & Claude-3.7.

## LICENCE

Le projet suit la [Licence AGPL-3.0](../LICENSE).
