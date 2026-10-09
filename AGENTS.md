# AGENTS.md — Project context for any agent working on this blog

> Read this file first if you've been asked to update or modify the blog.
> It collects everything that took hands-on time to learn, so you don't
> have to re-learn it. Keep it updated as the project evolves.

---

## 0. TL;DR

This is the personal academic website of **Tingting Wu (吴亭亭)**, an
undergraduate medical student (Clinical Medicine, Pediatrics track,
Class of 2024) at the University of South China.

Target hosting: **`https://lotuswutt.github.io/`** (GitHub Pages, rebuilt
from this repo on every push to `main` via GitHub Actions). The repo on
GitHub must be named **`LotusWuTT.github.io`** for the user-site URL to
work. If she instead wants to use the existing empty `T.WU` repo as a
*project* site, change `baseURL` in `config/_default/hugo.yaml` and
`hugoblox.yaml` to `https://lotuswutt.github.io/T.WU/`.

**Stack (inherited from the reference site at `D:\bloh\blog`):**

```
Hugo (Extended, pinned 0.160.x) ──► Hugo Blox Kit 0.12 (Go modules)
                          └──► Tailwind CSS v4 (compiled at build time)
                          └──► Pagefind (search index)
Default content language: zh (locale zh-CN) with an English homepage edition.
```

**Brand voice:** academic, restrained, evidence-first. No marketing copy.

---

## 1. The person behind the site

| Field | Value |
|---|---|
| 中文名 | 吴亭亭 |
| 英文名 / 显示名 | **Tingting Wu** |
| 角色 | Undergraduate medical student (在读本科) |
| 专业 | 临床医学（儿科方向），2024 年 9 月入学 |
| 单位 | 南华大学 医学院 (School of Medicine, University of South China), Hengyang, Hunan |
| GitHub | `LotusWuTT` |
| ORCID | `https://orcid.org/0009-0009-7224-6978` |
| 拼音 | Wú Tíngtíng, she/her |
| 技能背景 | 生物组学数据计算处理经验；较好的（英文）文献阅读能力 |
| 邮箱 | 暂无 — 需本人补充后加进 `links` 与首页 Contact |

> ⚠️ Skills in the author profile (R/Python, Zotero, levels) are reasonable
> defaults inferred from her background — confirm with her and adjust.

The author profile (used by the homepage hero + every blog post byline)
lives at **`data/authors/tingting-wu.yaml`**. **Always edit that file** if
you need to change name, role, links, bio, experience, skills, languages,
or interests.

> The short bio in `bio:` is what fills the "About" section on the
> homepage hero. Keep it bilingual (English first, then Chinese).

---

## 2. Repo layout

```
D:\amydream\amyting\blog\
├── .github/workflows/deploy.yml   ← GH Pages CI (hugo + npm install)
├── .nojekyll                     ← disables GH Pages' default Jekyll renderer
├── .gitignore                    ← excludes public/, resources/, node_modules/
├── AGENTS.md                     ← you are here
├── docs/README.md                ← maintainer guide (not served)
│
├── assets/css/main.css           ← ALL custom styling; design tokens --tt-*
├── config/_default/              ← 5 Hugo config files (see §3)
├── content/
│   ├── _index.md                 ← Chinese homepage widget list
│   ├── _index.en.md              ← English homepage
│   ├── authors/tingting-wu/      ← author index page
│   ├── blog/                     ← blog posts (page bundles)
│   │   └── reading-frontier-medicine-01/   ← first post
│   └── publications/             ← placeholder section (no publications yet)
│
├── data/authors/tingting-wu.yaml ← author profile (single source of truth)
├── hugoblox.yaml                 ← project metadata (baseURL, title)
├── go.mod / go.sum               ← Go module manifest for Hugo Blox imports
├── package.json / pnpm-lock.yaml ← Tailwind v4 + Pagefind runtime
├── netlify.toml                  ← leftover from template, unused
├── themes/                       ← intentionally empty (Go modules, not submodules)
├── layouts/                      ← local overrides (language chooser, flat cards,
│                                    cover suppression, favicon handling)
├── static/uploads/               ← static uploads (CV pdf, future images)
├── i18n/                         ← empty (bundles come from Hugo Blox module)
└── archetypes/                   ← `hugo new` templates
```

