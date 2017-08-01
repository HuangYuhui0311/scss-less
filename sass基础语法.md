# Sass的基础语法 #
- 变量
- 嵌套
- 混合宏
- 扩展/继承
- 占位符


## [Sass]普通变量与默认变量 ##



1. 普通变量：定义之后可以在全局范围内使用。

		$fontSize: 12px;
		body{
		    font-size:$fontSize;
		}

	编译后的css代码：

		body{
		    font-size:12px;
		}




2. 默认变量

	sass 的默认变量仅需要在值后面加上<span style="color:blue"> !default </span>即可。

		$baseLineHeight:1.5 !default;
		body{
		    line-height: $baseLineHeight; 
		}

	编译后的css代码：

		body{
		    line-height:1.5;
		}


	sass 的默认变量一般是用来设置默认值，然后根据需求来覆盖的，覆盖的方式也很简单，只需要在默认变量之前重新声明下变量即可。
 

		$baseLineHeight: 2;
		$baseLineHeight: 1.5 !default;
		body{
		    line-height: $baseLineHeight; 
		}

	编译后的css代码：

		body{
		    line-height:2;
		}


	可以看出现在编译后的 line-height 为 2，而不是我们默认的 1.5。默认变量的价值在进行组件化开发的时候会非常有用。

## [Sass]局部变量和全局变量 ##

Sass 中变量的作用域在过去几年已经发生了一些改变。直到最近，规则集和其他范围内声明变量的作用域才默认为本地。如果已经存在同名的全局变量，从 3.4 版本开始，Sass 已经可以正确处理作用域的概念，并通过创建一个新的局部变量来代替。


先来看一下代码例子：

	//SCSS
	$color: orange !default;//定义全局变量(在选择器、函数、混合宏...的外面定义的变量为全局变量)
	.block {
	  color: $color;//调用全局变量
	}
	em {
	  $color: red;//定义局部变量
	  a {
	    color: $color;//调用局部变量
	  }
	}
	span {
	  color: $color;//调用全局变量
	}

css 的结果：

//CSS
	.block {
	  color: orange;
	}
	em a {
	  color: red;
	}
	span {
	  color: orange;
	}

上面的示例演示可以得知，在元素内部定义的变量不会影响其他元素。如此可以简单的理解成，全局变量就是定义在元素外面的变量，如下代码：

	$color:orange !default;

$color 就是一个全局变量，而定义在元素内部的变量，比如 $color:red; 是一个局部变量。

除此之外，Sass 现在还提供一个 !global 参数。!global 和 !default 对于定义变量都是很有帮助的。我们之后将会详细介绍这两个参数的使用以及其功能。

## 全局变量的影子 ##

当在局部范围（选择器内、函数内、混合宏内...）声明一个已经存在于全局范围内的变量时，局部变量就成为了全局变量的影子。基本上，局部变量只会在局部范围内覆盖全局变量。

上面例子中的 em 选择器内的变量 $color 就是一个全局变量的影子。

	//SCSS
	$color: orange !default;//定义全局变量
	.block {
	  color: $color;//调用全局变量
	}
	em {
	  $color: red;//定义局部变量（全局变量 $color 的影子）
	  a {
	    color: $color;//调用局部变量
	  }
	}

## 什么时候声明变量？ ##

建议：创建变量只适用于感觉确有必要的情况下。不要为了某些骇客行为而声明新变量，这丝毫没有作用。只有满足所有下述标准时方可创建新变量：

- 该值至少重复出现了两次；
- 该值至少可能会被更新一次；
- 该值所有的表现都与变量有关（非巧合）。

基本上，没有理由声明一个永远不需要更新或者只在单一地方使用变量。

<span style="color:darkred">温馨小提示：您在学习 sass 时，除了在我们网页上可以做练习，还有一个便利在线编辑器网址如下：http://sassmeister.com/</span>

# [Sass]嵌套 #

Sass 中还提供了选择器嵌套功能，但这也并不意味着你在 Sass 中的嵌套是无节制的，因为你嵌套的层级越深，编译出来的 CSS 代码的选择器层级将越深，这往往是大家不愿意看到的一点。这个特性现在正被众多开发者滥用。

