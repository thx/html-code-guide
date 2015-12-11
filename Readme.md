<p align="center">
  <a href="http://thx.github.io/" target="_blank">
    <img src="http://gtms01.alicdn.com/tps/i1/TB12df6KpXXXXbfXpXXysQpFXXX-140-50.png" alt="THX Logo">
  </a>
</p>

<h1 align="center">HTML Code Guide <br></h1>

> HTML 编写指南

<dl>
  <dt>编辑：</dt>
  <dd>[壹丝](https://github.com/yisibl)</dd>
  <dt>反馈：</dt>
  <dd>[Issue](Issue)</dd>
  <dt>最后更新：</dt>
  <dd>2015-11-27</dd>
</dl>

<p>Copyright © 2015 THX</p>

----


## 前言

HTML 作为网页内容承载的基石，是每个前端都会用到的语言。在开发过程中保持一致的编码风格尤为重要，
使其能够更加容易理解和维护。

----

## Head

### [强制]使用 HTML5 DOCTYPE。

```html
<!DOCTYPE html>
```

### [强制]使用无 BOM 信息的 UTF-8 编码。

* `<meta charset="UTF-8">` 必须是 `head` 的第一个子元素。
* 包括空格和 DOCTYPE 声明在内，要在前512个字节以内。

详见：[HTML5 Charset能用吗？](http://www.qianduan.net/html5-charset-can-it/)

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        ...
    </head>
    <body>
        ...
    </body>
</html>
```

### [强制]在`head` 中添加 `title` 标签

### [强制]优先使用 IE 最新版本。

```html
<meta http-equiv="X-UA-Compatible" content="IE=edge">
```


### [推荐]使用更加标准的 lang 属性值 http://zhi.hu/XyIa。

简体中文：

```html
<html lang="zh-cmn-Hans">
```

繁体中文：

```html
<html lang="zh-cmn-Hant">
```

很少情况才需要加地区代码，通常是为了强调不同地区汉语使用差异，例如：

```html
<p lang="zh-cmn-Hans">
<strong lang="zh-cmn-Hans-CN">菠萝</strong>和<strong lang="zh-cmn-Hant-TW">鳳梨</strong>其实是同一种水果。只是大陆和台湾称谓不同，且新加坡、马来西亚一带的称谓也是不同的，称之为<strong lang="zh-cmn-Hans-SG">黄梨</strong>。
</p>
```

如果是个人编写的页面可以带上个人后缀，比如 HTML5 规范主要是由 Ian Hickson 来编写的，首页的 `lang` 写法为：

```html
<html lang="en-US-x-Hixie">
```


### [推荐]省略`link`，`style`，`script`标签中的 type 属性。

因为 `text/css` 和 `text/javascript` 分别是它们的默认值。

```html
<link rel="stylesheet" href="index.css">
<style>

</style>
<script src="index.js"></script>
<script>

</script>
```

参考 HTML5 规范：

  * [Using link](http://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-link-element)
  * [Using style](http://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-style-element)
  * [Using script](http://www.w3.org/TR/2011/WD-html5-20110525/scripting-1.html#the-script-element)

### [建议] 在 head 中引入页面需要的所有 CSS 资源。

### [建议] JavaScript 应当放在页面末尾（也就是`</body>`之前），或采用异步加载。

```html
<body>
    ...
    <script src="foo.js"></script>
</body>
</html>
```


### [建议] 移动页面或无需兼容 IE8 以下的页面省略资源协议。

使用[协议相对 URL](http://paulirish.com/2010/the-protocol-relative-url/)（Protocol-relative URL）引入 CSS，在 IE7/8 下，会发两次请求。是否使用应充分考虑页面针对的环境。

```html
<link rel="stylesheet" href="//g.alicdn.com/??tb/global/3.5.28/global-min.css,tb-page/tbindex/1.2.9/index-min.css">
...
<script src="//g.alicdn.com/??kissy/k/1.4.14/seed-min.js,tb/global/3.5.28/global-min.js"></script>
```


### [推荐]添加 `viewport`。

* 条件允许，可以配合 CSS @media 来适配移动页面。
* 不使用 `user-scalable=no`，因为这会导致页面始终无法放大，给视障用户或其他特殊情况下的用户造成不便。
* 不使用 `width=device-width`，因为这会导致 iPhone 5 添加到主屏后以 WebApp 全屏模式打开页面时出现[黑边](http://bigc.at/ios-webapp-viewport-meta.orz)。

  ```html
  <meta name="viewport" content="initial-scale=1, maximum-scale=1, minimum-scale=1">
  ```

### [可选]添加 favicon icon。

```html
<link rel="shortcut icon" type="image/ico" href="/favicon.ico">
```

更多用法：https://github.com/audreyr/favicon-cheat-sheet

----

### 通用模板

```html
<!DOCTYPE html>
<html lang="zh-cmn-Hans">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name ="viewport" content ="initial-scale=1, maximum-scale=1, minimum-scale=1">
  <meta name="format-detection" content="telephone=no">

  <title>Document</title>
  <link rel="stylesheet" href="index.css">
</head>
<body>

<script src="index.js"></script>
</body>
</html>
```


## 语法

### 缩进与换行

保持统一的代码缩进风格，有利于代码的阅读，也可以避免在 Git 等版本管理工具中造成冗余的 diff 信息。最重要的是千万不要空格和制表符（TAB）混用。

* [强制]使用2个空格为1次缩进，不得使用表符（TAB）缩进。
* [强制]嵌套元素应该缩进1次。
* [强制]使用 Unix 风格换行符（LF），保证跨平台的一致性。
* [推荐]删除行尾多余的空格。
* [推荐]每行不超过 80 个字符。  
可在编辑器中进行配置，例如 Sublime Text 中可以在配置文件中添加：

  ```config
  "rulers": [80],
  "word_wrap": true,
  "wrap_width": 80,
  ```

* [强制]项目的根目录必须包含 `.editorconfig` 文件，且当前使用的编辑器必须安装该插件，以此来
保证跨平台，跨编辑器的缩进与换行一致。推荐配置如下：

  ```config
  # editorconfig.org
  root = true

  [*]
  charset = utf-8
  indent_style = space
  indent_size = 2
  end_of_line = lf
  trim_trailing_whitespace = true
  insert_final_newline = true
  ```

更多参考：[如何保证统一的缩进风格？](https://github.com/cssdream/css-creating#1-如何保证统一的缩进风格)

### 标签

* [强制]使用小写标签名、属性名。
* [强制]使用双引号定义属性值，因为绝大多数 JS 编码规范中使用单引号来定义字符串。
* [强制]不在自闭合（self-closing）元素的尾部添加斜线，因为 HTML5 规范中明确说明这是可选的。
* [强制]不要省略可选的结束标签（closing tag），省略会不利于代码的维护。例如 `<li>`，`<p>`


## 语义化

HTML5 中对 HTML4 中的一些标签重新定义或修改了语义。

### <code class="external"><a href="http://www.w3.org/TR/html5/single-page.html#the-dl-element">dl</a></code> 元素

现在代表一组名称与值的关联列表，并且不再适用于聊天和对话。

* [推荐]定义术语（可以是多条术语，单条描述）：

  ```html
  <dl>
    <dt>Firefox</dt>
    <dt>Mozilla Firefox</dt>
    <dt>Fx</dt>
    <dd>
      <p>是一个自由及开源的网页浏览器，由 Mozilla 基金会及其子公司 Mozilla 公司开发。</p>
      <p>Firefox 被认为是 Netscape Navigator 的精神续作，因为 Netscape 于1998年被 AOL 收购前创建了 Mozilla 社区。</p>
    </dd>
  </dl>
  ```

* [推荐]文档的编辑信息：

  ```html
  <dl>
    <dt>编辑：</dt>
    <dd>[壹丝](https://github.com/yisibl)</dd>
    <dt>反馈：</dt>
    <dd>[Issue](Issue)</dd>
    <dt>最后更新：</dt>
    <dd>2015-11-13</dd>
  </dl>
  ```

* [推荐]FAQ 通常也适合使用 dl 元素。

  ```html
  <article>
   <h1>开店常见问题（FAQ）</h1>
   <dl>
    <dt>淘宝开店收费吗？</dt>
    <dd>目前在淘宝集市开店为免费，但为保障消费者利益，开店成功后部分类目需缴纳一定额度的消保保证金。</dd>
    <dt>如何修改淘宝会员名？</dt>
    <dd>亲，淘宝江湖，行不改名坐不改名姓，一旦注册成功将无法修改哦~</dd>
   </dl>
  </article>
  ```

**注意**：HTML5 中曾短暂的使用 `dialog` 元素来标记对话，但后来被废除了。现在纯粹的对话[推荐](http://www.w3.org/TR/html5/common-idioms.html#conversations) `p` 元素与标点符号搭配使用。

```html
<p> Costello: Look, you gotta first baseman?
<p> Abbott: Certainly.
<p> Costello: Who's playing first?
<p> Abbott: That's right.
<p> Costello becomes exasperated.
<p> Costello: When you pay off the first baseman every month, who gets the money?
<p> Abbott: Every dollar of it.
```

### <code class="external"><a href="http://www.w3.org/TR/html5/single-page.html#the-b-element">b</a></code> 元素

HTML4 中`b`元素只是一个用于将文本显示为粗体的表现性元素（presentational elements）。

HTML5 中代表一段文本，这段文本仅仅出于功利的目的被提请注意，这种目的里**没有传达任何额外的重要性**，也没有交替的语言和心情的意味，比如文档摘要的关键字，审查中的产品名，文本驱动的交互软件的可操作词，或文章的导引。

示例：

```html
<p>The <b>frobonitor</b> and <b>barbinator</b> components are fried.</p>
```

不正确的用法（应该使用 `strong` 元素）：

```html
<p><b>警告：</b> 不要将瓶子倒立放置!</p>
```


### <code class="external"><a href="http://www.w3.org/TR/html5/single-page.html#the-i-element">i</a></code> 元素

HTML4 中`i`元素只是一个用于将文本显示为斜体的表现性元素，很像`b`标签被用来将文本显示为粗体。

但 HTML5 中赋予了新的语义，用来表示一段有着交替的语言和心情意味的文本，或者用来表明一种不同的文本质量的方式偏离平常的散文，比如分类命名，技术术语，其它语言的惯用短语，一个念头，画外音，或西文的船名。

> 音调或情绪变化？

* [推荐]标记一个惯用短语：

  ```html
  <p>拉丁文 <i>Veni, vidi, vici</i> 经常在音乐、艺术、文学中被提到。</p>
  ```

* [推荐]标记一个船名：

  ```html
  <p><i>RMS Titanic</i> 是一艘奥林匹克级邮轮，于1912年04月处女航时撞上冰山后沉没。</p>
  ```


**注意：** `i` 元素并不是 `icon` 的意思，标记字体图标（iconfont）时应该使用 `span` 元素。


### 小结

HTML5 中重新定义了 `b` `i` 等元素，使其具有一定的语义，而不仅仅是表现性的（[W3C 文章](http://www.w3.org/International/questions/qa-b-and-i-tags)）。

无论如何，我们应当牢记，不应该使用 `b` 或 `i` 来实现加粗或倾斜的样式。

* [推荐] 只有在没有更适合的文本元素时，才使用 `b`, `i` 元素。例如：

  * `em` 可以表示强调或重读。
  * `strong` 可以表示重要性。
  * `mark` 可以表示相关性。
  * `cite` 可以标记著作名，如一本书、剧本或是一首歌。
  * `dfn` 可以标记术语的定义实例。
  * `var` 可以标记数学变量。

----

### <code class="external"><a href="http://www.w3.org/TR/html5/single-page.html#the-strong-element">strong</a></code> 元素

HTML4 中表示强烈的强调。

HTML5 中表示强烈的重要性、严重性或内容的紧迫性。`strong` 不会改变所在句子的语意，`em` 则会改变所在句子的语义。


示例：

「第一章」仅仅是个引用，`strong`` 里的内容才是真正的章节名。

```html
<h1>第一章 <strong>启程</strong></h1>
```

这里 `strong` 是为了和其他内容区分开来。

```html
<figure>
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a4/Ggb_by_night.jpg/1280px-Ggb_by_night.jpg">
  <figcaption>图1 <strong>金门大桥夜景</strong>。左方远处是旧金山市区。</figcaption>
</figure>
```


```html
<h1><strong>松树、枫树、桦树</strong>和其他我叫不出来名字的树木，郁郁葱葱的长满了屋后的山坡。</h1>
```


### <code class="external"><a href="http://www.w3.org/TR/html5/single-page.html#the-s-element">s</a></code> 元素

现在标示内容不再准确或不再有关联。


### <code class="external"><a href="http://www.w3.org/TR/html5/single-page.html#the-s-element">figure</a></code> 元素

不仅仅是用来标记图片，可以是音频、视频、代码、引用、表格等。而且只有当这些内容属于文档一部分时，才应该使用 figure 元素包裹起来。

## 可访问性

* [推荐] 重要的 `img` 标签添加有意义的 `alt` 属性文案。
* [推荐] 移动页面可以根据内容类型指定相应的 `input` type 属性（截图来自 iOS 9.1 Safari）。

```html
  <input type="number" placeholder="number">
```

<img src="http://gtms01.alicdn.com/tps/i1/TB1fgPGKFXXXXXfXVXXLIffVVXX-640-1136.png" width="320" alt="number">

**注意**：iOS 第三方输入法（如百度拼音）呼出 `number` 时为全键盘样式，所以如果是输入验证码等纯数字场景推荐使用 `tel`。

```html
  <input type="tel" placeholder="tel">
```

<img src="http://gtms02.alicdn.com/tps/i2/TB1HEDRKFXXXXb9XpXXLIffVVXX-640-1136.png" width="320" alt="tel">



```html
<input type="email" placeholder="email">
```

<img src="http://gtms03.alicdn.com/tps/i3/TB1bZnPKFXXXXchXpXXLIffVVXX-640-1136.png" width="320" alt="email">


**注意**：iOS 自带的拼音九宫格输入法无法呼出 email 键盘样式。


```html
<input type="url" placeholder="url">
```

<img src="http://gtms04.alicdn.com/tps/i4/TB1LmPKKFXXXXbwXFXXLIffVVXX-640-1136.png" width="320" alt="url">


```html
<input type="date" placeholder="date">
```

<img src="http://gtms01.alicdn.com/tps/i1/TB1g6_5KFXXXXX8XXXXLIffVVXX-640-1136.png" width="320" alt="date">


更多：

* http://quirksmode.org/html5/inputs/mobile.html
* http://mobileinputtypes.com/


## [废弃的元素](http://www.w3.org/TR/html5/obsolete.html#non-conforming-features)

以下元素不在HTML5 规范内，因为它们是纯粹表象（样式）的元素，应该使用 CSS来代替。

* `basefont`
* `big`
* `blink`
* `center`
* `font`
* `marquee`
* `multicol`
* `nobr`
* `spacer`
* `tt`

以下元素不在HTML5 规范内，因为使用它们会破坏可用性和可访问性。

* `frame`
* `frameset`
* `noframes`

以下元素很少被使用，因为他们容易造成混淆，或者它们的功能能被其他元素处理。

<dl>
  <dt><dfn><code>acronym</code></dfn></dt>
  <dd>因为它造成了大量的混淆，可以使用 abbr 表示缩写。</dd>
  <dt><dfn><code>dir</code></dfn></dt>
  <dd>使用 ul 代替。</dd>
  <dt><dfn><code>applet</code></dfn></dt>
  <dd>使用 embed 或 object 代替。</dd>
  <dt><dfn><code>hgroup</code></dfn></dt>
  <dd>使用 header 或 div 来分组</dd>
</dl>

## [废弃的属性]()

绝大部分 HTML4 中控制样式的属性都被废除，例如 `align`, `valign`, `bgcolor` 等。

以下这些属性允许使用，但是不鼓励Web开发者使用它们，而是强烈鼓励使用替代的解决方案:

* img 的 border 属性。如果存在其值必须是"0"。Web开发者可以使用CSS代替。

* script 的 language 属性。如果存在其值必须是"JavaScript"(不区分大小写)，并且不能与 type 属性冲突。作者可以简单地忽略它，因为它没什么作用。

* a 的 name 属性。Web开发者可以使用 id 属性代替。

更多参考：http://www.w3.org/TR/html5/obsolete.html#non-conforming-features



## SEO 优化

### [可选]添加页面描述

提供网页的简短说明。在某些情况下，此说明会被用作搜索结果中显示的一部分网页摘要。

```html
<meta name="description" content="">
```

### [可选]添加网页作者

```html
<meta name="author" content="name, email@gmail.com">
```

### [可选]添加网页搜索引擎索引方式

可以控制搜索引擎的抓取和索引编制行为，指定多个值时，请使用英文逗号进行分隔，通常有如下几种取值：none，noindex，nofollow，all，index 和 follow。默认值是`index, follow`（相当于`all`），不需要进行指定。

```html
<meta name="robots" content="noindex,follow">
```

更多：https://support.google.com/webmasters/answer/79812?hl=zh-Hans&ref_topic=4617741
