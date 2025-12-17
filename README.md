# My Hugo Blog

这是我的个人博客项目源码，基于 [Hugo](https://gohugo.io/) 静态网站生成器构建，使用了 [Reimu](https://github.com/D-Sketon/hugo-theme-reimu) 主题。

## 🚀 快速开始

### 1. 环境要求
*   [Hugo](https://gohugo.io/installation/) (推荐 Extended 版本)
*   [Git](https://git-scm.com/)

### 2. 本地运行
在项目根目录下打开终端：

```bash
# 启动本地预览服务器
hugo server
```

访问 `http://localhost:1313/` 即可预览博客。

> **提示**: 如果要预览草稿文章（`draft: true`），请使用 `hugo server -D`。

### 3. 新建文章
```bash
hugo new post/my-new-post.md
```
然后编辑 `content/post/my-new-post.md` 文件。

## 📂 项目结构说明

*   `content/`: 存放博客文章 (`post/`) 和其他页面。
*   `static/`: 存放图片、CSS 等静态资源（图片请放在这里，引用时直接用 `/images/...`）。
*   `themes/`: 存放网站主题。
*   `config/_default/params.yml`: **核心配置文件**，修改头像、公告、侧边栏等都在这里。
*   `hugo.toml`: 基础配置文件。

## 📚 常用文档
*   [Reimu 主题配置手册](REIMU_MANUAL.md) - 本项目的详细配置说明
*   [新建文章指南](NEW_POST_GUIDE.md) - 如何写一篇新博客

## 🛠️ 常用命令

| 命令 | 说明 |
|Data | Description|
| `hugo server` | 启动本地预览 |
| `hugo server -D` | 启动预览（包含草稿） |
| `hugo new post/xxx.md` | 新建文章 |
| `hugo` | 生成最终静态页面（输出到 `public/`） |

---
*Powered by [Hugo](https://gohugo.io) & [Reimu](https://github.com/D-Sketon/hugo-theme-reimu)*
