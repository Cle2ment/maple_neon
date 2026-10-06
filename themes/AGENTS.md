# themes/ KNOWLEDGE BASE

## OVERVIEW
3 self-contained CSS files users copy-paste into Cherry Studio **v2**'s 自定义 CSS panel (设置 → 显示设置). No build step, no @import between them. All files target the v2 theme API (unlayered injection + semantic CSS variables + `data-ui` hooks); full rules live in the root AGENTS.md.

## STRUCTURE
| File | Lines | Scope |
|------|-------|-------|
| `maple-neon.css` | 369 | Full superset: fonts + palette + official token mapping (`:root` + `.dark`) + marquee animations |
| `just-flowing-border.css` | 282 | Border animation only — no fonts, no token mapping. Contributed by @XiuDayyds |
| `maple-neon-font-minimal.css` | 59 | Fonts only (the v2 migration replaced the old byte-identical duplicate) |

## WHERE TO LOOK
| Task | File | Notes |
|------|------|-------|
| Modify the theme | `maple-neon.css` | Canonical file; CI syncs it into all READMEs on push |
| Border animation subset | `just-flowing-border.css` | From the animation section to EOF it is byte-identical to `maple-neon.css` — edit both in sync |
| Palette | `:root` of any file | `--mn-orange/-yellow/-violet/-cyan` + `--mn-hc-*`; README customization docs reference these names |
| Z-index stacking | `maple-neon.css` | `::before` = -1 (behind), `input/textarea` = 2 (foreground), `.ai-status-dot` = 3 (top) |
| Browser compat patches | `maple-neon.css` | `@supports` blocks at end: Firefox vs Safari mask rendering |

## CONVENTIONS
- Section dividers use Chinese inline comments: `/* === 字体配置 === */`. English only for browser compat notes.
- Shared keyframes (`ai-running-gradient`, `ai-thinking-pulse`, `ai-data-flow`) are byte-identical in the two files that have animations.
- Composer anchor is dual-written: `[data-ui~='chat.composer']` (v2) + `#inputbar` (v1 fallback). Neon border rendered via `::before` double-mask technique (`mask` + `-webkit-mask`, `mask-composite: exclude`).
- Activation: `:focus-within::before` is the primary trigger; `.ai-active` / `[data-ai-status="running"]` kept as best-effort enhancements (unverified in v2 DOM).
- Translucent derivatives use `color-mix(in srgb, var(--mn-*) N%, transparent)` — no `rgba()` literals.
- Fonts consume dual fallbacks: `var(--app-user-font-family, var(--user-font-family, <stack>))` (v2 name outer, v1 name inner).
- Responsive: `@media (max-width: 768px)`. Accessibility: `prefers-reduced-motion` + `prefers-contrast: more`.
- Zero `!important` by design (unlayered injection already wins — see root AGENTS.md).

## ANTI-PATTERNS (THEMES)
- **Do not reintroduce `!important`** — it inverts cascade-layer order and can lose to built-in `!important`.
- **Do not inline palette hex values** outside the `:root` definitions.
- **Do not use** `.ant-*` / `[theme-mode=...]` / `[os=...]` selectors, or the `/* cherry-studio:custom-css:v1 */` marker line.
- **Keep the 3 keyframes byte-identical** across `maple-neon.css` and `just-flowing-border.css`.
- **`prefers-contrast` valid values** are `no-preference | less | more | custom` — v1's `high` was an invalid value (dead code) fixed during migration; do not revert.
