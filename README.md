# Presentations

This repository contains talks and presentations using mitsuhiko's presentation system.

## Structure

```
.
├── dynamic/              # Dynamic HTML presentations
│   ├── example-talk/    # Example HTML-based talk
│   │   ├── index.html
│   │   └── presenter.json
│   └── marp-example/    # Example Marp-based talk
│       └── talk.md
├── pdfs/               # Static PDF presentations (optional)
├── .github/workflows/   # GitHub Actions for deployment
└── README.md           # This file
```

## Creating a New Talk

### Option 1: HTML-based Presentations

1. Create a new directory under `dynamic/`:
   ```bash
   mkdir -p dynamic/your-talk-name
   ```

2. Copy the template from `dynamic/example-talk/`:
   ```bash
   cp -r dynamic/example-talk/* dynamic/your-talk-name/
   ```

3. Edit `index.html` to add your slides:
   - Each slide is a `<section class="slide" data-slide="N">` element
   - Use `.step` class for incremental bullet points
   - Available CSS classes:
     - `.big-text` - Large emphasis text
     - `.huge-text` - Extra large emphasis text
     - `.center` - Center-aligned content
     - `.code` - Inline code styling
     - `.quote` - Blockquote styling
     - `.comparison` - Two-column layout

4. Update `presenter.json` with your talk title

### Option 2: Marp-based Presentations

1. Create a new directory under `dynamic/`:
   ```bash
   mkdir -p dynamic/your-talk-name
   ```

2. Create a markdown file (e.g., `talk.md`) with Marp syntax

3. The GitHub Actions workflow will automatically convert it to HTML

## Navigation Controls

- **Next slide**: Arrow Right, Space, Page Down, `l`, `j`
- **Previous slide**: Arrow Left, Page Up, `h`, `k`
- **First slide**: Home
- **Last slide**: End

## URL Navigation

Slides are accessible via URL hash:
- `#1` - Go to slide 1
- `#1.2` - Go to slide 1, step 2
- `#1~next` - Go to slide 1, then navigate to next
- `#1~prev` - Go to slide 1, then navigate to previous

## Deployment

Presentations are automatically deployed to GitHub Pages when you push to `main` or `master` branch.

Visit `https://<your-username>.github.io/presentations/` to see all talks.

## Features

- Responsive scaling (1920x1080 deck)
- Incremental slide steps
- Lazy iframe loading
- Presenter mode support
- URL-based navigation
- Custom styling via CSS

## Credit

Based on [mitsuhiko/talks](https://github.com/mitsuhiko/talks) presentation system.