选择器嵌套为样式表的作者提供了一个通过局部选择器相互嵌套实现全局选择的方法，Sass 的嵌套分为三种：

- 选择器嵌套
- 属性嵌套
- 伪类嵌套

## 选择器嵌套 ##

假设我们有一段这样的结构：

	<header>
	<nav>
	    <a href=“##”>Home</a>
	    <a href=“##”>About</a>
	    <a href=“##”>Blog</a>
	</nav>
	<header>

想选中 header 中的 a 标签，在写 CSS 会这样写：

	nav a {
	  color:red;
	}
	
	header nav a {
	  color:green;
	}

那么在 Sass 中，就可以使用选择器的嵌套来实现：

	nav {
	  a {
	    color: red;
	
	    header & {
	      color:green;
	    }
	  }  
	}

<span style="color:darkred">注：&是父选择器的标识符</span>

## 属性嵌套 ##

Sass 中还提供属性嵌套，CSS 有一些属性前缀相同，只是后缀不一样，比如：border-top/border-right，与这个类似的还有 margin、padding、font 等属性。假设你的样式中用到了：

	.box {
	    border-top: 1px solid red;
	    border-bottom: 1px solid green;
	}

在 Sass 中我们可以这样写：

	.box {
	  border: {
	   top: 1px solid red;
	   bottom: 1px solid green;
	  }
	}

## 伪类嵌套 ##

其实伪类嵌套和属性嵌套非常类似，只不过他需要借助`&`符号一起配合使用。我们就拿经典的“clearfix”为例吧：

	.clearfix{
		&:before,
		&:after {
		    content:"";
		    display: table;
		  }
		&:after {
		    clear:both;
		    overflow: hidden;
		  }
	}

编译出来的 CSS：

	clearfix:before, .clearfix:after {
	  content: "";
	  display: table;
	}
	.clearfix:after {
	  clear: both;
	  overflow: hidden;
	}

## 避免选择器嵌套： ##

- 选择器嵌套最大的问题是将使最终的代码难以阅读。开发者需要花费巨大精力计算不同缩进级别下的选择器具体的表现效果。
- 选择器越具体则声明语句越冗长，而且对最近选择器的引用(&)也越频繁。在某些时候，出现混淆选择器路径和探索下一级选择器的错误率很高，这非常不值得。

为了防止此类情况，我们应该尽可能避免选择器嵌套。然而，显然只有少数情况适应这一措施。

# [Sass]混合宏 #

- 声明混合宏
- 调用混合宏
- 混合宏的参数

## 声明混合宏 ##

<b>不带参数混合宏：</b>

在 Sass 中，使用“@mixin”来声明一个混合宏。如：

	@mixin border-radius{
	    -webkit-border-radius: 5px;
	    border-radius: 5px;
	}

其中 @mixin 是用来声明混合宏的关键词；border-radius 是混合宏的名称；大括号里面是复用的样式代码。

<b>带参数混合宏：</b>

除了声明一个不带参数的混合宏之外，还可以在定义混合宏时带有参数，如：

	@mixin border-radius($radius:5px){
	    -webkit-border-radius: $radius;
	    border-radius: $radius;
	}

<b>复杂的混合宏：</b>

上面是一个简单的定义混合宏的方法，当然， Sass 中的混合宏还提供更为复杂的，你可以在大括号里面写上带有逻辑关系（如：@if...@else），帮助更好的做你想做的事情,如：

	@mixin box-shadow($shadow...) {
	  @if length($shadow) >= 1 {
	    @include prefixer(box-shadow, $shadow);
	  } @else{
	    $shadow:0 0 4px rgba(0,0,0,.3);
	    @include prefixer(box-shadow, $shadow);
	  }
	}

这个 box-shadow 的混合宏，带有多个参数，这个时候可以使用“ … ”来替代。简单的解释一下，当 $shadow 的参数数量值大于或等于“ 1 ”时，表示有多个阴影值，反之调用默认的参数值“ 0 0 4px rgba(0,0,0,.3) ”。

