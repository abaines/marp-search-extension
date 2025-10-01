# marp-search-extension

Marp presentation for [abaines/search-extension](https://github.com/abaines/search-extension)

## Overview

This repository contains a comprehensive presentation about the search-extension project, covering:
- Requirements gathering approach
- Stakeholder engagement strategies
- Technology selection decisions
- Challenges encountered and solutions
- Final project outcomes

## Local Development

### Prerequisites
- Node.js (v20 or higher)
- npm

### Setup

```bash
# Install dependencies
npm install

# Build the presentation
npm run build

# Watch mode for development
npm run watch

# Build PDF version
npm run build:pdf
```

## Viewing the Presentation

The presentation is automatically deployed to GitHub Pages when changes are pushed to the main branch.

### Local Viewing
After building, open `index.html` in your web browser.

## GitHub Actions

This repository uses GitHub Actions to automatically build and deploy the presentation to GitHub Pages.

The workflow:
1. Triggers on push to main branch
2. Installs dependencies
3. Builds the presentation
4. Deploys to GitHub Pages

## Files

- `slides.md` - The main presentation source file (Marp markdown)
- `index.html` - Generated HTML presentation
- `.github/workflows/deploy.yml` - GitHub Actions workflow for deployment

