---
name: content-site-generator
description: >
  Generate structured documentation projects that produce both organized Markdown files and a polished single-page static website with sidebar navigation, slide-based presentation, and fullscreen mode. Use this skill whenever the user wants to: create a documentation site, build a knowledge base or plan document, organize information into a browsable static site, turn research or notes into a structured web-viewable format, or produce a "slide deck style" HTML document from content. Also trigger when the user mentions "建站", "靜態站", "文件網站", "資訊整理成網站", "做一個站台", or references generating docs/ + index.html output. If the user pastes information and wants it organized into a presentable format with navigation, use this skill.
---

# Content Site Generator

This skill produces documentation projects: a set of organized Markdown files in `docs/` plus a single-file static HTML website (`index.html`) that renders them as a navigable, presentation-ready site.

## Why this structure matters

The dual-output approach (Markdown + HTML) serves two purposes. The Markdown files are the source of truth — easy to version-control, diff, and edit. The HTML site makes the same content instantly presentable to stakeholders, teammates, or anyone with a browser. The site includes sidebar navigation, keyboard shortcuts, and a fullscreen presentation mode, so the same content works for both reading and presenting.

## Workflow

### Step 1: Understand the content

Read what the user provides — it could be raw text, meeting notes, research data, a topic direction, or a mix. Identify the natural structure: what are the major themes? What's the logical reading order? Are there relationships between sections (e.g., one section references another)?

If the user's input is vague, ask what audience the site is for and what level of detail they need. But if the input is rich enough, proceed directly.

### Step 2: Plan the document structure

Before writing anything, outline the chapter plan. Each chapter becomes one Markdown file and one slide in the HTML site. A typical project has 5–15 chapters.

Create a plan like this:
- 00: Cover / Overview (always present — summarizes the whole project)
- 01–N: Content chapters in logical order
- A1–AN: Appendices (optional — for supporting material, references, deep dives)

Share the outline with the user for confirmation before proceeding. Keep chapter titles concise (2–6 words).

### Step 3: Create the docs/ folder

Create `docs/INDEX.md` first — it's the table of contents. Then create each chapter as a numbered Markdown file.

**INDEX.md format:**
```markdown
# [Project Title] — 文件目錄

> **版本**：v1.0 | **最後更新**：[date]

---

## 文件結構

| 編號 | 文件 | 說明 |
|------|------|------|
| 01 | [章節標題](./01-slug.md) | 一句話說明 |
| 02 | [章節標題](./02-slug.md) | 一句話說明 |
...

### 附錄

| 編號 | 文件 | 說明 |
|------|------|------|
| A | [附錄標題](./appendix-slug.md) | 說明 |

---

## 快速導覽

**想了解 X？** → [01 章節名](./01-slug.md) + [02 章節名](./02-slug.md)
...
```

**Chapter file format:**
```markdown
# [Number]. [Title]

> 所屬文件：[INDEX](./INDEX.md)

---

## Section heading

Content here — use tables, lists, code blocks, diagrams as appropriate.
The markdown should be clean and readable on its own.
```

### Step 4: Generate index.html

This is the core output. Read `references/html-template.html` in this skill's directory to get the complete HTML boilerplate — it contains all the CSS, JavaScript, and structural HTML you need. Copy it as your starting point, then:

1. **Update metadata**: Change the `<title>`, sidebar header text, and version string.
2. **Create Slide 0 (Cover)**: Always a centered overview with project title, key stats, and chapter listing table.
3. **Create Slides 1–N**: One `<div class="slide">` per chapter. Convert the Markdown content into HTML using the component library (see `references/component-guide.md`).
4. **Create Appendix slides** (if any): Same structure, but use `data-num="A1"` etc.

Each slide follows this pattern:
```html
<div class="slide" data-title="章節標題" data-num="01">
  <div class="slide-card">
    <h2>章節完整標題</h2>
    <div class="subtitle">Chapter 01 — 副標題或簡述</div>
    <!-- Content converted from markdown using component classes -->
  </div>
</div>
```

The JavaScript automatically builds the sidebar navigation and progress dots from the `data-title` and `data-num` attributes — no manual nav creation needed.

The template also includes a **content width toggle** (中 / 大 / Full) in the topbar, allowing users to switch between three reading widths: 860px (中), 1200px (大), and 100% (Full). The user's choice is persisted via `localStorage`. The toggle is automatically hidden in fullscreen presentation mode. See `references/component-guide.md` § 16 for full CSS/HTML/JS details.

### Step 5: Handle assets (images)

