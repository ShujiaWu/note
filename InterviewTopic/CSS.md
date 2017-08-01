# 前端面试题--CSS部分

## 简要说一下CSS的元素分类

* 行内元素
    span a label input img strong em
* 块级元素
    div p h1 form ul li

## 隐藏元素的几种方式

Opacity: 通过设置元素的透明度来隐藏元素,是元素本身占据的空间不变。

Visibility: 通过设置元素为不可见来隐藏元素,隐藏的元素占据的空间不变。

display: 设置为none的时候,元素隐藏不占据文档空间。

## 列举CSS清除浮动的方式

* 使用带clear属性的空元素
* 使用overflow属性
* 使用after伪元素设置clear属性

## CSS 居中

### 水平居中
1. 行内元素: 通过设置 `text-align:center` 来实现水平居中。

1. Flex布局: 通过设置 `display: flex; justify-content: center;`

1. 块级元素： 

    宽度固定时，可以通过 `margin: 0 auto;` 来实现水平居中。

    将块级元素设置为 `inline-block`, 然后设置父元素的 `text-align:center`。

### 垂直居中
1. 行内元素: 

    通过设置 `line-heigh` 来实现.

    通过设置 `display: table-cell; vertical-align: middle;` 来实现。

