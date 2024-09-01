---
title: 如何使用Jekyll在GitHub Pages上搭建个人网站
date: 2024-08-31 18:36:00 +/-0800
categories: [Misc]
tags: [github]     # TAG names should always be lowercase
author: <author_id> 
description: 介绍如何使用Jekyll在GitHub Pages上搭建个人网站
---

本文基于Windows系统，其他系统请阅读官方文档。

## 1.安装依赖

### 1.1 安装git

可参考以下博客：

[git的安装与配置（详细） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/597447255)

> 不安装git，后续更新博客会报`No such file or directory - git rev-list --count HEAD`的错误。
{: .prompt-danger }

### 1.2 安装Ruby

下载地址：https://rubyinstaller.org/downloads/

选择 **Ruby+Devkit** 版本，我用的版本是3.3.4。

在安装向导最后一步勾选选项：

![image-20240901195135873](/images/2024-09-01-how-to-build-githubio.assets/image-20240901195031009.png)

在弹出的命令行窗口中选择 “MSYS2 and MINGW development tool chain”：

![image-20240901195135873](/images/2024-09-01-how-to-build-githubio.assets/image-20240901195135873.png)

检查是否安装成功：

```bash
ruby -v 
gem -v 
```

![image-20240901195229777](/images/2024-09-01-how-to-build-githubio.assets/image-20240901195229777.png)

### 1.3 安装Jekyll

打开一个新的CMD窗口，执行以下命令安装Jekyll和Bundler：

```bash
gem install jekyll bundler 
```

检查是否安装成功：

```bash
jekyll -v 
```

## 2 主题

**主题**(theme)提供了网站页面的布局和样式，详见官方文档[Themes](https://jekyllrb.com/docs/themes/)。

在以下页面选择你喜欢的主题：

[http://jekyllthemes.org/ ](http://jekyllthemes.org/ )

## 3 搭建网站

下面正式开始搭建网站。我使用的是[Chirpy](https://chirpy.cotes.page/posts/getting-started/)主题。

### 3.1 创建网站

打开[chirpy-starter](https://github.com/cotes2020/chirpy-starter)仓库，点击按钮 “Use this template” → “Create a new repository”。

<img src="/images/2024-09-01-how-to-build-githubio.assets/image-20240901195532758.png" alt="image-20240901195532758" style="zoom: 33%;" />

将新仓库命名为`<username>.github.io`，其中`<username>`是你的GitHub用户名，如果包含大写字母需要转换为小写。

### 3.2 安装依赖

使用`git clone`将新创建的仓库克隆到本地，并在项目根目录下执行

```bash
1 bundle 
```

### 3.3 配置

更新`_config.yml`：

```yml
#line 9：语言
lang: zh-CN  
#line 12：时区
timezone: Asia/Shanghai
#line 17：title
title: Acang's Blog 
#line 19：subtitle
tagline: 欢迎来到阿仓的博客
#line 26：url
url: "https://acang425.github.io"
```

还可以更新`_tabs\about.md`，修改个人展示页面。

### 3.4 启动本地服务器

要在本地预览网站内容，执行

```
1 bundle exec jekyll serve 
```

在浏览器访问 [http://127.0.0.1:4000/](http://127.0.0.1:4000/)。

### 3.5 添加个人博客

详见：
[Writing a New Post | Chirpy (cotes.page)](https://chirpy.cotes.page/posts/write-a-new-post/)

在_post文件夹中添加markdown文件，文件名格式为：`YYYY-MM-DD-title`。

在文件开头加入**Front Matter**：

```markdown
---
title: 论文阅读笔记
date: 2024-08-31 18:36:00 +/-0800
categories: [Deep Learning]
tags: [paper]     # TAG names should always be lowercase
author: <author_id> 
description: 一篇人脸三维模板反演论文的阅读笔记
---
```

其中`<author_id>` 来自`_data\authors.yml`：

```yaml
<author_id>:
  name: Jiaxin Hong
  url: https://acang425.github.io
```

若有本地图片，记得一起放进项目中，建议放在`images`中，并全局修改文件路径。

### 3.6 部署

在GitHub上打开仓库设置，点击左侧导航栏 “Pages”，在 “Build and deployment” - “Source” 下拉列表选择 “GitHub Actions”。

![image-20240901201036091](/images/2024-09-01-how-to-build-githubio.assets/image-20240901201036091.png)

提交本地修改并推送至远程仓库，即可访问个人网站。