## 调用混合宏 ##

在 Sass 中通过 @mixin 关键词声明了一个混合宏，在实际调用中，可以用关键词“@include”来调用声明好的混合宏。

	//声明
	@mixin border-radius{
	    -webkit-border-radius: 3px;
	    border-radius: 3px;
	}

	//调用
	button {
	    @include border-radius;
	}

这个时候编译出来的 CSS:

	button {
	  -webkit-border-radius: 3px;
	  border-radius: 3px;
	}

# [Sass]混合宏的参数 #

## 传一个不带值的参数 ##

	@mixin border-radius($radius){
	  -webkit-border-radius: $radius;
	  border-radius: $radius;
	}
	//调用
	.box {
	  @include border-radius(3px);
	}

## 传一个带值的参数 ##
	
	//在混合宏“border-radius”传了一个参数“$radius”，而且给这个参数赋予了一个默认值“3px”。
	@mixin border-radius($radius:3px){
	  -webkit-border-radius: $radius;
	  border-radius: $radius;
	}



在调用类似这样的混合宏时，会多有一个机会，假设你的页面中的圆角很多地方都是“3px”的圆角，那么这个时候只需要调用默认的混合宏“border-radius”:

	.btn {
	  @include border-radius;
	}

编译出来的 CSS:

	.btn {
	  -webkit-border-radius: 3px;
	  border-radius: 3px;
	}

但有的时候，页面中有些元素的圆角值不一样，那么可以随机给混合宏传值，如：

	.box {
	  @include border-radius(50%);
	}

编译出来的 CSS:

	.box {
	  -webkit-border-radius: 50%;
	  border-radius: 50%;
	}

## 传多个参数 ##

Sass 混合宏除了能传一个参数之外，还可以传多个参数，如：

	@mixin center($width,$height){
		width: $width;
		height: $height;
		position: absolute;
		top: 50%;
		left: 50%;
		margin-top: -($height) / 2;
		margin-left: -($width) / 2;
	}

在混合宏“center”就传了多个参数。在实际调用和其调用其他混合宏是一样的：

	.box-center {
		@include center(500px,300px);
	}

