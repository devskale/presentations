# AGENTS.md - Presentations Repository Guide

This repository contains HTML and Marp-based presentations that deploy to GitHub Pages.

## Presentations Index

- **[skaledev](https://devskale.github.io/presentations/skaledev/)** - `dynamic/skaledev/`
  - Current working presentation
  - Features WebGL backdrop and Marp slides
  - German content with skale.dev references

- **[Me and the Machine](dynamic/me-and-the-machine/me-and-the-machine.html)** - `dynamic/me-and-the-machine/`
  - Marp-based presentation
  - Original "Me and the Machine" talk by Armin Ronacher

- **[I Was Observing When My Agent Built Its Own Harness](dynamic/i-was-questioning-life/index.html)** - `dynamic/i-was-questioning-life/`
  - HTML presentation
  - Custom slide deck

- **[Example Talk](dynamic/example-talk/index.html)** - `dynamic/example-talk/`
  - HTML template presentation

- **[Marp Example](dynamic/marp-example/talk.html)** - `dynamic/marp-example/`
  - Basic Marp demonstration

## Build Commands

### Local Development

For Marp-based presentations (in `dynamic/*/`):

```bash
# Build HTML from markdown
npx @marp-team/marp-cli --html talk.md -o talk.html

# Run custom injection script (if present)
node inject-backdrop.js talk.html

# Serve locally for preview
python -m http.server 4005
# Then open http://localhost:4005/talk.html
```

Using Makefile (if available in talk directory):

```bash
make html      # Build HTML
make pdf       # Build PDF
make clean     # Remove build artifacts
make serve     # Start local server
make open      # Build and open in browser
```

### Deployment

Presentations automatically deploy to GitHub Pages on push to `main` or `master`. The CI workflow builds all talks in `dynamic/` and publishes to `_site/`.

Live URL: https://devskale.github.io/presentations/

## Code Style Guidelines

### Marp Markdown Files

- Frontmatter: Use `---` delimiters at top of file
- Required frontmatter keys: `marp: true`, `theme`, `paginate`, `backgroundColor`, `color`
- Custom styles in `style: |` block after frontmatter
- Use Google Fonts via `@import url()` in style block
- Slide separator: `---` on its own line
- Classes: Use `_class: lead` for title slides
- Quote sections: Use `section.quote` class for dark-themed quotes

### HTML Presentations

- Deck size: Fixed 1920x1080px, scales responsively via JS
- Font: "Zalando Sans Expanded" (primary), "DM Mono" (code)
- Colors: Dark theme `#0a1214` background, `#f0f4f5` text
- Slide structure: `<section class="slide" data-slide="N">`
- Incremental steps: Use `<li class="step">` inside `<ul class="steps">`
- Available CSS classes:
  - `.big-text` - Large emphasis (77px)
  - `.huge-text` - Extra large emphasis (102px)
  - `.center` - Center-align
  - `.code` - Inline code styling
  - `.quote` - Blockquote styling
  - `.comparison` - Two-column grid layout

### JavaScript (injection scripts)

- Shebang: `#!/usr/bin/env node` at top
- Modules: Use `require('fs')` for Node.js compatibility
- Argument handling: `process.argv[2]` for optional filename parameter
- Default values: Use `||` operator for fallback values
- String literals: Use template literals (backticks) for multi-line strings
- File operations: Use `fs.readFileSync()` and `fs.writeFileSync()`
- Console: Use `console.log()` for status messages
- Regex: Use `/pattern/flags` for string replacements

### File Naming

- Marp talks: `talk-name.md` (kebab-case)
- Output HTML: Same base name as markdown, `.html` extension
- Directories: `dynamic/talk-name/` (kebab-case)
- Scripts: `inject-backdrop.js`, descriptive names
- Assets: `waves.mp4`, `logo.svg`, descriptive names

### WebGL Shader Code (in injection scripts)

- GLSL strings: Use template literals with escaped backticks `\``
- Shader sources: Define `vsSource` (vertex) and `fsSource` (fragment)
- Uniforms: Use `u_` prefix for GLSL uniforms
- Attributes: Use `a_` prefix for vertex attributes
- Const values: UPPERCASE for constants in GLSL
- Helper functions: Snake_case for GLSL functions

### Formatting

- Indentation: 2 spaces for HTML, 2 spaces for JS
- Line length: No strict limit, but prefer under 100 chars
- Trailing whitespace: Remove
- Comments: Use `//` for JS comments, keep them minimal
- Empty lines: One blank line between logical sections

## Repository Structure

```
dynamic/
  ├── example-talk/           # HTML template
  │   ├── index.html
  │   └── presenter.json
  ├── talk-name/              # Marp-based talk
  │   ├── talk.md
  │   ├── inject-backdrop.js  # Optional
  │   ├── waves.mp4          # Assets
  │   └── Makefile           # Optional
.github/workflows/
  └── deploy.yml              # CI/CD
```

## Common Patterns

- WebGL backdrop injection: Replace after `<body>` tag, add canvas element
- Lazy iframe loading: Use `data-src` attribute, swap with `src` on activation
- Hash-based navigation: `#slideNumber.stepNumber` format
- Makefile targets: `all`, `html`, `pdf`, `clean`, `serve`, `open`
