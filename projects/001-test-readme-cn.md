---
title: "从零开始：用 Quarto + GitHub Pages 打造 PARA 系统博客"
date: 2025-12-02
categories: [Quarto, Blog, Tutorial, PARA]
description: "如何使用 Quarto 构建一个支持代码渲染、无需服务器、且拥有 PARA 知识管理架构的现代化个人网站。"
image: 001-test-cover.jpg # 建议找一张图放在同级目录，作为本文的封面
---

## 1. 为什么选择 Quarto?

作为技术人员或数据工作者，传统的 Hexo/Hugo 虽然强大，但对 Jupyter Notebook (`.ipynb`) 和 RMarkdown 的支持并不原生。**Quarto** 是 RStudio (Posit) 推出的下一代开源发布系统，它天生支持 Python/R/Julia 代码的执行与渲染，同时拥有极其简洁的配置逻辑。

这篇文章将记录我如何使用 **Quarto** 配合 **PARA 知识管理系统**，在 GitHub Pages 上搭建这个博客的全过程。

## 2. 常用命令速查 (Cheat Sheet)

在开始之前，这几个命令建议刻在脑子里，开发过程中会反复用到：

* **启动本地预览**:
    ```bash
    quarto preview
    ```
    *作用：启动本地服务器，保存文件后浏览器会自动刷新。*

* **清理缓存并重建** (救命命令):
    ```bash
    quarto render --clean
    ```
    *作用：当你发现改了配置没生效，或者页面样式错乱时，运行它！它会彻底清理缓存并重新编译。*

* **一键发布**:
    ```bash
    quarto publish gh-pages
    ```

这是一个**升级版**的博客教程文章。

我已将你刚才提到的需求全部融合进去了：

1.  **常用命令速查**：加入了 `render --clean` 和 `preview` 的说明。
2.  **配图说明**：特别强调了 Projects 在 Grid 布局下需要 `image` 才好看。
3.  **实战样例**：补充了 `areas` 里的文章写法，以及 `archives` 的工作原理。
4.  **字体调整**：把刚才的 Arial 12 配置也加进了配置文件代码中。

你可以直接复制这一整块代码，作为你的第一篇博客内容：


## 3. 初始化与 PARA 架构设计

在终端中运行以下命令，创建一个博客类型的项目骨架：

```bash
# 1. 创建项目
quarto create-project . --type website:blog

# 2. 清理默认文件
rm -rf posts about.qmd

# 3. 创建 PARA 目录
mkdir projects areas resources archives
````

我们需要分别为这四个目录创建索引文件 `index.qmd`，并指定不同的布局。

### Projects (网格视图)

Projects 适合展示作品集。
**注意：** 为了美观，`grid` 布局下的文章**强烈建议**配图，否则会显示为空白的灰色方块。

在 `projects/index.qmd` 中：

```yaml
---
title: "Projects"
listing:
  contents: .
  sort: "date desc"
  type: grid            # 网格布局
  categories: true
  fields: [image, date, title, description] # 显式要求显示图片
---
我的实战项目与代码作品。
```

### Areas (博客视图)

Areas 适合传统的长文阅读。

在 `areas/index.qmd` 中：

```yaml
---
title: "Areas"
listing:
  contents: .
  sort: "date desc"
  type: default         # 标准博客布局
  categories: true
---
深度思考与随笔。
```

### Archives (归档视图)

Archives 不需要写文章，它的作用是把所有其他文件夹的内容汇总在一起，形成一个时间线列表。

在 `archives/index.qmd` 中：

```yaml
---
title: "Archives"
listing:
  contents:             # 关键：这里引用其他三个文件夹
    - ../projects
    - ../areas
    - ../resources
  sort: "date desc"
  type: table           # 表格视图，像文件列表一样清晰
  fields: [date, title, categories]
---
所有内容的完整历史归档。
```

## 4\. 核心配置与字体调整

这是我的 `_quarto.yml` 配置，我调整了字体大小，使其更接近 Arial 12 的阅读体验：

```yaml
project:
  type: website
  output-dir: docs

website:
  title: "Standard Output"
  site-url: "[https://你的用户名.github.io](https://你的用户名.github.io)"
  navbar:
    right:
      - text: "Projects"
        href: projects/index.qmd
      - text: "Areas"
        href: areas/index.qmd
      - text: "Resources"
        href: resources/index.qmd
      - text: "Archives"
        href: archives/index.qmd
      - icon: github
        href: [https://github.com/你的用户名](https://github.com/你的用户名)

format:
  html:
    theme: litera
    css: styles.css
    toc: true
    # --- 字体微调 ---
    mainfont: "Arial, sans-serif"
    fontsize: 0.9em    # 0.9em 约等于 14.4px，视觉上接近 Word 的 12号字
    linestretch: 1.6   # 增加行高，提升阅读舒适度
```

## 5\. 实战：如何写文章 (Sample)

### 例子 A：写一个 Project (带封面图)

文件路径：`projects/my-app/index.qmd`

```markdown
---
title: "Python 爬虫实战"
date: 2025-12-05
categories: [Python, Project]
image: featured.png   # 【重要】Grid 布局需要这张图才好看！
description: "爬取豆瓣电影Top250的完整代码。"
---

这里是正文...
```

### 例子 B：写一篇 Area 随笔

文件路径：`areas/thoughts/index.qmd`

```markdown
---
title: "关于长期主义的思考"
date: 2025-12-06
categories: [Life, Thinking]
# Areas 默认列表布局不需要 image，当然加上也可以
---

这里是正文...
```

## 6\. 首页设计 (Dashboard)

为了让首页直观展示 PARA 文件夹，我们在根目录的 `index.qmd` 中使用栅格布局。
**关键点**：必须设置 `listing: false` 以去除底部的重复列表。

```markdown
---
title: "Standard Output"
listing: false          # 关键！防止首页底部出现杂乱的文章列表
about:
  template: jolla
  image: profile.jpg
  links:
    - icon: github
      href: [https://github.com](https://github.com)
---

👋 欢迎来到我的数字花园。

---

::: {.grid}

::: {.g-col-12 .g-col-md-6}
### 🚀 [Projects](projects/index.qmd)
**进行中的项目**
<br>
[📂 打开文件夹](projects/index.qmd){.btn .btn-outline-primary .btn-sm role="button"}
:::

::: {.g-col-12 .g-col-md-6}
### 💡 [Areas](areas/index.qmd)
**思考与随笔**
<br>
[📂 打开文件夹](areas/index.qmd){.btn .btn-outline-primary .btn-sm role="button"}
:::

:::
```


# 注意 markdown的``` 上下对应