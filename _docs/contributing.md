---
layout: default
title: Contributing Guide
nav_order: 9
description: "How to add content to Notes By Noel"
---

# Contributing Guide
{: .no_toc }

A guide for adding new notes and contributing to this documentation site.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Adding New Pages

### File Location

All documentation pages should be placed in the `_docs/` directory or its subdirectories.

```
_docs/
├── getting-started.md
├── about.md
├── programming/
│   ├── index.md
│   └── python-basics.md
└── your-new-topic/
    └── your-page.md
```

### Front Matter

Every page needs front matter at the top:

```yaml
---
layout: default
title: Your Page Title
parent: Parent Page (optional)
nav_order: 1
description: "A brief description for SEO"
---
```

#### Front Matter Options

| Field | Required | Description |
|:------|:---------|:------------|
| `layout` | Yes | Always use `default` |
| `title` | Yes | Page title shown in navigation |
| `parent` | No | Parent page for nested navigation |
| `nav_order` | No | Order in navigation (lower = higher) |
| `description` | No | SEO description |
| `has_children` | No | Set to `true` for parent pages |
| `permalink` | No | Custom URL path |

### Creating a Topic Category

To create a new topic with child pages:

1. Create a folder: `_docs/your-topic/`
2. Create an index file: `_docs/your-topic/index.md`
3. Add this front matter:

```yaml
---
layout: default
title: Your Topic
nav_order: 3
has_children: true
description: "Topic description"
---
```

4. Create child pages in the same folder with `parent: Your Topic`

## Content Guidelines

### Writing Style

- ✅ **Clear and concise** - Get to the point
- ✅ **Friendly tone** - Like explaining to a friend
- ✅ **Include examples** - Show, don't just tell
- ✅ **Add context** - Explain the "why" not just the "how"
- ❌ Avoid jargon without explanation
- ❌ Don't assume too much prior knowledge

### Code Blocks

Use triple backticks with language specification:

````markdown
```python
def hello():
    print("Hello, world!")
```
````

Supported languages include: `python`, `javascript`, `bash`, `ruby`, `yaml`, `json`, `html`, `css`, and many more.

### Information Blocks

Use blockquotes for important notes:

```markdown
> **💡 Tip**: This is a helpful tip for readers.

> **⚠️ Warning**: Be careful about this edge case.

> **📝 Note**: Additional context or explanation.
```

### Headings

Use hierarchical headings:

```markdown
# Page Title (H1) - Only one per page

## Major Section (H2)

### Subsection (H3)

#### Minor Section (H4)
```

### Tables

Create tables with pipe syntax:

```markdown
| Column 1 | Column 2 | Column 3 |
|:---------|:--------:|----------:|
| Left     | Center   | Right     |
| Aligned  | Aligned  | Aligned   |
```

### Links

```markdown
[External Link](https://example.com)
[Internal Link](../other-page)
[Link with Title](https://example.com "Hover text")
```

### Lists

```markdown
- Unordered list item
- Another item
  - Nested item
  - Another nested item

1. Ordered list item
2. Second item
3. Third item
```

## Styling Options

Just the Docs provides utility classes:

### Text Sizes

```markdown
Text with specific size
{: .fs-1 }  <!-- Smallest -->
{: .fs-9 }  <!-- Largest -->
```

### Font Weights

```markdown
Light text
{: .fw-300 }

Bold text
{: .fw-700 }
```

### Colors

```markdown
Green text
{: .text-green-200 }

Warning text
{: .text-yellow-300 }
```

### Buttons

```markdown
[Button Text](#link){: .btn }
[Primary Button](#link){: .btn .btn-primary }
[Outlined Button](#link){: .btn .btn-outline }
```

## Testing Locally

Before committing, test your changes:

1. Start the local server:
   ```bash
   bundle exec jekyll serve --livereload
   ```

2. Visit `http://localhost:4000`

3. Check:
   - Navigation appears correctly
   - All links work
   - Code blocks render properly
   - Search finds your content

## Best Practices

### File Naming

- Use lowercase
- Separate words with hyphens
- Be descriptive: `python-virtual-environments.md` not `pvenv.md`

### Images

Store images in an `assets/images/` folder:

```markdown
![Alt text](/assets/images/your-image.png)
```

### Internal Links

Use relative paths for internal links:

```markdown
[See Python Basics](programming/python-basics)
```

### Keep It Updated

When information changes:
- Update the content
- Add a note about what changed (if significant)
- Consider updating the "Last updated" date

## Commit Messages

Use clear, descriptive commit messages:

```
✅ Add: Python virtual environments guide
✅ Update: Fix broken links in JavaScript section
✅ Improve: Clarify Docker setup instructions
❌ fixed stuff
❌ update
```

## Need Help?

If you're unsure about something:

1. Look at existing pages for examples
2. Check the [Just the Docs documentation](https://just-the-docs.github.io/just-the-docs/)
3. Open an issue on GitHub

---

Happy documenting! 📝
