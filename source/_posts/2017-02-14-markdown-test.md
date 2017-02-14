---
title: Hexo  的 markdown 测试
date: 2017-02-14 16:55:58
tags: [markdown]

---
## hexo 的 markdown 测试
测试!!!

### 三级标题
asdfsadfsd
#### 四级标题
asdfsdaf

<!-- more -->
<!--
上面这个 more 表示前面的部分会在列表页作为 简介 的内容来显示
下面的部分只会在内容页显示
-->

*斜体* 或 _斜体_
**粗体**
***加粗斜体***
~~删除线~~

|学号|姓名|分数|
|-|-|-  |
|小明|男|75|
|小红|女|79|
|小陆|男|92|

- 无序列表项 一
- 无序列表项 二
- 无序列表项 三

1. 有序列表项 一
2. 有序列表项 二
3. 有序列表项 三

```javascript
console.log('hello hexo!');
```

链接: [github](https://github.com)

<!--
https://hexo.io/zh-cn/docs/asset-folders.html
在配置文件中将 post_asset_folder 设置为 true, 这样用命令新建文章的时候, 也会创建一个同名的文件夹, 可以用来存放图片
然后我们就可以直接使用 文件名 , hexo 会自动对应到 资源文件夹 里的图片
-->
图片测试:
![郁金香](郁金香.jpg)
