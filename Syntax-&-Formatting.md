#语法格式

如果你问我一个样式指南首先要描述什么，我会告诉你：编写代码的通用准则。

当几个开发者在同一项目中编写CSS时，迟早会陷入各自为政的境地。编码样式指南通过规范统一的样式，不仅防止了这种混乱现象，也减轻了阅读和维护代码的难度。

概括地说，我们希望做到（受[CSS Guidelines](http://cssguidelin.es/#syntax-and-formatting)所启发）：

* 使用两个空格代表缩进，而不是使用tab键；
* 理想上，每行保持为80个字符宽度；
* 正确书写多行CSS规则；
* 有意义的使用空格。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
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
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// Since Sass indented-syntax forces those coding standards
// There is no wrong way of proceeding
.foo
  display: block
  overflow: hidden
  padding: 0 1em
{% endhighlight %}
  </div>
</div>

在本部分中不会涉及有关文件组织的问题，相关讨论在[另一节](#architecture)中。

## 字符串

CSS中不要求字符串必须引号包裹，甚至是字符串中包含空格的。就拿font-family属性来说：无论你是否使用引号包裹，CSS解析器都可以正确解析。

因此，Sass*也*不强制要求字符串必须被引号包裹。更棒的是（你也会如此认为），被引号包裹和没被包裹的一对字符串完全等同（例如，`'abc'` 严格等同于 `abc`）。

话虽如此，不强制要求字符串被引号包裹的毕竟是少数，所以，在Sass中**字符串应该始终被单引号所包裹**（在*querty*键盘中单引号比双引号更容易输入）。即使不考虑与其他语言的一致性，单是考虑CSS的近亲JavaScript，也有数条理由这么做：

* color names are treated as colors when unquoted, which can lead to serious issues;
* most syntax highlighters will choke on unquoted strings;
* it helps general readability;
* there is no valid reason not to quote strings.

* 如果颜色名不被引号包裹，将会被解析为颜色值，显然这会导致严重问题；
* 大多数的语法高亮机制将会因未被引号包裹的字符串而罢工；
* 提高可读性；
* 没有正当理由不去用引号包裹字符串。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// 推荐方式
$font-stack: 'Helvetica Neue Light', 'Helvetica', 'Arial', sans-serif;

// 不推荐方式
$font-stack: "Helvetica Neue Light", "Helvetica", "Arial", sans-serif;

// 不推荐方式
$font-stack: Helvetica Neue Light, Helvetica, Arial, sans-serif;
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// 推荐方式
$font-stack: 'Helvetica Neue Light', 'Helvetica', 'Arial', sans-serif

// 不推荐方式
$font-stack: "Helvetica Neue Light", "Helvetica", "Arial", sans-serif

// 不推荐方式
$font-stack: Helvetica Neue Light, Helvetica, Arial, sans-serif
{% endhighlight %}
  </div>
</div>

<div class="note">
  <p>In the previous example, <code>sans-serif</code> is not being quoted because it is a specific CSS value that needs to be unquoted.</p>
</div>

URLs should be quoted as well, for the same reasons as above:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// 推荐方式
.foo {
  background-image: url('/images/kittens.jpg');
}

// 不推荐方式
.foo {
  background-image: url(/images/kittens.jpg);
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// 推荐方式
.foo
  background-image: url('/images/kittens.jpg')

// 不推荐方式
.foo
  background-image: url(/images/kittens.jpg)
{% endhighlight %}
  </div>
</div>

### 扩展阅读

* [All You Ever Need to Know About Sass Interpolation](http://webdesign.tutsplus.com/tutorials/all-you-ever-need-to-know-about-sass-interpolation--cms-21375)
* [SassyStrings](https://github.com/HugoGiraudel/SassyStrings)

## 数字

在Sass中，数字类型包括了长度、持续时间、频率、角度等等无单位数字类型。Sass允许在运行中计算这些度量值。

### 零值

当数字小于1时，应该在小数点前写出0.永远不要显示小数尾部的0。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
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
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// 推荐方式
.foo
  padding: 2em
  opacity: 0.5

// 不推荐方式
.foo
  padding: 2.0em
  opacity: .5
{% endhighlight %}
  </div>
</div>

### 单位

当定义长度时，`0` 后面不需要加单位。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// 推荐方式
$length: 0;

// 不推荐方式
$length: 0em;
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// 推荐方式
$length: 0

// 不推荐方式
$length: 0em
{% endhighlight %}
  </div>
</div>

在Sass中最常见的错误，是简单地认为单位只是字符串，认为它会被安全的添加到数字后面。这虽然听起来不错，但却不是单位正确的解析方式。可以把单位认为是代数符号，例如，在现实世界中，5英寸乘以5英寸得到25英寸。Sass也适用这样的逻辑。

将一个单位添加给数字的时候，实际上是让该数值乘以*1个单位*。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
$value: 42;

// 推荐方式
$length: $value * 1px;

// 不推荐方式
$length: $value + px;
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
$value: 42

// 推荐方式
$length: $value * 1px

// 不推荐方式
$length: $value + px
{% endhighlight %}
  </div>
</div>

需要注意的是加上一个*0unit*也可以正确解析，但是这种方式在某种程度上会造成一些混乱，所以我更愿意推荐上面的方式。事实上，将一个数字转换为其他兼容单位时，加0操作并不会造成错误。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
$value: 42 + 0px;
// -> 42px

$value: 1in + 0px;
// -> 1in

$value: 0px + 1in;
// -> 96px
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
$value: 42 + 0px
// -> 42px

$value: 1in + 0px
// -> 1in

$value: 0px + 1in
// -> 96px
{% endhighlight %}
  </div>
</div>

这一切最终取决于你想要达到怎样的效果。只要记住，像添加一个字符串一样添加一个单位并不是一种好的处理方式。

要删除一个值的单位，你需要除以*相同类型的1单位*。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
$length: 42px;

// 推荐方式
$value: $length / 1px;

// 不推荐方式
$value: str-slice($length + unquote(''), 1, 2);
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
$length: 42px

// 推荐方式
$value: $length / 1px

// 不推荐方式
$value: str-slice($length + unquote(''), 1, 2)
{% endhighlight %}
  </div>
</div>

给一个数值像以字符串形式添加单位的结果是产生一个字符串，同时要防止对数据的额外操作。从一个带有单位的数值中分离数字部分也会产生字符串，但些都不是你想要的。

### 计算

**最高级运算应该始终被包裹在括号中**。这么不做不仅是为了提高可读性，也是为了防止一些Sass强制要求对括号内内容计算的极端情况。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// 推荐方式
.foo {
  width: (100% / 3);
}

// 不推荐方式
.foo {
  width: 100% / 3;
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// 推荐方式
.foo
  width: (100% / 3)

// 不推荐方式
.foo
  width: 100% / 3
{% endhighlight %}
  </div>
</div>

### 幻数

"幻数"，是[old school programming](http://en.wikipedia.org/wiki/Magic_number_(programming)给*未命名数值常数*的命名。基本上，它们只是*just work*™但没有任何逻辑思维的随机数。

相信不用多说你也会理解，**幻数是一场瘟疫，应不惜一切代价以避免**。当你对数值的解析方式无法找到一个合理解释时，你可以对此提交一个内容宽泛的评论，包括你是怎样遇见这个问题以及你认为它应该怎样工作。承认自己不清楚一些机制的解析方式，远比让以后的开发者从零开始弄清它们更有帮助。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
/**
 * 1. Magic number. This value is the lowest I could find to align the top of
 * `.foo` with its parent. Ideally, we should fix it properly.
 */
.foo {
  top: 0.327em; /* 1 */
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
/**
 * 1. Magic number. This value is the lowest I could find to align the top of
 * `.foo` with its parent. Ideally, we should fix it properly.
 */
.foo
  top: 0.327em /* 1 */
{% endhighlight %}
  </div>
</div>

### 扩展阅读

* [Use Lengths, Not Strings](http://hugogiraudel.com/2013/09/03/use-lengths-not-strings/)
* [Correctly Adding Unit to Number](http://css-tricks.com/snippets/sass/correctly-adding-unit-number/)
* [Magic Numbers in CSS](http://css-tricks.com/magic-numbers-in-css/)
* [Sassy-Math](https://github.com/at-import/sassy-math)

## 颜色

颜色在CSS中占有重要地位。当涉及到操纵色彩时，Sass通过提供少数[powerful functions](http://sass-lang.com/documentation/Sass/Script/Functions.html)最终成为了极具价值的助手。

### 颜色格式

为了尽可能简单地使用颜色，我建议颜色格式要按照以下顺序排列：

1. [CSS颜色关键字](http://www.w3.org/TR/css3-color/#svg-color);
2. [HSL值](http://en.wikipedia.org/wiki/HSL_and_HSV);
3. [RGB值](http://en.wikipedia.org/wiki/RGB_color_model);
4. 十六进制。小写并尽可能简写。

对于初学者来说，颜色关键字往往比较通俗易懂。HSL表示方式不仅仅是人类大脑最易于接受的<sup>[citation needed]</sup>，它也可以让样式表作者轻松地调整色调、饱和度和亮度来修改颜色。如果一个颜色偏蓝、偏绿或者偏红，那么使用RGB更容易表示出来，但是却不容易表示三者的混合色。最后，十六进制是人类的大脑理解的极限了。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// 推荐方式
.foo {
  color: red;
}

// 不推荐方式
.foo {
  color: #FF0000;
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// 推荐方式
.foo
  color: red

// 不推荐方式
.foo
  color: #FF0000
{% endhighlight %}
  </div>
</div>

使用HSL值或者RGB值，通常在逗号 (`,`)后面追加一个空格，而不在前后括号 (`(`, `)`) 和值之间添加空格。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
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
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// 推荐方式
.foo
  color: rgba(0, 0, 0, 0.1)
  background: hsl(300, 100%, 100%)

// 不推荐方式
.foo
  color: rgba(0,0,0,0.1)
  background: hsl( 300, 100%, 100% )
{% endhighlight %}
  </div>
</div>

### 颜色和变量

当一个颜色被多次调用时，用一个有意义的变量名来保存它。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
$sass-pink: #c69;
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
$sass-pink: #c69
{% endhighlight %}
  </div>
</div>

现在，你就可以在任何需要的地方随意使用这个变量了。不过，如果你是在一个主题中使用，我不建议固定的使用这个变量。相反，可以使用另一个标示使用方式的变量来保存它。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
$main-theme-color: $sass-pink;
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
$main-theme-color: $sass-pink
{% endhighlight %}
  </div>
</div>

这样做可以防止一个主题变化而出现此类结果 `$sass-pink: blue`。

{% include donate.html %}

### 变量和变暗颜色

[`lighten`](http://sass-lang.com/documentation/Sass/Script/Functions.html#lighten-instance_method)和 [`darken`](http://sass-lang.com/documentation/Sass/Script/Functions.html#darken-instance_method) 函数都是通过增加或者减小HSL中颜色的亮度来实现调节的。基本上，它们就是[`adjust-color`](http://sass-lang.com/documentation/Sass/Script/Functions.html#adjust_color-instance_method)函数添加了 `$lightness`参数的别名。

问题是，这些函数经常并不能实现预期的结果。另一方方面，通过混合`白色` 或 `黑色`实现变量或变暗的 [`mix`](http://sass-lang.com/documentation/Sass/Script/Functions.html#mix-instance_method)函数，是一个不错的方法。

和上述两个函数相比，使用`mix`的好处是，当你降低颜色的比例时，它会渐进的接近黑色（或者白色），而 `darken` 和`lighten`立即变换颜色到黑色或白色。 

<figure>
  <img src="/assets/images/lighten-darken-mix.png" alt="Illustration of the difference between lighten/darken and mix Sass functions" />
  <figcaption>Illustration of the difference between <code>lighten</code>/<code>darken</code> and <code>mix</code> by <a href="http://codepen.io/KatieK2/pen/tejhz/" target="_blank">KatieK</a></figcaption>
</figure>

如果你不想每次都写`mix`函数，你可以创建两个易用的 `tint` 和`shade` ([Compass](http://compass-style.org/reference/compass/helpers/colors/#shade)的一部分)来处理相同的事：

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
/// Slightly lighten a color
/// @access public
/// @param {Color} $color - color to tint
/// @param {Number} $percentage - percentage of `$color` in returned color
/// @return {Color}
@function tint($color, $percentage) {
  @return mix($color, white, $percentage);
}

/// Slightly darken a color
/// @access public
/// @param {Color} $color - color to shade
/// @param {Number} $percentage - percentage of `$color` in returned color
/// @return {Color}
@function shade($color, $percentage) {
  @return mix($color, black, $percentage);
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
/// Slightly lighten a color
/// @access public
/// @param {Color} $color - color to tint
/// @param {Number} $percentage - percentage of `$color` in returned color
/// @return {Color}
@function tint($color, $percentage)
  @return mix($color, white, $percentage)

/// Slightly darken a color
/// @access public
/// @param {Color} $color - color to shade
/// @param {Number} $percentage - percentage of `$color` in returned color
/// @return {Color}
@function shade($color, $percentage)
  @return mix($color, black, $percentage)
{% endhighlight %}
  </div>
</div>

<div class="note">
  <p>The <a href="http://sass-lang.com/documentation/Sass/Script/Functions.html#scale_color-instance_method"><code>scale-color</code></a> function is designed to scale properties more fluidly by taking into account how high or low they already are. It should provide results that are as nice as <code>mix</code>'s but with a clearer calling convention. The scaling factor isn't exactly the same though.</p>
</div>



### 扩展阅读

* [A Visual Guide to Sass & Compass Color Functions](http://jackiebalzer.com/color)
* [How to Programmatically Go From One Color to Another](http://thesassway.com/advanced/how-to-programtically-go-from-one-color-to-another-in-sass)
* [Sass Color Variables That Don't Suck](http://davidwalsh.name/sass-color-variables-dont-suck)
* [Using Sass to Build Color Palettes](http://www.sitepoint.com/using-sass-build-color-palettes/)
* [Dealing with Color Schemes in Sass](http://www.sitepoint.com/dealing-color-schemes-sass/)

## 列表

列表就是Sass的数组。列表是一个一维的数据结构（不同于[maps](#maps)），用于保存任意类型的数值（包括列表，从而产生嵌套列表）。

列表需要遵守以下规范：

* 除非列表太长不能写在80字符宽度的单行中，否则应该始终单行显示；
* 除非适用于CSS，否则应该始终使用逗号作为分隔符；
* 除非为空或者嵌套在另一个列表中，否则始终不要使用括号；
* 始终不要添加尾部的逗号。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
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
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// 推荐方式
$font-stack: 'Helvetica', 'Arial', sans-serif

// 不推荐方式 (since it is not supported)
$font-stack:
  'Helvetica',
  'Arial',
  sans-serif

// 不推荐方式
$font-stack: 'Helvetica' 'Arial' sans-serif

// 不推荐方式
$font-stack: ('Helvetica', 'Arial', sans-serif)

// 不推荐方式
$font-stack: ('Helvetica', 'Arial', sans-serif,)
{% endhighlight %}
  </div>
</div>

When adding new items to a list, always use the provided API. Do not attempt to add new items manually.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
$shadows: 0 42px 13.37px hotpink;

// 推荐方式
$shadows: append($shadows, $shadow, comma);

// 不推荐方式
$shadows: $shadows, $shadow;
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
$shadows: 0 42px 13.37px hotpink

// 推荐方式
$shadows: append($shadows, $shadow, comma)

// 不推荐方式
$shadows: $shadows, $shadow
{% endhighlight %}
  </div>
</div>

### 扩展阅读

* [SassyLists](http://sassylists.com)

## 图

从Sass3.3开始，样式表作者可以使用图这种数据结构，Sass团队为图关联了数组、哈希表甚至是Javascript对象。图是一种映射任何类型键值对（可以是任何类型，包括内嵌图，不过不推荐这种内嵌方式）的数据结构。

图的使用应该遵循下述规范：

* 冒号(`:`)之后添加空格；
* 左开括号(`(`)要和冒号 (`:`)写在同一行；
* 如果键是字符串（99%都是字符串），则**使用括号包裹起来**。
* 每一个键值对单独一行；
* 每一个键值对以逗号(`,`)结尾；
* 为最后一个键值对添加**尾部逗号** (`,`)，方便添加新键值对、删除和重排已有键值对；
* 单独一行书写右闭括号 (`)`)；
* 右闭括号 (`)`)和分号(`;`)之间不使用空格和换行。

示例:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// 推荐方式
$breakpoints: (
  'small': 767px,
  'medium': 992px,
  'large': 1200px,
);

// 不推荐方式
$breakpoints: ( small: 767px, medium: 992px, large: 1200px );
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// 推荐方式
$breakpoints: ('small': 767px, 'medium': 992px, 'large': 1200px,)

// 不推荐方式
$breakpoints: ( 'small': 767px, 'medium': 992px, 'large': 1200px )

// 不推荐方式
$breakpoints: (small: 767px, medium: 992px, large: 1200px,)

// 不推荐方式 (since it is not supported)
$breakpoints: (
  'small': 767px,
  'medium': 992px,
  'large': 1200px,
)
{% endhighlight %}
  </div>
</div>



###  调试Sass的图

如果你感到困惑并想了解Sass的图到底有怎样的魔力，请不要担心，Sass中始终存在一个自动保存运行过程的机制。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
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
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
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
{% endhighlight %}
  </div>
</div>

如果你想深入了解图的实现机制，可以添加下述函数。该混合宏可以自动显示图的运行机制。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
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
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
/// Compute the maximum depth of a map
/// @param {Map} $map
/// @return {Number} max depth of `$map`
@function map-depth($map)
  $level: 1

  @each $key, $value in $map
    @if type-of($value) == 'map'
      $level: max(map-depth($value) + 1, $level)

  @return $level;
{% endhighlight %}
  </div>
</div>



### 扩展阅读

* [Using Sass Maps](http://www.sitepoint.com/using-sass-maps/)
* [Debugging Sass Maps](http://www.sitepoint.com/debugging-sass-maps/)
* [Real Sass, Real Maps](http://blog.grayghostvisuals.com/sass/real-sass-real-maps/)
* [Sass Maps are Awesome](http://viget.com/extend/sass-maps-are-awesome)
* [Sass list-maps](https://github.com/lunelson/sass-list-maps)
* [Sass Maps Plus](https://github.com/lunelson/sass-maps-plus)
* [Sassy-Maps](https://github.com/at-import/sassy-maps)
* [Introduction to Sass Maps Usage and Examples](http://webdesign.tutsplus.com/tutorials/an-introduction-to-sass-maps-usage-and-examples--cms-22184)

## CSS 规则集

在这里，极有可能颠覆每个人对书写CSS规则集的认知（根据众多规范整理而成，包括CSS Guidelines](http://cssguidelin.es/#anatomy-of-a-ruleset)）：

* 相关联的选择器写在同一行；不相关联选择器分行书写；
* 最后一个选择器和左开大括号(`{`)中间书写一个空格；
* 每个声明单独一行；
* 冒号(`:`)后添加空格；
* 所有声明的尾部都添加一个分号 (`;`)；
* 右闭大括号(`}`)单独一行；

示例:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
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
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// 推荐方式
.foo, .foo-bar,
.baz
  display: block
  overflow: hidden
  margin: 0 auto

// 不推荐方式
.foo,
.foo-bar, .baz
    display: block
    overflow: hidden
    margin: 0 auto
{% endhighlight %}
  </div>
</div>

添加与CSS相关的规范时，我们需要注意：

* 本地变量在其他任何变量之前声明，并和其他声明用空行分隔开；
* 不需 `@content`的混合宏在放在其他声明之前；
* 嵌套选择器在新行声明；
* 需要`@content` 的混合宏在嵌套选择器后声明；
* 右闭大括号(`}`)上一行无需空行；

示例:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
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
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo, .foo-bar,
.baz
  $length: 42em

  +ellipsis
  +size($length)
  display: block
  overflow: hidden
  margin: 0 auto

  &:hover
    color: red

  +respond-to('small')
    overflow: visible
{% endhighlight %}
  </div>
</div>

### 扩展阅读

* [Anatomy of a Ruleset](http://cssguidelin.es/#anatomy-of-a-ruleset)

## 声明顺序

I cannot think of many topics where opinions are as divided as they are regarding declaration sorting in CSS. Concretely, there are two factions here:

难以想象竟有这么多关于划分CSS声明顺序的讨论。具体而言，有如下两派：

* 坚持以字母顺序排列；
* 以类型（position, display, colors, font, miscellaneous...）顺序排列；

这两种方式各有利弊。一方面，字母排序方式通俗易懂（至少对于语言中使用拉丁字母的），所以排序的过程完全没有争议。但是，这种排序的结果却十分奇怪，如`bottom` 和 `top`竟然彼此不相邻。为什么animations属性出现在display属性之前？字母排序方式有太多诸如此来的怪相了。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
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
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
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
{% endhighlight %}
  </div>
</div>

另一方面，按照类型排序则让属性显得更具有意义。每个和字体相关的属性被声明在一起，`top` 和 `bottom`也结合在一起，最终审阅CSS规则集感觉就像是在读故事。除非你坚持诸如 [Idiomatic CSS](https://github.com/necolas/idiomatic-css)的规定，类型声明顺序可以有更丰富充实的表现。`white-space`应该放在哪里：font还是dispaly? `overflow`应该归属何处？如何进行组内排序（如果是字母排序，这岂不成了个笑话）？

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
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
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo
  height: 100px
  width: 100px
  overflow: hidden
  position: absolute
  bottom: 0
  right: 0
  background: black
  color: white
  font-weight: bold
  font-size: 1.5em
{% endhighlight %}
  </div>
</div>

此外也有其他类型排序的分支，比如[Concentric CSS](https://github.com/brandon-rhodes/Concentric-CSS)，他看起来相当流行。Concentric CSS的基础是依赖盒模型定义顺序：由外而内。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
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
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo
  width: 100px
  height: 100px
  position: absolute
  right: 0
  bottom: 0
  background: black
  overflow: hidden
  color: white
  font-weight: bold
  font-size: 1.5em
{% endhighlight %}
  </div>
</div>

我必须说我不能对此下任何判定。一份[recent poll on CSS-Tricks](http://css-tricks.com/poll-results-how-do-you-order-your-css-properties/)确认，超过45%的开发者使用类型顺序声明，而只有14%使用字母顺序。此外还有39%的开发者随意而为，这其中就包括我。 

<figure>
  <img src="/assets/images/css_order_chart.png" alt="" />
  <figcaption>Chart showing how developers order their CSS declarations</figcaption>
</figure>

因此，我不会在此强加规范选择怎样的声明顺序。只要你长久的在自己的样式表中保持一致的风格，那么选择喜欢的声明顺序就可以了。

<div class="note">
  <p>A <a href="http://peteschuster.com/2014/12/reduce-file-size-css-sorting/">recent study</a> shows that using <a href="https://github.com/csscomb/csscomb.js">CSS Comb</a> (which uses <a href="https://github.com/csscomb/csscomb.js/blob/master/config/csscomb.json">type ordering</a>) for sorting CSS declarations ends up shortening the average file size under Gzip compression by 2.7%, compared to 1.3% when sorting alphabetically.</p>
</div>



### 扩展阅读

* [CSS Comb](https://github.com/csscomb/csscomb.js)
* [Concentric CSS](https://github.com/brandon-rhodes/Concentric-CSS)
* [Idiomatic CSS](https://github.com/necolas/idiomatic-css)
* [On Declaration Sorting](http://meiert.com/en/blog/20140924/on-declaration-sorting/)
* [Reduce File Size With CSS Sorting](http://peteschuster.com/2014/12/reduce-file-size-css-sorting/)
* [Poll Results: How Do You Order Your CSS Properties?](http://css-tricks.com/poll-results-how-do-you-order-your-css-properties/)

## 选择器嵌套

Sass中一个正在被众多开发者滥用的功能，就是*选择器嵌套*。选择器嵌套为样式表作者提供了一个通过局部选择器的相互嵌套实现全局选择的方法。比如下述Sass选择器的嵌套：

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
.foo {
  .bar {
    &:hover {
      color: red;
    }
  }
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo
  .bar
    &:hover
      color: red
{% endhighlight %}
  </div>
</div>

生成的CSS:

{% highlight css %}
.foo .bar:hover {
  color: red;
}
{% endhighlight %}

从Sass3.3开始，可以在同一行中使用最近选择器引用(`&`)来实现高级选择器，比如：

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
.foo {
  &-bar {
    color: red;
  }
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo
  &-bar
    color: red
{% endhighlight %}
  </div>
</div>

... will generate this CSS:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
.foo-bar {
  color: red;
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo-bar
  color: red
{% endhighlight %}
  </div>
</div>

这种方式通常被用来配合[BEM naming conventions](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)基于原生选择器（比如`.block`）生成`.block__element` and `.block--modifier`选择器。

<div class="note">
  <p>While it might be anecdotal, generating new selectors from the current selector reference (<code>&</code>) makes those selectors unsearchable in the codebase since they do not exist per se.</p>
</div>

选择器嵌套最大的问题是将使最终的代码难以阅读。开发者需要花费巨大精力计算不同缩进级别下选择器具体的表现效果。CSS最终的表现效果往往不是浅显易懂的。

选择器越具体则声明语句越冗长，而且对最近选择器的引用(`&`)也越频繁。在某些时候，出现混淆选择器路径和探索下一级选择器的错误率很高，这非常不值得。

为了防止这种情况，我们应该**避免在伪类和伪元素外使用选择器嵌套**。这是唯一允许和建议使用的选择器嵌套方式。

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
.foo {
  color: red;

  &:hover {
    color: green;
  }

  &::before {
    content: 'pseudo-element';
  }
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo
  color: red

  &:hover
    color: green

  &::before
    content: 'pseudo-element'
{% endhighlight %}
  </div>
</div>

使用选择器嵌套选择伪类和伪元素不仅使有道理的（因为它的处理功能与选择器紧密相关），而且有助于保持总体的一致性。

### 扩展阅读

* [Beware of Selector Nesting](http://www.sitepoint.com/beware-selector-nesting-sass/)
* [The Inception Rule](http://thesassway.com/beginner/the-inception-rule)
* [Avoid nested selectors for more modular CSS](http://thesassway.com/intermediate/avoid-nested-selectors-for-more-modular-css)
