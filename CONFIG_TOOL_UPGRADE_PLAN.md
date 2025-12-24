# Blog Config Tool Upgrade Plan

This document outlines the roadmap for upgrading the `blog-config-tool` to support full visualization of all configuration options available in the [Hugo Reimu Theme](https://github.com/D-Sketon/hugo-theme-reimu).

## Goal
Achieve 100% GUI coverage for `config/_default/params.yml`, enabling users to manage every aspect of their blog without manual YAML editing.

---

## Phase 1: Core Service Integration (High Priority)
*Focus: Making the "broken" toggles functional by adding necessary parameters.*

### 1. Advanced Comment System (`comment`)
*   **Requirements**: 
    *   Dynamic forms based on selected provider (Valine, Waline, Twikoo, Giscus, Gitalk, Disqus).
    *   Fields for API Keys, Server URLs, Repo info, etc.
    *   Multi-language title configuration.

### 2. Full Search Configuration (`algolia_search`)
*   **Requirements**:
    *   Inputs for `appID`, `apiKey` (Search-Only), `indexName`, and `hits.per_page`.

### 3. Sponsor & Copyright Details (`sponsor` & `article_copyright`)
*   **Requirements**:
    *   **Sponsor**: Custom tips, QR code image uploads (Alipay/WeChat).
    *   **Copyright**: Granular toggles (author, link, date) and license type selector (CC BY-NC-SA, etc.).

---

## Phase 2: Media & Atmosphere (The "Reimu" Vibe)
*Focus: Interactive elements and visual polish.*

### 1. Live2D Models (`live2d` & `live2d_widgets`)
*   **Requirements**:
    *   Toggle between New/Old Live2D versions.
    *   Position control (left/right).

### 2. Music Player (`player`)
*   **Requirements**:
    *   Global/Mobile toggles.
    *   Position selector (`before_sidebar`, `after_sidebar`, etc.).
    *   **APlayer**: Loop, autoplay, fixed mode.
    *   **Meting**: Data source (Netease/Tencent), Playlist ID, API URL.

### 3. Typography & Icons (`font`, `icon_font`)
*   **Requirements**:
    *   **Google Fonts**: Manage font family lists for articles and code.
    *   **Custom Fonts**: CSS URL and font name inputs.
    *   **Iconfont**: Project ID input.

---

## Phase 3: Content & Utilities (Quality of Life)
*Focus: Enhancing the reading experience.*

### 1. Math & Diagrams (`math` & `mermaid`)
*   **Requirements**:
    *   Mutually exclusive toggle for KaTeX vs. MathJax3.
    *   Mermaid zoom settings.

### 2. Sharing & Regionalization (`share` & `rss` & `icp`)
*   **Requirements**:
    *   **Share**: Multi-select list for social platforms.
    *   **RSS**: Article limits and full content toggles.
    *   **ICP**: Chinese mainland regulatory info (ICP Number, Beian, Moe ICP).

### 3. Site Decorations (`outdate`, `triangle_badge`, `home_categories`)
*   **Requirements**:
    *   Outdated article warning (days, message).
    *   Corner triangle badge (icon, link).
    *   Homepage category cards (category name, cover image).

---

## Phase 4: Advanced Systems (Experimental)
*Focus: Performance and low-level injection.*

### 1. SPA & Performance
*   **Requirements**: PJAX, Service Worker, and Quicklink (timeout/priority) toggles.
*   **Visuals**: Material Theme (dynamic color scheme) toggle.

### 2. Code Injector (`injector`)
*   **Requirements**:
    *   Multi-line text areas for `head_begin`, `head_end`, `body_begin`, `body_end`, `sidebar_begin`, `sidebar_end`.
    *   Safety warnings regarding JS injection.

---

## Technical Refactoring Roadmap

To prevent the codebase from becoming unmanageable as options grow, the following refactoring is required:

### 1. Schema-First Development
*   Update `shared/types/config.ts` to strictly mirror the full `params.yml` structure before building UI.

### 2. Component Decomposition
*   Split `ConfigEditor.tsx` into domain-specific sections:
    *   `BasicSettings.tsx`
    *   `CommentSettings.tsx`
    *   `MediaSettings.tsx` (Images, Player, Live2D)
    *   `StyleSettings.tsx` (Font, Sidebar, DarkMode)
    *   `FeatureSettings.tsx` (Search, Math, Mermaid)
    *   `AdvancedSettings.tsx` (Injector, PJAX, SW)

### 3. Reusable Form UI
*   Standardize input components: `ArrayField`, `SelectField`, `SwitchField`, and `ImagePicker`.

---

## Execution Roadmap

1.  **Step 1**: Sync `shared/types/config.ts` with theme defaults.
2.  **Step 2**: Decompose `ConfigEditor.tsx` into modular components.
3.  **Step 3**: Implementation of Phase 1 (Core Services).
4.  **Step 4**: Implementation of Phase 2 (Media/Vibe).
5.  **Step 5**: Implementation of Phase 3 & 4.
