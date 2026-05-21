# mafei 的技术博客

基于 **Hexo** 框架 + **Fluid** 主题搭建的个人技术博客，部署在 **GitHub Pages**。

- 博客地址：https://1823184701.github.io/mafei.github.io/
- 源码仓库：https://github.com/1823184701/mafei.github.io

---

## 目录结构

```
myweb/
├── node_modules/          # 依赖包（已 gitignore）
├── public/                # 构建生成的静态文件（已 gitignore）
├── scaffolds/             # 文章模板（scaffolds）
│   ├── post.md            #   文章模板
│   ├── draft.md           #   草稿模板
│   └── page.md            #   页面模板
├── source/                # 源文件目录
│   └── _posts/            #   ← 文章存放位置
│       └── hello-world.md
├── themes/                # 主题目录
├── _config.yml            # ★ 站点主配置文件
├── _config.fluid.yml      # ★ Fluid 主题配置文件
├── package.json           # Node.js 依赖管理
└── .gitignore
```

---

## 文章管理

### 文章存放位置

所有文章存放在 **`source/_posts/`** 目录下，格式为 Markdown (`.md`) 文件。

### 创建新文章

**方式一：命令行（推荐，自动生成模板）**
```
npx hexo new post "文章标题"
```

**方式二：手动创建**
在 `source/_posts/` 下手动新建 `.md` 文件，需包含 Front-matter。

### 文章格式示例

```markdown
---
title: 文章标题
date: 2026-05-21 23:30:00
updated: 2026-05-22 10:00:00
tags:
  - JavaScript
  - 前端
categories:
  - 技术分享
cover: /img/cover.jpg        # 封面图（可选）
excerpt: 这是一段文章摘要     # 摘要（可选）
---

## 这里是正文

支持完整的 **Markdown** 语法：

### 代码块

```javascript
function hello() {
  console.log("Hello World!");
}
```

### 表格

| 列1 | 列2 |
|-----|-----|
| 内容 | 内容 |

### 图片

![替代文字](/img/example.jpg)

### 链接

[GitHub](https://github.com)

### 引用

> 这是一段引用文字

### 列表

- 无序列表项 1
- 无序列表项 2

1. 有序列表项 1
2. 有序列表项 2
```

### Front-matter 字段说明

| 字段 | 必填 | 说明 |
|------|------|------|
| `title` | ✅ | 文章标题 |
| `date` | ✅ | 发布日期（`hexo new` 自动生成） |
| `updated` | ❌ | 更新日期（留空自动取文件 mtime） |
| `tags` | ❌ | 标签（数组） |
| `categories` | ❌ | 分类（数组，支持层级如 `[技术, 前端]`） |
| `cover` | ❌ | 封面图路径 |
| `excerpt` | ❌ | 文章摘要（不填则自动截取开头） |

### 文章模板（scaffolds）

`scaffolds/post.md` 是文章模板，`hexo new post` 会按此生成新文件：

```markdown
---
title: {{ title }}
date: {{ date }}
tags:
---
```

可自行修改模板内容，添加常用字段（如 `categories:`、`cover:`）。

### 草稿功能

```bash
npx hexo new draft "草稿标题"    # 创建草稿（存于 source/_drafts/）
npx hexo publish "草稿标题"      # 发布草稿
```

---

## 配置管理

### 配置文件位置

| 文件 | 作用 | 路径 |
|------|------|------|
| **`_config.yml`** | ★ 站点主配置 | 项目根目录 |
| **`_config.fluid.yml`** | ★ Fluid 主题配置 | 项目根目录 |
| `package.json` | Node.js 依赖 | 项目根目录 |
| `.gitignore` | Git 忽略规则 | 项目根目录 |
| `scaffolds/post.md` | 文章模板 | `scaffolds/` |

### 博客名称修改

编辑 **`_config.yml`** 中的 `title` 字段：

```yaml
# _config.yml
title: mafei 的技术博客          # ← 浏览器标签标题
subtitle: '记录技术与思考'        # ← 副标题（首页显示）
author: mafei                    # ← 作者名
description: '个人技术博客...'    # ← 站点描述（SEO）
language: zh-CN                  # ← 语言
timezone: 'Asia/Shanghai'        # ← 时区
```

