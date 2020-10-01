---
title: 基于 Hexo + NexT 的静态博客配置
date: 2020-09-30 22:00:00
tags: Hexo
---

此处为简述，在.md文件的`<!--more-- >`前面添加。

如果`<!--more-- >`放在文章首，那就默认没有折叠效果。

通过安装Hexo框架、 新建Hexo网站、安装NexT主题，并进行配置，生成静态博客网站。

<!--more-->

# 一、使用hexo框架搭建静态博客

## 1.安装好node.js 和 Git

## 2.安装淘宝的cnpm

```cpp
npm install -g cnpm --registry=http://registry.npm.taobao.org

cnpm -v  //查看安装版本
```

## 3.安装 hexo 框架

```cpp
cnpm install -g hexo-cli

hexo -v   //查看hexo版本
```

## 4.新建一个博客网站

```kotlin
hexo init  //新建一个网站
```

## 5.启动服务器

```kotlin
hexo server
```

- 打开浏览器中，输入 [http://localhost:4000](https://links.jianshu.com/go?to=http%3A%2F%2Flocalhost%3A4000) 访问博客
- ctrl+c 关闭服务器

## 6.新建一篇博客

```cpp
hexo new "第一篇博客"
```

- 文件路径：`source/_posts/第一篇博客.md`
- 也可以直接在 `source/_posts/`中新建.md文件
- 每个.md文件头都有`Front-matter`部分，注意其内容

## 7.清除缓存文件

```undefined
hexo clean
```

建议每次生成站点或部署之前都用该命令清理一下缓存

## 8.生成静态文件

```undefined
hexo generate
```

## 7.再次启动服务器

```undefined
hexo server
```

在刚才打开的浏览器博客页面刷新，出现新写的文章

## 8.简便操作（不建议）

```kotlin
hexo clean && hexo d -g					//这是先generate、再deploy， -g 参数在后面。。。。。。。
```

- 可能在generate的时候出现`Error`，建议还是`hexo clean`、 `hexo g`、 `hexo s` 一步步来。





# 二、站点配置文件

**博客主目录下修改站点配置文件`_config.yml` 来更改基本信息**

```kotlin
# Site
title: 学道之人
subtitle: ''
description: '信念这玩意真不是说出来的，是做出来的。'
keywords:
author: 学道之人「xuedao01」
language: zh-CN								//这里修改成zh-CN（而不是zh-Hans）是为了和NexT主题的语言包匹配
timezone: ''									//默认使用计算机本地时区
```

```kotlin
theme: next										//修改主题，默认是landscape
```

```php
# Deployment									//部署到Github Pages
## Docs: https://hexo.io/docs/one-command-deployment

deploy:
  type: git
  repo: git@github.com:xuedao01/xuedao01.github.io.git
  branch: master
```





# 三、主题配置文件

## 1.安装NexT主题

进入Hexo博客主目录下

```
git clone https://github.com/theme-next/hexo-theme-next themes/next\n
```

修改博客配置文件`_config.yml`  ，添加next主题

```
hexo clean 
hexo g
hexo s
```

## 2.设置NexT主题的Scheme风格

- Next主题有四种Scheme风格
- 打开`themes/next/ _config.yml` ，搜索 `Scheme Settings`，设置为`scheme: Pisces`（第三个）

## 3.NexT设置中文语言：

- 打开`站点配置文件_config.yml`，`# Site`下的`language`设置为`zh-CN`即可。
- 到 themes - next - languages文件夹下，发现中文支持文件有`zh-CN.yml`，而不是`zh-Hans`
- 故也可将zh-CN.yml文件名改成zh-Hans，再在站点配置文件`_config.yml`设置为`zh-Hans`

- 参考：https://blog.csdn.net/mqdxiaoxiao/article/details/93251246

## 4.menu设置

主题配置文件搜索`Menu Settings`，取消对应项注释

```
menu:
  home: / || fa fa-home
  about: /about/ || fa fa-user
  tags: /tags/ || fa fa-tags
  categories: /categories/ || fa fa-th
  archives: /archives/ || fa fa-archive
```

hexo添加对应新菜单，如：

```
hexo new page archives
```

然后就可以看到在source下多了一个archives的文件夹，里面有一个index.md文件。

可以自行添加，比如在`menu`添加`favorite`项，在主题的语言文件`zh-CN.yml`添加翻译`favorite: 收藏夹`

## 5.右上角添加跳转黑色Github小图标

- 首先到[GitHub Corners](http://tholman.com/github-corners/)或者[GitHub Ribbons](https://github.blog/2008-12-19-github-ribbons/)选择自己喜欢的图标，然后copy相应的代码
- 然后将刚才复制的代码粘贴到`next/layout/_layout.swig`文件中<div class="headband"></div>下面一行
- 再把代码中的`href`后面的值替换成你要跳转的地址，比如你的GitHub主页
- 以下是上面的效果采用的代码

```html
<a href="https://your-url" class="github-corner" aria-label="View source on GitHub"><svg width="80" height="80" viewBox="0 0 250 250" style="fill:#151513; color:#fff; position: absolute; top: 0; border: 0; right: 0;" aria-hidden="true"><path d="M0,0 L115,115 L130,115 L142,142 L250,250 L250,0 Z"></path><path d="M128.3,109.0 C113.8,99.7 119.0,89.6 119.0,89.6 C122.0,82.7 120.5,78.6 120.5,78.6 C119.2,72.0 123.4,76.3 123.4,76.3 C127.3,80.9 125.5,87.3 125.5,87.3 C122.9,97.6 130.6,101.9 134.4,103.2" fill="currentColor" style="transform-origin: 130px 106px;" class="octo-arm"></path><path d="M115.0,115.0 C114.9,115.1 118.7,116.5 119.8,115.4 L133.7,101.6 C136.9,99.2 139.9,98.4 142.2,98.6 C133.8,88.0 127.5,74.4 143.8,58.0 C148.5,53.4 154.0,51.2 159.7,51.0 C160.3,49.4 163.2,43.6 171.4,40.1 C171.4,40.1 176.1,42.5 178.8,56.2 C183.1,58.6 187.2,61.8 190.9,65.4 C194.5,69.0 197.7,73.2 200.1,77.6 C213.8,80.2 216.3,84.9 216.3,84.9 C212.7,93.1 206.9,96.0 205.4,96.6 C205.1,102.4 203.0,107.8 198.3,112.5 C181.9,128.9 168.3,122.5 157.7,114.1 C157.9,116.9 156.7,120.9 152.7,124.9 L141.0,136.5 C139.8,137.7 141.6,141.9 141.8,141.8 Z" fill="currentColor" class="octo-body"></path></svg></a><style>.github-corner:hover .octo-arm{animation:octocat-wave 560ms ease-in-out}@keyframes octocat-wave{0%,100%{transform:rotate(0)}20%,60%{transform:rotate(-25deg)}40%,80%{transform:rotate(10deg)}}@media (max-width:500px){.github-corner:hover .octo-arm{animation:none}.github-corner .octo-arm{animation:octocat-wave 560ms ease-in-out}}</style>
```

参考：https://blog.csdn.net/mqdxiaoxiao/article/details/93796367

主题配置文件里面，貌似有类似功能（没试过）

```yaml
# `Follow me on GitHub` banner in the top-right corner.
github_banner:
  enable: false
  permalink: https://github.com/yourname
  title: Follow me on GitHub
```

## 6.左侧边栏社交链接

侧栏社交链接的修改包含两个部分，第一是链接，第二是链接图标。 两者配置均在 **主题配置文件** 中。

1. 链接放置在 `social` 字段下，一行一个链接。其键值格式是 `显示文本: 链接地址`。

   配置示例

   ```
   # Social links
   social:
     GitHub: https://github.com/your-user-name
     Twitter: https://twitter.com/your-user-name
     微博: http://weibo.com/your-user-name
     豆瓣: http://douban.com/people/your-user-name
     知乎: http://www.zhihu.com/people/your-user-name
     # 等等
   ```

2. 设定链接的图标，对应的字段是 `social_icons`。其键值格式是 `匹配键: Font Awesome 图标名称`， `匹配键` 与上一步所配置的链接的 `显示文本` 相同（大小写严格匹配），`图标名称` 是 Font Awesome 图标的名字（不必带 `fa-` 前缀）。 `enable` 选项用于控制是否显示图标，你可以设置成 `false` 来去掉图标。

   配置示例

   ```
   # Social Icons
   social_icons:
     enable: true
     # Icon Mappings
     GitHub: github
     Twitter: twitter
     微博: weibo
   ```

- 参考：http://theme-next.iissnan.com/theme-settings.html#author-sites

## 7.搜索服务

- 添加本地自定义站点内容搜索，可以通过文字标题或文字内容关键字搜索出相应文章

1. 安装 `hexo-generator-searchdb`，在站点的根目录下执行以下命令：

   ```
   $ npm install hexo-generator-searchdb --save
   ```

2. 编辑站点配置文件，新增以下内容到任意位置：

   ```
   search:
     path: search.xml
     field: post
     format: html
     limit: 10000
   ```

3. 编辑主题配置文件，启用本地搜索功能：

   ```
   # Local search
   local_search:
     enable: true
   ```

- 参考：[https://www.himmy.cn/2019/07/06/hexo个人博客next主题添加local-search本地搜索](https://www.himmy.cn/2019/07/06/hexo个人博客next主题添加local-search本地搜索)
- 官方介绍：http://theme-next.iissnan.com/third-party-services.html#search-system
- NexT貌似自带：主题配置文件中`# Search Services`

## 8.添加文章边框阴影效果

1.在next文件夹下找到themes\next\source\css\ _common\components\post下的post.styl

2.添加相应样式如下：（我怕影响到其他样式，所以将post-block样式单独拿出来写了。）

```kotlin
.use-motion {						//我这里是第34行
		//里面的第一个if{}
}
```

```
if (hexo-config('motion.transition.post_block')) {
    .post-block {
      opacity: 0;
      margin-top: 60px;
      margin-bottom: 60px;
      padding: 25px;
      -webkit-box-shadow: 0 0 5px rgba(202, 203, 203, .5);
      -moz-box-shadow: 0 0 5px rgba(202, 203, 204, .5);
    }
    .pagination, .comments{
      opacity: 0;
    }
  }
```

3.执行`hexo clean`，重新`hexo g`，即可看到效果

- 参考-1（旧版的做法）：[https://www.himmy.cn/2019/07/06/hexo博客next主题下添加文章边框阴影效果/](https://www.himmy.cn/2019/07/06/hexo博客next主题下添加文章边框阴影效果/)

- 参考-2（贴吧大神新版）：https://tieba.baidu.com/p/6365333284



## 9.Hexo 自动添加 Read More 标记（未实现）

- 官方说明：http://theme-next.iissnan.com/faqs.html#read-more
- 参考：[https://twiceyuan.com/2014/05/25/hexo自动添加readmore标记/](https://twiceyuan.com/2014/05/25/hexo自动添加readmore标记/)



## 10.字数和阅读时间统计

安装：

```
$ npm install hexo-symbols-count-time
```

在 Hexo 的 _ config.yml 中添加 Hexo-symbols-count-time 选项：

```
symbols_count_time:
  symbols: true
  time: true
  total_symbols: true
  total_time: true
  exclude_codeblock: false
  awl: 2
  wpm: 300
  suffix: "mins."
```

- 来源：https://github.com/theme-next/hexo-symbols-count-time



## 11.访问统计

使用 leancloud_visitors 经常不显示，改用不算子。

在主题的配置文件中搜索`busuanzi_count`，将下面的enable属性设为true即可。不算子的缺点是统计不是很准（只多不少，很容易刷数据），将就着用吧。



## 12.版权声明

修改主题配置文件：

```
creative_commons:
  license: by-nc-sa
  sidebar: false
  post: true
  language: zh-CN
```

## 13.修改选中文本颜色

1.在next文件夹下找到themes\next\source\css\ _common\components\post下的post.styl

2.添加相应样式如下：

```css
// 修改选中字符的颜色
/* webkit, opera, IE9 */
::selection {
    background: #00c4b6;
    color: #f7f7f7;
}
/* firefox */
::-moz-selection {
    background: #00c4b6;
    color: #f7f7f7;
}
```

参考：https://www.jianshu.com/p/2a8d399f1266

RGB查询：https://www.fontke.com/tool/rgb/f7f7f7/

## 14.代码高亮

站点配置文件`_config.yml`中，设置如下

```yml
highlight:
  enable: true
  line_number: true
  auto_detect: true
  tab_replace: false
```

主题配置文件中：

```yaml
codeblock:
  # Code Highlight theme
  # Available values: normal | night | night eighties | night blue | night bright | solarized | solarized dark | galactic
  # See: https://github.com/chriskempson/tomorrow-theme
  highlight_theme: galactic
  # Add copy button on codeblock
  copy_button:
    enable: true
    # Show text copy result.
    show_result: true
    # Available values: default | flat | mac
    style: mac
```

有个坑：选中代码文本显示黑色，和黑色背景很不搭配

修改：`next-->source-->css-->_common-->scaffolding-->highlight ` 中的 `theme.styl`文件，找到想要修改的那个主题，参考“修改选中文本颜色”部分修改即可。

自动识别代码语言高亮（貌似）：[https://eggsywelsh.github.io/2016/11/10/hexo代码高亮/](https://eggsywelsh.github.io/2016/11/10/hexo代码高亮/)

## 15.其他设置具体看主题配置文件

如：阅读进度栏