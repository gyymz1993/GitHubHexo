---
title: 熟悉Hexo
date: 2016-12-07 15:29:30
tags: hexo
---

欢迎我的博客，我会为你们奉献更多的干货，感谢大家的支持
## Please read happily

<!-- more -->
<The rest of contents | 余下全文>

分类和标签
categories:
- Diary
tags:
- PS3
- Games

引用块
在文章中插入引言，可包含作者、来源和标题。

别号： quote

‘{% blockquote [author[, source]] [link] [source_link_title] %}’
content
‘{% endblockquote %}’


代码块
在文章中插入代码。
别名： code
‘{% codeblock [title] [lang:language] [url] [link text] %}‘
code snippet
’{% endcodeblock %}’

Image
在文章中插入指定大小的图片。
‘{% img [class names] /path/to/image [width] [height] [title text [alt text]] %}’


Link
在文章中插入链接，并自动给外部链接添加 target="_blank" 属性。
’{% link text url [external] [title] %}‘


Vimeo
在文章中插入 Vimeo 视频。
‘{% vimeo video_id %}’


引用文章
引用其他文章的链接。
‘{% post_path slug %}’
‘{% post_link slug [title] %}’


