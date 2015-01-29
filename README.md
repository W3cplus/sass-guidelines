# Sass Guidelines中文版本

有一份规范的指南能协助您更理智的，更好维护和更好扩展Sass。

>Sass指南已经翻译成好几种语言，感谢这些[贡献者](https://github.com/HugoGiraudel/sass-guidelines/blob/gh-pages/_data/languages.yml)。你可以在控制面板中切换需要的语言。

##关于作者

我是[Hugo Giraudel](http://hugogiraudel.com)，一名即将迁居柏林的法国前端工程师。到目前为止，我已经使用Sass两年多了，并开发了一些与之相关的项目，比如:[SassDoc](http://sassdoc.com) 和 [Sass-Compatibility](http://sass-compatibility.github.io)。

我也写了几个关于Sass的库,主要是想把玩、探究它：[SassyJSON](https://github.com/HugoGiraudel/SassyJSON)、[SassyLists](http://sassylists.com)、[SassySort](https://github.com/HugoGiraudel/SassySort)、 [SassyCast](https://github.com/HugoGiraudel/SassyCast)、[SassyMatrix](https://github.com/HugoGiraudel/SassyMatrix)、 [SassyBitwise](https://github.com/HugoGiraudel/SassyBitwise)、[SassyIteratorsGenerators](https://github.com/HugoGiraudel/SassyIteratorsGenerators)、[SassyLogger](https://github.com/HugoGiraudel/SassyLogger)、[SassyStrings](https://github.com/HugoGiraudel/SassyStrings) 和 [SassyGradients](https://github.com/HugoGiraudel/SassyGradients)。

可以通过[Twitter联系我](https://twitter.com/HugoGiraudel)。

##贡献

Sass指南是我利用空暇时间维持的一个免费项目。不用多说,相信你也能够理解，持续更新、编写文档和其他相关事宜是一件工作量不小的事情。不过，知道你喜欢这个指南我已经很满足了。

现在，如果你想要为它做些贡献，一个很好的建议是：使用社交网络分享它，也可以在[GitHub repository](https://github.com/HugoGiraudel/sass-guidelines)上提交修正错误的issue或者pull-request。

在开始之前最后但不是最终的一句话：如果你喜欢这份样式指南，如果它对你或你的团队大有裨益，请考虑支持它！

[支持Sass指南](https://gum.co/sass-guidelines)、[分享Sass指南](https://twitter.com/share?text=Sass+Guidelines%2C+An+opinionated+styleguide+for+writing+sane%2C+maintainable+and+scalable+Sass+by+%40HugoGiraudel+%E2%80%93&url=http://sass-guidelin.es)

##关于Sass

[Sass](http://sass-lang.com)的[开发文档](http://sass-lang.com/documentation/file.SASS_REFERENCE.html)中如此描述自己：

>Sass是CSS的一个扩展,它使CSS的使用起来更加优雅和强大。

Sass的终极目标是解决CSS的缺陷。如我们所知，CSS并不是一个完美的语言。CSS虽然简单易学，却也能迅速制造严重的混淆，尤其是在工程浩大的项目中。

这就是Sass出现的契机，作为一种元语言，通过提供额外的功能和工具可以改善CSS的语法。同时，保留了CSS的原有特性。

Sass存在的关键不是将CSS变成一种全功能编程语言，它只是想修复缺陷。正因如此，学习Sass如同学习CSS一样简单：它只在CSS的基础上添加了几个额外功能。

话虽如此，使用这些功能的方式却是多种多样的。有一些是好的，有一些是坏的，还有一些令人费解。这份样式指南就是为了给你一个统一的和历经实践的方式来编写Sass代码。

####扩展阅读

- [Sass](http://sass-lang.com)
- [Sass documentation](http://sass-lang.com/documentation/file.SASS_REFERENCE.html)
- [Sass中文教程](http://www.w3cplus.com/blog/tags/302.html)

##Ruby Sass or LibSass

[Sass的第一次提交](https://github.com/hcatlin/sass/commit/fa5048ba405619273e474a50400c7243fbff54fe)还要追溯到距今八年之久的2006年底——可见它已经走过了一段漫长的道路。最开始是基于Ruby，随后便各种版本滋生。其中最成功的要属[LibSass](https://github.com/sass/libsass)（使用C语言编写），它与Ruby原生版本具有最佳兼容性。

在2014年， [Ruby Sass和LibSass团队决定同步推出下一个版本](https://github.com/sass/libsass/wiki/The-LibSass-Compatibility-Plan)。从那时起，LibSass开始积极释放版本以校验与Ruby Sass的不同，最后剩下的不一致之处被汇总在[Sass-Compatibility](http://sass-compatibility.github.io) 项目中。如果你知道两个版本中尚未被发现的不一致之处，请提交一个issue使更多开发者了解。

回到选择编译器的问题上来。实际上，这只取决于你。如果是在一个Ruby on Rails的项目中，最好使用Ruby Sass，它在这种情况下是最合适的。当然你也要知道，在未来Ruby Sass会一直引领LibSass的开发并作为其开发参考。

另一方面，LibSass更关注于自身与项目之间的整合。如果你想在非Ruby项目中使用，比如NodeJS，[node-sass](https://github.com/sass/node-sass) 会是个不错的选择。使用LibSass最主要的优势还是因为它的速度，而且比Ruby Sass更快。

####扩展阅读

- [LibSass](https://github.com/sass/libsass)
- [Sass-Compatibility](http://sass-compatibility.github.io)
- [Switching from Ruby Sass to LibSass](http://www.sitepoint.com/switching-ruby-sass-libsass/)

##Sass或SCSS

有一个剧烈的争论关于**Sass**名字中的含义，并对此有充足的理由：Sass意味着一个预处理器和它独有的语法。这样很不方便，不是吗？

如你所知，Sass最初定义的语法，其中决定性的特征是缩进敏感。很快，Sass的维护者决定提供一个被称为**SCSS**（**Sassy CSS**）的语法以弱化Sass和CSS之间的差异。

从那时起，Sass（预处理器）开始提供两种不同的语法：Sass（非全大写，[please](http://sassnotsass.com)），也被称为**缩进语法**，和SCSS。使用哪一种语法完全取决于你，两者在功能上是完全等同的，只是在审美上有所偏颇。

Sass的空白敏感语法通过缩进以摆脱大括号、分号和其他符号，从而实现了简洁凝练的语法格式。与之相比，SCSS则更容易学习，因为它只是在CSS上添加了一点点额外的功能。

我自己更喜欢SCSS，因为它更接近CSS的原生面貌，对开发者来说具有友好性。因此，样式指南全文将使用SCSS而不是Sass语法格式来演示。

####扩展阅读

- [What's the difference between Sass and SCSS](http://www.sitepoint.com/whats-difference-sass-scss/)

##其他预编译器

忽略其他特性，Sass对自己的定位首先是一个预处理器。其最主要的竞争对手包括[LESS](http://lesscss.org/)，一个基于NodeJS的预处理器，因著名CSS框架[Bootstrap](http://getbootstrap.com/)的使用而声名鹊起。此外还有[Stylus](http://learnboost.github.io/stylus/) ，一种对形式无所限制的LESS版本。它是一种无论你想怎么样使用，大都能顺利转换成CSS的程序语言。

**为什么选择Sass胜过LESS以及其他预处理器？**，这始终是一个待解决的问题。就在刚刚，我们还建议在Ruby项目中使用Sass，因为Sass初创于Ruby并且在Ruby on Rails中运行良好。现在随着LibSass与Sass的逐步接近，上述建议显然已经不再绝对和必须。

我之所以喜欢Sass源于它最大程度保留了CSS的原生特性。Sass的设计基于非常坚实的设计原则：大部分的设计顺其自然的来源于核心设计师们的信条，比如添加额外的功能会增加语言的复杂度，但以实用性衡量极具价值的话便得以保留；同时，使用Sass来美化一个块级元素，那么美化前后的效果应该是可预见和可推理的。同时，Sass比其他预处理器更加关注细节。据我所知，核心设计者们非常关心Sass与CSS在细节上的一致性，并确保所有的常用方式具有高度一致的表现。

换言之，Sass并不想成为一个通过在编程语言顶层添加特殊功能实现有关用户逻辑处理的预处理器，以取悦于像我一样喜欢傻瓜式编程的程序员。它更准确的定位是一款软件，旨在解决实际问题。通过提供实用功能改善CSS的短板。

预处理器之外，我们还需要提及一下后处理器。得益于[postCSS](https://github.com/postcss/postcss)和[CSSNext](https://github.com/cssnext/cssnext)项目，后处理器最近几个月得到了显著曝光。后处理器几乎等同于预处理器，稍有不同的是它并不支持即将发布的CSS语法。

你可以认为预处理器是腻子脚本，用来支持尚未实现的CSS功能。举例来说，你可能会像[CSS 规范](http://dev.w3.org/csswg/css-variables/)中描述的一样使用变量，然后用预处理器编译样式表，在这个过程中后处理器只会找出变量出现的地方并替换成真实值——Sass就是这么做的。

后处理器背后的思维是，一旦浏览器支持了新的特性（比如CSS变量），后处理器就不再做这方面处理，而是让浏览器执行相关处理。

虽然在当下提供对未来语法功能的支持是一件很了不起的事情，但我还是喜欢在大多数的工作中使用Sass。当然，在一些情况下我认为后处理器比Sass更适合，比如CSS前缀。稍后我们会讲到这个问题。

####扩展阅读

- [LESS](http://lesscss.org/)
- [Stylus](http://learnboost.github.io/stylus/)
- [CSSNext](https://github.com/cssnext/cssnext)
- [postCSS](https://github.com/postcss/postcss)

##简介

###为什么需要一个样式指南?

一个样式指南并不是一份便于阅读并使代码处于理想状态的文档。它在一个项目的生命周期中是一份关键文档，描述了编写代码的方式和采用这样方式的原因。它可能在小项目中显得有些矫枉过正，但却能在保持代码库整洁，提高可扩展性和可维护性上提供诸多便利。

不用多说相信你也可以理解，参与项目的开发者越多，代码样式指南就越显的必要。与之相同，项目的规模越大，代码样式指南也会越加重要。

[Harry Roberts](http://csswizardry.com)的[CSS Guidelines](http://cssguidelin.es/#the-importance-of-a-styleguide)就非常好:

<blockquote>
    <p>样式指南（注意不是视觉风格指南）用于团队是一个很有价值工具：</p>
    <ul>
        <li>长时间内便于创建和维护项目</li>
        <li>便于不同能力的和专业的开发使用</li>
        <li>便于任何时间加入团队的不同开发人员</li>
        <li>便于新员工培训</li>
        <li>便于开发人员创建代码库</li>
    </ul>
</blockquote>

###免责声明

首先第一件事是：**这不是一份CSS样式指南**。本文档不会讨论诸如约定CSS类名、模块化开发模式和有关ID的疑惑等CSS范畴内的问题。本文档中的准则只着眼于处理Sass的专有内容。

此外，这份样式指南是我独创的，所以会显得有些**个人主观倾向**。你可以将它看成是我通过多年实践研究出的方法和建议的集合。这也让我有机会接触到少数极具见地的资源，所以一定要浏览一下**扩展阅读**。

显然，这里讲的肯定不是进行Sass编程的唯一方式，而且它是否符合你的项目要求还有待检验。你可以随意选择，并使其适应需求。正如我们所说的，**具体情况具体分析**。

###核心原则

最后，如果有一件事是我想从整个样式指南中传授的，那就是：**Sass以简为美，简约至上**。

感谢我过去使用Sass时傻傻的尝试，比如 [bitwise operators](https://github.com/HugoGiraudel/SassyBitwise)、[iterators and generators](https://github.com/HugoGiraudel/SassyIteratorsGenerators) 和 [a JSON parser](https://github.com/HugoGiraudel/SassyJSON)，从而认识到了可以用预处理器来做什么。

同时，CSS是一门简单的语言，那么Sass在书写常规CSS的时候就不应该更复杂。[KISS principle](http://en.wikipedia.org/wiki/KISS_principle) (Keep It Simple Stupid)在这里是一个核心原则，甚至在有些情况下要优先于[DRY principle](http://en.wikipedia.org/wiki/Don%27t_repeat_yourself) (Don't Repeat Yourself)。

有时候，一点点重复可以更好的保持代码的可维护性，而不是建立一个头重脚轻、臃肿复杂、不可维护的系统。

此外，请允许我再一次引用[Harry Roberts](https://csswizardry.com)的观点，**实用胜过完美**。有些时候，你可能会发现自己违背了这里所描述的规则。如果感觉自己的方式有道理，感觉很正确，那就继续做吧。编写代码从来都不是一家之言。

####扩展阅读

- [KISS principle](http://en.wikipedia.org/wiki/KISS_principle)
- [DRY principle](http://en.wikipedia.org/wiki/Don%27t_repeat_yourself)
- [Keep Sass Simple](http://www.sitepoint.com/keep-sass-simple/)

##语法格式

如果你问我一个样式指南首先要描述什么，我会告诉你：编写代码的通用准则。

当几个开发者在同一项目中编写CSS时，迟早会陷入各自为政的境地。编码样式指南通过规范统一的样式，不仅防止了这种混乱现象，也减轻了阅读和维护代码的难度。

概括地说，我们希望做到（受[CSS Guidelines](http://cssguidelin.es/#syntax-and-formatting)所启发）：

- 使用两个空格代表缩进，而不是使用tab键；
- 理想上，每行保持为80个字符宽度；
- 正确书写多行CSS规则；
- 有意义的使用空格。

```
// 推荐方式
.foo {
  display: block;
  overflow: hidden;
  padding: 0 1em;
}
// 不推荐方式
.foo {
    display: block; overflow: hidden;

    padding: 0 1em;
}
```

在本部分中不会涉及有关文件组织的问题，相关讨论在另一节中。

###字符串

CSS中不要求字符串必须用引号包裹，甚至是字符串中包含空格的。就拿`font-family`属性来说：无论你是否使用引号包裹，CSS解析器都可以正确解析。

因此，Sass**也不**强制要求字符串必须被引号包裹。更棒的是（你也会如此认为），被引号包裹和没被包裹的一对字符串完全等同（例如，`'abc'` 严格等同于 `abc`）。

话虽如此，不强制要求字符串被引号包裹的毕竟是少数，所以，在Sass中**字符串应该始终被单引号所包裹**（在**querty**键盘中单引号比双引号更容易输入）。即使不考虑与其他语言的一致性，单是考虑CSS的近亲JavaScript，也有数条理由这么做：

- 如果颜色名不被引号包裹，将会被解析为颜色值，显然这会导致严重问题；
- 大多数的语法高亮机制将会因未被引号包裹的字符串而罢工；
- 提高可读性；
- 没有正当理由不去用引号包裹字符串。

```
//推荐方式
$font-stack: 'Helvetica Neue Light', 'Helvetica', 'Arial', sans-serif;
//不推荐方式
$font-stack: "Helvetica Neue Light", "Helvetica", "Arial", sans-serif;
//不推荐方式
$font-stack: Helvetica Neue Light, Helvetica, Arial, sans-serif;
```

**注：**在前面的示例中，`sans-serif`并没有用引号`''`包裹起来，因为它是CSS指定的一样属性值，所以不需要使用引号包裹起来。

URL最好也用引号包裹起来，原因和上面所描述一样：

    // 推荐方式
    .foo {
      background-image: url('/images/kittens.jpg');
    }
    // 不推荐方式
    .foo {
      background-image: url(/images/kittens.jpg);
    }

####扩展阅读

- [All You Ever Need to Know About Sass Interpolation](http://webdesign.tutsplus.com/tutorials/all-you-ever-need-to-know-about-sass-interpolation--cms-21375)
- [SassyStrings](https://github.com/HugoGiraudel/SassyStrings)

###数字

在Sass中，数字类型包括了长度、持续时间、频率、角度等等无单位数字类型。Sass允许在运行中计算这些度量值。

####零值

当数字小于`1`时，应该在小数点前写出`0.`永远不要显示小数尾部的`0`。

    // 推荐方式
    .foo {
      padding: 2em;
      opacity: 0.5;
    }
    // 不推荐方式
    .foo {
      padding: 2.0em;
      opacity: .5;
    }

####单位

当定义长度时，`0` 后面不需要加单位。

    // 推荐方式
    $length: 0;
    // 不推荐方式
    $length: 0em;

在Sass中最常见的错误，是简单地认为单位只是字符串，认为它会被安全的添加到数字后面。这虽然听起来不错，但却不是单位正确的解析方式。可以把单位认为是代数符号，例如，在现实世界中，`5`英寸乘以`5`英寸得到`25`英寸。Sass也适用这样的逻辑。

将一个单位添加给数字的时候，实际上是让该数值乘以*`1`个单位*。

    $value: 42;
    // 推荐方式
    $length: $value * 1px;
    // 不推荐方式
    $length: $value + px;

需要注意的是加上一个*`0unit`*也可以正确解析，但是这种方式在某种程度上会造成一些混乱，所以我更愿意推荐上面的方式。事实上，将一个数字转换为其他兼容单位时，加`0`操作并不会造成错误。

    $value: 42 + 0px;
    // -> 42px
    $value: 1in + 0px;
    // -> 1in
    $value: 0px + 1in;
    // -> 96px

这一切最终取决于你想要达到怎样的效果。只要记住，像添加一个字符串一样添加一个单位并不是一种好的处理方式。

要删除一个值的单位，你需要除以*相同类型的`1`单位*。

    $length: 42px;
    // 推荐方式
    $value: $length / 1px;
    // 不推荐方式
    $value: str-slice($length + unquote(''), 1, 2);

给一个数值以字符串形式添加单位的结果是产生一个字符串，同时要防止对数据的额外操作。从一个带有单位的数值中分离数字部分也会产生字符串，但这些都不是你想要的。

####计算

**最高级运算应该始终被包裹在括号中**。这么做不仅是为了提高可读性，也是为了防止一些Sass强制要求对括号内内容计算的极端情况。

    // 推荐方式
    .foo {
      width: (100% / 3);
    }
    // 不推荐方式
    .foo {
      width: 100% / 3;
    }


####幻数

"幻数"，是<a href="http://en.wikipedia.org/wiki/Magic_number_(programming)#Unnamed_numerical_constants" >古老的学校编程</a>给*未命名数值常数*的命名。基本上，它们只是*能工作*™但没有任何逻辑思维的随机数。

相信不用多说你也会理解，**幻数是一场瘟疫，应不惜一切代价以避免**。当你对数值的解析方式无法找到一个合理解释时，你可以对此提交一个内容宽泛的评论，包括你是怎样遇见这个问题以及你认为它应该怎样工作。承认自己不清楚一些机制的解析方式，远比让以后的开发者从零开始弄清它们更有帮助。

    /**
     * 1. Magic number. This value is the lowest I could find to align the top of
     * `.foo` with its parent. Ideally, we should fix it properly.
     */
    .foo {
      top: 0.327em; /* 1 */
    }


####扩展阅读

- [Use Lengths, Not Strings](http://hugogiraudel.com/2013/09/03/use-lengths-not-strings/)
- [Correctly Adding Unit to Number](http://css-tricks.com/snippets/sass/correctly-adding-unit-number/)
- [Magic Numbers in CSS](http://css-tricks.com/magic-numbers-in-css/)
- [Sassy-Math](https://github.com/at-import/sassy-math)

###颜色

颜色在CSS中占有重要地位。当涉及到操纵色彩时，Sass通过提供少数的[函数功能](http://sass-lang.com/documentation/Sass/Script/Functions.html)，最终成为了极具价值的助手。

####颜色格式

为了尽可能简单地使用颜色，我建议颜色格式要按照以下顺序排列：

- [CSS颜色关键字](http://www.w3.org/TR/css3-color/#svg-color);
- [HSL值](http://en.wikipedia.org/wiki/HSL_and_HSV);
- [RGB值](http://en.wikipedia.org/wiki/RGB_color_model);
- 十六进制。小写并尽可能简写。

对于初学者来说，颜色关键字往往比较通俗易懂。HSL表示方式不仅仅是人类大脑最易于接受的，它也可以让样式表作者轻松地调整色调、饱和度和亮度来修改颜色。如果一个颜色偏蓝、偏绿或者偏红，那么使用`RGB`更容易表示出来，但是却不容易表示三者的混合色。最后，十六进制是人类大脑理解的极限了。

    // 推荐方式
    .foo {
      color: red;
    }
    // 不推荐方式
    .foo {
      color: #FF0000;
    }

使用HSL值或者RGB值，通常在逗号 (`,`)后面追加一个空格，而不在前后括号 (`(`, `)`) 和值之间添加空格。

    // 推荐方式
    .foo {
      color: rgba(0, 0, 0, 0.1);
      background: hsl(300, 100%, 100%);
    }
    // 不推荐方式
    .foo {
      color: rgba(0,0,0,0.1);
      background: hsl( 300, 100%, 100% );
    }


####颜色和变量

当一个颜色被多次调用时，最好用一个有意义的变量名来保存它。

    $sass-pink: #c69;

现在，你就可以在任何需要的地方随意使用这个变量了。不过，如果你是在一个主题中使用，我不建议固定的使用这个变量。相反，可以使用另一个标识方式的变量来保存它。

    $main-theme-color: $sass-pink

这样做可以防止一个主题变化而出现此类结果 `$sass-pink: blue`。

####变量和变暗颜色

[`lighten`](http://sass-lang.com/documentation/Sass/Script/Functions.html#lighten-instance_method)和 [`darken`](http://sass-lang.com/documentation/Sass/Script/Functions.html#darken-instance_method) 函数都是通过增加或者减小HSL中颜色的亮度来实现调节的。基本上，它们就是[`adjust-color`](http://sass-lang.com/documentation/Sass/Script/Functions.html#adjust_color-instance_method)函数添加了 `$lightness`参数的别名。

问题是，这些函数经常并不能实现预期的结果。另一方面，通过混合`白色` 或 `黑色`实现变量或变暗的 [`mix`](http://sass-lang.com/documentation/Sass/Script/Functions.html#mix-instance_method)函数，是一个不错的方法。

和上述两个函数相比，使用`mix`的好处是，当你降低颜色的比例时，它会渐进的接近黑色（或者白色），而 `darken` 和`lighten`立即变换颜色到黑色或白色。

![变量和变暗颜色](http://www.w3cplus.com/sites/default/files/blogs/2015/1501/lighten-darken-mix.png "变量和变暗颜色")

[KatieK](http://codepen.io/KatieK2/pen/tejhz/)通过Illustration绘制了`lighten`/`darken`和`mix`之间的差别

如果你不想每次都写`mix`函数，你可以创建两个易用的 `tint` 和`shade` ([Compass](http://compass-style.org/reference/compass/helpers/colors/#shade)的一部分)来处理相同的事：

    // Slightly lighten a color
    // @access public
    // @param {Color} $color - color to tint
    // @param {Number} $percentage - percentage of `$color` in returned color
    // @return {Color}
    @function tint($color, $percentage) {
      @return mix($color, white, $percentage);
    }
    // Slightly darken a color
    // @access public
    // @param {Color} $color - color to shade
    // @param {Number} $percentage - percentage of `$color` in returned color
    // @return {Color}
    @function shade($color, $percentage) {
      @return mix($color, black, $percentage);
    }

**注：**[`scale-color`](http://sass-lang.com/documentation/Sass/Script/Functions.html#scale_color-instance_method)函数的设计初衷是为了更流畅地调试属性——以实际的高低为调试基础。它如同`mix`一样好用，并且提供了更清晰地调用约定。比例因子并不完全相同。

####扩展阅读

- [A Visual Guide to Sass & Compass Color Functions](http://jackiebalzer.com/color)
- [How to Programmatically Go From One Color to Another](http://thesassway.com/advanced/how-to-programtically-go-from-one-color-to-another-in-sass)
- [Sass Color Variables That Don't Suck](http://davidwalsh.name/sass-color-variables-dont-suck)
- [Using Sass to Build Color Palettes](http://www.sitepoint.com/using-sass-build-color-palettes/)
- [Dealing with Color Schemes in Sass](http://www.sitepoint.com/dealing-color-schemes-sass/)

###列表

列表就是Sass的数组。列表是一个一维的数据结构（不同于[maps](#maps)），用于保存任意类型的数值（包括列表，从而产生嵌套列表）。

列表需要遵守以下规范：

- 除非列表太长不能写在80字符宽度的单行中，否则应该始终单行显示；
- 除非适用于CSS，否则应该始终使用逗号作为分隔符；
- 除非为空或者嵌套在另一个列表中，否则始终不要使用括号；
- 始终不要添加尾部的逗号。

```
// 推荐方式
$font-stack: 'Helvetica', 'Arial', sans-serif;
// 不推荐方式
$font-stack:
  'Helvetica',
  'Arial',
  sans-serif;

// 不推荐方式
$font-stack: 'Helvetica' 'Arial' sans-serif;

// 不推荐方式
$font-stack: ('Helvetica', 'Arial', sans-serif);

// 不推荐方式
$font-stack: ('Helvetica', 'Arial', sans-serif,);
```

当需要给列表添加一个新列表项时，请遵守其提供的API，不要试图手动给列表添加列表项。

    $shadows: 0 42px 13.37px hotpink;
    // 推荐方式
    $shadows: append($shadows, $shadow, comma);
    // 不推荐方式
    $shadows: $shadows, $shadow;


####扩展阅读

- [SassyLists](http://sassylists.com)

###Maps

从Sass3.3开始，样式表作者可以使用map这种数据结构——Sass团队使map可以映射关联数组、哈希表甚至是Javascript对象。map是一种映射任何类型键值对（可以是任何类型，包括内嵌maps，不过不推荐这种内嵌方式）的数据结构。

map的使用应该遵循下述规范：

- 冒号(`:`)之后添加空格；
- 左开括号(`(`)要和冒号 (`:`)写在同一行；
- 如果键是字符串（99%都是字符串），则**使用括号包裹起来**。
- 每一个键值对单独一行；
- 每一个键值对以逗号(`,`)结尾；
- 为最后一个键值对添加**尾部逗号** (`,`)，方便添加新键值对、删除和重排已有键值对；
- 单独一行书写右闭括号 (`)`)；
- 右闭括号 (`)`)和分号(`;`)之间不使用空格和换行。

示例:

// 推荐方式
$breakpoints: (
  'small': 767px,
  'medium': 992px,
  'large': 1200px,
);
// 不推荐方式
$breakpoints: ( small: 767px, medium: 992px, large: 1200px );

###调试Sass的map

如果你感到困惑并想了解Sass的map到底有怎样的魔力，请不要担心，Sass中始终存在一个自动保存运行过程的机制。

    @mixin debug-map($map) {
      @at-root {
        @debug-map {
          __toString__: inspect($map);
          __length__: length($map);
          __depth__: if(function-exists('map-depth'), map-depth($map), null);
          __keys__: map-keys($map);
          __properties__ {
            @each $key, $value in $map {
              #{'(' + type-of($value) + ') ' + $key}: inspect($value);
            }
          }
        }
      }
    }
    =debug-map($map)
      @at-root
        @debug-map
          __toString__: inspect($map)
          __length__: length($map)
          __depth__: if(function-exists('map-depth'), map-depth($map), null)
          __keys__: map-keys($map)
          __properties__
            @each $key, $value in $map
              #{'(' + type-of($value) + ') ' + $key}: inspect($value)

如果你想深入了解map的实现机制，可以添加下述函数。该混合宏可以自动显示map的运行机制。

    /// Compute the maximum depth of a map
    /// @param {Map} $map
    /// @return {Number} max depth of `$map`
    @function map-depth($map) {
      $level: 1;
      @each $key, $value in $map {
        @if type-of($value) == 'map' {
          $level: max(map-depth($value) + 1, $level);
        }
      }
      @return $level;
    }

####扩展阅读

- [Using Sass Maps](http://www.sitepoint.com/using-sass-maps/)
- [Debugging Sass Maps](http://www.sitepoint.com/debugging-sass-maps/)
- [Real Sass, Real Maps](http://blog.grayghostvisuals.com/sass/real-sass-real-maps/)
- [Sass Maps are Awesome](http://viget.com/extend/sass-maps-are-awesome)
- [Sass list-maps](https://github.com/lunelson/sass-list-maps)
- [Sass Maps Plus](https://github.com/lunelson/sass-maps-plus)
- [Sassy-Maps](https://github.com/at-import/sassy-maps)
- [Introduction to Sass Maps Usage and Examples](http://webdesign.tutsplus.com/tutorials/an-introduction-to-sass-maps-usage-and-examples--cms-22184)

###CSS 规则集

在这里，极有可能颠覆每个人对书写CSS规则集的认知（根据众多规范整理而成，包括[CSS Guidelines](http://cssguidelin.es/#anatomy-of-a-ruleset)）：

- 相关联的选择器写在同一行；不相关联选择器分行书写；
- 最后一个选择器和左开大括号(`{`)中间书写一个空格；
- 每个声明单独一行；
- 冒号(`:`)后添加空格；
- 所有声明的尾部都添加一个分号 (`;`)；
- 右闭大括号(`}`)单独一行；

示例:

    // 推荐方式
    .foo, .foo-bar,
    .baz {
      display: block;
      overflow: hidden;
      margin: 0 auto;
    }
    // 不推荐方式
    .foo,
    .foo-bar, .baz {
        display: block;
        overflow: hidden;
        margin: 0 auto }

添加与CSS相关的规范时，我们需要注意：

- 本地变量在其他任何变量之前声明，并和其他声明用空行分隔开；
- 不需 `@content`的混合宏在放在其他声明之前；
- 嵌套选择器在新行声明；
- 需要`@content` 的混合宏在嵌套选择器后声明；
- 右闭大括号(`}`)上一行无需空行；

示例:

    .foo, .foo-bar,
    .baz {
      $length: 42em;
      @include ellipsis;
      @include size($length);
      display: block;
      overflow: hidden;
      margin: 0 auto;
      &:hover {
        color: red;
      }
      @include respond-to('small') {
        overflow: visible;
      }
    }

####扩展阅读

- [Anatomy of a Ruleset](http://cssguidelin.es/#anatomy-of-a-ruleset)

###声明顺序

难以想象竟有这么多关于划分CSS声明顺序的讨论。具体而言，有如下两派：

- 坚持以字母顺序排列；
- 以类型（`position`, `display`, `colors`, `font`, miscellaneous...）顺序排列；

这两种方式各有利弊。一方面，字母排序方式通俗易懂（至少对于语言中使用拉丁字母的人来说），所以排序的过程完全没有争议。但是，这种排序的结果却十分奇怪，如`bottom` 和 `top`竟然彼此不相邻。为什么`animations`属性出现在`display`属性之前？字母排序方式有太多诸如此类的怪相了。

```
.foo {
  background: black;
  bottom: 0;
  color: white;
  font-weight: bold;
  font-size: 1.5em;
  height: 100px;
  overflow: hidden;
  position: absolute;
  right: 0;
  width: 100px;
}
.foo
  background: black
  bottom: 0
  color: white
  font-weight: bold
  font-size: 1.5em
  height: 100px
  overflow: hidden
  position: absolute
  right: 0
  width: 100px
```

另一方面，按照类型排序则让属性显得更具有意义。每个和字体相关的属性被声明在一起，`top` 和 `bottom`也结合在一起，最终审阅CSS规则集感觉就像是在读故事。除非你坚持诸如 [Idiomatic CSS](https://github.com/necolas/idiomatic-css)的规定，不然类型声明顺序可以有更丰富充实的表现。`white-space`应该放在哪里：font还是dispaly? `overflow`应该归属何处？如何进行组内排序（如果是字母排序，这岂不成了个笑话）？

    .foo {
      height: 100px;
      width: 100px;
      overflow: hidden;
      position: absolute;
      bottom: 0;
      right: 0;
      background: black;
      color: white;
      font-weight: bold;
      font-size: 1.5em;
    }

此外也有其他类型排序的分支，比如[Concentric CSS](https://github.com/brandon-rhodes/Concentric-CSS)，他看起来相当流行。Concentric CSS的基础是依赖盒模型定义顺序：由外而内。

    .foo {
      width: 100px;
      height: 100px;
      position: absolute;
      right: 0;
      bottom: 0;
      background: black;
      overflow: hidden;
      color: white;
      font-weight: bold;
      font-size: 1.5em;
    }

我必须说我不能对此下任何判定。一份[CSS-Tricks做的统计报告](http://css-tricks.com/poll-results-how-do-you-order-your-css-properties/)确认，超过45%的开发者使用类型顺序声明，而只有14%使用字母顺序。此外还有39%的开发者随意而为，这其中就包括我。

![CSS-Tricks做的统计报告](http://www.w3cplus.com/sites/default/files/blogs/2015/1501/css_order_chart.png "CSS-Tricks做的统计报告")

因此，我不会在此强加规范选择怎样的声明顺序。只要你长久的在自己的样式表中保持一致的风格，那么选择喜欢的声明顺序就可以了。

**注：**最近一份[研究报告](http://peteschuster.com/2014/12/reduce-file-size-css-sorting/)表明，使用[CSS Comb](https://github.com/csscomb/csscomb.js)(一种排序的[类型](https://github.com/csscomb/csscomb.js/blob/master/config/csscomb.json))对CSS进行排序，按类型顺序声明，Gzip压缩文件大小平均达到2.7%,而按字母顺序排序压缩的文件大小平均达到1.3%。

####扩展阅读

- [CSS Comb](https://github.com/csscomb/csscomb.js)
- [Concentric CSS](https://github.com/brandon-rhodes/Concentric-CSS)
- [Idiomatic CSS](https://github.com/necolas/idiomatic-css)
- [On Declaration Sorting](http://meiert.com/en/blog/20140924/on-declaration-sorting/)
- [Reduce File Size With CSS Sorting](http://peteschuster.com/2014/12/reduce-file-size-css-sorting/)
- [Poll Results: How Do You Order Your CSS Properties?](http://css-tricks.com/poll-results-how-do-you-order-your-css-properties/)

###选择器嵌套

Sass中一个正在被众多开发者滥用的功能，就是**选择器嵌套**。选择器嵌套为样式表作者提供了一个通过局部选择器的相互嵌套实现全局选择的方法。

####一般规则

比如下述Sass选择器的嵌套：

    .foo {
      .bar {
        &:hover {
          color: red;
        }
      }
    }

生成的CSS:

    .foo .bar:hover {
      color: red;
    }

从Sass3.3开始，可以在同一行中使用最近选择器引用(`&`)来实现高级选择器，比如：

    .foo {
      &-bar {
        color: red;
      }
    }

生成CSS:

    .foo-bar {
      color: red;
    }

这种方式通常被用来配合[BEM全名方式](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)使用，基于原选择器（比如`.block`）生成`.block__element` and `.block--modifier`选择器。

**注：**传说中，使用`&`能在当前选择器下产生新的选择器，这样代码库中选择器无法控制，因为他们本身不存在。

选择器嵌套最大的问题是将使最终的代码难以阅读。开发者需要花费巨大精力计算不同缩进级别下选择器具体的表现效果。CSS最终的表现效果往往不是浅显易懂的。

选择器越具体则声明语句越冗长，而且对最近选择器的引用(`&`)也越频繁。在某些时候，出现混淆选择器路径和探索下一级选择器的错误率很高，这非常不值得。

####特殊规则

为了防止这种情况，我们应该**避免在伪类和伪元素外使用选择器嵌套**。这是唯一允许和建议使用的选择器嵌套方式。

    .foo {
      color: red;
      &:hover {
        color: green;
      }
      &::before {
        content: 'pseudo-element';
      }
    }


使用选择器嵌套选择伪类和伪元素不仅仅有道理的（因为它的处理功能与选择器紧密相关），而且有助于保持总体的一致性。

当然，如果使用类似`.is-active`类名来控制当前选择器状态，也可以这样使用选择器嵌套。

    .foo {
      // ...
      &.is-active {
        font-weight: bold;
      }
    }

这并不是最重要的，当一个元素的样式在另一个容器中有其他指定的样式时，可以使用嵌套选择器让他们保持在同一个地方。

    .foo {
      // ...
      .no-opacity & {
        display: none;
      }
    }

当一个没太多经验的开发者，不对类似于`.no-opacity &`这样的选择器造成混淆。可能创建一个`mixin`来处理。

    /// Helper mixin to provide simple API to selector nesting
    /// @param {String} $selector - Selector
    @mixin when-inside($selector) {
      #{$selector} & {
        @content;
      }
    }

重写刚才的示例，他看起来像这样：

    .foo {
      // ...
      @include when-inside('.no-opacity') {
        display: none;
      }
    }

这所有的一切，有些是无关紧要的细节，关键是要保持一致性。如果你觉得完全有信心搞定选择器嵌套，然后你就使用了选择器嵌套。可你还要确保你的整个团队也能搞定选择器的嵌套。

####扩展阅读

- [Beware of Selector Nesting](http://www.sitepoint.com/beware-selector-nesting-sass/)
- [The Inception Rule](http://thesassway.com/beginner/the-inception-rule)
- [Avoid nested selectors for more modular CSS](http://thesassway.com/intermediate/avoid-nested-selectors-for-more-modular-css)

##命名约定

在本节，我们不会讨论适用于大规模和可维护的最佳CSS命名方案，因为这不仅仅超过了个人的能力范围，也不是一个Sass样式指南可以解决的问题。我个人推荐遵从[CSS Guidelines](http://cssguidelin.es/#naming-conventions)的建议。

良好的命名对保持整体代码的一致性和可读性非常重要，在Sass中可以命名的地方如下：

- 变量；
- 函数；
- 混合宏。

由于Sass占位符遵循和类名相同的命名模式，因此被视为常规的CSS选择器，也就在这个列表中故意忽略掉了。

就变量、函数和混合宏的命名而言，我们坚持一些很 *CSS-y*的风格：**小写连字符分隔**，有意义的命名。

    $vertical-rhythm-baseline: 1.5rem;
    @mixin size($width, $height: $width) {
      // ...
    }
    @function opposite-direction($direction) {
      // ...
    }

####扩展阅读

- [CSS Guidelines' Naming Conventions](http://cssguidelin.es/#naming-conventions)

##常量

如果你恰巧是一个框架开发者或某个库的维护者，你会发现自己正在使用的变量并不需要在所有情况下都进行更新：此时是多么类似一个常量。不幸的是（或者幸运的是？），Sass不提供任何方式定义这样的实体，所以我们要坚持严格的命名约定来阐述我们的想法。

对于众多编程语言，我建议使用全大写方式书写常量。这不仅是一个由来已久的编程习惯，而且可以很好的与小写连字符变量加以区别。

    // 推荐方式
    $CSS_POSITIONS: top, right, bottom, left, center;
    // 不推荐方式
    $css-positions: top, right, bottom, left, center;

####扩展阅读

- [Dealing With Constants in Sass](http://www.sitepoint.com/dealing-constants-sass/)

##命名空间

如果你打算分发你的Sass代码，比如一个库、框架、栅格系统或者其他的什么，为了防止与其他人的代码发生冲突，你就可能会考虑使用命名空间包裹你所有的变量、函数、混合宏和占位符。

举例来说，如果你参加了一个名为*Sassy Unicorn*的项目——这意味着全球的开发者都可能会使用它（谁都有可能，对吧？），你可能会考虑使用`su-`作为一个命名空间。这确实非常独特，既不会引发命名冲突，又足够短小而没有书写困难。

    $su-configuration: ( ... );
    @function su-rainbow($unicorn) {
      // ...
    }

**注：**需要注意的是，自动命名空间功能绝对是即将到来的Sass4.0中重构的`@import`的一个设计目标。随着即将取得结果，将会越来越少的需要手动命名，最终，手动命名库名实际上会越来越难用。

####扩展阅读

- [Please Respect the Global CSS Namespace](http://blog.kaelig.fr/post/44554267597/please-respect-the-global-css-namespace)

##注释

CSS是一个棘手的语言，充满了骇客行为和古怪的事情。因此，应该大量注释，特别是如果有人打算六个月或一年后要继续阅读和更新这些代码。不要让任何人处于如此境地：**这不是我写的，上帝，为什么会这样**。

CSS的实现很简单，但我们需要为此付出巨大的注释量。解释如下：

- 一个文件的结构或者作用；
- 规则集的目标；
- 使用幻数背后的目的；
- CSS声明的原因；
- CSS声明的顺序；
- 方法执行背后的逻辑思维。

在这里，我可能还遗漏了其他各种各样的缘由。在代码完成之时立即注释，往往只需花费一点时间；而过一阵时间再来为一小段代码注释，则是完全不现实和令人恼怒的。

###写注释

理想上，**任何**CSS规则集之前都应该使用C风格注释来解释CSS块的核心。这个注释也要记录对规则集特定部分编号的解释。比如：

    /**
     * Helper class to truncate and add ellipsis to a string too long for it to fit
     * on a single line.
     * 1. Prevent content from wrapping, forcing it on a single line.
     * 2. Add ellipsis at the end of the line.
     */
    .ellipsis {
      white-space: nowrap; /* 1 */
      text-overflow: ellipsis; /* 2 */
      overflow: hidden;
    }

基本上，任何不能明显看出意义的地方都应该注释，但不要随处注释。记住不要**注释太多**，掌握尺度让每一处注释都有意义。

当注释Sass的一个特定部分时，应该使用Sass单行注释而不是C风格的注释块。这么做将不会输出注释，即使是在开发时的扩展模式。

    // Add current module to the list of imported modules.
    // `!global` flag is required so it actually updates the global variable.
    $imported-modules: append($imported-modules, $module) !global;

###扩展阅读

- [CSS Guidelines' Commenting section](http://cssguidelin.es/#commenting)

###文档

每一个旨在代码库中复用的变量、函数、混合宏和占位符，都应该使用[SassDoc](http://sassdoc.com)记录下来作为全部API的一部分。

    /// Vertical rhythm baseline used all over the code base.
    /// @type Length
    $vertical-rhythm-baseline: 1.5rem;

**注：**需要三个斜杠(`/`)。

SassDoc主要有两个作用：

- 作为公有或私有API的一部分，在所有的地方使用一个注释系统强制标准化注释。
- 通过使用任意的SassDoc终端(CLI tool, Grunt, Gulp, Broccoli, Node...)，能够生成API文档的HTML版本。

![SassDoc](http://www.w3cplus.com/sites/default/files/blogs/2015/1501/preview-image.png "SassDoc")

这里有一个深入整合SassDoc生成文档的例子：

    /// Mixin helping defining both `width` and `height` simultaneously.
    ///
    /// @author Hugo Giraudel
    ///
    /// @access public
    ///
    /// @param {Length} $width - Element's `width`
    /// @param {Length} $height ($width) - Element's `height`
    ///
    /// @example scss - Usage
    ///   .foo {
    ///     @include size(10em);
    ///   }
    ///
    ///   .bar {
    ///     @include size(100%, 10em);
    ///   }
    ///
    /// @example css - CSS output
    ///   .foo {
    ///     width: 10em;
    ///     height: 10em;
    ///   }
    ///
    ///   .bar {
    ///     width: 100%;
    ///     height: 10em;
    ///   }
    @mixin size($width, $height: $width) {
      width: $width;
      height: $height;
    }

####扩展阅读

- [SassDoc](http://sassdoc.com)
- [SassDoc: a Documentation Tool for Sass](http://www.sitepoint.com/sassdoc-documentation-tool-sass/)
- [New Features and New Look for SassDoc](http://webdesign.tutsplus.com/articles/new-features-and-a-new-look-for-sassdoc--cms-21914)
