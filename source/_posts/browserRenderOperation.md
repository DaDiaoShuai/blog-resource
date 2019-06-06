---
title: 浏览器渲染原理
date: 2019-04-19
tags: FE
category: 前端
description: 浏览器渲染原理深入浅出
---

浏览器渲染大致分为几个部分：DOM --> CSSOM --> Render Tree --> Layout --> Paint

1. 不带`defer`或者`async`属性声明的script标签会阻塞DOM资源的加载

2. DOM与CSSOM**一般**来说是同步构建的，互不影响的；但是遇到不带`defer`或者`async`属性声明的script标签则CSSOM会阻塞DOM，因为script里面的内容可能会有操作CSSOM的部分，所以这时候顺序一般是先加载CSSDOM，然后加载script，最后加载DOM

3. 带`defer`或者`async`的script标签不回影响DOM加载。而且区别在于，前者的声明是告诉浏览器`js`在文档加载完毕后再进行加载，后者则是异步加载`js`，虽然不影响DOM加载，但是不能保证在`DOMContentLoaded`或前或后加载完毕，但保证在`load`前加载完毕。

4. `repaint`与`reflow`
    重绘是指样式图层重绘，但不影响文档布局，例如颜色相关、透明度等属性；回流或者说重排是指影响样式布局受到影响，导致需要重新对DOM进行重新`Layout`，常见操作例如对元素的位置和尺寸大小都会造成`Reflow`。重排一定会导致重绘，重绘不一定会重排。所以减少重绘或者重排对页面性能提升很关键。

    - 常见引起回流的操作：
        + 添加或者删除可见的DOM元素；
        + 元素尺寸改变——边距、填充、边框、宽度和高度
        + 内容变化，比如用户在input框中输入文字
        + 浏览器窗口尺寸改变——resize事件发生时
        + 计算 offsetWidth 和 offsetHeight 属性
        + 设置 style 属性的值
    - 常见引起重绘的属性和方法：
        color、borde-style、visibility、background ···
    
    如何减少重绘和回流：
    - 使用 transform 替代 top
    - 使用 visibility 替换 display: none ，因为前者只会引起重绘，后者会引发回流（改变了布局）
    - 不要把节点的属性值放在一个循环里当成循环里的变量
        ``` javascript
        for(let i = 0; i < 1000; i++) {
            // 获取 offsetTop 会导致回流，因为需要去获取正确的值
            console.log(document.querySelector('.test').style.offsetTop)
        }
        ```
    - 不要使用 table 布局，可能很小的一个小改动会造成整个 table 的重新布局
    - 动画实现的速度的选择，动画速度越快，回流次数越多，也可以选择使用 requestAnimationFrame
    - CSS 选择符从右往左匹配查找，避免节点层级过多
    - 将频繁重绘或者回流的节点设置为图层，图层能够阻止该节点的渲染行为影响别的节点。比如对于 video 标签来说，浏览器会自动将该节点变为图层。

### 页面性能优化策略

1. JS优化： `<script>` 标签加上 defer属性 和 async属性 用于在不阻塞页面文档解析的前提下，控制脚本的下载和执行。
    - defer属性： 用于开启新的线程下载脚本文件，并使脚本在文档解析完成后执行。
    - async属性： HTML5新增属性，用于异步下载脚本文件，下载完毕立即解释执行代码。
2. CSS优化： `<link>` 标签的 rel属性 中的属性值设置为 preload 能够让你在你的HTML页面中可以指明哪些资源是在页面加载完成后即刻需要的,最优的配置加载顺序，提高渲染性能


### 总结
- 浏览器工作流程：构建DOM -> 构建CSSOM -> 构建渲染树 -> 布局 -> 绘制。
- CSSOM会阻塞渲染，只有当CSSOM构建完毕后才会进入下一个阶段构建渲染树。
- 通常情况下DOM和CSSOM是并行构建的，但是当浏览器遇到一个不带defer或async属性的script标签时，DOM构建将暂停，如果此时又恰巧浏览器尚未完成CSSOM的下载和构建，由于JavaScript可以修改CSSOM，所以需要等CSSOM构建完毕后再执行JS，最后才重新DOM构建。