编译出来 CSS:

	.box-center {
		width: 500px;
		height: 300px;
		position: absolute;
		top: 50%;
		left: 50%;
		margin-top: -150px;
		margin-left: -250px;
	}

  有一个特别的参数“…”。当混合宏传的参数过多之时，可以使用参数来替代，如：

	@mixin box-shadow($shadows...){
	  @if length($shadows) >= 1 {
	    -webkit-box-shadow: $shadows;
	    box-shadow: $shadows;
	  } @else {
	    $shadows: 0 0 2px rgba(#000,.25);
	    -webkit-box-shadow: $shadow;
	    box-shadow: $shadow;
	  }
	}

在实际调用中：

	.box {
	  @include box-shadow(0 0 1px rgba(#000,.5),0 0 2px rgba(#000,.2));
	}

编译出来的CSS:

	.box {
	  -webkit-box-shadow: 0 0 1px rgba(0, 0, 0, 0.5), 0 0 2px rgba(0, 0, 0, 0.2);
	  box-shadow: 0 0 1px rgba(0, 0, 0, 0.5), 0 0 2px rgba(0, 0, 0, 0.2);
	}

## 混合宏的不足 ##

混合宏在实际编码中给我们带来很多方便之处，特别是对于复用重复代码块。但其最大的不足之处是会生成冗余的代码块。比如在不同的地方调用一个相同的混合宏时。如：

	@mixin border-radius{
	  -webkit-border-radius: 3px;
	  border-radius: 3px;
	}
	
	.box {
	  @include border-radius;
	  margin-bottom: 5px;
	}
	
	.btn {
	  @include border-radius;
	}

示例在“.box”和“.btn”中都调用了定义好的“border-radius”混合宏。先来看编译出来的 CSS：

	.box {
	  -webkit-border-radius: 3px;
	  border-radius: 3px;
	  margin-bottom: 5px;
	}
	
	.btn {
	  -webkit-border-radius: 3px;
	  border-radius: 3px;
	}

上例明显可以看出，Sass 在调用相同的混合宏时，并不能智能的将相同的样式代码块合并在一起。这也是 Sass 的混合宏最不足之处。

## [Sass]扩展/继承 ##

在 Sass 中是通过关键词 “@extend”来继承已存在的类样式块，从而实现代码的继承。如下所示：

	//SCSS
	.btn {
	  border: 1px solid #ccc;
	  padding: 6px 10px;
	  font-size: 14px;
	}
	
	.btn-primary {
	  background-color: #f36;
	  color: #fff;
	  @extend .btn;
	}
	
	.btn-second {
	  background-color: orange;
	  color: #fff;
	  @extend .btn;
	}

编译出来之后：

	//CSS
	.btn, .btn-primary, .btn-second {
	  border: 1px solid #ccc;
	  padding: 6px 10px;
	  font-size: 14px;
	}
	
	.btn-primary {
	  background-color: #f36;
	  color: #fff;
	}
	
	.btn-second {
	  background-clor: orange;
	  color: #fff;
	}

从示例代码可以看出，在 Sass 中的继承，可以继承类样式块中所有样式代码，而且编译出来的 CSS 会将选择器合并在一起，形成组合选择器。

## [Sass]占位符 % ##

 % 声明的代码，如果不被 @extend 调用的话，不会产生任何代码。来看一个演示：

	%mt5 {
	  margin-top: 5px;
	}
	%pt5{
	  padding-top: 5px;
	}

这段代码没有被 @extend 调用，他并没有产生任何代码块，只是静静的躺在你的某个 SCSS 文件中。只有通过 @extend 调用才会产生代码：

	.btn {
	  @extend %mt5;
	  @extend %pt5;
	}
	
	.block {
	  @extend %mt5;
	
	  span {
	    @extend %pt5;
	  }
	}

编译出来的CSS

	//CSS
	.btn, .block {
	  margin-top: 5px;
	}
	
	.btn, .block span {
	  padding-top: 5px;
	}

从编译出来的 CSS 代码可以看出，通过 @extend 调用的占位符，编译出来的代码会将相同的代码合并在一起。这也是我们希望看到的效果，也让你的代码变得更为干净。

## [Sass]混合宏 VS 继承 VS 占位符 ##

初学者都常常纠结于这个问题“什么时候用混合宏，什么时候用继承，什么时候使用占位符？”其实他们各有各的优点与缺点：

<b>a) Sass 中的混合宏使用</b>

- 混合宏不会自动合并相同的样式代码，如果在样式文件中调用同一个混合宏，会产生多个对应的样式代码，造成代码的冗余，这也是 CSSer 无法忍受的一件事情。不过他并不是一无事处，他可以传参数。

- 个人建议：如果你的代码块中涉及到变量，建议使用混合宏来创建相同的代码块。

<b>b) Sass 中继承</b>

- 使用继承后，编译出来的 CSS 会将使用继承的代码块合并到一起，通过组合选择器的方式向大家展现，比如 .mt, .block, .block span, .header。这样编译出来的代码相对于混合宏来说要干净的多，也是 CSSer 期望看到。但是他不能传变量参数。

- 个人建议：如果你的代码块不需要专任何变量参数，而且有一个基类已在文件中存在，那么建议使用 Sass 的继承。

<b>c) 占位符</b>

- 编译出来的 CSS 代码和使用继承基本上是相同，只是不会在代码中生成占位符 mt 的选择器。那么占位符和继承的主要区别的，“占位符是独立定义，不调用的时候是不会在 CSS 中产生任何代码；继承是首先有一个基类存在，不管调用与不调用，基类的样式都将会出现在编译出来的 CSS 代码中。”

来看一个表格：![](img/07.jpg)

## [Sass]插值#{} ##

	$properties: (margin, padding);
	@mixin set-value($side, $value) {
	    @each $prop in $properties {
	        #{$prop}-#{$side}: $value;
	    }
	}
	.login-box {
	    @include set-value(top, 14px);
	}