### Design tokens

`assets/css/main.css` uses `--tt-*` variables (paper / ink / rule / accent).
Accent color is **deep rose `#9d174d`** (light) / `#f9a8d4` (dark) — it must
stay in sync with `hugoblox.theme.colors.primary` in
`config/_default/params.yaml` (hover colors are hardcoded in main.css).

---

## 3. Config files (under `config/_default/`)

| File | Purpose |
|---|---|
| `hugo.yaml` | Base Hugo config (`baseURL`, language, build flags) |
| `languages.yaml` | Chinese/English definitions, titles, descriptions, nav menus |
| `menus.yaml` | Empty fallback; active menus live in `languages.yaml` |
| `module.yaml` | Hugo Blox Go-module imports. **Do not touch** without reason |
| `params.yaml` | **Site identity** (name, tagline, description), theme colors, header. Most likely file for branding changes |

The root `hugoblox.yaml` is **project metadata** (baseURL, title, keywords) —
keep it in sync with `hugo.yaml`/`params.yaml` when the URL or identity
changes.

---

## 4. Content conventions

### 4.1 Frontmatter

Posts (YAML):

```yaml
---
title: "My post"
summary: "One-liner for cards & SEO."
date: "2026-10-09"
authors:
  - tingting-wu
tags:
  - Research Notes     # type label, see §4.2
  - <topic-tag>
categories:
  - research-notes     # mirrors the primary tag
---
```

### 4.2 Tag taxonomy

Top-level tags are **type labels** — use one on every post:

| Tag | When |
|---|---|
| `Course Notes` | 课程学习笔记 |
| `Research Notes` | 阅读笔记 / 复现 / 思考 |
| `Tools` | 工具、资源、教程 |
| `Opinion` | 立场稿、反思 |
| `Method Notes` | 具体方法的笔记 |

Then add **subject tags** freely: `Literature Reading`, `Precision Medicine`,
`Multi-omics`, `Pediatrics`, `Genetics`, `Single-cell`, `AI in Medicine`, …

### 4.3 Posts structure

Each post lives in `content/blog/<slug>/index.md` as a **page bundle**.
**Slug rules:** lowercase ASCII, hyphen-separated (e.g.
`reading-frontier-medicine-01`).

### 4.4 Homepage widgets

`content/_index.md` is the landing-page widget list:

1. `resume-biography-3` — Hero (id: `about`)
2. `markdown` — Current work (id: `now`), Interests (id: `research`), Contact (id: `contact`)
3. `collection` — Blog aggregation (id: `writing`)

Section ids are load-bearing: `main.css` styles `#now`, `#research`,
`#contact`, `#writing` by id, and menus link `/#about`, `/#research`,
`/#writing`. Keep them.

### 4.5 Bilingual structure

- Default language `zh` (locale zh-CN); English at `/en/` (`.en.md` suffixes).
- The English homepage links selected Chinese posts with translated titles.
- Add `index.en.md` beside a post when a full translation is ready.

### 4.6 Citations in posts

Prefer DOI links (`https://doi.org/...`) and **verify every DOI before
publishing** (a plain `curl -s -o /dev/null -w "%{http_code}" -L
https://doi.org/<doi>` returning 200/302/403 is a pass; 404 means broken).
When a DOI can't be verified, cite textually (journal + year) and point to
a search URL instead of guessing the DOI.

---

## 5. Build / dev / deploy workflow

### 5.1 Local dev

Prerequisites: **Hugo Extended 0.160.x** (0.162+ breaks the
css.TailwindCSS pipeline with Hugo Blox 0.12 — see §8).

```bash
cd D:\amydream\amyting\blog
npm install                  # first time only
hugo server --buildDrafts    # http://localhost:1313
```

### 5.2 Production build

```bash
hugo --gc --minify
```

Outputs to `public/` (gitignored). Never commit `public/`, `resources/`,
`hugo_stats.json`.

### 5.3 GitHub Pages CI

`.github/workflows/deploy.yml` runs on every push to `main`:
checkout → Go 1.23 → Node 20 → Hugo 0.160.1 Extended → `npm install` →
`hugo --gc --minify --printPathWarnings` → deploy artifact.

**One-time setup on her GitHub account:**

