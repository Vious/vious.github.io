# Blog 维护指南 / Blog Maintenance Guide

## 目录结构 / Directory Structure

```
blog/
├── index.html          # Blog 主页 (自动渲染)
├── posts.json          # 文章清单 (核心配置文件)
├── posts/              # 所有 Markdown 文章放这里
│   ├── welcome.md
│   └── deep-learning-intro.md
└── HOWTO.md            # 本指南
```

---

## 如何写一篇新文章 / How to Write a New Post

### Step 1: 创建 Markdown 文件

在 `blog/posts/` 目录下新建一个 `.md` 文件，比如 `my-new-post.md`。

文件开头必须包含 **元数据块** (frontmatter)，格式如下：

```markdown
---
title: 你的文章标题
date: 2026-05-06
tags: [标签1, 标签2, 标签3]
---

正文从这里开始...

## 二级标题

正常写 Markdown 即可。
```

**字段说明：**

| 字段 | 必填 | 说明 |
|------|------|------|
| `title` | ✅ | 文章标题 |
| `date` | ✅ | 日期，格式 `YYYY-MM-DD` |
| `tags` | ✅ | 标签数组，用 `[tag1, tag2]` 格式 |

### Step 2: 在 `posts.json` 中注册

编辑 `blog/posts.json`，在数组里添加一条记录：

```json
{
    "title": "你的文章标题",
    "date": "2026-05-06",
    "tags": ["标签1", "标签2", "标签3"],
    "file": "posts/my-new-post.md"
}
```

> **注意**：`title`、`date`、`tags` 必须与 `.md` 文件中 frontmatter 一致。
> `file` 是相对于 `blog/` 目录的路径。

### Step 3: 部署

将修改推送到 GitHub：

```bash
git add blog/
git commit -m "Add new blog post: 你的文章标题"
git push
```

等待几分钟，GitHub Pages 自动部署完成后即可访问 `https://vious.github.io/blog/`。

---

## 标签系统 / Tag System

### 如何使用标签

- 每篇文章可以有**多个标签**
- 标签会自动收集并显示在 Blog 主页顶部
- 点击任意标签即可筛选该分类的文章
- 点击 **All** 显示全部文章
- 筛选后的 URL 会带上 `#标签名`，可以直接分享链接

### 建议的标签命名

| 类别 | 示例标签 |
|------|----------|
| 研究领域 | `AI`, `Computer Vision`, `Image Generation`, `Semantic Segmentation` |
| 内容类型 | `tutorial`, `paper-notes`, `project`, `thoughts` |
| 技术栈 | `PyTorch`, `Python`, `C++` |

---

## 文章格式 / Markdown Tips

博客支持标准 Markdown 语法，包括：

- **标题** `##`, `###`
- **加粗** `**bold**` 和 *斜体* `*italic*`
- **代码块** 使用 ` ```python ... ``` `
- **表格** 使用 `| col1 | col2 |`
- **图片** `![alt](path/to/image.png)`
- **引用** `> quote text`
- **链接** `[text](url)`

### 插入图片

在 `blog/` 下新建 `images/` 文件夹，将图片放入，然后引用：

```markdown
![描述](./images/my-image.png)
```

---

## 常见问题 / FAQ

### Q: 文章修改后不更新？
A: GitHub Pages 有缓存，通常 1-3 分钟生效。可以强制刷新 (Ctrl+F5) 试试。

### Q: 怎么删除文章？
A: 
1. 从 `blog/posts.json` 中移除对应条目
2. (可选) 删除 `posts/` 下的 `.md` 文件

### Q: 可以加更多自定义样式吗？
A: 编辑 `blog/index.html`，在 `<style>` 标签中添加 CSS 即可。

### Q: 支持数学公式吗？
A: 目前不内置支持。如需 LaTeX 公式，可以在 `index.html` 中添加 KaTeX CDN：
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/katex.min.css">
<script src="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/katex.min.js"></script>
```

---

## 总结 / TL;DR

1. 在 `blog/posts/` 新建 `.md` 文件，写好 frontmatter
2. 在 `blog/posts.json` 添加条目
3. `git push` 即可