编译成 CSS：

	.login-box {
	    margin-top: 14px;
	    padding-top: 14px;
	}

这是 Sass 插值中一个简单的实例。当你想设置属性值的时候你可以使用字符串插入进来。另一个有用的用法是构建一个选择器。可以这样使用：

	@mixin generate-sizes($class, $small, $medium, $big) {
	    .#{$class}-small { font-size: $small; }
	    .#{$class}-medium { font-size: $medium; }
	    .#{$class}-big { font-size: $big; }
	}
	@include generate-sizes("header-text", 12px, 20px, 40px);

编译出来的 CSS:

	.header-text-small { font-size: 12px; }
	.header-text-medium { font-size: 20px; }
	.header-text-big { font-size: 40px; }

一旦你发现这一点，你就会想到超级酷的 mixins，用来生成代码或者生成另一个 mixins。然而，这并不完全是可能的。第一个限制，这很可能会删除用于 Sass 变量的插值。

	$margin-big: 40px;
	$margin-medium: 20px;
	$margin-small: 12px;
	@mixin set-value($size) {
	    margin-top: $margin-#{$size};
	}
	.login-box {
	    @include set-value(big);
	}

上面的 Sass 代码编译出来，你会得到下面的信息：

	error style.scss (Line 5: Undefined variable: “$margin-".)

所以，#{}语法并不是随处可用，你也不能在 mixin 中调用：

	@mixin updated-status {
	    margin-top: 20px;
	    background: #F00;
	}
	$flag: "status";
	.navigation {
	    @include updated-#{$flag};
	}

上面的代码在编译成 CSS 时同样会报错：

	error style.scss (Line 7: Invalid CSS after "...nclude updated-": expected "}", was "#{$flag};")
幸运的是，可以使用 @extend 中使用插值。例如：

	%updated-status {
	    margin-top: 20px;
	    background: #F00;
	}
	.selected-status {
	    font-weight: bold;
	}
	$flag: "status";
	.navigation {
	    @extend %updated-#{$flag};
	    @extend .selected-#{$flag};
	}
	

上面的 Sass 代码是可以运行的，可以动态的插入 .class 和 %placeholder。当然他们不能接受像 mixin 这样的参数，上面的代码编译出来的 CSS:

	.navigation {
	    margin-top: 20px;
	    background: #F00;
	}
	.selected-status, .navigation {
	    font-weight: bold;
	}
## [Sass]注释 ##
- //
- /**/

## [Sass]数据类型 ##

 Sass 和 JavaScript 语言类似，也具有自己的数据类型，在 Sass 中包含以下几种数据类型：

- 数字: 如，1、 2、 13、 10px；
- 字符串：有引号字符串或无引号字符串，如，"foo"、 'bar'、 baz；
- 颜色：如，blue、 #04a3f9、 rgba(255,0,0,0.5)；
- 布尔型：如，true、 false；
- 空值：如，null；
- 值列表：用空格或者逗号分开，如，1.5em 1em 0 2em 、 Helvetica, Arial, sans-serif。


SassScript 也支持其他 CSS 属性值（property value），比如 Unicode 范围，或 !important 声明。然而，Sass 不会特殊对待这些属性值，一律视为无引号字符串 (unquoted strings)。

在编译 CSS 文件时不会改变其类型。只有一种情况例外，使用 #{ }插值语句 (interpolation) 时，有引号字符串将被编译为无引号字符串，这样方便了在混合指令 (mixin) 中引用选择器名。

需要注意的是：当 deprecated = property syntax 时 （暂时不理解是怎样的情况），所有的字符串都将被编译为无引号字符串，不论是否使用了引号。

## Sass列表函数（Sass list functions）： ##

- nth函数（nth function） 可以直接访问值列表中的某一项；
- join函数（join function） 可以将多个值列表连结在一起；
- append函数（append function） 可以在值列表中添加值； 
- @each规则（@each rule） 则能够给值列表中的每个项目添加样式。


<a href="http://www.imooc.com">资源来源：慕课网</a>