1. Create repo **`LotusWuTT/LotusWuTT.github.io`** (public, empty).
2. Push this project: `git remote add origin
   https://github.com/LotusWuTT/LotusWuTT.github.io.git && git push -u origin main`.
3. Repo Settings → Pages → **Source: "GitHub Actions"** (not "Branch").
4. First deploy takes a minute; then `https://lotuswutt.github.io/` is live.

**CRITICAL:** Pages Source must be "GitHub Actions". If it flips back to a
branch, the site serves Jekyll output instead.

---

## 6. Common tasks — quick recipes

### 6.1 Add a new blog post

```bash
mkdir content/blog/<slug>
```

Write `content/blog/<slug>/index.md` with the frontmatter from §4.1.
Cards, RSS and the search index pick it up automatically.

### 6.2 Update author bio / role / links

Edit `data/authors/tingting-wu.yaml` — single source of truth.

### 6.3 Change site name / tagline

Edit `config/_default/params.yaml` → `hugoblox.identity` **and**
`languages.yaml` titles **and** `hugoblox.yaml` (keep in sync).

### 6.4 Change accent color

1. `config/_default/params.yaml` → `hugoblox.theme.colors.primary`
2. `assets/css/main.css` → `--tt-accent-warm` (light+dark) and the
   hardcoded hover colors (`#9d174d` / `#f9a8d4`).

### 6.5 Add email / more links

Add to `links:` in `data/authors/tingting-wu.yaml`, then mirror in the
Contact section of `content/_index.md` and `_index.en.md`.

---

## 7. Verification checklist before any "all done"

```bash
# 1. Build succeeds
hugo --gc --minify

# 2. Local preview shows intended change
hugo server --buildDrafts    # open localhost:1313

# 3. CSS is fresh and single-entry (no custom.css)
ls public/css/

# 4. Identity fields present
grep -E "Tingting Wu|吴亭亭|LotusWuTT" public/index.html

# 5. Post exists
ls public/blog/reading-frontier-medicine-01/index.html

# 6. Commit + push
git add -A && git commit -m "<what changed>" && git push origin main
```

---

## 8. Lessons inherited from the reference site (do not repeat)

1. **Pin Hugo to 0.160.x.** Hugo 0.162 changed the `css.TailwindCSS`
   sandbox config; Hugo Blox 0.12 + Tailwind v4 fails the build on 0.162+.
2. **No README.md at repo root** — GH Pages may Jekyll-render it over the
   site. Keep it at `docs/README.md`; `.nojekyll` exists at root for
   defense in depth.
3. **Only one CSS entry file** (`assets/css/main.css`). A second file
   alongside it gets emitted too and fights it.
4. **Never run `hugo mod tidy` in CI** — it rewrites go.mod/go.sum and can
   pull an incompatible Hugo Blox minor. The manifest is committed.
5. **Use `npm install` in CI**, not `pnpm install` (pnpm isn't in PATH on
   the runner after setup-node; npm works fine for these deps).
6. **Never commit** `public/`, `resources/`, `hugo_stats.json`,
   `node_modules/`.

---

## 9. Public URLs

| URL | What |
|---|---|
| `https://lotuswutt.github.io/` | Production site (after first deploy) |
| `https://github.com/LotusWuTT/LotusWuTT.github.io` | Target repo (create it) |
| `https://github.com/LotusWuTT` | Her GitHub account |
| `https://orcid.org/0009-0009-7224-6978` | Her ORCID |

---

## 10. Style + voice notes for user-facing prose

- **No marketing tone.**
- **Bilingual posture:** Chinese posts are primary; mirror key statements
  in English on the English homepage.
- **Citations > opinions.** Claims about the literature link the paper.
- **She is a medical student, not a PI.** Voice should be a learner who
  reads carefully and says precisely what she verified — never overclaim.

---

## 11. Change log

- **2026-10-09** — Site created from the reference blog at `D:\bloh\blog`
  (Hugo + Hugo Blox academic-cv, bilingual, flat academic cards). Personal
  identity, author profile, homepages, publications placeholder and color
  scheme rewritten for Tingting Wu. First post added:
  `reading-frontier-medicine-01` (frontier-medicine reading framework +
  three-direction digest, all citations DOI-verified).
