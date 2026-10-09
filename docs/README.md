# T.WU · Tingting Wu 的个人学术博客

这是吴亭亭（Tingting Wu）的个人学术主页与博客。南华大学临床医学专业
2024 级本科生（儿科方向），关注儿童精准医学、生物组学数据计算处理与
前沿医学文献阅读。

- 线上地址（首次部署后生效）：<https://lotuswutt.github.io/>
- GitHub：<https://github.com/LotusWuTT>
- ORCID：<https://orcid.org/0009-0009-7224-6978>

> 本文件放在 `docs/` 目录而不是仓库根目录，是为了避免 GitHub Pages
> 把它当作站点首页渲染。

## 技术栈

Hugo（Extended 0.160.x）+ Hugo Blox Kit（academic-cv 模板）+ Tailwind
CSS v4 + Pagefind 站内搜索。中文为默认语言，`/en/` 下有英文版首页。

## 本地预览

```bash
npm install          # 首次
hugo server --buildDrafts
# 打开 http://localhost:1313
```

正式构建：`hugo --gc --minify`（输出到 `public/`，已 gitignore）。

## 写一篇新文章

1. 新建目录：`content/blog/<英文小写短横线 slug>/index.md`
2. 按下面格式写 frontmatter：

```yaml
---
title: '文章标题'
summary: '一句话摘要（列表卡片用）。'
date: '2026-10-09'
authors:
  - tingting-wu
tags:
  - Research Notes      # 类型标签：Course Notes / Research Notes / Tools / Opinion / Method Notes
  - Multi-omics         # 主题标签随意加
categories:
  - research-notes
---
```

3. 正文是 Markdown；引用文献尽量给 `https://doi.org/...` 链接。
4. `hugo server --buildDrafts` 预览无误后 commit + push 即自动发布。

## 部署到 GitHub Pages（一次性）

1. 用她的 GitHub 账号（LotusWuTT）新建公开仓库，名字必须是
   **`LotusWuTT.github.io`**（这样站点地址才是
   `https://lotuswutt.github.io/`）。
2. 在本目录：

```bash
git remote add origin https://github.com/LotusWuTT/LotusWuTT.github.io.git
git push -u origin main
```

3. 仓库 **Settings → Pages → Source 选择 "GitHub Actions"**（重要，
   不要选 Branch）。
4. 等 Actions 跑完（约一分钟），打开 `https://lotuswutt.github.io/`。

之后每次 `git push`，GitHub Actions 会自动重新构建和发布。

> 如果想改用现有的 `T.WU` 仓库作为项目页（地址会变成
> `https://lotuswutt.github.io/T.WU/`），需要同步修改
> `config/_default/hugo.yaml` 与 `hugoblox.yaml` 里的 `baseURL`。
> 推荐还是用 `LotusWuTT.github.io` 用户站点，地址更干净。

## 日常维护入口

| 想改什么 | 改哪里 |
|---|---|
| 个人简介 / 方向 / 链接 | `data/authors/tingting-wu.yaml` |
| 首页各板块文案 | `content/_index.md`（中文）、`content/_index.en.md`（英文） |
| 站点名 / 导航菜单 | `config/_default/languages.yaml`、`params.yaml` |
| 主题色 | `params.yaml` 的 `colors.primary` + `assets/css/main.css` 里的 `#9d174d` / `#f9a8d4` |

更多工程细节（版本锁定、CI 注意事项、常见坑）见仓库根目录 `AGENTS.md`。
