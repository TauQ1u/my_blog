# TauQ1u 的博客

基于 [Hugo](https://gohugo.io/) + [Stack 主题](https://github.com/CaiJimmy/hugo-theme-stack) 的个人博客，推送到本仓库后由 GitHub Actions 自动构建并部署到 GitHub Pages。

在线地址：[https://tauq1u.github.io/my_blog/](https://tauq1u.github.io/my_blog/)

---

## 一、站点结构

```
blog/
├── config/_default/     # 站点配置（标题、菜单、参数都在这里）
│   ├── hugo.toml        # 基础配置：网址、标题、标签法
│   ├── params.toml      # 头像、图标、小部件、评论(giscus)
│   ├── menu.toml        # 菜单与社交链接（GitHub / B站）
│   └── languages.toml   # 多语言标题与副标题
├── content/             # ★ 你的所有内容都在这里
│   ├── _index.md        # 主页（即"关于"页，改自我介绍改这个文件）
│   ├── computer/        # 板块：计算机（科研·技术栈·比赛）
│   ├── other/           # 板块：其他（CS·音乐·随笔）
│   ├── post/            # 未归板块的文章（一般不用）
│   ├── tags/            # 六个方向标签（含分类页图片）
│   └── page/            # 归档、搜索等独立页面
├── assets/img/          # 头像(Profile.png)、网站图标(Site.png)
├── picture/             # 图片素材库（换头像改这里面的 Profile.png）
├── layouts/             # 自定义模板（分类页、页脚，一般不用动）
└── public/              # 构建产物，不要手动改
```

## 二、写文章放在哪

博客有两个板块，文章按板块分目录存放：

| 想写的内容               | 放在哪个目录          |
| ------------------------ | --------------------- |
| 科研、课程、论文笔记     | `content/computer/` |
| 技术栈、教程、踩坑记录   | `content/computer/` |
| 比赛（ACM、CTF、数模等） | `content/computer/` |
| CS（反恐精英）           | `content/other/`    |
| 音乐                     | `content/other/`    |
| 随笔、生活               | `content/other/`    |

### 最简单的方式：一条命令新建文章

```bash
hugo new content computer/我的第一篇文章/index.md
# 或者"其他"板块：
hugo new content other/我的随笔/index.md
```

> Windows 如果提示找不到 `hugo` 命令，先去 [https://github.com/gohugoio/hugo/releases](https://github.com/gohugoio/hugo/releases) 下载 `hugo_extended_xxx_windows-amd64.zip`，解压后把 `hugo.exe` 所在目录加入系统环境变量 Path。

### 文章格式（front matter 模板）

新建的文件开头已经生成好模板，改成这样即可：

```markdown
---
title: "我的文章标题"          # 必填
description: "一句话介绍"      # 显示在文章卡片上，建议填
date: 2026-10-05               # 发布日期
image: cover.jpg               # 封面图（可选，把图片和 index.md 放同一文件夹）
tags:                          # ← 方向标签，从下面六个里选
  - 科研
math: false                    # 写数学公式时改成 true
---

这里开始写正文，支持 Markdown 语法。
```

**方向标签（六个，名字不能错）：**

| 板块   | 可用标签                           |
| ------ | ---------------------------------- |
| 计算机 | `科研`、`技术栈`、`比赛`     |
| 其他   | `CS反恐精英`、`音乐`、`随笔` |

文章头部和结尾会自动显示标签，点击标签可查看该方向下的所有文章。

### 文章里的图片

推荐用**页面捆绑**：把图片放在文章自己的文件夹里，正文直接引用文件名：

```
content/computer/我的文章/
├── index.md
└── 截图.png
```

```markdown
![说明文字](截图.png)
```

## 三、常用修改速查

| 想改什么                        | 改哪里                                                                     |
| ------------------------------- | -------------------------------------------------------------------------- |
| 自我介绍（主页/关于页）         | `content/_index.md`                                                      |
| 换头像                          | 替换`picture/Profile.png` 后，复制覆盖到 `assets/img/Profile.png`      |
| 网站图标                        | 替换`assets/img/Site.png`                                                |
| 站点标题 / 副标题               | `config/_default/hugo.toml`、`config/_default/languages.toml`          |
| GitHub / B站链接                | `config/_default/menu.toml`                                              |
| 新增一个方向（标签+分类页图片） | 在`content/tags/` 下新建目录，参照现有标签的结构（`_index.md` + 图片） |
| 版权协议文字                    | `config/_default/params.toml` 的 `[article.license]`                   |
| 每页文章数量                    | `config/_default/hugo.toml` 的 `pagerSize`                             |

## 四、本地预览与发布

```bash
# 本地预览（保存文件后浏览器自动刷新，Ctrl+C 停止）
hugo server

# 然后浏览器打开 http://localhost:1313/my_blog/zh/
```

发布只有三步：

```bash
git add -A
git commit -m "写点这次改了什么"
git push
```

push 后 GitHub Actions 会自动构建并部署，一两分钟后线上生效。

> ⚠️ 如果装了 Watt Toolkit（steam++）之类的 GitHub 加速工具，**push/pull 前要暂时关闭 GitHub 加速**，否则会被本地反代拦截导致推送失败（报错 `no DAV locking support`）。

## 五、评论区（giscus）

评论基于 [giscus](https://giscus.app)，评论数据存放在 GitHub Discussions 里。

**首次启用还需要两步（只做一次）：**

1. 打开 [https://github.com/TauQ1u/my_blog/settings](https://github.com/TauQ1u/my_blog/settings)，勾选 **Discussions** 功能；
2. 打开 [https://giscus.app](https://giscus.app)，在配置页：
   - `repository` 填 `TauQ1u/my_blog`；
   - 按提示安装 giscus 的 GitHub App；
   - Discussion 分类选 **General**；
   - 页面下方会生成 `data-repo-id` 和 `data-category-id` 两个值。

把这两个值填进 `config/_default/params.toml` 的 `[comments.giscus]` 里对应的
`repoID` / `categoryID`，重新部署即可。

## 六、其他说明

- 目前只维护中文内容；其他语言（en/ja/zh-hant）是主题自带的空壳，不用管。
- 分类页（菜单"分类"）只显示 `content/tags/` 里配了图片的方向，新增方向记得放 `_index.md` 和图片。
- 归档页、搜索页无需维护，自动生成。
