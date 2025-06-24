+++
title = 'Hugo 博客搭建指南'
slug = 'hugo-blog-guide'
date = 2025-06-22T18:20:00+08:00
lastmod = 2025-06-23T23:20:00+08:00
draft = false
categories = ["Blog"]
tags = ["hugo","blog","tinker"]
+++

## 写在前面

这是这个新博客的第一篇文章。

从 22 年至今，已搭建了三次博客。每一次的搭建，都是一次折腾之旅。从 Typecho 到 Halo，从 LNMP 架构到 Docker 部署。从最初选择平台时的纠结，到日夜调试配置时的兴奋……

一路走来，心态也在悄然发生变化。

如今我逐渐明白，博客的技术架构和细节美化并没有那么重要。真正关键的，是那动笔记录的过程。

在一次一次的键盘敲击中，将思绪梳理成文字，将技术沉淀为知识。用合适的方式表达自我，输出有价值的内容。这才是 Blog 的意义所在。

希望我可以将这个博客可以运营的更久吧。: )

---

花了半个月时间，参考了许多网上的优秀实践，在功能上取长补短，搭建了这么一个还算令我自己满意的博客。

在记忆还尚未模糊的当下，于此记录搭建博客的细节。这既是为自己留下的的总结与备份，也希望为后来者提供一些参考，少走一些弯路。

