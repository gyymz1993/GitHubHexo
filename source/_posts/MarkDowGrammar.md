---
title: 手把手教你MarkDown写作
date: 2016-12-09 11:29:30
tags: mardown
---

欢迎我的小博，我正在努力学习，我会在不久将来给你们分享更多的干货，希望你们喜欢。
## Please read happily

<!-- more -->
<The rest of contents | 余下全文>


###  Markdown 支持以下这些符号前面加上反斜杠来帮助插入普通的符号：
  \     *     #   {}   `  _ 
 ``` bash
$ 语法: \*   \#
```

### 字符也要转换。比如你要链接到：
1 在 HTML 文件中，有两个字符需要特殊处理： ***   < 和 &    ***
如果你只是想要显示这些字符的原型，你必须要使用实体的形式。
  ``` bash
$ 像是 &lt;和 &amp;
```
2 http://images.google.com/images?num=30&q=larry+bird
你必须要把网址转换写为：
  ``` bash
$  http://images.google.com/images?num=30&amp;q=larry+bird
```


### 文字加粗  
- **该文字是粗体** 
  ``` bash
$  加粗字体使用两个*或者一个_包起来
```

### 单行代码块   
`Hellow  word`  
``` bash
$  单行代码块使用符号 `包起来  
```

### 多行代码块使用符号
```  
		Hellow  word
		Hellow  word
		Hellow  word
```
``` bash
$   多行代码块使用符号  ``` 包起来  
```

### 这是引用的文字    
``` bash
$  引用的文字前面加> 
```

### 链接
``` bash
$  语法：[你要显示的文字](链接的地址)
     例如：[简书](http://www.jianshu.com)
```

### 插入图片
``` bash
$  语法：[站外图片上传中……(1)]
     例如：[站外图片上传中……(2)]
     注：当想插入本地图片时，直接将图片拖入你要放的位置*
```
### 有序列表
``` bash
$  语法：直接输入数字加空格
     例如：1 是有序1
```

### 无序列表
``` bash
$  语法：直接-加空格或者*
```

### 使用标题栏
``` bash
$  语法：# 这是 H1  ea210b
        ## 这是 H2
        ###### 这是 H6
```

### Github为文章增加多个categories和tags
``` bash
$  语法：categories:
         - hexo
         - mardDown
         tags:
         - Github
         - tags
```

### Github为文章增加多个html
```html
<span class="duoshuo-count"></span>
```
``` bash
$  语法：
	```html
	<!-- 这是代码中注释  -->
	<span class="duoshuo-count  2da7cc"></span>
	```
```



### Github为文章增加多个json
```json
{
    "data": {
        "message": "json",
    },
    "erroe": "0",
}
```
``` bash
$  语法：
	```json
{
    "data": {
        "message": "json",
    },
    "erroe": "0",
}
```





