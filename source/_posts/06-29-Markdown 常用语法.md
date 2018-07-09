---
title: Markdown 常用语法
date: 2018-06-29 13:45:37
tags: Learning
reward: true
toc: true
comments: true
---
### 快捷键

| 快捷键              |  功能                         |
|:-------------------|:-----------------------------|
| Ctrl + B           |  Toggle bold                 |
| Ctrl + I           |  Toggle italic               |
| Alt + S            |  Toggle strikethrough        |
| Ctrl + Shift + ]   |  Toggle heading (uplevel)    |
| Ctrl + Shift + [   |  Toggle heading (downlevel)  |
| Alt + C            |  Check/Uncheck task list item|
<!-- more -->

### 标题

    # h1
    ## h2
    ### h3
    #### h4
    ##### h5
    ###### h6

### 分级标题

    一级标题
    ======================
    二级标题
    ---------------------

### 引用

    > hello world!

    > hello world!
      hello world!
      hello world!

    > aaaaaaaaa
    >> bbbbbbbbb
    >>> cccccccccc  

### 行内标记

    标记之外`hello world`标记之外

### 代码块

```
  <div>
      <div></div>
      <div></div>
      <div></div>
  </div>
```

### 插入链接

    [百度1](http://www.baidu.com/ "百度一下")

    [百度2][2]

      [2]: http://www.baidu.com/

### 插入图片

    ![](/assets/images/avatar.jpg 'dome')

    ![name][01]

      [01]: /assets/images/avatar.jpg 'dome'

### 插入图片带有链接

    [![](/assets/images/avatar.jpg '百度')](http://www.baidu.com)

    [![](/assets/images/avatar.jpg '百度')][5]

      [5]: http://www.baidu.com

### 视频插入

    <iframe height=498 width=510 src='http://player.youku.com/embed/XMjgzNzM0NTYxNg==' frameborder=0 'allowfullscreen'></iframe>

### 表格

    |    a    |       b       |      c     |
    |:-------:|:------------- | ----------:|
    |   居中  |     左对齐    |   右对齐   |
    |=========|===============|============|

### 序表

    1. one
    2. two
    3. three

    * one
    * two
      * ww
    * three

### 任务列表

    - [ ] last
    - [x] first

### 脚注

    Markdown[^1]

      [^1]: Markdown是一种纯文本标记语言

### 分隔符

    ***
    ---
    * * *