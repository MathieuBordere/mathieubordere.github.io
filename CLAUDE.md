# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Zola-based static site generator project for a personal blog hosted at https://letmetweakit.com. The site is built using the Zola framework and deployed to GitHub Pages.

## Commands

### Development
- `zola serve` - Start local development server with hot reload
- `zola build` - Build the site for production
- `zola check` - Validate content and links

### Deployment
The site automatically builds and deploys to GitHub Pages on every push to the `main` branch via GitHub Actions (see `.github/workflows/build-deploy.yaml`).

## Architecture

### Directory Structure
- `config.toml` - Main Zola configuration file with site settings
- `content/` - All content files in Markdown format
  - `content/blog/` - Blog posts with `_index.md` for section configuration
- `templates/` - Tera template files for HTML layout
  - `base.html` - Base template with common HTML structure
  - `blog.html` - Template for blog section listing
  - `blog-page.html` - Template for individual blog posts
  - `index.html` - Homepage template
- `static/` - Static assets (CSS, images, etc.)
- `public/` - Generated site output (created by `zola build`)

### Content Management
- Blog posts are Markdown files in `content/blog/`
- Front matter uses TOML format with `+++` delimiters
- The blog section is configured to sort posts by date
- Syntax highlighting is enabled for code blocks

### Templating
- Uses Tera templating engine (similar to Jinja2)
- Templates use `{% block content %}` for content injection
- Base template provides common HTML structure for all pages

### Configuration
- Site URL: https://letmetweakit.com
- Sass compilation enabled
- Search index generation enabled
- Code syntax highlighting enabled