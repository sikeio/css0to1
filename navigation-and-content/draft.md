•••••

![](DraggedImage-4.png)

首先对于导航模块，需要使用 `nav` 标签。而导航内部有五个链接，这五个链接可以看做一个无编号列表。所以可以很容易地编写出对应的 HTML 代码：

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

不过对于模块语义的理解不同人会不一样，比如导航内的五个链接并不一定非要认为是一个无编号列表，也可以简单地将他们看做五个 `a` 标签的堆叠，从而对应的代码为：

```html
<nav class="main-nav">
<a href="#">Work</a>
<a href="#">Experience</a>
<a href="#">Photos</a>
<a href="#">Contact</a>
</nav>
```

但总体上使用的标签不能和语义本身偏离太多。

{If we use <a>, we can avoid the annoying list styling removal... but list is a very common technique, so maybe let's use it.}

，如这里使用 `footer` 标签肯定是不好的。

另外新手容易滥用 `div` 标签，需要注意的是只有模块本身没有明确的语义或者用现有的标签无法准确描述其语义时才应使用。

前文说过非常容易犯的错误是把语义和样式混淆，对应到这里的例子就是图中链接的文字都是全大写的，而我们编写的 HTML 标签应该是用常规的写法。这是因为“全大写”是样式范畴，而非文本语义的范畴。

区分某个效果是否是样式范畴的方法很简单：设想你准备给这个网站改版换个样式，那么这个效果会不会随着改版而改变呢？很容易知道，当网站改版时，这个导航中的文字很可能又恢复成首字母大写，所以这个效果属于样式范畴。

至于如何使用 CSS 来实现文本的大小写变换就留个同学们自行查阅了。

有了 HTML 代码，接下来我们就可以观察模块的样式并实现对应的 CSS 了。我们先来概括主导航条的布局特点：

1. 4个链接在同一行显示；
2. 4个链接的内容居中显示。

这里以第一份 HTMl 为准。首先4个链接在同一行显示，我们很容易想到可以通过行元素或者浮动元素实现，而我们使用的 `li` 元素是块元素，所以我们要设置其 `display` 属性为 `inline` 来使其成为行元素。接下来居中的实现方法大家应该已经知道，这里就不再赘述了。

只需要注意的是 `ul` 元素默认会有 `list-style` 和 `margin`, `padding`，记得清除即可。最后效果如下：

其余的样式修改比较简单，大家可以自己动手试试。

![](DraggedImage-5.png)

这时我们发现导航条的内容没有内边距，给 `li` 加上 `padding: 10px` 后发现只有左右边距变化了，而上下边距依然没有。这是因为行元素只能设置其左右内边距和外边距，而不能设置其高度和上下内外边距。如果想设置高度的话就要使用块元素了，但块元素没有办法实现整体居中效果。这时可以使用 `inline-block`，`inline-block` 元素可以简单理解为对外表现为行元素，而对内表现为块元素。这样问题就迎刃而解了，效果如下：

![](DraggedImage-6.png)

具体的字号字体会和目标页面不太一样，如果大家有兴趣可以认真模仿下。CSS 中最难的部分不在于字号、阴影这样的样式，而在于布局的方法，这也是这篇教程主要想介绍的。

## 第六步 实现小节

接下来我们来实现页面下面的部分。还是按照第五步介绍的流程，可以看到接下来是由很多结构和职能相似的模块组成，对于这样有内在相关性的内容，我们可以使用 `section` 来实现。`section`、`div` 和 `article` 的差别可以参见 [HTML5 中 div section article 的区别](http://www.qianduan.net/html5-differences-in-the-div-section-article/)。
我们以第一个小节为例：

![](DraggedImage-7.png)

页面顶部是一个标题、一个分隔符和一个描述。可以使用如下 HTML 实现：

```html
<section class="info-section whatido">
<header>
<h2>What I Do</h2>
<p class="info-section__description">I'm Teng. I design and develop things on the web. Oh, and I like curry.</p>
</header>
<ul class="whatido__skill-list">
<li>
<h3>Code</h3>
<p>I like building things on the web. I've built games, tools, and web apps.</p>
</li>
<li>
<h3>Design / UX</h3>
<p>I like creating happiness by making things look good and work well.</p>
</li>
<li>
<h3>Product</h3>
<p>I like taking products from idea to reality to users and beyond!</p>
</li>
</ul>
</section>
```

其中需要注意的：

1. 文字的拼写。虽然效果图中的文字都是全大写的，但是写在 HTML 里一定要根据实际的写法写（如 `Design/UX`）；
2. 合理的区域划分。标题和描述统一作为小节的头部用 `header` 包裹，这样更加利于模块的重用。

与模块重用紧密相关的另一个话题就是 CSS 样式命名，这里使用了 BEM 命名方法，会在之后的正式课程详细介绍。大家有兴趣提前了解的话可以简单参考：[BEM思想之彻底弄清BEM语法](http://www.w3cplus.com/css/mindbemding-getting-your-head-round-bem-syntax.html)。

另外标题下面的分隔符这里并没有占用单独的标签，因为分隔符属于样式范畴（想想改版时分隔符可能就会去掉），可以使用 `h2` 标签的 `:after` 伪元素来实现，这样可以使得 HTML 更加语义化。然而这只是理想化的实现方法，因为 `:after` 并不兼容所有浏览器（还记得怎么查看 CSS 的兼容性吗？），所以如果有兼容旧浏览器的要求，是可以使用一个单独的元素实现分隔符的，因为实现起来非常简单，这里不再介绍。

另外底下的三个技能可以使用 `float` 使其向左浮动起来，并设置每个元素的宽度为 `33.3%`。

但是有个问题是每个元素都有一个边距，如果设置边距的话宽度就会超过父元素的三分之一，这是因为边距的大小是算在宽度外的。这时可以使用 `box-sizing` 来解决这个问题，具体可以参考：[box-sizing](http://zh.learnlayout.com/box-sizing.html)。

接下来的内容就很简单了，几个元素的居中大家应该已经熟练掌握了。三个技能图片应该使用背景图片而非 `img` 元素。至于何时使用背景何时使用 `img` 元素，判断方法与上面的类似：思考改版时图片是否会改变。
