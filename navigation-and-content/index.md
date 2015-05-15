# 实现导航和页面内容

# 导航布局的实现思路

我们需要做出这个效果：

![](nav.jpg)

1. 4 个链接在同一行显示；
2. 4 个链接的内容居中显示。

挺简单的。套用第一节课介绍的居中方法，我们可以这么做：

1. 把每个链接变成 inline 元素
2. 把容器设定为 `text-align: center`

# 混淆语义和样式

有了实现思路，就可以开始写代码啦！这时候新手常常会犯一个错误，在编写 HTML 的时候以样式为出发点来决定用什么元素:

+ 导航容器是个块元素，那用 `div` 啦~
+ 链接应该是行元素，那用 `span` 就可以啦~
+ 链接要用大写，那就用大写呗~

```html
<div class="nav">
  <span class="nav__item"><a href="#">WORK</a></span>
  <span class="nav__item"><a href="#">EXPERIENCE</a></span>
  <span class="nav__item"><a href="#">PHOTOS</a></span>
  <span class="nav__item"><a href="#">CONTACT</a></span>
</div>
```

Naive！

![](naive.jpg)

# HTML 语义

在编写 HTML 的时候我们需要先了解模块在页面中的职能（即语义），然后依据各个模块的职能来选择合适的元素：

1. 导航模块应该使用 `nav`
2. 文章模块就应该使用 `article`
3. 头部模块应该使用 `header`
4. 无编号列表模块应该使用 `ul`

HTML5 引入了一系列的语义标签，如 header, article, section, header, nav, 等等。

在编写主导航的时候我们应该这么分析：

+ 主导航这个容器应该用 nav
+ 容器里面有个列表，用 ul
+ 每个链接放在个别的条目 li 里面

主导航的 HTML：

```html
<nav class="main-nav">
  <ul>
    <li><a href="#">Work</a></li>
    <li><a href="#">Experience</a></li>
    <li><a href="#">Photos</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```

注意，虽然设计里链接的文字都是全大写的，我们编写的 HTML 它们应该是用常规的写法。这是因为 “全大写” 是样式范畴，而非文本语义的范畴。

你可能觉得这边用 div 还是用 nav 没什么差别，但用了 ul 好像更麻烦了一点。列表的默认风格是这样的：

![](nav-as-list.jpg)

我们需要:

+ 消除列表本身的默认间隔
+ 消除列表条目的默认风格
+ 把列表条目编程行元素

为什么要这么蛋疼？遵照 HTML 语义有什么好处呢？

1. 分离内容和页面的表现方法。

  假如我们要把导航改成垂直的菜单，不需要去修改 HTML 把 span 变成 div
2. 看到一个 nav 就知道是导航，不需要去看它的风格。方便和别的前端工程师协作。

对于模块语义的理解不同人会不一样，比如导航内的 4 个链接并不一定非要认为是一个无编号列表，也可以简单地将他们看做 4 个 `a` 标签的堆叠，从而对应的代码为：

```html
<nav class="main-nav">
  <a href="#">Work</a>
  <a href="#">Experience</a>
  <a href="#">Photos</a>
  <a href="#">Contact</a>
</nav>
```

但总体上使用的标签不能和语义本身偏离太多。语义 HTML 就好像代码缩进，虽然对页面实现来说没有太大的差别，但不用的结果会令人看起来浑身不舒服。

总结我们上面说说的，在实现页面中的一个模块的时候我们可以分成以下几个步骤：

1. 了解模块在页面中的职能（语义）；
2. 编写 HTML 代码；
3. 观察模块的布局特点；
4. 编写 CSS 代码。

### HTML5 语义标签的浏览器支持

+ [Can I Use: Semantic Elements](http://caniuse.com/#search=semantic)

IE8 虽然不支持，但我们引用的 normalize.css [解决了这个问题](https://github.com/necolas/normalize.css/blob/2bdda84272650aedfb45d8abe11a6d177933a803/normalize.css#L33-L60)。

Dive Into HTML5 有对 [语义 HTML 深入的介绍](http://diveintohtml5.info/semantics.html)。

# 实现主导航

我们现在就来来实现导航的风格。

![](nav.jpg)

1. 4 个链接在同一行显示；
2. 4 个链接的内容居中显示。

每当你有一系列相关的模块，你通常会把它们放在一个列表里面。通常我们需要去覆盖列表的默认风格。这是一个很常见的技巧。

Bootstrap 很多组件都是这样实现的。比如：

[分页](http://getbootstrap.com/components/#pagination-default)

```html
<ul class="pagination">
  <li>
    <a href="#" aria-label="Previous">
      <span aria-hidden="true">&laquo;</span>
    </a>
  </li>
  <li><a href="#">1</a></li>
  <li><a href="#">2</a></li>
  <li><a href="#">3</a></li>
  <li><a href="#">4</a></li>
  <li><a href="#">5</a></li>
  <li>
    <a href="#" aria-label="Next">
      <span aria-hidden="true">&raquo;</span>
    </a>
  </li>
</ul>
```

[面包屑](http://getbootstrap.com/components/#breadcrumbs)

```html
<ol class="breadcrumb">
  <li><a href="#">Home</a></li>
  <li><a href="#">Library</a></li>
  <li class="active">Data</li>
</ol>
```

[垂直菜单](http://getbootstrap.com/components/#dropdowns)

```html
<ul class="dropdown-menu" role="menu" aria-labelledby="dropdownMenu1">
  <li role="presentation"><a role="menuitem" tabindex="-1" href="#">Action</a></li>
  <li role="presentation"><a role="menuitem" tabindex="-1" href="#">Another action</a></li>
  <li role="presentation"><a role="menuitem" tabindex="-1" href="#">Something else here</a></li>
  <li role="presentation"><a role="menuitem" tabindex="-1" href="#">Separated link</a></li>
</ul>
```

### CSS 设计模式 - 去除列表的风格

[去除列表的风格 Demo](demo/override-lists.html)

![](demo-override-lists.jpg)

**HTML**:

```html
<h1>Unstyled list with block items</h1>

<ul class="nostyle">
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
</ul>

<h1>List with inline items</h1>

<ul class="nostyle inline-items">
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
</ul>
```

**CSS**:

```css
ul.nostyle {
  list-style: none;
  padding: 0;
  margin: 0;
}

ul.inline-items li {
  display: inline;
}
```

**实现原理**：

+ `list-style: none;` 把列表装饰去掉
+ `padding: 0; margin: 0;` 把浏览器默认的间隔清除

`li` 默认是块元素。需要元素在同行显示的话记得把它们变成行元素:

+ `display: inline`

### 练习 - 实现主导航

我们把比较繁琐的的设计风格写好了，布局就看你的啦！

![](nav-before-layout.jpg)

```css
.main-nav {
  background-color: #333;
}

.main-nav ul li {
  margin: 15px 10px;
}

.main-nav ul li a {
  color: #fff;
  font-weight: 300;
  font-size: 0.9rem;
  text-transform: uppercase;
  text-decoration: none;
}

.main-nav ul li a:hover {
  text-decoration: underline;
}
```

实现的过程中你可能会发现左右边距变化了，而上下边距不生效：

![](nav-with-inline-items.jpg)

这是因为 inline 元素只能设置其左右内边距和外边距，而不能设置其高度和上下内外边距。和垂直高度有关的 padding, margin, height 都无效。

这时可以使用 `display: inline-block`。`inline-block` 元素可以简单理解为对外表现为行元素，而对内表现为块元素。

+ 上下 padding, margin 有效
+ 容器的 text-align 会对它居中

结果：

![](nav.jpg)