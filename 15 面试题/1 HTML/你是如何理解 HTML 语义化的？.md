# 你是如何理解 HTML 语义化的？

## HTML是什么？

HTML定义了网页内容的含义和结构。它使用“标记”来注明文本、图片、和其它内容，以便在web浏览器中显示， 其中标记是指标签。

- 使用正确的标签标记内容，使机器和人们易于理解
- 语义化标签有利于提高SEO的效率

因为html的历史因素，标签使用混乱，通常是div+span的方式，HTML5中新元素可以让前端工作者正确定义标签。



### header

用于展示介绍性内容，比如Logo，搜索框，作者名称等等

### footer

章节内容或者根节点的页脚。通常包含章节作者，版权数据或者相关链接

### article

表示文档、页面、应用或网站中的独立结构，可独立分配或可复用的结构

- 标题作为子元素
- 元素嵌套使用，则该元素代表与外层元素有关的文章，博客评论的元素嵌套在博客文章的元素
- 作者信息通过`address`提供，但适合嵌套
- 发布日期和时间：`time ` `datetime`

### aside

表示一个和其余页面内容几乎五官的部分，被认为是独立于该内容的一部分并且可以被单独拆分出来而不会使整体受影响，常见为侧边栏或者标注框。

### nav

表示页面的一部分，提供导航链接，常见示例：菜单，目录，索引

```html
<nav>
  <ul>
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```



### section

表示一个包含在文档中的独立部分

```html
<section>
  <h1>Heading</h1>
  <p>Bunch of awesome content</p>
</section>
<section>
  <h2>Heading</h2>
  <img src="bird.jpg" alt="bird">
</section>
```



### audio

在文档中嵌入音频内容

### video

嵌入媒体播放器

