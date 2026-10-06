# PROJECT KNOWLEDGE BASE

**Generated:** 2026-10-06
**Commit:** d6c264d (v2 migration uncommitted on top)
**Branch:** master
**Repo:** https://github.com/Cle2ment/maple_neon (renamed from Cle2ment/CherryStudio_themes; remote + README language links updated)

## OVERVIEW
Maple Neon — a pure CSS theme for Cherry Studio (desktop LLM client). Mixes Maple Mono font family with neon-styled input bar marquee animations. Targets **Cherry Studio v2.0+** (v2 theme API: unlayered custom CSS + semantic CSS variables + `data-ui` hooks). Zero build system, no JS/TS — users copy-paste CSS into 设置 → 显示设置 → 自定义 CSS.

## STRUCTURE
```
./
├── themes/       # Deliverable theme CSS (3 variants)
├── templates/    # Cherry Studio upstream CSS reference (gitignored, untracked — local-only)
├── docs/         # Multilingual README translations (zh, fr, ja)
├── examples/     # Screenshots (light/dark mode)
├── .github/      # CI: auto-syncs CSS into READMEs on push
├── .idea/        # JetBrains IDE config (SCSS watcher disabled)
└── .vscode/      # VS Code: AI assistant language set to zh-CN
```

## WHERE TO LOOK
| Task | Location | Notes |
|------|----------|-------|
| Modify the theme | `themes/maple-neon.css` | Canonical file; CI syncs to all READMEs |
| Understand Cherry Studio's CSS architecture | `templates/index.css` | **v1.2.x era reference** — antd/`[theme-mode]` based; do NOT use as v2 selector reference |
| Update Cherry Studio reference CSS | `templates/update-template.bat` | Downloads from upstream GitHub (still points at v1-era structure) |
| Add a translation | `docs/README.{lang}.md` | Mirror structure of `README.zh.md` |
| Preview screenshots | `examples/` | main-page-light.png / main-page-dark.png |
| CI pipeline | `.github/workflows/sync-theme-to-readme.yml` | Triggers on push to `themes/maple-neon.css` |

## CONVENTIONS
- **No build step** — theme ships as raw CSS. No `package.json`, no bundler, no npm.
- **v2 theme API rules (themes/)**:
  - **Zero `!important`** — custom CSS injects unlayered and beats layered built-ins; `!important` inverts layer order and can LOSE to built-in `!important`.
  - **Palette lives only in `:root`**: `--mn-orange` `#ff6a01` / `--mn-yellow` `#f8c91c` / `--mn-violet` `#8a2be2` / `--mn-cyan` `#00d4ff` (+ `--mn-hc-*` high-contrast set). Derive translucents via `color-mix()`, never inline hex twice. README customization docs reference these names — renaming breaks the contract.
  - **Selector hooks**: dark mode = `.dark`, light = `:root`/`.light` (`[theme-mode]` removed in v2). Structure = `[data-ui~='chat.composer']` etc. (`~=` only). `#inputbar` kept as v1 fallback (dual-written). No `.ant-*` (antd removed), no `[os=...]` (undocumented in v2).
  - **Fonts**: consume `var(--app-user-font-family, var(--user-font-family, <stack>))` (v2 name outer, v1 name inner).
  - **NEVER include** the line `/* cherry-studio:custom-css:v1 */` — it marks migrated v1 CSS and disables injection.
  - Token overrides: accent/interaction/code tokens only (`--primary`, `--ring`, `--link`, `--chart-*`, `--inline-code`, `--code-block`); never surface tokens (`--background`/`--card`/`--sidebar*`) — would dye the whole window.
- **`templates/` is gitignored and untracked** — local-only reference material; it never ships with the repo. `.gitignore` line 9 lists `/templates`; `git ls-files templates/` is empty.
- **Commit style**: `docs: ... [skip ci]` for CI auto-commits.
- **Comments**: Chinese inline, English for structural headers. Section dividers use `/* === SECTION === */`.
- **Font stack**: Maple Mono NF CN (code) + Microsoft YaHei (UI) + DreamHan Sans/Serif (Chinese). All optional — have fallbacks. Windows-specific fonts are merged into the main stacks (missing fonts auto-skip; no `[os]` branch).

## ANTI-PATTERNS (THIS PROJECT)
- **`!important`**: themes/ is now zero-`!important` by design (see CONVENTIONS). Legacy `!important` remains inside `templates/` (v1-era upstream reference) — do not copy patterns from there.
- **Unsystematic z-index**: Uses raw values -1, 1, 2, 3 without a documented scale. Document if adding new layers.
- **Dead code in templates**: See `templates/AGENTS.md` for specific locations and cleanup guidance.
- **Stale screenshots**: `examples/` still shows the v1 UI; v2 screenshots need a manual re-capture.

## UNIQUE STYLES
- **Three distinct variants (since v2 migration)**: `maple-neon.css` = full superset (fonts + palette + official token mapping + animations); `maple-neon-font-minimal.css` = fonts only (~59 lines); `just-flowing-border.css` = animation only (palette + marquee, no fonts/tokens). From the animation section to EOF, `just-flowing-border.css` is byte-identical to `maple-neon.css` — keep it that way when editing shared sections.
- **CSS embedded in READMEs**: All 4 READMEs contain an inline ` ```css ` block auto-synced by CI. NEVER manually edit the CSS block in READMEs — it will be overwritten.
- **Bilingual comments**: CSS uses Chinese comments (`/* 字体配置 */`) for section headers. New code should follow this style.
- **`prefers-contrast: more`**: v1 code used invalid value `high` (dead code, never matched); fixed to `more` in v2 migration — high-contrast users now actually get the `--mn-hc-*` palette. Do not revert to `high`.

## COMMANDS
```bash
# Update Cherry Studio reference templates
cd templates && .\update-template.bat

# Check what happens when theme is pushed (CI dry-run)
# CI triggers on: push to main/master, file changed: themes/maple-neon.css
```

## NOTES
- **Cherry Studio compatibility**: Theme targets **v2.0+** (verified against v2.1.x API). v1.2.x is no longer a target (v1 CSS pasted into v2 gets auto-disabled with a `/* cherry-studio:custom-css:v1 */` marker — READMEs document this for upgrading users). v2 API sources: `docs.cherryai.com.cn` custom-css page + `CherryHQ/cherry-studio` `packages/ui/docs/` (variable-catalog, design-token-system) + `docs/references/components/ui-semantic-contract.md`.
- **FIXMEs in templates/scrollbar.css**: v1-era upstream workarounds; `templates/` predates v2 and was not re-synced.
- **Verification** (no test suite): parse with `biome`; grep gates (`!important`=0, no `.ant-`/`[theme-mode`/`[os=`/`custom-css:v1`); variant keyframes byte-diff; optional browser harness (v2-mock DOM: host styles in `@layer` + `.dark` + `data-ui` hooks) for computed-style checks. Final visual check still requires pasting into the real Cherry Studio app.
- **Font downloads optional**: v2 has built-in 字体设置 (writes `--app-user-font-family`/`--app-user-code-font-family`); theme stacks still prefer Maple Mono NF CN / DreamHan if installed. See `README.md` for links.
