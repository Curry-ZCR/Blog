# Gemini Context: My Hugo Blog

This is the source code for a personal blog built with [Hugo](https://gohugo.io/) and the [Reimu](https://github.com/D-Sketon/hugo-theme-reimu) theme.

## Project Overview

*   **Type:** Static Site / Blog
*   **Engine:** Hugo (Extended)
*   **Theme:** Reimu
*   **Content Language:** Chinese (Simplified)
*   **Deployment:** GitHub Pages (via GitHub Actions)

## Key Directories

*   **`content/`**: Contains markdown files for posts and pages.
    *   `content/post/`: Blog posts.
    *   `content/about.md`: About page.
*   **`static/`**: Static assets (images, favicon, etc.). Files here are copied to the root of the published site.
    *   `static/images/`: Store post images here.
*   **`themes/reimu/`**: The Reimu theme source.
*   **`config/_default/`**: Configuration files.
    *   `params.yml`: **Primary config** for theme settings (avatar, sidebar, social links).
*   **`hugo.toml`**: Main Hugo site configuration (URL, title, theme selection).
*   **`blog-config-tool/`**: (Local Utility) A full-stack Node.js/React application for visually managing the blog's configuration and posts. (See its own `GEMINI.md` for details).

## Development Workflow

### Prerequisites
*   Hugo Extended (latest version recommended)
*   Git

### Common Commands

| Action | Command | Description |
| :--- | :--- | :--- |
| **Start Server** | `hugo server` | Starts local dev server at `http://localhost:1313`. |
| **Start (Drafts)**| `hugo server -D` | Starts server including content marked `draft: true`. |
| **New Post** | `hugo new post/filename.md` | Creates a new post file with front matter. |
| **Build** | `hugo` | Generates static site in `public/`. |

### Configuration

*   **Site Basics:** Edit `hugo.toml` for base URL, title, and language.
*   **Theme Settings:** Edit `config/_default/params.yml` for visual/widget settings.
*   **Menus:** Typically configured in `hugo.toml` or `config/_default/menus.toml` (check specific file if present).

## Deployment

Deployment is automated via GitHub Actions:
*   **Workflow:** `.github/workflows/blog.yaml`
*   **Trigger:** Push to `main` branch.
*   **Process:**
    1.  Checkout code.
    2.  Setup Hugo.
    3.  Build site (`hugo -D`).
    4.  Deploy `public/` folder to `Curry-ZCR/Curry-ZCR.github.io` (gh-pages).

## Related Documentation
*   `README.md`: Basic usage guide.
*   `REIMU_MANUAL.md`: Detailed theme configuration guide.
*   `NEW_POST_GUIDE.md`: Guide for writing new posts.