If the user provides images, save them in an `assets/` folder at the project root. Reference them in the HTML with relative paths:

```html
<img class="zoomable" src="assets/diagram.png" alt="描述" style="max-width:100%; border-radius:10px; margin:16px 0;">
```

**All `<img>` tags must include `class="zoomable"`** to enable click-to-zoom (lightbox). The HTML template already contains the lightbox overlay, CSS, and JavaScript — just add the class and it works. The only exception is the lightbox's own `<img id="lightboxImg">` element, which should never have this class.

Images can also be placed inside `.slide-card` with appropriate sizing. For simple text-based diagrams (timelines, directory trees, step lists), use the `.diagram` CSS class (dark code-block style). For **architecture diagrams** (system structure, flowcharts, data flows), use Mermaid — see below.

### Step 5b: Mermaid diagrams (architecture diagrams only)

Not all diagrams should use Mermaid. Use Mermaid specifically for **architecture diagrams** — system structure, component relationships, flowcharts with decision points, Gantt charts, and sequence diagrams. For plain-text timelines, tree structures, or simple step lists (fewer than 3 steps), stick with the `.diagram` CSS class.

The HTML template already includes Mermaid.js (CDN v11.12.0) and the `initMermaid()` function. To add a Mermaid diagram to a slide:

```html
<div class="mermaid-wrap">
  <div class="mermaid">
graph TD
  A[Component A] --> B[Component B]
  B --> C[Component C]

  classDef blue fill:#e8f0fe,stroke:#0066cc,color:#1d1d1f
  class A,B,C blue
  </div>
  <div class="mermaid-label">▲ Diagram caption</div>
</div>
```

**Critical rules for Mermaid syntax** (these cause rendering failures if ignored):

1. **No emoji** — SVG renderer cannot calculate emoji character widths, producing `<rect> attribute width: negative` errors. Write `A[Mac Mini]` not `A["🖥 Mac Mini"]`.
2. **No `\n` line breaks in labels** — use ` - ` to join text instead. Write `A[First - Second]` not `A["First\nSecond"]`.
3. **No special characters** — avoid fullwidth parentheses `（）`, arrows `⇄`, middle dots `·`. Use ASCII equivalents.
4. **Use `classDef` for batch styling** — more stable than per-node `style` directives.
5. **Hidden DOM workaround** — because `.slide` defaults to `display: none`, the template's `initMermaid()` temporarily makes all slides visible before calling `mermaid.run()`, then restores them. After rendering, it calls `_mermaidInjectExpandButtons()` to add fullscreen expand buttons. This is already handled in the template — no extra work needed.

The template also includes a **click-to-fullscreen** feature for all Mermaid diagrams: hovering shows an expand icon in the top-right corner, and clicking opens a fullscreen overlay (94vw × 92vh white card with blur backdrop) displaying the SVG scaled to fill the available space. Users can close it via the ✕ button, ESC key, or clicking the dark background. This is fully automatic — no extra HTML or JS needed beyond the standard `.mermaid-wrap` structure. See `references/component-guide.md` § 18 for implementation details.

See `references/component-guide.md` § 17–18 for the complete Mermaid component reference including CSS, supported chart types, color definitions, and fullscreen overlay details.

### Step 6: Create CLAUDE.md

Create a `CLAUDE.md` at the project root as a guide for future AI assistants (or yourself) working on this project. This file ensures anyone maintaining the site later understands the project structure and the docs-to-HTML sync workflow.

The CLAUDE.md should include:

