# Presentations

This directory contains Marp presentations for the Spec-Driven Development project.

## Creating New Presentations

1. Create a new `.md` file in this directory
2. Start with the Marp frontmatter:
```yaml
---
marp: true
theme: default
---
```

## Running Presentations

To preview presentations locally:
```bash
npx @marp-team/marp-cli presentations/your-presentation.md --preview
```

To export to PDF:
```bash
npx @marp-team/marp-cli presentations/your-presentation.md --pdf
```

To export to HTML:
```bash
npx @marp-team/marp-cli presentations/your-presentation.md --html
```

## Available Themes

- `default` - Clean, professional theme
- `gaia` - Modern, colorful theme
- `uncover` - Minimal theme with reveal effects

## Tips

- Use `---` to separate slides
- Use `--` to create slide breaks within content
- Add `<!-- _class: invert -->` for dark slides
- Use `![bg](image.jpg)` for background images