[**本文源码**](https://github.com/Ruixi-Cheng/ruixi-cheng.github.io)，开发过程非常详细的写在git里，供大家参考。

## 为什么是 Hugo?

![hugo](https://gohugo.io/images/hugo-logo-wide.svg)。

私以为，对于个人开发者而言，动态博客的一些复杂功能——如用户系统、权限管理，性能监控等——显得较为多余。毕竟，写作的核心在于内容本身。

[Hugo](https://github.com/gohugoio/hugo) 是一个 Go 语言编写、开源的静态网站生成器。它构建速度极快，语法简洁，功能丰富，社区活跃，具备高度的灵活性和可扩展性。这些特性使得它成为搭建个人博客的理想选择。

## Hugo 入门

### 安装

从 [Github Releases](https://github.com/gohugoio/hugo/releases/) 内下载适用于你系统的软件包、二进制可执行文件，或直接直接从源码编译。(建议使用 Hugo Extended 以获得额外功能的支持。)

安装完成后，在终端内运行以下命令以确认是否安装完成 ：

```bash
hugo version
# hugo v0.147.8-10da2bd765d227761641f94d713d094e88b920ae+extended linux/amd64 BuildDate=2025-06-07T12:59:52Z VendorInfo=gohugoio
```

### 主题选择

Hugo 官网的[主题页面](https://themes.gohugo.io/)提供了许多不同用途的主题以供选择。

笔者选择了 [PaperMod](https://github.com/adityatelange/hugo-PaperMod) 主题。

### Hugo 新建站点

使用以下命令创建一个站点：

```bash
hugo new site test.io   # 创建新站点
cd test.io/
git init    # 创建 git 仓库，方便主题安装和后期管理
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod  # 使用 git submodule 添加主题
echo "theme = 'PaperMod'" >> hugo.toml  # 在配置文件中指定使用 PaperMod 主题
hugo server # 启动 Hugo 本地服务器
```

你会在终端中看到本地站点的 URL（通常为 http://localhost:1313）。通过浏览器访问即可看见 PaperMod 的默认页面效果：

[![pVeEjDH.png](https://s21.ax1x.com/2025/06/24/pVeEjDH.png)](https://imgse.com/i/pVeEjDH)

### 站点结构

{{<collapse openByDefault=true summary="新建站点的结构：">}}
```bash
test.io/
├── archetypes
│   └── default.md  # 文章模板
├── assets  # css、js等资源
├── content # 博客内容
├── data    # 一些数据
├── hugo.toml   # 网站配置文件
├── i18n # 多语言相关文件
├── layouts # 网站布局相关
├── public # 渲染后的 HTML 代码目录
├── static  # 网站的字体和 favicons
└── themes # 主题文件夹
    └── PaperMod
```
{{</collapse>}}

{{<collapse summary="我的博客的结构：">}}
```bash
.
├── archetypes
│   └── default.md
├── assets
│   └── css
│       ├── common
│       ├── core
│       └── extended
├── config  # config 可以拆成多文件
│   └── _default
│       ├── hugo.toml
│       ├── languages.toml
│       ├── menu.en.toml
│       ├── menu.ja.toml
│       └── menu.zh.toml
├── content
│   ├── about   # 三种语言的页面文档，下同
│   │   ├── _index.en.md
│   │   ├── _index.ja.md
│   │   └── _index.zh.md
│   ├── archives    # 归档
│   ├── categories  # 分类
│   │   ├── tech
│   │   └── test
│   ├── friends # 友链
│   ├── posts   # 文章
│   │   ├── hugo-papermod-blog-guide
│   │   └── Test-Post
│   └── search  # 搜索
├── data    # 数据
│   ├── friends.toml
│   └── notice.toml
├── i18n    # 多语言翻译
│   ├── en.yaml
│   ├── ja.yaml
│   └── zh.yaml
├── layouts # 部分自定义网络结构
│   ├── _default
│   │   ├── about.html
│   │   ├── friends.html
│   │   ├── _markup
│   │   └── terms.html
│   ├── partials
│   │   ├── comments.html
│   │   ├── extend_footer.html
│   │   ├── extend_head.html
│   │   ├── footer.html
│   │   ├── header.html
│   │   ├── math.html
│   │   ├── post_meta.html
│   │   └── toc.html
│   └── shortcodes
│       ├── collapse.html
│       ├── friends.html
│       ├── notice.html
│       ├── quote.html
│       ├── sidenote.html
│       └── social_icons.html
├── LICENSE
├── public
├── README.md
├── static  # 字体和网站图标
│   ├── favicon-16x16.png
│   ├── favicon-32x32.png
│   ├── favicon.png
│   ├── favicon.svg
│   └── fonts
└── themes
```
{{</collapse>}}

### Hugo 的基础命令

使用 `hugo new` 根据**文章模板**新增内容：

```bash
hugo new posts/Test-Post.md
```

{{<collapse summary="**效果如下**：">}}
```bash
content/
└── posts
    └── Test-Post.md
```
{{</collapse>}}

使用 `hugo` 正式生成静态网页：

```bash
hugo
```

{{<collapse summary="**效果如下**：">}}
```bash
public/
├── 404.html
├── assets
│   └── css
│       └── stylesheet.8fe10233a706bc87f2e08b3cf97b8bd4c0a80f10675a143675d59212121037c0.css
├── categories
│   ├── index.html
│   └── index.xml
├── index.html
├── index.xml
├── page
│   └── 1
│       └── index.html
├── posts
│   ├── index.html
│   ├── index.xml
│   └── page
│       └── 1
│           └── index.html
├── sitemap.xml
└── tags
    ├── index.html
    └── index.xml
```
{{</collapse>}}

使用 `hugo server` 开启本地预览服务器

```bash
hugo server -D # -D 参数会生成草稿内容
```

然后你应该就可以在 http://localhost:1313 预览网站。

一些我常用的参数：

|         参数          |     含义     |
| :-------------------: | :----------: |
| --cleanDestinationDir | 清空输出目录 |
|          -D           | 构建草稿内容 |
|    --bind 0.0.0.0     | 允许外部访问 |
|        -p 1313        |  指定端口号  |
|       --baseURL       | 设置基础 URL |

## Hugo 配置

[Hugo 配置文件](https://gohugo.io/configuration/)一般为站点根目录下的单一配置文件 `hugo.toml` 或 `hugo.yaml` 、 `hugo.json` 文件。

笔者选择了 `.toml` 文件。

或是将配置拆分为多个文件，建立文件夹如下：

```bash
config/
└── _default
    ├── hugo.toml 
    ├── languages.toml
    ├── menu.en.toml
    ├── menu.ja.toml
    └── menu.zh.toml
```

详见<https://gohugo.io/configuration/introduction/#configuration-directory>

笔者配置如下，供大家参考：

{{<collapse summary="hugo.toml">}}
```toml
baseURL = 'https://ruixi.top/'  # 网站根地址
title = "Ruixi's Blog"  # 网站标题
theme = 'PaperMod'  # 使用的主题名称
languageCode = 'en-US'

defaultTheme = "dark"  # 默认使用暗色背景主题
buildDrafts = false # 是否构建草稿
buildFuture = false # 是否构建未来发布的内容
buildExpired = false # 是否构建已过期的内容
defaultContentLanguage = "en" # 顶部首先展示的语言界面
enableRobotsTXT = true # 是否生成 robots.txt 文件
enableInlineShortcodes = true # 是否启用内联 shortcode
enableEmoji = true # 是否启用 Emoji 表情支持
defaultContentLanguageInSubdir = true # 是否要在地址栏加上默认的语言代码

[minify]
  disableXML = true   # 防止 XML 文件被压缩出错
  minifyOutput = true # 启用压缩优化输出体积

[permalinks]
  post = "/:slug/"  # 自定义文章永久链接格式

[caches]
  [caches.images]
    dir = ':cacheDir/images'    # 设置图片缓存目录

[outputs]
  home = ["HTML", "RSS", "JSON"]

[markup]
  [markup.highlight]
    codeFences = false
  [markup.goldmark]
    [markup.goldmark.renderer]
      unsafe = true
    [markup.goldmark.extensions]
      typographer = false # 禁用goldmark符号替换

[services]
  [services.googleAnalytics] 
    id = 'G-H5HDF4EPT6' # Google Analytics ID

[params]
  author = "Ruixi"  # 站点作者信息
  defaultTheme = "dark" # 网站标题
  math = true # 数学公式支持
  comments = true # 评论功能
  showToc = true    # 显示文章目录（TOC）
  tocOpen = true    # TOC 是否默认展开
  showPostNavLinks = true   # 显示文章导航链接
  showBreadCrumbs = true    # 显示面包屑导航
  showRssButtonInSectionTermList = true  # RSS 相关按钮显示
  showAllPagesInArchive = true         # 在归档页面显示所有页面
  showCodeCopyButtons = true           # 显示代码块复制按钮
  showWordCount = true                 # 显示文章字数统计
  showLastMod = true                # 显示最后修改时间
  disableScrollToTop = false  # 启用返回顶部按钮
  displayFullLangName = true
  fancyBox = true  # 启用 Fancybox 灯箱效果
  dateFormat = "2006/01/02"         # 日期格式化
  hideSummary = false

  [params.assets]
    favicon = "favicon.png"

  [params.fuseOpts]
    isCaseSensitive = false # 是否大小写敏感
    shouldSort = true # 是否排序
    location = 0
    distance = 1000
    threshold = 0.4
    minMatchCharLength = 2 # limit = 20 # 限制返回的搜索结果数量 
    keys = ["title", "permalink", "summary", "content"]
    includeMatches = true
```
{{</collapse>}}

{{<collapse summary="language.toml">}}
```toml
[en]
title = "Ruixi's Blog"
languageName = "English"
languageCode = "en"

[en.params.homeInfoParams]
Title = "Hi there. 👋"
Content = "This is Ruixi's cozy corner on the web."

[[en.params.socialIcons]]
name = "Github"
title = "Github"
icon = "Github"
url = "https://github.com/Ruixi-Cheng/"
[[en.params.socialIcons]]
name = "Bilibili"
title = "Bilibili"
icon = "Bilibili"
url = "https://space.bilibili.com/329971737"

[zh]
...

[ja]
...

```
{{</collapse>}}

{{<collapse summary="menu.en.toml">}}
```toml
[[main]]
name = "Posts"
title = "Posts"
pageRef = "/posts/"
weight = 1  # 权重值，决定先后顺序
[[main]]
name = "Categories"
title = "Categories"
pageRef = "/categories/"
weight = 2
[[main]]
name = "Tags"
title = "Tags"
pageRef = "/tags/"
weight = 3
[[main]]
name = "Archives"
title = "Archives"
pageRef = "/archives/"
weight = 4
[[main]]
name = "Search"
title = "Search"
pageRef = "/search/"
weight = 5
[[main]]
name = "Friends"
title = "Friends"
pageRef = "/friends/"
weight = 6
[[main]]
name = "About"
title = "About"
pageRef = "/about/"
weight = 7
```
{{</collapse>}}

## 文章元数据

在 `archetypes/default.md` 中，我们添加以下内容
```toml
+++
title = 'title'
slug = 'slug'   # url标签
date = 2025-06-22T18:20:00+08:00
lastmod = 2025-06-22T18:20:00+08:00 #最后编辑时间
draft = true    是否为草稿
categories = ["categories"] #类别
tags = ["tags"] #标签
+++
```

在用 `hugo new` 新建文章的时候，这些数据应会被自动添加。如果自己之间在 `post` 目录下新建文章也不要忘记手动添加这些数据。

## 创建常用页面

在使用 Hugo 构建个人博客时，除了基本的文章发布功能外，我们通常还会添加一些额外的页面，如「归档」、「关于」和「友链」等。

### 「归档」页面

在 `content` 目录中创建 `archive.md` 文件，或是 `archive` 文件夹。

```bash
content/archives/
├── _index.en.md
├── _index.ja.md
└── _index.zh.md
```

内容如下：

```markdown
+++
title = "Archives"
layout = "archives"
+++
```

在配置文件的 `[[menu.main]]` 添加如下字段即可：

```toml
name = "Archives"
title = "Archives"
pageRef = "/archives/"
weight = 4
```

关于 `toml` 的结构,本文不做过叙述。

### 「关于」页面

添加 `layouts/_default/about.html` 文件。

```html
{{- define "main" }}

<header class="page-header">
    <h1>{{ .Title }}</h1>
    {{- if .Description }}
    <div class="post-description">
        {{ .Description }}
    </div>
    {{- end }}
</header>

<section>
    <br>
    {{ .Content }}
</section>

{{- end }}{{/* end main */}}
```

再如上文新增「归档」页面,创建 `about.md` 文件，或是 `about` 文件夹。
Markdown内容如下：

```markdown
+++
title = "About"
layout = "about"
+++
写你想写的内容
```

Hugo 配置文件添加相关菜单字段即可。

### 「友链」页面

添加 `layout/shortcodes/friends.html` 文件。
```html
<div class="friends">
    {{ range .Site.Data.friends.list.friends}}
    <div class="friend-skeleton">
        <a href="{{ .link }}" target="_blank">
            <div class="friend">
                <img class="friend-avatar" src="{{ .image }}" />
                <div class="friend-content">
                    <div class="friend-name">{{ .title }}</div>
                    <div class="friend-description">{{ .intro }}</div>
                </div>
            </div>
        </a>
    </div>
    {{ end }}
</div>
```

添加 `assets/css/extended/friends.css` 文件：

{{<collapse summary="friends.css">}}
```css
.friends {
    --link-count-per-row: 1;
}

@media screen and (min-width: 640px) {
    .friends {
        --link-count-per-row: 2;
    }
}

.friends {
    display: grid;
    grid-template-columns: repeat(var(--link-count-per-row), 1fr);
    grid-gap: 20px;
}

.friend-skeleton {
    height: 100px;
    /* 调整为合适的高度 */
    display: inline-block;
    position: relative;
}

.friend {
    height: 100%;
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    transition: 0.67s cubic-bezier(0.19, 1, 0.22, 1);
    border-radius: var(--radius);
    box-shadow: 0 3px 1px -2px rgba(0, 0, 0, 0.2),
        0 2px 2px 0 rgba(0, 0, 0, 0.14), 0 1px 5px 0 rgba(0, 0, 0, 0.12) !important;
    overflow: hidden;
    display: flex;
    align-items: center;
    /* 垂直居中 */
    padding: 16px;
    background-color: var(--entry);
    /* 可选背景色 */
}

.friend:hover {
    transform: translateY(-8px);
    box-shadow: 0 3px 5px -1px rgba(0, 0, 0, 0.2),
        0 5px 8px 0 rgba(0, 0, 0, 0.14), 0 1px 14px 0 rgba(0, 0, 0, 0.12) !important;
}

.friend-avatar {
    object-fit: cover;
    width: 72px;
    height: 72px;
    border-radius: 50%;
    /* 圆形头像 */
    margin-right: 16px;
    /* 和文字之间留点空隙 */
    flex-shrink: 0;
    /* 防止被压缩 */
    border: 2px solid color-mix(in srgb, var(--primary) 48%, transparent);
}

.friend-content {
    display: flex;
    flex-direction: column;
    justify-content: center;
    flex: 1;
    overflow: hidden;
}

.friend-name {
    font-size: 1.2rem;
    font-weight: bold;
    margin-bottom: 4px;
}

.friend-description {
    font-size: 0.9rem;
    color: var(--secondary);
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
```
{{</collapse>}}

添加 `layouts/_default/friends.html` 文件：

```html
{{- define "main" }}

<header class="page-header">
    <h1>{{ .Title }}</h1>
    {{- if .Description }}
    <div class="post-description">
        {{ .Description }}
    </div>
    {{- end }}
</header>

<section>
    <br>
    {{ .Content }}
</section>

{{- end }}{{/* end main */}}
```

最后在 `content` 文件夹中新增 `friends.md` 或 `friends` 文件夹。

内容如下,这是一个和「关于」很类似的页面，只是多调用了 `friends` Shortcode。

```text
+++
title = "Friends"
layout = "friends"
+++

{{</* friends */>}}
```

友链数据储存在 `data/friends.toml`

```toml
[list]
[[list.friends]]
title = "张三的博客"
intro = "张三"
link = "https://zhangsan.github.io/"
image = "图片url"
[[list.friends]]
title = "李四的博客"
intro = "李四"
link = "https://lisi.top/"
image = "图片url"
```
### 「搜索」页面

「搜索」是 PaperMod 主题自带的页面

在 `content` 文件夹中新增 `search.md` 或对应的 `search` 文件夹。
```markdown
+++
title = "Search"
layout = "search"
+++
```
在 Hugo 配置文件中按需修改相关参数，并添加相关菜单字段即可。
```toml
[params.fuseOpts]
    isCaseSensitive = false # 是否大小写敏感
    shouldSort = true # 是否排序
    location = 0
    distance = 1000
    threshold = 0.4
    minMatchCharLength = 2 # limit = 20 # 限制返回的搜索结果数量 
    keys = ["title", "permalink", "summary", "content"]
    includeMatches = true
```

### 「标签」界面

「标签」也是 PaperMod 自带的页面，直接添加 Hugo 配置文件的相关菜单字段即可。

不过我改动了许多的「标签」页面 CSS。

{{<collapse summary="assets/css/extended/tag-cloud.css">}}
```css
/*标签云*/
.terms-tags {
    text-align: center;
}

.terms-tags a {
    font-size: 24px;
    font-weight: 100; 
    color: var(--primary);
    display: inline-block; 
    background: none;
    border-radius: var(--radius);
    transition: transform 0.5s;
}

.terms-tags a:hover {
    background: color-mix(in srgb, var(--code-block-bg) 100%, transparent);
    border-radius: var(--radius);
    transform: scale(1.2);
    transition: all 0.3s ease;
}

.dark.terms-tags a {
    font-size: 24px;
    font-weight: 100; 
    color: var(--primary);
    display: inline-block; 
    background: none;
    border-radius: var(--radius);
    transition: transform 0.5s;
}

.dark .terms-tags a:hover {
    background: color-mix(in srgb, var(--code-block-bg) 50%, transparent);
    box-shadow: 0 0 15px var(--code-bg);
    border-radius: var(--radius);
    transform: scale(1.2);
    transition: all 0.3s ease;
}

.terms-tags li {
    margin: 5px;
}
```
{{</collapse>}}

### 「分类」页面

将 `themes/PaperMod/layouts/_default/terms.html` 复制到 `layouts/_default/terms.html` 并对其进行修改。

{{<collapse summary="修改后的 terms.html">}}
```html
{{- define "main" }}

{{- if .Title }}
<header class="page-header">
    <h1>{{ i18n .Title | default .Title }}</h1>
    {{- if .Description }}
    <div class="post-description">
        {{ .Description }}
    </div>
    {{- end }}
</header>
{{- end }}

{{ if (eq .Type "categories") }}
<div class="container">
    {{- $type := .Type }}
    {{- range $key, $value := .Data.Terms.Alphabetical }}
    {{- $name := .Name }}
    {{- $count := .Count }}
    {{- $maxCount := 5 }}
    {{ $actualCount := 0 }}

    {{ if lt $count $maxCount }}
    {{ $actualCount = $count }}
    {{ else }}
    {{ $actualCount = $maxCount }}
    {{ end }}

    {{- with $.Site.GetPage (printf "/%s/%s" $type $name) }}
    <a href="{{ .Permalink }}">
        <div class="card" style="--cards: {{ $count }};">
            <div class="child">
                <h2>{{ i18n .Title | default .Title }}</h2>
                {{ with .Page.Params.description }}
                <span>{{ . }}</span>
                {{ end }}
                <p>{{ $count }} {{ i18n "category_articles_count" }}</p>
                {{ if .Page.Params.image }}
                <img src="{{ .Page.Params.image | relURL }}" alt="{{ .Page.Params.alt }}" />
                {{ end }}
            </div>
            {{ range seq 1 $actualCount }}
            <div class="child"></div>
            {{ end }}
        </div>
    </a>
    {{- end }}
    {{- end }}
</div>

{{ else if (eq .Type "tags") }}

<ul class="terms-tags">
    {{- $type := .Type }}
    {{- range $key, $value := .Data.Terms.Alphabetical }}
    {{- $name := .Name }}
    {{- $count := .Count }}
    {{- with site.GetPage (printf "/%s/%s" $type $name) }}
    <li>
        <a href="{{ .Permalink }}">{{ .Name }} <sup><strong><sup>{{ $count }}</sup></strong></sup> </a>
    </li>
    {{- end }}
    {{- end }}
</ul>

{{ end}}

<style>
    .container {
        max-width: 900px;
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
        grid-gap: 48px;
        margin: 0 auto;
    }

    .card {
        cursor: pointer;
        position: relative;
        height: 0;
        padding-bottom: 120%;
        --offset-multiplier: 4px;
        transition: transform 0.6s ease;
        --translate: 0;
        transform: translate(var(--translate), var(--translate));
    }

    .card:hover {
        --offset-multiplier: 6px;
        --translate: calc(-1px * (var(--cards) - 1));
        transition: transform 0.3s ease, -webkit-transform 0.3s ease;
    }

    .child {
        position: absolute;
        width: 100%;
        height: 100%;
        padding: 8px 16px 8px 16px;
        box-sizing: border-box;
        background: var(--entry);
        box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1), 0px -4px 8px rgba(0, 0, 0, 0.1);
        border-radius: 6px;
        transition: inherit;
        --translate: calc(var(--offset) * var(--offset-multiplier));
        transform: translate(var(--translate), var(--translate));
        z-index: 5;
        font-family: 'LXGWWenKai', monospace !important;
        color:rgba(var(--nordrgb4), 0.9);
    }

    .child p {
        bottom: 1rem;
        right: 1rem;
        position: absolute;
        color:rgba(var(--nordrgb4), 0.4);
        font-family: 'NotoSansSC', monospace !important;
    }

    .child img {
        position: absolute;
        top: 60%;
        left: 50%;
        border-radius: var(--radius);
        transform: translate(-50%, -50%);
        width: auto;
        height: auto;
        max-width: 90%;
        max-height: 90%;
        z-index: -100;
        opacity: 0.5;
    }

    .child:nth-child(1) {
        --offset: 0;
        z-index: 4;
    }

    .child:nth-child(2) {
        --offset: 1;
        z-index: 3;
    }

    .child:nth-child(3) {
        --offset: 2;
        z-index: 2;
    }

    .child:nth-child(4) {
        --offset: 3;
        z-index: 1;
    }

    .child:nth-child(5) {
        --offset: 4;
        z-index: 0;
    }

    .child:nth-child(6) {
        --offset: 5;
        z-index: -1;
    }

    .child:nth-child(7) {
        --offset: 6;
        z-index: -2;
    }

    .child:nth-child(8) {
        --offset: 7;
        z-index: -3;
    }

    .child:nth-child(9) {
        --offset: 8;
        z-index: -4;
    }

    .child:nth-child(10) {
        --offset: 9;
        z-index: -5;
    }

    @media (max-width: 768px) {
        .container {
            grid-gap: 16px;
            padding: 0 24px;
            max-width: 80%
        }

        .child p {
            font-size: 0.85rem;
            right: 0.5rem;
            bottom: 0.5rem;
        }
    }
</style>

{{- end }}{{/* end main */ -}}
```
{{</collapse>}}

主要是为其增加了 `categories` 内容和相关 CSS 样式。

{{< notice notice-info >}}
本博客的 CSS 中的颜色代码部分无法直接使用，请根据自身情况修改
{{< /notice >}}

在 `content/categories/` 内新建文件 `类别名.md`

```
content/categories/
└── test
    ├── _index.en.md
    ├── _index.ja.md
    └── _index.zh.md
```

内容如下：
```markdown
+++
title = "test"
description = "test"
image = "图片URL" 
alt = "test Cover" # 封面图片的替代文本
caption = "A brief description of the image" # 封面图片的标题或描述
+++

This is the test category page.
```

这样就新增了一个类别。效果如图：

[![「标签」页面.png](https://s21.ax1x.com/2025/06/24/pVeVaPx.png)](https://imgse.com/i/pVeVaPx)

## 功能增强

### 评论系统
