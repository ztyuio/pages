---
toc: true
comments: true
categories: [Jekyll]
---



# 使用fastpages模板过程中遇到的一些问题



## Search页面读取不到相应的JS文件：

> ERROR '/assets/js/vendor/lunr.min.js' not found.
> ERROR '/assets/js/search.js' not found.
> ERROR '/assets/js/vendor/lunr.min.js' not found.
> ERROR '/assets/js/search.js' not found.

### 解决办法

在search.html中找到了引用js的代码

```js
<script src="/assets/js/vendor/lunr.min.js"></script>
<script src="/assets/js/search.js"></script>
```

地址直接引用导致找不到，在地址之前加上\{\{ site.baseurl \}\}

之后Search页面可以成功读取到Js文件。

## Search页面搜索功能很奇怪：

1. 只支持英文检索

2. 搜索获得的页面因为permalink设置的关系，跳转不正确

没有修改之前跳转的地址是

> http://localhost:4000/jekyll/Jekyll-Error.html

​		实际文档的（permalink默认地址）是

> http://localhost:4000/pages/jekyll/Jekyll-Error.html

​	缺了一个{ site.baseurl }

由此可知（0208）前两天更新的这个Search的作者没有考虑到baseurl的问题。

### 解决办法

找到search.js，有几个地方有代码

> "url": "\{\{ site.url \}\}\{\{ page.url \}\}"

在其中插入了 \{\{ site.baseurl \}\} 

(这里因为有双引号所以在原始文档加上了反斜杠进行转义)

> "url": "\{\{ site.url \}\}\{\{ site.baseurl \}\}\{\{ page.url \}\}"

最后在Search页面得到了想要的结果。

### 待解决

lunr.js 的中文检索。

