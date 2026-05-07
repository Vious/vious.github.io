---
title: How to Use & Maintain This Blog
date: 2026-05-07
tags: [meta, guide, tutorial]
---

## Overview

This is a **zero-dependency, fully offline** personal blog system. There's no database, no build step, no static site generator — just plain Markdown files and a single HTML page that renders everything in the browser.

### Architecture

```
blog/
├── index.html          ← The blog app (you're looking at it)
├── posts.json          ← Post manifest (title, date, tags, file path)
├── css/
│   ├── github-markdown.min.css      ← GitHub-style markdown base
│   └── github-markdown-light.css    ← Light theme colors
├── js/
│   ├── marked.esm.js    ← Markdown parser (v16)
│   └── highlight.min.js ← Code syntax highlighter
└── posts/
    ├── welcome.md       ← Your markdown posts go here
    ├── deep-learning-intro.md
    └── ...
```

---

## How to Write a New Post

### Step 1: Create a Markdown File

Create a new `.md` file inside `blog/posts/`. The filename should be descriptive (e.g., `my-awesome-post.md`).

Every post **must** start with YAML frontmatter:

```yaml
---
title: Your Post Title
date: 2026-05-07
tags: [tag1, tag2, tag3]
---
```

| Field   | Required | Description |
|---------|----------|-------------|
| `title` | ✅ Yes   | The post title (displayed on cards and detail page) |
| `date`  | ✅ Yes   | Publication date in `YYYY-MM-DD` format |
| `tags`  | ✅ Yes   | Array of tags for categorization and filtering |

After the `---` closing delimiter, write your content in standard Markdown. All GitHub Flavored Markdown features are supported:

- **Headings** (`##`, `###`, etc.)
- **Bold**, *italic*, ~~strikethrough~~
- **Code blocks** with syntax highlighting (specify language: ` ```python `)
- **Tables**, lists, blockquotes
- **Links** and **images**
- **Inline code** with backticks

### Step 2: Register in `posts.json`

Open `blog/posts.json` and add your new post entry:

```json
[
    {
        "title": "Your Post Title",
        "date": "2026-05-07",
        "tags": ["tag1", "tag2"],
        "file": "posts/your-file-name.md"
    },
    ...
]
```

> ⚠️ **Important**: The `file` path is relative to `blog/index.html`, so always start with `posts/`.

### Step 3: That's It!

Push your changes to GitHub and the post goes live. No build step, no configuration — just commit and push.

---

## Tag System

Tags are fully dynamic. Any tag you put in `posts.json` (or frontmatter) automatically appears in the filter bar at the top of the blog page.

- Click a tag pill to filter posts by that tag
- Click **All** to show all posts
- Each tag shows a count of how many posts use it

**Tips for good tagging:**
- Use consistent casing (e.g., always `Deep Learning`, not mix of `deep learning` and `Deep Learning`)
- Keep tags broad enough to be useful but specific enough to be meaningful
- Common patterns: technology names (`Python`, `PyTorch`), topic areas (`Computer Vision`, `NLP`), post types (`tutorial`, `research`, `opinion`)

---

## Code Syntax Highlighting

Code blocks automatically get syntax highlighting. Just specify the language after the opening backticks:

````markdown
```python
def hello():
    print("Hello, world!")
```
````

Supported languages include: `python`, `javascript`, `cpp`, `java`, `rust`, `go`, `bash`, `html`, `css`, `json`, `yaml`, `markdown`, and many more (everything highlight.js supports).

---

## Images

To include images in your posts:

1. Place the image file in `blog/posts/` (or a subfolder like `blog/posts/images/`)
2. Reference it with a relative path:

```markdown
![Alt text](posts/images/my-image.png)
```

---

## Customization

### Changing the Look

- **Colors & theme**: Edit the CSS variables in `<style>` inside `blog/index.html`. The `:root` block at the top controls all colors.
- **Font**: Change the `font-family` in `body` or `.markdown-body` styles.
- **Layout width**: Modify `max-width: 860px` on `.blog-container`.

### Adding Dark Mode

To add a dark mode toggle, you could:
1. Add a second set of CSS variables under a `[data-theme="dark"]` selector
2. Use JavaScript to toggle the `data-theme` attribute on `<html>`

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Post not appearing | Check `posts.json` — make sure the `file` path is correct and relative to `blog/index.html` |
| Markdown not rendering | Ensure the file starts with `---` frontmatter and has a closing `---` |
| Tags not showing | Tags must be a JSON array in `posts.json`, e.g., `["tag1", "tag2"]` |
| Code not highlighted | Make sure you specify a language: ` ```python ` not just ` ``` ` |
| Page loads blank | Open browser console (F12) — check for errors loading `posts.json` or markdown files |

---

## FAQ

**Q: Can I use this without GitHub Pages?**
Yes! Just open `blog/index.html` in any browser. It works fully offline — no server needed.

**Q: Do I need to run any build commands?**
No. There is zero build step. Everything happens in the browser.

**Q: How do I delete a post?**
Remove its entry from `posts.json` and delete the `.md` file from `posts/`.

**Q: Can I change a post after publishing?**
Yes — just edit the `.md` file and push. Changes appear immediately.
