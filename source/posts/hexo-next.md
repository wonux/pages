---
title: Hexo Next使用笔记
date: 2017-03-08 15:02:22
updated: 2017-03-10 14:53:02
comments: ture
categories:
- Git
tags: 
- hexo
- pages
---

## 关于Next

- NexT is built for easily use with elegant appearance. First things first, always keep things simple.
- NexT 主旨在于简洁优雅且易于使用，所以首先要尽量确保 NexT 的简洁易用性。

这是一个扩展主题，由[iissnan](https://github.com/iissnan)开发，`精于心，简于形`的理念。

本文根据官方文档整理，记录了自己搭建过程和常用配置，如需完整说明，请参考[Next官方文档](http://theme-next.iissnan.com).

## 安装Next

Hexo 安装主题的方式非常简单，只需要将主题文件拷贝至站点目录的 themes 目录下， 然后修改下配置文件即可。具体到 NexT 来说，安装步骤如下。 

### 下载主题

如果你熟悉 Git， 建议你使用 克隆最新版本 的方式，之后的更新可以通过 git pull 来快速更新， 而不用再次下载压缩包替换。 

```cmd
cd your-hexo-site
git clone https://github.com/iissnan/hexo-theme-next themes/next
```

### 启用主题

当 克隆/下载 完成后，打开`站点配置文件`， 找到 theme 字段，并将其值更改为 next。 

### 验证主题

首先启动 Hexo 本地站点，并开启调试模式（即加上 --debug），整个命令是 hexo s --debug。 在服务启动的过程，注意观察命令行输出是否有任何异常信息，如果你碰到问题，这些信息将帮助他人更好的定位错误。 当命令行输出中提示出：

```output
INFO  Hexo is running at http://0.0.0.0:4000/. Press Ctrl+C to stop.
```

此时即可使用浏览器访问 http://localhost:4000 ,检查站点是否正确运行。

## 主题设定

在 Hexo 中有两份主要的配置文件，其名称都是 `_config.yml`。 其中，一份位于站点根目录下，主要包含 Hexo 本身的配置；另一份位于主题目录下，这份配置由主题作者提供，主要用于配置主题相关的选项。
为了描述方便，在以下说明中，将前者称为 `站点配置文件`， 后者称为 `主题配置文件`。 

### 选择 Scheme

Scheme 是 NexT 提供的一种特性，借助于 Scheme，NexT 为你提供多种不同的外观。同时，几乎所有的配置都可以 在 Scheme 之间共用。目前 NexT 支持三种 Scheme，他们是：

- Muse - 默认 Scheme，这是 NexT 最初的版本，黑白主调，大量留白
- Mist - Muse 的紧凑版本，整洁有序的单栏外观
- Pisces - 双栏 Scheme，小家碧玉似的清新

Scheme 的切换通过更改 `主题配置文件`，搜索 scheme 关键字。 你会看到有三行 scheme 的配置，将你需用启用的 scheme 前面注释 # 即可。 

```config
#scheme: Muse
#scheme: Mist
scheme: Pisces
```

### 设置 语言

编辑 `站点配置文件`， 将 language 设置成你所需要的语言。建议明确设置你所需要的语言，例如选用简体中文，配置如下：

```config
language: zh-Hans
```

### 设置 菜单

菜单配置包括三个部分，第一是菜单项（名称和链接），第二是菜单项的显示文本，第三是菜单项对应的图标。 NexT 使用的是 Font Awesome 提供的图标， Font Awesome 提供了 600+ 的图标，可以满足绝大的多数的场景，同时无须担心在 Retina 屏幕下 图标模糊的问题。

编辑 `主题配置文件`，修改以下内容：

- 设定菜单内容，对应的字段是 menu。
  菜单内容的设置格式是：item name: link。其中 item name 是一个名称，这个名称并不直接显示在页面上，她将用于匹配图标以及翻译。 

```config
menu:
  home: /
  archives: /archives
  about: /about
  categories: /categories
  tags: /tags
  #commonweal: /404.html
```

- 置菜单项的显示文本。
  在第一步中设置的菜单的名称并不直接用于界面上的展示。Hexo 在生成的时候将使用 这个名称查找对应的语言翻译，并提取显示文本。这些翻译文本放置在 NexT 主题目录下的 languages/{language}.yml （{language} 为你所使用的语言）。 

- 设定菜单项的图标，对应的字段是 menu_icons。 
  此设定格式是 item name: icon name，其中 item name 与上一步所配置的菜单名字对应，icon name 是 Font Awesome 图标的 名字。而 enable 可用于控制是否显示图标，你可以设置成 false 来去掉图标。 

```config
menu_icons:
  enable: true
  # Icon Mapping.
  home: home
  about: user
  categories: th
  tags: tags
  archives: archive
  commonweal: heartbeat
```

### 设置 侧栏

默认情况下，侧栏仅在文章页面（拥有目录列表）时才显示，并放置于右侧位置。 可以通过修改 `主题配置文件` 中的 sidebar 字段来控制侧栏的行为。侧栏的设置包括两个部分，其一是侧栏的位置， 其二是侧栏显示的时机。

- 设置侧栏的位置，修改 sidebar.position 的值，支持的选项有：
  - left - 靠左放置
  - right - 靠右放置


```config
sidebar:
  position: left
```

> 目前仅 Pisces Scheme 支持 position 配置。影响版本`5.0.0`及更低版本。

- 设置侧栏显示的时机，修改 sidebar.display 的值，支持的选项有：
  - post - 默认行为，在文章页面（拥有目录列表）时显示
  - always - 在所有页面中都显示
  - hide - 在所有页面中都隐藏（可以手动展开）
  - remove - 完全移除

#### 侧边栏社交链接

侧栏社交链接的修改包含两个部分，第一是`链接`，第二是`链接图标`。 两者配置均在 `主题配置文件` 中。
- `链接`放置在 social 字段下，一行一个链接。其键值格式是 显示文本: 链接地址。

```config
# Social links
social:
  GitHub: https://github.com/your-user-name
  Twitter: https://twitter.com/your-user-name
  微博: http://weibo.com/your-user-name
  豆瓣: http://douban.com/people/your-user-name
  知乎: http://www.zhihu.com/people/your-user-name
  # 等等
```

- `链接的图标`，对应的字段是 social_icons。其键值格式是 匹配键: Font Awesome 图标名称，匹配键与上一步所配置的链接的显示文本相同（大小写严格匹配），图标名称是Font Awesome 图标的名字（不必带 fa- 前缀）。enable 选项用于控制是否显示图标，你可以设置成 false 来去掉图标。

```config
# Social Icons
social_icons:
  enable: true
  # Icon Mappings
  GitHub: github
  Twitter: twitter
  微博: weibo
```

#### 友情链接

编辑 主题配置文件 添加：

```config
# Blog rolls
links_title: Links
links:
  MacTalk: http://macshuo.com/
  Title: http://example.com/
```

#### Table Of Contents

#### Sidebar Avatar

- in theme directory(source/images): /images/avatar.jpg
- in site  directory(source/uploads): /uploads/avatar.jpg


### 开启打赏功能

越来越多的平台（微信公众平台，新浪微博，简书，百度打赏等）支持打赏功能，付费阅读时代越来越近，特此增加了打赏功能，支持微信打赏和支付宝打赏。 只需要 主题配置文件 中填入 微信 和 支付宝 收款二维码图片地址 即可开启该功能。

```config
reward_comment: 坚持原创技术分享，您的支持将鼓励我继续创作！
wechatpay: /path/to/wechat-reward-image
alipay: /path/to/alipay-reward-image
```

### 站点建立时间

这个时间将在站点的底部显示，例如 © 2013 - 2015。 编辑 主题配置文件，新增字段 since。

```config
since: 2013
```

### 网站logo设置

- 通过网站[favicon在线制作()制]作favicon图片，logo最好设置32*32。 
- next主题：将图片放在站点source/目录下 
- 在next主题配置文件中添加：favicon: /favicon.ico

### 设置 头像

编辑 `站点配置文件`， 新增字段 `avatar`， 值设置成头像的链接地址。其中，头像的链接地址可以是： 
- 完整的互联网 URI:  http://example.com/avatar.png 
- 站点内的地址:    
  将头像放置主题目录下的 source/uploads/ （新建uploads目录若不存在）配置为：avatar: /uploads/avatar.png 
  或者 放置在 source/images/ 目录下配置为：avatar: /images/avatar.png

### 设置 作者昵称

编辑 站点配置文件， 设置 `author` 为你的昵称。

### 站点描述

编辑 `站点配置文件`， 设置 `description` 字段为你的站点描述。站点描述可以是你喜欢的一句签名:) 

### 为博客加入动态背景

首先找到`\themes\next\layout\_layout.swig`，在末尾前加上下面一句:（这里提供两种样式，当然你也可以自由更改）。

- 默认灰色线条
```config
<script type="text/javascript" src="/js/src/particle.js"></script>
```

- 浅蓝色线条

```config
<script type="text/javascript" src="/js/src/particle.js" count="50" zindex="-2" opacity="1" color="0,104,183"></script>
```

然后在 `themes\source\js\src` 下新建文件 `particle.js` 写上以下代码:

```config
!function(){function n(n,e,t){return n.getAttribute(e)||t}function e(n){return document.getElementsByTagName(n)}function t(){var t=e("script"),o=t.length,i=t[o-1];return{l:o,z:n(i,"zIndex",-1),o:n(i,"opacity",.5),c:n(i,"color","0,0,0"),n:n(i,"count",99)}}function o(){c=u.width=window.innerWidth||document.documentElement.clientWidth||document.body.clientWidth,a=u.height=window.innerHeight||document.documentElement.clientHeight||document.body.clientHeight}function i(){l.clearRect(0,0,c,a);var n,e,t,o,u,d,x=[w].concat(y);y.forEach(function(i){for(i.x+=i.xa,i.y+=i.ya,i.xa*=i.x>c||i.x<0?-1:1,i.ya*=i.y>a||i.y<0?-1:1,l.fillRect(i.x-.5,i.y-.5,1,1),e=0;e<x.length;e++)n=x[e],i!==n&&null!==n.x&&null!==n.y&&(o=i.x-n.x,u=i.y-n.y,d=o*o+u*u,d<n.max&&(n===w&&d>=n.max/2&&(i.x-=.03*o,i.y-=.03*u),t=(n.max-d)/n.max,l.beginPath(),l.lineWidth=t/2,l.strokeStyle="rgba("+m.c+","+(t+.2)+")",l.moveTo(i.x,i.y),l.lineTo(n.x,n.y),l.stroke()));x.splice(x.indexOf(i),1)}),r(i)}var c,a,u=document.createElement("canvas"),m=t(),d="c_n"+m.l,l=u.getContext("2d"),r=window.requestAnimationFrame||window.webkitRequestAnimationFrame||window.mozRequestAnimationFrame||window.oRequestAnimationFrame||window.msRequestAnimationFrame||function(n){window.setTimeout(n,1e3/45)},x=Math.random,w={x:null,y:null,max:2e4};u.id=d,u.style.cssText="position:fixed;top:0;left:0;z-index:"+m.z+";opacity:"+m.o,e("body")[0].appendChild(u),o(),window.onresize=o,window.onmousemove=function(n){n=n||window.event,w.x=n.clientX,w.y=n.clientY},window.onmouseout=function(){w.x=null,w.y=null};for(var y=[],s=0;m.n>s;s++){var f=x()*c,h=x()*a,g=2*x()-1,p=2*x()-1;y.push({x:f,y:h,xa:g,ya:p,max:6e3})}setTimeout(function(){i()},100)}();
```

### 设置 RSS

NexT 中 RSS 有三个设置选项，满足特定的使用场景。 更改 主题配置文件，设定 rss 字段的值：

- false：禁用 RSS，不在页面上显示 RSS 连接。

- 留空：使用 Hexo 生成的 Feed 链接。 你可以需要先安装 `hexo-generator-feed` 插件。

```cmd
npm install hexo-generator-feed --save
```

- 具体的链接地址：适用于已经烧制过 Feed 的情形。

### 添加「标签」「分类」页面

- 新建页面

在终端窗口下，定位到 Hexo 站点目录下。使用 hexo new page 新建一个页面，命名为 tags ：

```cmd
cd your-hexo-site
hexo new page tags
```

- 设置页面类型

编辑刚新建的页面，将页面的类型设置为 tags ，主题将自动为这个页面显示标签云。页面内容如下：

```config
title: 标签/分类
date: 2014-12-22 12:39:04
type: "tags"/"categories"
comments: false
---
```

> 注意：如果有启用 多说 或者 Disqus 评论，页面也会带有评论。 若需要关闭的话，请添加字段 comments 并将值设置为 false.

- 修改菜单

在菜单中添加链接。编辑 主题配置文件 ， 添加 tags 到 menu 中，如下:

```config
menu:
  home: /
  archives: /archives
  categories: /categories
  tags: /tags
```

### 设置代码高亮主题

NexT 使用 Tomorrow Theme 作为代码高亮，共有5款主题供你选择。 NexT 默认使用的是 白色的 normal 主题，可选的值有 normal，night， night blue， night bright， night eighties。
更改 highlight_theme 字段，将其值设定成你所喜爱的高亮主题。



## 集成常用的第三方服务

### 多说评论

在 `主题配置文件` 中新增 `duoshuo_shortname` 字段，值设置`多说域名`。 

> 请注意为了确保多说索引的页面地址正确，需要在 站点配置文件 中正确设置 url 为你站点的域名。 若您的评论跳转到 http://yoursite.com ，请检查下 url 的配置是否正确。 

### 多说分享

编辑 站点配置文件， 添加字段 `duoshuo_share`， 值为 true。

> 多说分享必须与多说评论同时使用.

### Local Search

添加百度/谷歌/本地 自定义站点内容搜索.

1. 安装 hexo-generator-searchdb，在站点的根目录下执行以下命令：

```cmd
npm install hexo-generator-searchdb --save
```

2. 编辑 `站点配置文件`，新增以下内容到任意位置：

```config
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

3. 编辑 主题配置文件，启用本地搜索功能：

```config
# Local search
local_search:
  enable: true
```

### 阅读次数统计（LeanCloud）

配置LeanCloud:
在注册完成LeanCloud帐号并验证邮箱之后，我们就可以登录我们的LeanCloud帐号，进行一番配置之后拿到AppID以及AppKey这两个参数即可正常使用文章阅读量统计的功能了。

```order
控制台 => 创建应用 => 创建class [Counter,无限制]=> 设置 => 应用Key [AppID,AppKey]
```

复制AppID以及AppKey并在NexT主题的_config.yml文件中我们相应的位置填入即可，正确配置之后文件内容像这个样子:

```config
leancloud_visitors:
  enable: true
  app_id: joaeuuc4hsqudUUwx4gIvGF6-gzGzoHsz
  app_key: E9UJsJpw1omCHuS22PdSpKoh
```

这个时候重新生成部署Hexo博客，应该就可以正常使用文章阅读量统计的功能了。

> 需要特别说明的是：记录文章访问量的唯一标识符是文章的发布日期以及文章的标题，因此请确保这两个数值组合的唯一性，如果你更改了这两个数值，会造成文章阅读数值的清零重计。

详细参考：[ 为NexT主题添加文章阅读量统计功能](https://notes.wanghao.work/2015-10-21-%E4%B8%BANexT%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E9%98%85%E8%AF%BB%E9%87%8F%E7%BB%9F%E8%AE%A1%E5%8A%9F%E8%83%BD.html#%E9%85%8D%E7%BD%AELeanCloud)

#### 将阅读量改为热度（更个性）

看到好多人的博客不是阅读次数（阅读量），而是xxx度，那么可以继续这样修改，首先在Next主题的`/themes/next/languages/zh-Hans`文件中查找”阅读次数“这几个字，可以看到，在`post`中的`visitors`被定义为“阅读次数”，把这里的“阅读次数”改为“热度”。
那么怎么在页面中显示呢。打开Next主题文件夹中`layout/_macro/post.swig`，在这个文件里加上摄氏度的标志，在`<span class="leancloud-visitors-count"></span>`下面增加一行`<span>℃</span>`即可。

### 不蒜子统计

#### 全局配置

编辑`主题配置文件` 中的`busuanzi_count`的配置项。
当`enable: true`时，代表开启全局开关。若`site_uv`、`site_pv`、`page_pv`的值均为`false`时，不蒜子仅作记录而不会在页面上显示。

#### 站点UV配置 

`site_uv: true`时，代表在页面底部显示站点的UV值。
`site_uv_header`和`site_uv_footer`为自定义样式配置，相关的值留空时将不显示，可以使用（带特效的）font-awesome。显示效果为[site_uv_header]UV值[site_uv_footer]。

```config
# 效果：本站访客数12345人次
site_uv: true
site_uv_header: 本站访客数
site_uv_footer: 人次
```

#### 站点PV配置

当`site_pv: true`时，代表在页面底部显示站点的PV值。
`site_pv_header`和`site_pv_footer`为自定义样式配置，相关的值留空时将不显示，可以使用（带特效的）font-awesome。显示效果为[site_pv_header]PV值[site_pv_footer]。

```config
# 效果：本站总访问量12345次
site_pv: true
site_pv_header: 本站总访问量
site_pv_footer: 次
```

#### 单页PV配置

当`page_pv: true`时，代表在文章页面的标题下显示该页面的PV值（阅读数）。
`page_pv_header`和`page_pv_footer`为自定义样式配置，相关的值留空时将不显示，可以使用（带特效的）font-awesome。显示效果为[page_pv_header]PV值[page_pv_footer]。

```config
# 效果：本文总阅读量12345次
page_pv: true
page_pv_header: 本文总阅读量/热度
page_pv_footer: 次/℃
```

> 单页PV配置可以和LeanCloud阅读次数选择其一。

### 为项目主页添加README

在Github上的博客仓库主页空荡荡的，没有`README`。如果把`README.md`放入`source`文件夹，hexo g生成时会被解析成html文件，放到public文件夹，生成时又会自动删除。
解决方法很简单，在`站点配置文件`中，搜索`skip_render:`，在其冒号后加一个空格然后加上`README.md`即可。

---

效果参见：[我的博客](http://wonux.coding.me): wonux.wang


