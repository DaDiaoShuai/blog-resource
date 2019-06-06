---
title: HTML中head元素介绍
date: 2019-01-11
tags: FE
toc: true
comments: true
category: 前端
---

### 一、常见元素介绍

有效的`<head>`标签通常包含`meta, link, title, style, script`等等，它们提供了有关浏览器、搜索引擎等如何通过web技术去感知和呈现文档的信息的能力
<!--more-->

``` HTML
<!-- 这个不用说 -->
<meta charset="utf-8">

<!-- 这个也不用说了 -->
<title>Page Title</title>

<!-- 
这个要说一下：我感觉挺有用却用的很少的一个标签元素，w3school个的定义是 「为页面上的所有链接规定默认地址或默认目标值」
这个「默认地址」href 准确来说应该是页面上所有的相对路径的根地址。
「目标值」target 例如一个a标签链接点击之后是在当前页面打开还是新打开一个标签页。
它还有其他几个属性值，
    _blank：新标签页
    _self(默认值)：当前页
    _parent：在父iframe中打开链接
    _top： 在整个窗口中打开链接
    [framename]：也可以指定某个iframe中打开链接
 -->
<base href="https://4bros.cn" target="_blank">

<!-- 引用一个外部css文件 -->
<link rel="stylesheet" href="style.css">

<!-- 网站图标 Icons -->
<!-- size属性只用于rel="icon" 顾名思义 -->
<link rel="icon" href="favicon.ico" size="any">
<!-- IOS 图标rel参数 -->
<!-- apple-touch-icon 图片自动处理成圆角和高光等效果。 -->
<link rel="apple-touch-icon" href="favicon.ico" size="any">
<!-- apple-touch-icon-precomposed 禁止系统自动添加效果，直接显示设计原图。 -->
<link rel="apple-touch-icon-precomposed" href="favicon.ico" size="any">
<!-- iPhone 和 iTouch，默认 57x57 像素，必须有 -->
<link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-57x57-precomposed.png" />
<!-- iPad，72x72 像素，可以没有，但推荐有 -->
<link rel="apple-touch-icon-precomposed" sizes="72x72" href="/apple-touch-icon-72x72-precomposed.png" />
<!-- Retina iPhone 和 Retina iTouch，114x114 像素，可以没有，但推荐有 -->
<link rel="apple-touch-icon-precomposed" sizes="114x114" href="/apple-touch-icon-114x114-precomposed.png" />
<!-- Retina iPad，144x144 像素，可以没有，推荐使用 -->
<link rel="apple-touch-icon-precomposed" sizes="144x144" href="/apple-touch-icon-144x144-precomposed.png" />

<!-- 行内样式 -->
<style>/* ...*/</style>

<!-- javascript -->
<script src="script.js"></script>
<!-- or -->
<script>
// function func() { ... }
</script>

```

