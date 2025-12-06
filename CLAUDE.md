# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Hugo static site for ictd.ru (Межрегиональный центр тендерной документации), a tender documentation service operated by Кошлаков Евгений Владимирович. The site is built with Hugo static site generator using the hugo-serif-theme and deployed to GitHub Pages.

## Development Commands

### Building and Running Locally

```bash
# Run development server with live reload
hugo server

# Run development server with drafts enabled
hugo server -D

# Build the site (output goes to /public)
hugo

# Build with minification (production build)
hugo --minify
```

### Hugo Version

- Local development: v0.152.2+extended (macOS ARM64)
- CI/CD (GitHub Actions): v0.111.3 (hugo.yml) or v0.102.3 (pages.yml)
- Minimum required: v0.55.0 with extended features enabled

## Site Architecture

### Configuration

- **config.toml**: Main site configuration
  - Base URL: https://ictd.ru
  - Theme: hugo-serif-theme (located in themes/ directory)
  - Language: en-us (though content is in Russian)
  - Hugo extended mode required for SCSS compilation
  - Custom color scheme: primary #f24088, custom fonts (Playfair Display, Source Sans Pro)

### Content Structure

- **content/_index.md**: Homepage content and metadata
- **content/contact.md**: Contact page
- **content/pricing.md**: Pricing/service cost page
- **content/testimonials/**: Client testimonials/reviews
- **content/404/**: Custom 404 error page

### Data Files

- **data/contact.yaml**: Contact information (email, phone, person name)
- **data/features.json**: Service features
- **data/social_off.json**: Social media configuration (currently disabled)

### Menu Structure

Main navigation includes: Домой (Home), Отзывы (Testimonials), Контакты (Contact), Стоимость (Pricing)

### Theme Customization

The hugo-serif-theme is included in themes/hugo-serif-theme/. Key directories:
- layouts/: Template files organized by content type (services, team, testimonials, etc.)
- assets/: SCSS and other frontend assets
- partials/: Reusable template components

## Deployment

### GitHub Pages Deployment

The site auto-deploys to GitHub Pages on pushes to the main branch via GitHub Actions:

- **Primary workflow**: .github/workflows/hugo.yml (Hugo v0.111.3)
- **Secondary workflow**: .github/workflows/pages.yml (Hugo v0.102.3)
- Output directory: ./public
- Deployment uses Hugo extended with Dart Sass support

### Build Process

1. Checkout code with recursive submodules
2. Install Hugo CLI (extended version) and Dart Sass
3. Build with `hugo --minify --baseURL` set to GitHub Pages URL
4. Upload ./public as artifact
5. Deploy to GitHub Pages environment

## Important Notes

- Always use Hugo extended version (required for SCSS compilation)
- The public/ directory is gitignored and regenerated on each build
- Theme is not a submodule but directly included in the repository
- Site content is in Russian despite languageCode="en-us" in config
- Contact information is stored in data/contact.yaml, not hardcoded in templates
