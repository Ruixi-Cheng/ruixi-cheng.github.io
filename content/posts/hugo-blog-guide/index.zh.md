+++
title = 'Hugo 博客搭建指南'
slug = 'hugo-blog-guide'
date = 2025-06-22T18:20:00+08:00
lastmod = 2025-06-27T13:30:00+08:00
draft = false
categories = ["Blog"]
tags = ["hugo","blog","tinker"]
+++

## 写在前面

这是这个新博客的第一篇文章。

从 22 年至今，我已搭建过三次博客。每一次都是技术探索与折腾的过程：从 Typecho 到 Halo，从 LNMP 架构到 Docker 部署……经历了无数次配置调试与反复取舍。

一路走来，我的心态也在悄然发生变化：曾经执着于博客的技术架构与视觉效果，而现在，我更加重视写作本身的意义。

在一次一次的键盘敲击中，将思绪梳理成文字，将技术沉淀为知识。用合适的方式表达自我，输出有价值的内容。这才是 Blog 的意义所在。

这一次，我再次找回最初那份搭建博客的初心与动力，将这个新的博客搭建了起来。

希望这个博客能长久地运营下去吧。: )

---

花了半个月时间，参考了许多网上的优秀实践，并结合自己的需求进行了功能整合与定制，搭建了这么一个令我较为满意的博客。

在记忆尚新的当下，于此记录搭建博客的细节。这既是为自己留下的总结与备忘，也希望为后来者提供一些参考，少走一些弯路。

