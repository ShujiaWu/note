# 前端面试题--HTML部分

## XHTML和HTML有什么区别

HTML是一种基本的WEB网页设计语言，XHTML是一个基于XML的置标语言

最主要的不同：

* XHTML 元素必须被正确地嵌套。
* XHTML 元素必须被关闭。
* 标签名必须用小写字母。
* XHTML 文档必须拥有根元素

## 前端页面有哪三层构成

* 结构层 HTML
* 表示层 CSS
* 行为层 JS

## 主流的浏览器有哪些，他们的内核是什么

浏览器 | 内核 
---------|----------
 IE | IE内核 
 火狐 | Gecko ['gekəʊ]
 谷歌 | Webkit,Blink
 Opera | Presto ['prestəʊ]
 Safari | Webkit

## 什么是语义化的HTML

* 用正确的标签做正确的事情。
* 使用正确的标签使得页面内容结构化，便于浏览器解析和搜索引擎抓取。
* 在没有CSS样式样式的情况下也能容易阅读。
* 对于阅读源码的人能够容易的对页面内容进行分块，便于阅读和维护。

## HTML5 为什么只需要写 \<!DOCTYPE HTML\>
HTML5 不基于 `SGML` （Standard Generalized Markup language，标准通用标记语言），因此不需要对 `DTD` （Document Type Definition，文档类型定义） 进行引用，但是需要doctype来规范浏览器的行为（让浏览器按照它们应该的方式来运行）。

而HTML4.01基于 `SGML` ，所以需要对 `DTD` 进行引用，才能告知浏览器文档所使用的文档类型。

## DOCTYPE 的作用？标准模式与兼容模式各有什么区别?

!DOCTYPE声明位于位于HTML文档中的第一行，告知浏览器以什么样的文档标准解析页面。

如果文档类型申明不正确或者不存在将导致文档以兼容模式来呈现。

标准模式：页面的布局、样式、JS运作模式都是以浏览器支持的最高标准运行。

兼容模式：页面以宽松、向后兼容的方式解析、运行，模拟老式浏览器的行为，防止站点无法工作。

## HTML5 有哪些新特性、移除了哪些元素。

新增：

* 多媒体： `video` 和 `audio`
* 绘图： `Canvas` 和 `SVG`
* 本地存储：`localStorage` 、`sessionStorage`、`Web SQL`
* 新技术： `webworker` `websocket` `Geolocation`
* 更加语义化的标签： `artical` 、 `header`  、 `footer`  、 `nav`  、 `section`等
* 表单： `calendar` 、 `date` 、 `time` 、 `email` 、 `url` 、 `search`

移除：
`font` 、 `frame` 、 `frameset` 、 `noframes` 等元素被移除

## cookies、sessionStorage、localStorage的区别

cookies 用于存储用户的信息，会在浏览器和服务器间来回传递。

sessionStorage 和 localStorage 只保存在本地。

sessionStorage 和 localStorage 拥有更大、独立的存储空间、丰富的接口。

## 如何实现浏览器内多个标签页之间的通信

调用localstorge、cookies等本地存储方式