1. **專案概述** — What the project is about, in one or two sentences. Mention this is a report-style static site — all pages are pure HTML with no server-side dependencies, so it can be viewed by opening `index.html` directly in a browser via `file://` protocol (no web server or `localhost` needed).
2. **專案結構** — A file tree showing `CLAUDE.md`, `index.html`, `docs/`, and `assets/` (if present), with brief annotations.
3. **關鍵概念** — Key domain terms or concepts specific to this project, so future editors have context.
4. **網站更新流程** — Step-by-step instructions for syncing changes:
   - How to check which docs changed (`git diff`)
   - How to identify which parts of `index.html` need updating
   - How to update `index.html` (it's a single-file static site with all content embedded)
   - How to verify and commit (`git add` + `git commit` with conventional commit prefix)
5. **驗證方式** — Explain that since the site is fully static, verification should be done by opening `index.html` directly with a browser (e.g., `open index.html` on macOS). Do NOT start a localhost server — it's unnecessary for a static single-file site.
6. **Mermaid 圖表規範** (if the project uses Mermaid) — When to use Mermaid vs `.diagram`, syntax rules (no emoji, no `\n`, no special characters), HTML usage pattern, click-to-fullscreen overlay feature (related CSS classes, HTML structure, JS injection mechanism, and implementation notes), and link to `docs/mermaid-guide.md` if one exists.
7. **工作慣例** — Conventions: language (繁體中文), commit message prefixes (`feat:` / `fix:` / `docs:` / `style:`), version number location (`docs/INDEX.md`), and the rule to update INDEX.md version/date after changes.

Use the project's actual file names, chapter titles, and structure — not generic placeholders. Write in 繁體中文 to match the project content.

### Step 7: Verify and deliver

After generating both the docs/ and index.html:
1. Verify the slide count matches the chapter count + cover + appendices
2. Verify all `data-num` values are sequential and correct
3. Verify the INDEX.md lists every chapter
4. Open `index.html` directly in the browser to spot-check rendering (e.g., `open index.html` on macOS). Since the site is fully static with no external dependencies, it works via `file://` protocol — do NOT start a localhost server, it's unnecessary.

Deliver the complete project folder to the user.

## Design style

This skill uses **UED AI design language** — the same style as UED AI 成果分享 presentations:
- **Cover**: blue-purple mesh gradient (`#72C9B8 → #6EA8F5 → #7B8FF5 → #A78BFA`)
- **Content slides**: white cards with navy headings (`#1B2559`) and blue accent bar (`#4A7CF7 → #7B6FF0`)
- **Cards**: colored backgrounds (blue/purple/green/orange/yellow)
- **Font**: Noto Sans TC (Google Fonts)

## Layout selection guide

Map each content type to the best layout before writing HTML:

| Content type | Layout | Components |
|-------------|--------|------------|
| 封面 | cover | `.slide-cover` + `.cover-inner` + `.cover-title` |
| 章節轉場 | section-header | `.slide-section-bg` + `.section-big-title` |
| 一般說明 | standard | `accent-bar` + `.key-point` + paragraphs |
| 兩項對比 | two-col | `.two-col` + `.card` × 2 |
| 三類分群 | three-col | `.three-col` + `.card` × 3 |
| 調查/統計 | bar-chart | `.bar-row` + `.bar-track` in `.two-col` |
| 排行榜 | ranking | `.rank-item` + `.rank-medal` |
| 流程時間軸 | timeline | `.timeline` + `.tl-step` + `.tl-line` + `.three-col` |
| 功能截圖 | screenshot | `.two-col` + `.screenshot-box` |

## Content conversion guidelines

When converting Markdown content to HTML for slides, the goal is to make information scannable and visually structured. Don't just wrap paragraphs in `<p>` tags — actively use the component library to make the content engaging:

- **Every non-cover slide** → use `.slide-title-wrap` + `.accent-bar` + `<h2>` (NOT plain `<h2>`)
- **Key takeaways** → `.key-point` callout
- **Two topics side by side** → `.two-col` with `.card` variants
- **Three categories** → `.three-col` with `.card` variants (blue/purple/green)
- **Survey / usage data** → `.bar-row` + `.bar-track` horizontal bar chart
- **Rankings** → `.rank-item` + `.rank-medal` + `.rank-title`
- **Project phases** → `.timeline` + `.tl-step` with three-col phase cards below
- **Process flows** → `.flow` + `.flow-step` + `.flow-arrow`
- **Comparisons / structured data** → `.table-wrap` + `<table>` with colored rows
- **Metrics / numbers** → `.stat-row` + `.stat-card` or `.stat-number` (big)
- **Section grouping** → `.section-banner` with gradient colors
- **Important notes** → `.info-box` (blue) or `.info-box.warn` (orange)
- **Architecture diagrams** (system structure, component relationships) → `.mermaid-wrap` + Mermaid syntax
- **Text diagrams** (timelines, trees, simple code blocks) → `.diagram` (dark block)
- **Tags / categories** → `.pill` or `.badge` (UED badge: `.badge-blue`, `.badge-purple`, etc.)

Read `references/component-guide.md` for the complete set of available components with examples. Sections 19–29 cover all UED-specific layouts.

## Language convention

Write all documentation content in **繁體中文** (Traditional Chinese) unless the user explicitly requests another language. Technical terms and proper nouns can remain in English.

## File naming convention

- Markdown files: `[number]-[english-slug].md` (e.g., `01-core-concept.md`)
- INDEX.md: always uppercase
- index.html: always lowercase
- Assets: descriptive English names (e.g., `network-diagram.png`)