修改后需重新部署生效：
```bash
npx hexo clean && npx hexo generate && npx hexo deploy
```

### 博客名称在导航栏的显示

编辑 **`_config.fluid.yml`** 中的 `navbar.blog_title`：

```yaml
# _config.fluid.yml
navbar:
  blog_title: "mafei 的技术博客"   # ← 导航栏左侧标题
```

### 常用配置项速查

#### `_config.yml`（站点主配置）

| 配置项 | 说明 | 当前值 |
|--------|------|--------|
| `title` | 站点标题 | mafei 的技术博客 |
| `subtitle` | 副标题 | 记录技术与思考 |
| `author` | 作者 | mafei |
| `language` | 语言 | zh-CN |
| `timezone` | 时区 | Asia/Shanghai |
| `url` | 站点 URL | https://1823184701.github.io/mafei.github.io |
| `permalink` | 文章链接格式 | `:year/:month/:day/:title/` |
| `theme` | 使用的主题 | fluid |
| `deploy.type` | 部署方式 | git |
| `deploy.repo` | 部署仓库 | https://github.com/1823184701/mafei.github.io.git |
| `deploy.branch` | 部署分支 | gh-pages |
| `index_generator.per_page` | 首页每页文章数 | 10 |

#### `_config.fluid.yml`（主题配置节选）

| 配置项 | 说明 | 位置 |
|--------|------|------|
| `navbar.blog_title` | 导航栏标题 | 约第 365 行 |
| `favicon` | 浏览器标签图标 | 约第 18 行 |
| `code.copy_btn` | 代码块复制按钮 | 约第 34 行 |
| `fun_features.typing` | 副标题打字机效果 | 约第 73 行 |
| `fun_features.typing.loop` | 打字机是否循环 | 约第 87 行 |
| `page.index.banner_img` | 首页背景图 | — |
| `page.post.banner_img` | 文章页背景图 | — |
| `footer.content` | 页脚文字 | — |
| `comments.type` | 评论系统（如 `giscus`/`twikoo`/`valine`） | — |

---

## 主题

当前使用 **Fluid** 主题（https://github.com/fluid-dev/hexo-theme-fluid）。

- 主题文件位于 `node_modules/hexo-theme-fluid/`（不直接修改）
- 主题配置通过项目根目录的 **`_config.fluid.yml`** 覆盖
- 更多配置指南：https://hexo.fluid-dev.com/docs/guide/

---

## 常用命令速查

```bash
npx hexo new post "文章标题"     # 创建新文章
npx hexo new draft "标题"        # 创建草稿
npx hexo publish "标题"          # 发布草稿
npx hexo server                  # 本地预览（http://localhost:4000）
npx hexo generate                # 构建静态文件
npx hexo deploy                  # 部署到 GitHub Pages
npx hexo clean                   # 清理缓存
```

或通过 `package.json` 中的 scripts：
```bash
npm run server    # = hexo server
npm run build     # = hexo generate
npm run deploy    # = hexo deploy
npm run clean     # = hexo clean
```

---

## 部署流程

```
本地写文章 → hexo generate 构建 → hexo deploy 推送 gh-pages 分支 → GitHub Pages 自动更新
```

- **源码分支**：`main`（`_posts/`、`_config.yml` 等）
- **部署分支**：`gh-pages`（仅含构建后的静态文件）

修改配置或写完文章后执行：
```bash
git add -A && git commit -m "xxx" && git push origin main   # 保存源码
npx hexo clean && npx hexo generate && npx hexo deploy       # 构建并发布
```

---

## 相关链接

- [Hexo 文档](https://hexo.io/docs/)
- [Fluid 主题文档](https://hexo.fluid-dev.com/docs/)
- [Fluid 主题 GitHub](https://github.com/fluid-dev/hexo-theme-fluid)
- [GitHub Pages 文档](https://docs.github.com/en/pages)
