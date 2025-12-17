# Reimu 主题博客管理与配置指南

这份文档是基于您的 Hugo 博客项目（使用 Reimu 主题）的详细管理手册。它涵盖了从基础配置、内容发布到高级功能的各个方面。

## 1. 项目结构概览

目前的目录结构及关键文件/文件夹说明：

- **`hugo.toml`**: 站点的基础配置文件（语言、标题、主题指定等）。
- **`content/`**: 存放所有博客文章和页面内容。
  - `post/`: 存放博文。
  - `archives/`: 归档页面配置 (需要包含 `_index.md`)。
- **`static/`**: 存放静态资源（图片、favicon）。此处的文件会直接复制到网站根目录。
- **`themes/reimu/`**: 主题源码目录。**不要直接修改这里的文件**，以免后续升级困难。
- **`data/`**: (建议新建) 用于存放封面、友链等数据文件。
- **`config/`**: (建议新建) 用于存放更详细的主题配置文件。

---

## 2. 初始配置（重要）

Reimu 主题推荐使用 `config` 目录来管理配置，而不是仅仅依赖 `hugo.toml`。请执行以下操作完成初始化：

### 2.1 创建配置文件副本
为了方便管理，我们需要将主题的默认配置文件复制到您的项目根目录下：

1.  **创建目录**: 在项目根目录下创建一个名为 `config` 的文件夹。
2.  **创建子目录**: 在 `config` 内创建 `_default` 文件夹。
3.  **复制配置文件**:
    - 将 `themes/reimu/config/_default/params.yml` 复制到您的 `config/_default/params.yml`。
    - 这是**核心主题配置文件**，几乎所有外观、功能开关都在这里修改。

### 2.2 创建数据文件
1.  **复制数据文件**:
    - 将 `themes/reimu/config/data/` 目录下的所有文件（`covers.yml`, `friends.yml`, `vendor.yml`）复制到您的项目根目录下的 `data/` 文件夹中（如果没有 `data` 文件夹请新建）。
    - `covers.yml`: 配置随机封面图。
    - `friends.yml`: 配置友情链接。

---

## 3. 常用个性化设置

以下设置主要在您刚刚复制的 `config/_default/params.yml` 中修改，或者在 `hugo.toml` 中配置。

### 3.1 基础信息
在 `hugo.toml` 中修改：
```toml
baseURL = "https://your-domain.com/" # 您的域名
title = "博客标题"
languageCode = "zh-CN"
```

### 3.2 头像与封面
将您的图片放入 `static/` 文件夹中（建议建立子文件夹如 `static/images/`）。

- **头像**:
  - 默认路径: `static/avatar/avatar.webp`
  - 修改: 在 `params.yml` 中搜索 `avatar`，修改为您图片的路径（相对于 static 目录），例如: `avatar: "images/my-avatar.jpg"`
- **首页头图 (Banner)**:
  - 默认路径: `themes/reimu/static/images/banner.webp`
  - 修改: 在 `params.yml` 中搜索 `banner`，修改为 `banner: "images/my-banner.jpg"`
- **随机封面**:
  - 编辑 `data/covers.yml`，添加图片链接（可以是本地 `static` 下的路径，也可以是网络 URL）。

### 3.3 侧边栏与社交链接
在 `params.yml` 中配置：
- **社交图标**: 找到 `social` 部分，填入您的 GitHub, Bilibili 等主页链接。
- **侧边栏位置**: 默认在右侧。如需修改，可在文章 Front-matter 中指定 `sidebar: left`。

### 3.4 开启评论系统
Reimu 支持多种评论系统 (Valine, Waline, Twikoo 等)。以 **Valine** 为例：
1. 在 `params.yml` 中找到 `valine` 部分。
2. 将 `enable` 设置为 `true`。
3. 填入您的 `appId` 和 `appKey` (需在 LeanCloud 注册)。

### 3.5 开启数学公式与流程图
在 `params.yml` 中：
- **数学公式**: 设置 `math.katex.enable: true` 或 `math.mathjax.enable: true` (二选一)。
- 文章中启用: 在文章头部的 Front-matter 中添加 `math: true`。
- **流程图 (Mermaid)**: 文章 Front-matter 中添加 `mermaid: true`。

---

## 4. 内容管理与写作

### 4.1 新建文章
在命令行运行：
```powershell
hugo new post/您的文章标题.md
```
或者直接在 `content/post/` 目录下新建 `.md` 文件。

### 4.2 文章属性 (Front-matter)
文章开头的 YAML 区域决定了文章的属性。常用字段如下：

```yaml
---
title: "文章标题"
date: 2024-03-20T10:00:00+08:00
draft: false          # 是否为草稿 (true 则不显示)
categories: ["分类A"]  # 分类
tags: ["标签1", "标签2"] # 标签
cover: "image.jpg"    # 文章专属封面图 (可选)
# cover: false        # 设为 false 可隐藏封面
# cover: rgb(255,0,0) # 设为颜色值可显示纯色背景
description: "文章摘要" # 首页显示的文章摘要
sidebar: right        # left | right (侧边栏位置)
toc: true             # 是否显示目录
math: true            # 是否启用数学公式
mermaid: true         # 是否启用流程图
comments: true        # 是否开启评论
sticky: 1             # 置顶优先级 (数字越大越靠前)
---
```

### 4.3 建立必要页面
为了保证主题正常运行，请确保以下文件存在（参考 `themes/reimu/exampleSite/content`）：

1.  **归档页面**: `content/archives/_index.md`
    ```yaml
    ---
    title: "归档"
    layout: "archives"
    ---
    ```
2.  **关于页面**: `content/about.md` (可选)
3.  **友链页面**: `content/friend.md` (可选)

---

## 5. 常用写作短代码 (Shortcodes)

Reimu 提供了一些增强写作体验的工具：

- **链接卡片**:
  ```html
  {{< link title="标题" link="https://example.com" >}}
  ```
- **照片墙**:
  ```html
  {{< gallery >}}
  ![描述](图片URL1)
  ![描述](图片URL2)
  {{< /gallery >}}
  ```
- **标签页 (Tabs)**:
  ```html
  {{< tabs >}}
  <!-- 标题1 -->
  内容1...
  <!-- 标题2 -->
  内容2...
  {{< /tabs >}}
  ```
- **警告提示块**:
  ```html
  {{< alertBlockquote type="tip" >}}
  这是一个提示信息。
  {{< /alertBlockquote >}}
  ```
  type 可选: `note`, `tip`, `important`, `warning`, `danger`。

---

## 6. 常见问题

1.  **修改了配置不生效？**
    - 确保您修改的是 `config/_default/params.yml` 而不是主题文件夹里的。
    - 也可以尝试停止 `hugo server` 并重新运行。

2.  **想自定义 CSS？**
    - 不建议修改主题 CSS。可在 `static/css/` 下新建 `custom.css`，然后在 `hugo.toml` 或 `params.yml` 中引入（视具体支持情况，通常建议直接在 `layouts/partials/head.html` 覆盖，或查看是否有 `custom_css` 配置项）。*注：Reimu 并没有直接暴露 custom_css 选项，高级修改需在 `layouts` 文件夹覆盖同名文件。*

3.  **如何更新主题？**
    - 如果是通过 Git Submodule 安装：`git submodule update --remote`。
    - 更新后请对比 `params.yml` 是否有新增配置项。

---

祝您使用愉快！如有更多问题，可参考 [Reimu GitHub 仓库](https://github.com/D-Sketon/hugo-theme-reimu)。
