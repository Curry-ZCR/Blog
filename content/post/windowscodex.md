---
title: 'Windows配置codex'
date: 2025-12-18
draft: false
tags:
  - codex，AI，教程
cover: 'avatar/1.webp'
description: '在Windows上面配置codex，包含终端和vscode
---

# **切换到 “镜像 (Mirrored)” 网络模式**

## 1. 在 Windows 用户目录下（例如 C:\Users\你的用户名\ ）创建或编辑文件 .wslconfig 。

## 2. 在文件中加入类似内容：

```bash
[wsl2]
[experimental]
networkingMode=mirrored
autoProxy=true
dnsTunneling=true
firewall=true
```

## 3. 在 PowerShell 或命令提示符中执行：

```bash
wsl --shutdown
```

## 4. 重新启动 WSL（比如打开 Ubuntu 等发行版）。

# **在wsl上安装codex**

```bash
# 下载并安装 nvm：
curl -o- <https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh> | bash
# 代替重启 shell
\\. "$HOME/.nvm/nvm.sh"
# 下载并安装 Node.js：
nvm install 24
# 验证 Node.js 版本：
node -v # Should print "v24.11.1".
# 验证 npm 版本：
npm -v # Should print "11.6.2".
```

## 安装codex

```json
npm i -g @openai/codex
```

## **在 WSL 模式下打开位于 Windows 的文件夹**

如果你希望借助 WSL 的 Linux 环境（比如用 Linux shell、工具链、路径）同时项目文件存放在Windows，那么可以这样操作：

### 1.在 Windows 上启动 VS Code，确保已安装 “Remote – WSL” 扩展（或 “WSL” 扩展包）以便支持WSL 模式。

![image.png](attachment:39872f63-2c54-4df7-83b6-c585a1fb606b:image.png)

**2.在 VS Code 中点击左下角绿色的 “><” 或 “WSL” 图标，选择 “Remote-WSL: 新建窗口” 或**

**“Connect to WSL”。**

**3.如果你的项目在 Windows 的 D:\project ，在 WSL 中可以通过 /mnt/d/project 来访 问**