开发过程均已提交 Github：[**项目源码**](https://github.com/Ruixi-Cheng/ruixi-cheng.github.io)

## 为什么是 Hugo?

<img src="https://gohugo.io/images/hugo-logo-wide.svg" alt="hugo" />

私以为，对于个人开发者而言，动态博客的一些复杂功能——如用户系统、权限管理，性能监控等——显得较为多余。毕竟，写作的核心在于内容本身。

[Hugo](https://github.com/gohugoio/hugo) 是一个 Go 语言编写、开源的静态网站生成器。它构建速度极快，语法简洁，功能丰富，社区活跃，具备高度的灵活性和可扩展性。这些特性使得它成为搭建个人博客的理想选择。

## Hugo 入门

### 安装

从 [Github Releases](https://github.com/gohugoio/hugo/releases/) 内下载适用于你系统的软件包、二进制可执行文件，或直接直接从源码编译。(建议使用 Hugo Extended 以获得额外功能的支持。)

安装完成后，在终端内运行以下命令以验证是否安装成功 ：

```bash
hugo version
# 输出示例：hugo v0.147.8-10da2bd765d227761641f94d713d094e88b920ae+extended linux/amd64 BuildDate=2025-06-07T12:59:52Z VendorInfo=gohugoio
```

### 主题选择

Hugo 官网的 [主题页面](https://themes.gohugo.io/) 提供了许多不同用途的主题以供选择。

笔者选择了 [PaperMod](https://github.com/adityatelange/hugo-PaperMod) 主题，因其简洁现代的设计风格和良好的功能支持。

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

<img src="https://s21.ax1x.com/2025/06/24/pVeKOY9.png" alt="新站点.png" />

### 站点结构

{{<collapse openByDefault=true summary="新建站点的结构：">}}
```bash
test.io/
├── archetypes
│   └── default.md  # 文章模板
├── assets          # css、js等资源
├── content         # 博客内容
├── data            # 一些数据
├── hugo.toml       # 网站配置文件
├── i18n            # 多语言相关文件
├── layouts         # 网站布局相关
├── public          # 渲染后的 HTML 代码目录
├── static          # 网站的字体和 favicons
└── themes          # 主题文件夹
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
├── config          # config 可以拆成多文件
│   └── _default
│       ├── hugo.toml
│       ├── languages.toml
│       ├── menu.en.toml
│       ├── menu.ja.toml
│       └── menu.zh.toml
├── content
│   ├── about       # 三种语言的页面文档，下同
│   │   ├── _index.en.md
│   │   ├── _index.ja.md
│   │   └── _index.zh.md
│   ├── archives    # 归档
│   ├── categories  # 分类
│   │   ├── tech
│   │   └── test
│   ├── friends     # 友链
│   ├── posts       # 文章
│   │   ├── hugo-papermod-blog-guide
│   │   └── Test-Post
│   └── search      # 搜索
├── data            # 数据
│   ├── friends.toml
│   └── notice.toml
├── i18n            # 多语言翻译
│   ├── en.yaml
│   ├── ja.yaml
│   └── zh.yaml
├── layouts         # 部分自定义网络结构
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
├── static          # 字体和网站图标
│   ├── favicon-16x16.png
│   ├── favicon-32x32.png
│   ├── favicon.png
│   ├── favicon.svg
│   └── fonts
└── themes
```
{{</collapse>}}

### Hugo 的基础命令

使用 `hugo new` 根据**文章模板**在 `content` 文件夹中新增内容：

```bash
hugo new posts/Test-Post.md
```
结构如下：
{{<collapse summary="**content**">}}
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

构建完成后，Hugo 会将所有内容输出到 `public` 目录下，结构如下：

{{<collapse summary="**public**">}}
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

然后你可以访问 http://localhost:1313 预览网站。

一些我常用的参数：

|         参数          |     含义     |
| :-------------------: | :----------: |
| --cleanDestinationDir | 清空输出目录 |
|          -D           | 构建草稿内容 |
|    --bind 0.0.0.0     | 允许外部访问 |
|        -p 1313        |  指定端口号  |
|       --baseURL       | 设置基础 URL |

## Hugo 配置

[Hugo 配置文件](https://gohugo.io/configuration/) 一般为站点根目录下的单一配置文件 `hugo.toml` 或 `hugo.yaml` 、 `hugo.json` 文件。

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

详见 <https://gohugo.io/configuration/introduction/#configuration-directory>

笔者配置如下，供大家参考：

{{<collapse summary="hugo.toml">}}
```toml
baseURL = 'https://ruixi.top/'  # 网站根地址
title = "Ruixi's Blog"          # 网站标题
theme = 'PaperMod'              # 使用的主题名称
languageCode = 'en-US'

defaultTheme = "dark"           # 默认使用暗色背景主题
buildDrafts = false             # 是否构建草稿
buildFuture = false             # 是否构建未来发布的内容
buildExpired = false            # 是否构建已过期的内容
defaultContentLanguage = "en"   # 顶部首先展示的语言界面
enableRobotsTXT = true          # 是否生成 robots.txt 文件
enableInlineShortcodes = true   # 是否启用内联 shortcode
enableEmoji = true              # 是否启用 Emoji 表情支持
defaultContentLanguageInSubdir = true # 是否要在地址栏加上默认的语言代码

[minify]
  disableXML = true             # 防止 XML 文件被压缩出错
  minifyOutput = true           # 启用压缩优化输出体积

[permalinks]
  post = "/:slug/"              # 自定义文章永久链接格式

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
      typographer = false       # 禁用goldmark符号替换

[services]
  [services.googleAnalytics] 
    id = 'G-H5HDF4EPT6'         # Google Analytics ID

[params]
  author = "Ruixi"              # 站点作者信息
  defaultTheme = "dark"         # 网站标题
  math = true                   # 数学公式支持
  comments = true               # 评论功能
  showToc = true                # 显示文章目录（TOC）
  tocOpen = true                # TOC 是否默认展开
  showPostNavLinks = true       # 显示文章导航链接
  showBreadCrumbs = true        # 显示面包屑导航
  showRssButtonInSectionTermList = true  # RSS 相关按钮显示
  showAllPagesInArchive = true  # 在归档页面显示所有页面
  showCodeCopyButtons = true    # 显示代码块复制按钮
  showWordCount = true          # 显示文章字数统计
  showLastMod = true            # 显示最后修改时间
  disableScrollToTop = false    # 启用返回顶部按钮
  displayFullLangName = true
  fancyBox = true               # 启用 Fancybox 灯箱效果
  dateFormat = "2006/01/02"     # 日期格式化
  hideSummary = false

  [params.assets]
    favicon = "favicon.png"

  [params.fuseOpts]
    isCaseSensitive = false     # 是否大小写敏感
    shouldSort = true           # 是否排序
    location = 0
    distance = 1000
    threshold = 0.4
    minMatchCharLength = 2      # limit = 20 # 限制返回的搜索结果数量 
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
slug = 'slug'                       # URL 标识符
date = 2025-06-22T18:20:00+08:00
lastmod = 2025-06-22T18:20:00+08:00 # 最后编辑时间
draft = true                        # 是否为草稿
categories = ["categories"]         # 类别
tags = ["tags"]                     # 标签
+++
```

在用 `hugo new` 新建文章的时候，这些字段应会被自动添加在文件开头。如果自己在 `post` 目录下新建文章，请手动添加这些数据。

## 创建常用页面

在使用 Hugo 构建个人博客时，除了基本的文章发布功能外，我们通常还会创建一些额外的页面，如「归档」、「关于」和「友链」等。

### 「归档」页面

在 `content` 目录中创建 `archive.md` 文件，或是 `archive` 文件夹结构如下：

```bash
content/archives/
├── _index.en.md
├── _index.ja.md
└── _index.zh.md
```

archive.md：

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
pageRef = "/archives/"  # 页面链接地址
weight = 4              # 菜单排序权重值
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
Markdown 内容如下：

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
    shouldSort = true       # 是否排序
    location = 0            # 匹配起始位置
    distance = 1000         # 字符距离阈值
    threshold = 0.4         # 匹配相似度阈值
    minMatchCharLength = 2  # limit = 20 # 限制返回的搜索结果数量 
    keys = ["title", "permalink", "summary", "content"] # 搜索字段
    includeMatches = true   # 返回匹配项详情
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

参考了 [道与的不拆笔记 - PaperMod 主题自定义类别页面 （纸张合并本拟物风格）](https://daoyuchan.com/log/build_categories_page/)。

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

<img src="https://s21.ax1x.com/2025/06/24/pVeMSOK.png" alt="「分类」页面.png" />

## 博客样式优化

### 修改字体

我们可以为博客应用自定义字体，以提升阅读体验和整体视觉风格。。

笔者的博客用了以下三种字体：
- `NotoSansSC` ：作为正文字体
- `FiraCode Nerd Font` ：作为代码字体
- `霞鹜文楷`（LXGWWenKai）：作为点缀

为了减少网页加载时间并适配现代浏览器，我们可以将本地字体文件转换为更高效的 `woff2` 格式。

用 Google 开源的 [`woff2`](https://github.com/google/woff2) 工具进行压缩：

```bash
./woff2_compress FiraCodeNerdFont-Regular.ttf
```

将压缩后的字体文件放入 Hugo 的静态资源目录 `static/fonts` 文件夹:

```bash
static/fonts/
├── FiraCodeNerdFont-Regular.woff2
├── LXGWWenKai-Regular.woff2
└── NotoSansSC-Regular.woff2
```
为了让浏览器提前加载关键字体资源，提高首次渲染性能，可以在 `layouts/partials/extend_head.html` 文件中添加如下 `<link>` 标签：

```html
<link rel="preload" href="{{ "fonts/FiraCodeNerdFont-Regular.woff2" | relURL }}" as="font" type="font/woff2" crossorigin>
<link rel="preload" href="{{ "fonts/NotoSansSC-Regular.woff2" | relURL }}" as="font" type="font/woff2" crossorigin>
<link rel="preload" href="{{ "fonts/LXGWWenKai-Regular.woff2" | relURL }}" as="font" type="font/woff2" crossorigin>
```

再添加 `assets/css/extended/fonts.css` 文件

```css
/* 自定义字体 */
@font-face {
    font-family: 'NotoSansSC';
    src: url('/fonts/NotoSansSC-Regular.woff2') format('woff2');
    font-display: swap;
}

@font-face {
    font-family: 'FiraCodeNerdFont';
    src: url('/fonts/FiraCodeNerdFont-Regular.woff2') format('woff2');
    font-display: swap;
}

@font-face {
    font-family: 'LXGWWenKai';
    src: url('/fonts/LXGWWenKai-Regular.woff2') format('woff2');
    font-display: swap;
}

/* 应用于整个网站 */
body {
    font-size: medium !important;
    font-family: 'NotoSansSC', sans-serif !important;
}
/* 应用于代码块 */
code, pre {
    font-family: 'FiraCodeNerdFont', monospace !important;
}
```

如果希望对某些特定元素使用不同的字体，可以直接在对应的 CSS 类中调用：

{{<collapse summary="示例：对分类的 .child 组件应用霞鹜文楷">}}
```css
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
```
{{</collapse>}}

### 修改博客整体配色

将 `themes/PaperMod/assets/css/core/theme-vars.css` 文件复制到 `assets/css/core/theme-vars.css` 并自行更改。

笔者根据 [Nord](https://www.nordtheme.com/) 配色，对博客颜色主题进行了深度定制：

{{<collapse summary="Nord 配色">}}
```css
:root {
    --gap: 24px;
    --content-gap: 20px;
    --main-width: 720px;
    --nav-width: 1280px;
    --article-width: 640px;
    --toc-width: 320px;
    --header-height: 60px;
    --footer-height: 60px;
    --radius: 8px;

    --nord0: #2e3440;
    --nord1: #3b4252;
    --nord2: #434c5e;
    --nord3: #4c566a;
    --nord4: #d8dee9;
    --nord5: #e5e9f0;
    --nord6: #eceff4;
    --nordw: #ffffff;
    --nord7: #8fbcbb;
    --nord8: #88c0d0;
    --nord9: #81a1c1;
    --nord10: #5e81ac;
    --nord11: #bf616a;
    --nord12: #d08770;
    --nord13: #ebcb8b;
    --nord14: #a3be8c;
    --nord15: #b48ead;

    --nordrgb0: 46, 52, 64;
    --nordrgb1: 59, 66, 82;
    --nordrgb2: 67, 76, 94;
    --nordrgb3: 76, 86, 106;
    --nordrgb4: 216, 222, 233;
    --nordrgb5: 229, 233, 240;
    --nordrgb6: 236, 239, 244;
    --nordrgbw: 255, 255, 255;
    --nordrgb7: 143, 188, 187;
    --nordrgb8: 136, 192, 208;
    --nordrgb9: 129, 161, 193;
    --nordrgb10: 94, 129, 172;
    --nordrgb11: 191, 97, 106;
    --nordrgb12: 208, 135, 112;
    --nordrgb13: 235, 203, 139;
    --nordrgb14: 163, 190, 140;
    --nordrgb15: 180, 142, 173;

    /* Light mode colors using Nord */
    --theme: var(--nordw);
    --entry: var(--nord6);
    --primary: var(--nord1);
    --secondary: var(--nord3);
    --tertiary: var(--nord6);
    --content: var(--nord2);
    --code-block-bg: var(--nord6);
    --code-bg: var(--nord6);
    --border: var(--nord4);


}

.dark {
    --theme: var(--nord0);
    --entry: var(--nord1);
    --primary: var(--nord6);
    --secondary: var(--nord4);
    --tertiary: var(--nord1);
    --content: var(--nord5);
    --code-block-bg: var(--nord1);
    --code-bg: var(--nord1);
    --border: var(--nord3);
}
```
{{</collapse>}}

你可以根据自己的喜好修改配色文件。

### 修改代码高亮样式

本博客使用了 `highlight.js` 插件来实现代码高亮，而不是 Hugo 自带的 `Chroma` 渲染器。至于为何选择 `highlight.js`，笔者一时也记不清具体原因了 ToT。

首先，在 Hugo 配置文件中将 `Chroma` 禁用，避免冲突：

```toml
[markup]
  [markup.highlight]
    codeFences = false
```

然后在 `layouts/partials/extend_footer.html` 文件内添加 `highlight.js` 插件。

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.11.1/highlight.min.js"></script>
<script>
   document.addEventListener('DOMContentLoaded', (event) => {
      document.querySelectorAll('pre code').forEach((block) => {
         hljs.highlightElement(block);
      });
   });
</script>
```

最后将你希望使用的代码高亮样式文件（`.css`）放在 `assets/css/extended` 文件夹下即可。可以在 <https://cdnjs.com/libraries/highlight.js> 下载你喜欢的高亮样式主题。

以下是一个简单的 CSS 示例，可以为明暗模式分别设置不同的代码高亮样式：

```css
.hljs {
    color: #383a42;
    background: #fafafa
}

.hljs-comment,
.hljs-quote {
    color: #a0a1a7;
    font-style: italic
}

...

body.dark {
    .hljs {
        background: #2e3440
    }

    .hljs,
    .hljs-subst {
        color: #d8dee9
    }

    ...

}
```
本博客采用的代码高亮样式为：
- 明亮模式：`Atom One Light` 
- 黑暗模式：`Nord`

{{<collapse summary="本博客代码高亮样式：assets/css/extended/hljs.css">}}
```css
pre code.hljs {
    display: block;
    overflow-x: auto;
    padding: 1em !important
}

code.hljs {
    padding: 3px 5px
}

/*

Atom One Light by Daniel Gamage
Original One Light Syntax theme from https://github.com/atom/one-light-syntax

base:    #fafafa
mono-1:  #383a42
mono-2:  #686b77
mono-3:  #a0a1a7
hue-1:   #0184bb
hue-2:   #4078f2
hue-3:   #a626a4
hue-4:   #50a14f
hue-5:   #e45649
hue-5-2: #c91243
hue-6:   #986801
hue-6-2: #c18401

*/
.hljs {
    color: #383a42;
    background: #fafafa
}

.hljs-comment,
.hljs-quote {
    color: #a0a1a7;
    font-style: italic
}

.hljs-doctag,
.hljs-keyword,
.hljs-formula {
    color: #a626a4
}

.hljs-section,
.hljs-name,
.hljs-selector-tag,
.hljs-deletion,
.hljs-subst {
    color: #e45649
}

.hljs-literal {
    color: #0184bb
}

.hljs-string,
.hljs-regexp,
.hljs-addition,
.hljs-attribute,
.hljs-meta .hljs-string {
    color: #50a14f
}

.hljs-attr,
.hljs-variable,
.hljs-template-variable,
.hljs-type,
.hljs-selector-class,
.hljs-selector-attr,
.hljs-selector-pseudo,
.hljs-number {
    color: #986801
}

.hljs-symbol,
.hljs-bullet,
.hljs-link,
.hljs-meta,
.hljs-selector-id,
.hljs-title {
    color: #4078f2
}

.hljs-built_in,
.hljs-title.class_,
.hljs-class .hljs-title {
    color: #c18401
}

.hljs-emphasis {
    font-style: italic
}

.hljs-strong {
    font-weight: bold
}

.hljs-link {
    text-decoration: underline
}

body.dark {
    .hljs {
        background: #2e3440
    }

    .hljs,
    .hljs-subst {
        color: #d8dee9
    }

    .hljs-selector-tag {
        color: #81a1c1
    }

    .hljs-selector-id {
        color: #8fbcbb;
        font-weight: 700
    }

    .hljs-selector-attr,
    .hljs-selector-class {
        color: #8fbcbb
    }

    .hljs-property,
    .hljs-selector-pseudo {
        color: #88c0d0
    }

    .hljs-addition {
        background-color: rgba(163, 190, 140, .5)
    }

    .hljs-deletion {
        background-color: rgba(191, 97, 106, .5)
    }

    .hljs-built_in,
    .hljs-class,
    .hljs-type {
        color: #8fbcbb
    }

    .hljs-function,
    .hljs-function>.hljs-title,
    .hljs-title.hljs-function {
        color: #88c0d0
    }

    .hljs-keyword,
    .hljs-literal,
    .hljs-symbol {
        color: #81a1c1
    }

    .hljs-number {
        color: #b48ead
    }

    .hljs-regexp {
        color: #ebcb8b
    }

    .hljs-string {
        color: #a3be8c
    }

    .hljs-title {
        color: #8fbcbb
    }

    .hljs-params {
        color: #d8dee9
    }

    .hljs-bullet {
        color: #81a1c1
    }

    .hljs-code {
        color: #8fbcbb
    }

    .hljs-emphasis {
        font-style: italic
    }

    .hljs-formula {
        color: #8fbcbb
    }

    .hljs-strong {
        font-weight: 700
    }

    .hljs-link:hover {
        text-decoration: underline
    }

    .hljs-comment,
    .hljs-quote {
        color: #4c566a
    }

    .hljs-doctag {
        color: #8fbcbb
    }

    .hljs-meta,
    .hljs-meta .hljs-keyword {
        color: #5e81ac
    }

    .hljs-meta .hljs-string {
        color: #a3be8c
    }

    .hljs-attr {
        color: #8fbcbb
    }

    .hljs-attribute {
        color: #d8dee9
    }

    .hljs-name {
        color: #81a1c1
    }

    .hljs-section {
        color: #88c0d0
    }

    .hljs-tag {
        color: #81a1c1
    }

    .hljs-template-variable,
    .hljs-variable {
        color: #d8dee9
    }

    .hljs-template-tag {
        color: #5e81ac
    }

    .language-abnf .hljs-attribute {
        color: #88c0d0
    }

    .language-abnf .hljs-symbol {
        color: #ebcb8b
    }

    .language-apache .hljs-attribute {
        color: #88c0d0
    }

    .language-apache .hljs-section {
        color: #81a1c1
    }

    .language-arduino .hljs-built_in {
        color: #88c0d0
    }

    .language-aspectj .hljs-meta {
        color: #d08770
    }

    .language-aspectj>.hljs-title {
        color: #88c0d0
    }

    .language-bnf .hljs-attribute {
        color: #8fbcbb
    }

    .language-clojure .hljs-name {
        color: #88c0d0
    }

    .language-clojure .hljs-symbol {
        color: #ebcb8b
    }

    .language-coq .hljs-built_in {
        color: #88c0d0
    }

    .language-cpp .hljs-meta .hljs-string {
        color: #8fbcbb
    }

    .language-css .hljs-built_in {
        color: #88c0d0
    }

    .language-css .hljs-keyword {
        color: #d08770
    }

    .language-diff .hljs-meta,
    .language-ebnf .hljs-attribute {
        color: #8fbcbb
    }

    .language-glsl .hljs-built_in {
        color: #88c0d0
    }

    .language-groovy .hljs-meta:not(:first-child),
    .language-haxe .hljs-meta,
    .language-java .hljs-meta {
        color: #d08770
    }

    .language-ldif .hljs-attribute {
        color: #8fbcbb
    }

    .language-lisp .hljs-name,
    .language-lua .hljs-built_in,
    .language-moonscript .hljs-built_in,
    .language-nginx .hljs-attribute {
        color: #88c0d0
    }

    .language-nginx .hljs-section {
        color: #5e81ac
    }

    .language-pf .hljs-built_in,
    .language-processing .hljs-built_in {
        color: #88c0d0
    }

    .language-scss .hljs-keyword,
    .language-stylus .hljs-keyword {
        color: #81a1c1
    }

    .language-swift .hljs-meta {
        color: #d08770
    }

    .language-vim .hljs-built_in {
        color: #88c0d0;
        font-style: italic
    }

    .language-yaml .hljs-meta {
        color: #d08770
    }
}
```
{{</collapse>}}

### 修改表格样式

参考了 <https://yunpengtai.top/posts/hugo-journey/#%e8%a1%a8%e6%a0%bc>。

PaperMod 主题自带的表格样式不是很好看，笔者对其进行了修改。

效果如下：

<img src="https://s21.ax1x.com/2025/06/26/pVmlX8J.png" alt="表格样式-修改前.png" style="zoom: 50%;" />

*表格样式-修改前*

![表格样式-修改后.png](https://s21.ax1x.com/2025/06/26/pVmlOC4.png)

*表格样式-修改后*

添加 `assets/css/extended/table.css` 文件即可：

{{<collapse summary="table.css">}}
```css
table,
.dark table {
  border-collapse: collapse;
  display: table;
  margin-bottom: 1rem;
  width: 100%;
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;

  thead th {
    text-align: center;
    vertical-align: middle;
    border-bottom: 2px solid var(--code-bg);
  }

  td,
  th {
    text-align: center;
    vertical-align: middle;
    border-top: 1px solid var(--code-bg);
    border-bottom: 1px solid var(--code-bg);
  }

  tbody tr:hover {
    background-color: var(--code-bg);
  }

  tbody tr:nth-of-type(2n + 1) {
    background-color: var(--code-bg);
  }

  tr:last-of-type {
    border-bottom: 2px solid var(--code-bg);
  }
}
```
{{</collapse>}}

### 侧边悬浮目录

参考了 <https://yunpengtai.top/posts/hugo-journey/#%e4%be%a7%e8%be%b9%e6%82%ac%e6%b5%ae%e7%9b%ae%e5%bd%95>。

## 功能增强

### giscus 评论系统集成

#### 基础集成

参考了 [意琦行的个人博客 - Hugo 博客引入 Giscus 评论系统](https://www.lixueduan.com/posts/blog/02-add-giscus-comment/)。

本博客的评论系统为 [giscus](https://giscus.app/)，允许访客通过 GitHub 账号发表评论和互动。

>利用 GitHub Discussions 实现的评论系统，让访客借助 GitHub 在你的网站上留下评论和反应吧！本项目深受 utterances 的启发。
>- 开源。🌏
>- 无跟踪，无广告，永久免费。📡 🚫
>- 无需数据库。所有数据均储存在 GitHub Discussions 中。
>- 支持自定义主题！🌗
>- 支持多种语言。🌐
>- 高可配置性。🔧
>- 自动从 GitHub 拉取新评论与编辑。🔃
>- 可自建服务！🤳

*摘自 giscus 官网。*

在其官网上填写你的仓库信息和你想要的配置，你会得到如下的 HTML 代码:

```html
<script src="https://giscus.app/client.js"
        data-repo="[ENTER REPO HERE]"
        data-repo-id="[ENTER REPO ID HERE]"
        data-category="[ENTER CATEGORY NAME HERE]"
        data-category-id="[ENTER CATEGORY ID HERE]"
        data-mapping="specific"
        data-term='posts/{{ .Params.slug }}'
        data-strict="1"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="top"
        data-theme="transparent_dark"
        data-lang="zh-CN"
        data-loading="lazy"
        crossorigin="anonymous"
        async>
</script>
```

将上述代码保存至 `layouts/partials/comments.html` 文件，并在 Hugo 配置文件中启用评论功能：

```toml
[params]
comments = true
```

至此，即可完成 giscus 的基础集成。

#### 实现多语言支持

本博客实现了评论系统的多语言支持。

笔者对 `comments.html` 进行了修改，使其根据当前页面的语言自动切换 giscus 的界面语言。

{{<collapse summary="修改后的 comments.html">}}
```html
{{ $giscusLang := "en" }} {{ if eq site.Language.Lang "zh" }} {{ $giscusLang =
"zh-CN" }} {{ else if eq site.Language.Lang "zh-tw" }} {{ $giscusLang = "zh-TW"
}} {{ else if eq site.Language.Lang "zh-hk" }} {{ $giscusLang = "zh-HK" }} {{
else if eq site.Language.Lang "ar" }} {{ $giscusLang = "ar" }} {{ else if eq
site.Language.Lang "be" }} {{ $giscusLang = "be" }} {{ else if eq
site.Language.Lang "bg" }} {{ $giscusLang = "bg" }} {{ else if eq
site.Language.Lang "ca" }} {{ $giscusLang = "ca" }} {{ else if eq
site.Language.Lang "cs" }} {{ $giscusLang = "cs" }} {{ else if eq
site.Language.Lang "da" }} {{ $giscusLang = "da" }} {{ else if eq
site.Language.Lang "de" }} {{ $giscusLang = "de" }} {{ else if eq
site.Language.Lang "el" }} {{ $giscusLang = "gr" }} {{ else if eq
site.Language.Lang "eo" }} {{ $giscusLang = "eo" }} {{ else if eq
site.Language.Lang "es" }} {{ $giscusLang = "es" }} {{ else if eq
site.Language.Lang "eu" }} {{ $giscusLang = "eu" }} {{ else if eq
site.Language.Lang "fa" }} {{ $giscusLang = "fa" }} {{ else if eq
site.Language.Lang "fr" }} {{ $giscusLang = "fr" }} {{ else if eq
site.Language.Lang "he" }} {{ $giscusLang = "he" }} {{ else if eq
site.Language.Lang "hu" }} {{ $giscusLang = "hu" }} {{ else if eq
site.Language.Lang "id" }} {{ $giscusLang = "id" }} {{ else if eq
site.Language.Lang "it" }} {{ $giscusLang = "it" }} {{ else if eq
site.Language.Lang "ja" }} {{ $giscusLang = "ja" }} {{ else if eq
site.Language.Lang "km" }} {{ $giscusLang = "kh" }} {{ else if eq
site.Language.Lang "ko" }} {{ $giscusLang = "ko" }} {{ else if eq
site.Language.Lang "nl" }} {{ $giscusLang = "nl" }} {{ else if eq
site.Language.Lang "pl" }} {{ $giscusLang = "pl" }} {{ else if eq
site.Language.Lang "pt" }} {{ $giscusLang = "pt" }} {{ else if eq
site.Language.Lang "ro" }} {{ $giscusLang = "ro" }} {{ else if eq
site.Language.Lang "ru" }} {{ $giscusLang = "ru" }} {{ else if eq
site.Language.Lang "th" }} {{ $giscusLang = "th" }} {{ else if eq
site.Language.Lang "tr" }} {{ $giscusLang = "tr" }} {{ else if eq
site.Language.Lang "uk" }} {{ $giscusLang = "uk" }} {{ else if eq
site.Language.Lang "uz" }} {{ $giscusLang = "uz" }} {{ else if eq
site.Language.Lang "vi" }} {{ $giscusLang = "vi" }} {{ end }}

<script src="https://giscus.app/client.js"
        data-repo="[在此输入仓库]"
        data-repo-id="[在此输入仓库 ID]"
        data-category="[在此输入分类名]"
        data-category-id="[在此输入分类 ID]"
        data-mapping="specific"
        data-term='posts/{{ .Params.slug }}'
        data-strict="1"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="top"
        data-theme="transparent_dark"
        data-lang="{{ $giscusLang }}"
        data-loading="lazy"
        crossorigin="anonymous"
        async>
</script>
```
{{</collapse>}}

效果示例：

<img src="https://s21.ax1x.com/2025/06/25/pVeaUnH.png" alt="en评论区.png" />
*英文界面*
<img src="https://s21.ax1x.com/2025/06/25/pVeaaBd.png" alt="ja评论区.png" />
*日语界面*

通过以上配置，即可在 Hugo 博客中实现评论系统的多语言适配。

#### 多语言共享评论区

若希望多个语言版本的文章共享同一评论区，需要确保所有语言版本使用相同的  `slug`。

为此，在 Hugo 配置文件中设置链接规则：

```toml
[permalinks]
post = "/:slug/"
```

这样，每篇文章的 URL 格式变为 `https://[你的域名]/[语言代码（如果配置了多语言）]/posts/[文章的 slug]`。

例如，本篇博文的元数据如下：

```toml
+++
title = 'Hugo 博客搭建指南'
slug = 'hugo-blog-guide'
date = 2025-06-22T18:20:00+08:00
lastmod = 2025-06-25T15:50:00+08:00
draft = false
categories = ["Blog"]
tags = ["hugo","blog","tinker"]
+++
```
则其 URL 为： `http://ruixi.top/zh/posts/hugo-blog-guide/`。

在 `comments.html` 中设置了如下参数：

```
data-mapping="specific"
data-term='posts/{{ .Params.slug }}'
```
这些参数会使 giscus 以文章的 `posts/[:slug]` 为关键字去匹配 GitHub Discussions 中的评论话题，从而实现跨语言共享评论区。

### 折叠块功能

参考 <https://yunpengtai.top/posts/hugo-journey/>。

这是一个非常实用的小功能，能在博客内折叠隐藏较长或非核心内容（长代码块、文字等），提升页面整洁度与阅读体验。

效果展示：

{{<collapse summary="这是折叠的代码">}}
```c
#include <stdio.h>
int main()
{
   printf("Hello, World!");
   return 0;
}
```
{{</collapse>}}

为此,需新增 `layouts/shortcodes/collapse.html` 文件：

```html
{{ if .Get "summary" }}
{{ else }}
{{ warnf "missing value for param 'summary': %s" .Position }}
{{ end }}
<p><details {{ if (eq (.Get "openByDefault") true) }} open=true {{ end }}>
  <summary markdown="span">{{ .Get "summary" | markdownify }}</summary>
  {{ .Inner | markdownify }}
</details></p>
```

使用也很方便，参考下图：

<img src="https://s21.ax1x.com/2025/06/26/pVejYuV.png" alt="折叠块代码.png" />

支持两个参数：
- `summary`：用于设置折叠面板的标题（必填）
- `openByDefault`：布尔值，控制面板是否默认展开（可选）
  
### Fancybox 图片灯箱效果

参考了 [人生筆記簿 - hugo-使用-fancybox-实现图片灯箱-放大功能](https://blog.muxilong.com/pocket/hugo/hugo-%E4%BD%BF%E7%94%A8-fancybox-%E5%AE%9E%E7%8E%B0%E5%9B%BE%E7%89%87%E7%81%AF%E7%AE%B1-%E6%94%BE%E5%A4%A7%E5%8A%9F%E8%83%BD/)。

添加 `layouts/_default/_markup/render-image.html` 文件：

```html
{{if .Page.Site.Params.fancybox }}
<div class="post-img-view">
    <a data-fancybox="gallery" href="{{ .Destination | safeURL }}" data-caption="{{ .Text }}">
        <img src="{{ .Destination | safeURL }}" alt="{{ .Text }}" {{ with .Title}} title="{{ . }}" {{ end }} />
    </a>
</div>
{{ end }}
```

修改 Hugo 配置文件，以启用灯箱效果：

```toml
[param]
fancyBox = true
```

在 `layouts/partials/extend_footer.html` 中增加：

```html
{{if .Page.Site.Params.fancybox }}
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/fancybox/3.5.7/jquery.fancybox.css" />
<script src="https://cdnjs.cloudflare.com/ajax/libs/fancybox/3.5.7/jquery.fancybox.min.js"></script>
{{ end }}
```
### 盘古之白

受到 [🏄‍♂️ 不入流的人生解决方案 - 不入流的文体｜关于「盘古之白」和「直角引号」](https://eddy.lu/posts/pangu/#%e7%9b%98%e5%8f%a4%e4%b9%8b%e7%99%bd%e6%98%af%e4%bb%80%e4%b9%88) 的启发。

在中文与英文、数字或符号混排时，应适当加入一个空格，这能让文字之间的界限更清晰，视觉上也更舒适。

> 漢學家稱這個空白字元為「盤古之白」，因為它劈開了全形字和半形字之間的混沌。
> 
> 另有研究顯示，打字的時候不喜歡在中文和英文之間加空格的人，感情路都走得很辛苦，有七成的比例會在 34 歲的時候跟自己不愛的人結婚，而其餘三成的人最後只能把遺產留給自己的貓。畢竟愛情跟書寫都需要適時地留白。
> 
> 與大家共勉之。

本博客在写作过程中尽量遵循「盘古之白」的排版原则。不过为了以防万一，也引入了一个 JS 插件自动处理这个问题。

在 `layouts/partials/extend_footer.html` 内新增以下代码来引入 [pangu.js](https://github.com/vinta/pangu.js)。

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/pangu/4.0.7/pangu.js"></script>
<script>
   pangu.spacingPage();
</script>
```

### 更优雅的引用

参考了 <https://yunpengtai.top/posts/hugo-journey/#blockquote>，并结合自己的需求进行了增强。

在博客中引用名人名言时，使用自定义的 `quote` 短代码让内容更美观。

e.g.: 莎士比亚引用

```markdown
{{</* quote author="William Shakespeare" */>}}
To be, or not to be, that is the question:
Whether 'tis nobler in the mind to suffer
The slings and arrows of outrageous fortune,
Or to take Arms against a Sea of troubles,
And by opposing end them: to die, to sleep
{{</* /quote */>}}
```

渲染效果如下：

{{< quote author="William Shakespeare" >}}
To be, or not to be, that is the question:
Whether 'tis nobler in the mind to suffer
The slings and arrows of outrageous fortune,
Or to take Arms against a Sea of troubles,
And by opposing end them: to die, to sleep
{{< /quote >}}

创建短代码模板文件 `layouts/shortcodes/quote.html`，内容如下：

```html
<blockquote class="quote">
    {{- $content := .Inner -}}
    {{- if not (strings.HasPrefix $content "<p>") -}}
        <p style="white-space: pre-line">{{ .Inner }}</p>
    {{- else -}}
        {{ $content }}
    {{- end -}}

    {{- with .Get "author" -}}
        <footer class="blockquote-footer text-right">
            — {{ . }}
        </footer>
    {{- end -}}
</blockquote>
```

添加样式文件 `assets/css/extended/quote.css`，内容如下：

```css
/* 公共样式提取 */
blockquote.quote{
  position: relative;
  margin: 1em auto;
  padding-left: 2.5em !important;
  border: none;
  font-style: italic; /* 统一引用文字风格 */
  line-height: 1.6;
  background: var(--theme) !important;
  color: var(--secondary);
}

/* 引号统一样式 */
blockquote.quote::before{
  content: "\"";
  position: absolute;
  left: 0;
  top: 0;
  font-size: 3em;
  font-weight: bold;
  font-style: italic;
  line-height: 1;
  color: var(--secondary); /* 可根据主题色设置颜色 */
}

blockquote.quote footer.blockquote-footer {
  margin-top: 1rem;
  font-size: 0.9em;
  color: var(--secondary);
  text-align: right;
}
```