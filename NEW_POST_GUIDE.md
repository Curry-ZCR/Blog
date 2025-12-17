# 新建博客文章流程指南

本文档详细介绍了如何在您的 Hugo 博客（Reimu 主题）中创建、编辑和发布一篇新的博客文章。

## 1. 创建文章文件

有两种方式可以创建新文章：**使用命令行（推荐）** 或 **手动创建**。

### 方式一：使用命令行（推荐）
在项目根目录（`d:\Blog\dev`）打开终端（PowerShell 或 CMD），运行以下命令：

```powershell
# 语法：hugo new post/文件名.md
# 例如创建一篇名为 "my-first-blog" 的文章：
hugo new post/my-first-blog.md
```

> **注意**：文件名建议使用**英文**或**拼音**，因为这会成为文章 URL 的一部分。

如果不小心创建错了位置，可以直接在文件管理器中移动文件到 `content/post/` 目录下。

### 方式二：手动创建
直接在文件资源管理器中：
1. 进入 `content/post/` 文件夹。
2. 新建一个 `.md` 文件，例如 `study-notes.md`。
3. **必须**在文件开头手动复制粘贴 Front-matter（文章属性块），见下文。

---

## 2. 编辑文章属性 (Front-matter)

打开刚才创建的 `.md` 文件，文件最上方被 `---` 包裹的区域就是文章的属性配置。请根据需要修改：

```yaml
---
title: "这里填写文章标题"       # 文章大标题
date: 2024-03-20T16:00:00+08:00 # 创建时间（自动生成）
draft: true                     # 是否为草稿？
                                # true: 草稿，只有运行 hugo server -D 才能看到
                                # false: 正式发布，所有人可见
categories: ["学习笔记"]        # 文章分类
tags: ["Hugo", "教程"]          # 文章标签
cover: "images/covers/1.jpg"    # (可选) 文章专属封面图
                                # 填写 static 目录下的相对路径
                                # 或者填写网络 URL
                                # 留空或删除此行则使用随机封面
description: "这是一篇关于..."  # (可选) 文章摘要，显示在首页卡片上
toc: true                       # 是否显示右侧目录
math: false                     # 是否启用数学公式渲染
mermaid: false                  # 是否启用流程图渲染
sticky: 0                       # 置顶优先级，数字越大越靠前 (0为不置顶)
---
```

> **关键点**：
> *   写完后，记得将 `draft: true` 改为 **`draft: false`**，否则生成网站时不会包含这篇文章。

---

## 3. 撰写正文内容

在 `---` 下方即可开始使用 Markdown 语法撰写正文。

### 常用 Markdown 语法
```markdown
## 二级标题
### 三级标题

**加粗文字**
*斜体文字*

- 无序列表项 1
- 无序列表项 2

1. 有序列表项 1
2. 有序列表项 2

>虽然但是，这是一段引用文本。
```

### 插入图片
1.  **存放图片**：建议在 `static/images/` 下建立一个以文章名为名的文件夹，例如 `static/images/2024/my-first-blog/`，将图片放入其中。
2.  **引用图片**：
    ```markdown
    ![图片描述](/images/2024/my-first-blog/image.png)
    ```
    > **注意**：引用路径**不要**包含 `static`，直接以 `/` 开头即可。

### 使用主题特色功能 (Shortcodes)
Reimu 主题提供了一些漂亮的组件：

*   **提示块**：
    ```markdown
    {{< alertBlockquote type="tip" >}}
    这是一个提示信息
    {{< /alertBlockquote >}}
    ```
    (type 可选: `info`, `note`, `tip`, `warning`, `danger`)

---

## 4. 本地预览

在发布之前，先在本地查看效果。在终端运行：

```powershell
hugo server
```

*   如果您的文章 `draft: true`（草稿状态），请运行 `hugo server -D` 才能看到。
*   打开浏览器访问提示的地址（通常是 `http://localhost:1313/`）。
*   修改 `.md` 文件并保存后，浏览器会自动刷新显示最新内容。

---

## 5. 发布文章

1.  确认文章内容无误。
2.  将 Front-matter 中的 `draft` 改为 **`false`**。
3.  保存文件。
4.  (如果您配置了自动部署) 提交 Git 推送即可：
    ```powershell
    git add .
    git commit -m "Add new post: my-first-blog"
    git push
    ```

---

## 6. 常见问题

*   **图片不显示？**
    *   检查图片是否放在 `static` 目录下。
    *   检查 Markdown 引用路径是否以 `/` 开头，且**不包含** `/static/`（例如应为 `/images/xxx.jpg`）。
*   **首页看不到文章？**
    *   检查 `content/post/` 目录下是否有 `_index.md` 文件（通常用于归档配置）。
    *   检查文章的 `draft` 属性是否为 `true`。