### 二、Meta
- 下面这两个`<meta>`标签是为了确保网页能够正常呈现的基本元素，且应该写在别的元素前面
``` HTML
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
...
<title>Title</title>
```
- 启用[CSP(Content Security Policy)](https://www.cnblogs.com/alisecurity/p/5924023.html)即”网页安全政策“
``` HTML
<meta http-equiv="Content-Security-Policy" content="default-src 'self'; object-src 'none'; style-src cdn.example.org third-party.org; child-src https:"">
<!-- 上面代码中，CSP 做了如下配置。
脚本：只信任当前域名
标签：不信任任何URL，即不加载任何资源
样式表：只信任cdn.example.org和third-party.org
框架（frame）：必须使用HTTPS协议加载
其他资源：没有限制
启用后，不符合 CSP 的外部资源就会被阻止加载。 -->
```

更多关于[CSP(Content Security Policy)](https://www.cnblogs.com/alisecurity/p/5924023.html)的内容请参考链接,里面讲的算是超级详细了。

- SEO优化
```HTML
<!-- APP的名称，这个配置应该在APP里加上 -->
<meta name="application-name" content="Application Name">
<!-- 添加对网页的简短描述，不能超过150个字符 -->
<meta name="description" content="页面的描述">
<!-- 页面关键词 -->
<meta name="keywords" content="html5,css,js,keywords"/>
<!-- 定义网页作者 -->
<meta name="author" content="Coolb" />
<!-- 定义网页搜索引擎索引方式，robotterms是一组使用英文逗号「,」分割的值，通常有如下几种取值：none，noindex，nofollow，all，index和follow。 -->
<meta name="robots" content="index,follow" />
<meta name="googlebot" content="index,follow"> <!-- Google -->
```
 
- viewport 多为移动端添加
```HTML
<meta name ="viewport" content ="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no">
<!-- content 参数解释：
    width  　　　　 viewport 宽度(数值/device-width)
    height            viewport 高度(数值/device-height)
    initial-scale  初始缩放比例
    maximum-scale  最大缩放比例
    minimum-scale  最小缩放比例
    user-scalable  是否允许用户缩放(yes/no) -->

<!-- minimal-ui iOS 7.1 beta 2 中新增属性，可以在页面加载时最小化上下状态栏。这是一个布尔值，可以直接这样写： -->
<meta name="viewport" content="width=device-width, initial-scale=1, minimal-ui">

<!-- IOS -->
<meta name="apple-mobile-web-app-title" content="标题">添加到主屏后的标题（iOS 6 新增）
<meta name="apple-mobile-web-app-capable" content="yes" />是否启用 WebApp 全屏模式
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />设置状态栏的背景颜色
<!-- 
只有在 "apple-mobile-web-app-capable" content="yes" 时生效
content 参数：
default 默认值。
black 状态栏背景是黑色。
black-translucent 状态栏背景是黑色半透明。
设置为 default 或 black ,网页内容从状态栏底部开始。
设置为 black-translucent ,网页内容充满整个屏幕，顶部会被状态栏遮挡。 -->
 ```

### 三、Link
```HTML
<!-- 有助于防止出现内容重复的问题 -->
<link rel="canonical" href="http://example.com/article/?page=2">
<!-- 链接到当前文档的一个 AMP HTML 版本 -->
<link rel="amphtml" href="https://example.com/path/to/amp-version.html">
<!-- 链接到一个指定 Web 应用程序“安装”凭据的 JSON 文件 -->
<link rel="manifest" href="manifest.json">
<!-- 链接到关于页面所有者的信息 -->
<link rel="author" href="author.txt">
<!-- 指向一个适用于链接内容的版权申明 -->
<link rel="license" href="copyright.html">
<!-- 给出可能的你的另一种语言的文档位置参考 -->
<link rel="alternate" href="https://es.example.com/" hreflang="es">
<!-- 提供了关于作者或其他人的信息 -->
<link rel="me" href="https://google.com/profiles/coolb" type="text/html">
<link rel="me" href="mailto:name@example.com">
<link rel="me" href="sms:+15035550125">

<!-- 链接到一个描述历史记录、文档或其他具有历史意义的材料的集合的文档 -->
<link rel="archives" href="https://example.com/archives/">
<!-- 链接到层次结构中的顶级资源 -->
<link rel="index" href="http://example.com/article/">
<!-- 提供了自我引用 - 当文档有多个可能的引用时非常有用 -->
<link rel="self" type="application/atom+xml" href="http://example.com/atom.xml">
<!-- 分别是一系列页面中的第一个，最后一个，上一个和下一个页面 -->
<link rel="first" href="http://example.com/article/">
<link rel="last" href="http://example.com/article/?page=42">
<link rel="prev" href="http://example.com/article/?page=1">
<link rel="next" href="http://example.com/article/?page=3">

<!-- 当使用第三方服务来维护博客时使用 -->
<link rel="EditURI" href="https://example.com/xmlrpc.php?rsd" type="application/rsd+xml" title="RSD">
<!-- 当另一个 WordPress 博客链接到你的 WordPress 博客或文章时形成一个自动化的评论 -->
<link rel="pingback" href="https://example.com/xmlrpc.php">
<!-- 当你在自己的页面上链接到一个 url 时通知它 -->
<link rel="webmention" href="https://example.com/webmention">
<!-- 启用通过 Micropub 客户端发布你的域名 -->
<link rel="micropub" href="https://example.com/micropub">
<!-- 打开搜索 -->
<link rel="search" href="/open-search.xml" type="application/opensearchdescription+xml" title="Search Title">
<!-- Feeds -->
<link rel="alternate" href="https://feeds.feedburner.com/example" type="application/rss+xml" title="RSS">
<link rel="alternate" href="https://example.com/feed.atom" type="application/atom+xml" title="Atom 0.3">

<!-- 预取，预载，预浏览 -->
<!-- 更多信息：https://css-tricks.com/prefetching-preloading-prebrowsing/ -->
<link rel="dns-prefetch" href="//example.com/">
<link rel="preconnect" href="https://www.example.com/">
<link rel="prefetch" href="https://www.example.com/">
<link rel="prerender" href="https://example.com/">
<link rel="preload" href="image.png" as="image">
```
### 四、More
```HTML
<!-- 告诉Google不要为此文档提供翻译 -->
<meta name="google" content="notranslate">
<!-- 校验网站所有权 -->
<meta name="google-site-verification" content="verification_token">
<meta name="yandex-verification" content="verification_token">
<meta name="msvalidate.01" content="verification_token">
<meta name="alexaVerifyID" content="verification_token">
<meta name="p:domain_verify" content="code_from_pinterest">
<meta name="norton-safeweb-site-verification" content="norton_code">

<meta name="generator" content="program">构建网站用的软件的标识
<meta name="referrer" content="no-referrer">允许控制引用者信息的传递方式
<meta name="format-detection" content="telephone=no" />禁止数字识自动别为电话号码
<meta name="format-detection" content="email=no" />不让android识别邮箱
<meta name="renderer" content="webkit">启用360浏览器的极速模式(webkit)
<meta http-equiv="X-UA-Compatible" content="IE=edge">避免IE使用兼容模式
<meta name="HandheldFriendly" content="true">针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓
<meta name="MobileOptimized" content="320">微软的老式浏览器
<meta name="x5-orientation" content="portrait">QQ强制竖屏
<meta name="full-screen" content="yes">UC强制全屏
<meta name="x5-fullscreen" content="true">QQ强制全屏
<meta name="browsermode" content="application">UC应用模式
<meta name="x5-page-mode" content="app">QQ应用模式
<meta http-equiv="Cache-Control" content="no-siteapp" />禁止百度转码
<meta name="msapplication-tap-highlight" content="no">windows phone 点击无高光
<meta name="Copyright" content="" />  公司
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">   让IE浏览器用最高级内核渲染页面 还有用 Chrome 框架的页面用webkit 内核 
<meta name="apple-mobile-web-app-capable" content="yes">  IOS6全屏
<meta name="mobile-web-app-capable" content="yes">  Chrome高版本全屏
<meta name="renderer" content="webkit">  让360双核浏览器用webkit内核渲染页面
<meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL"> 添加智能 App 广告条 Smart App Banner（iOS 6+ Safari）
<meta http-equiv="x-dns-prefetch-control" content="off">通过设置off来完全关闭DNS预取
<meta http-equiv="set-cookie" content="name=value; expires=date; path=url">在客户端web浏览器上设置cookie
<meta http-equiv="Window-Target" content="_value">指定要在特定框架中显示的文档
 ```

>参考：
 https://gethead.info/#meta 
 https://blog.csdn.net/xmtblog/article/details/46226717
 https://www.cnblogs.com/alisecurity/p/5924023.html