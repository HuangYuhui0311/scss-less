## Sass 和 SCSS 的区别 ： ##

Sass 和 SCSS 其实是同一种东西，我们平时都称之为 Sass，两者之间不同之处有以下两点：

- 文件扩展名不同，Sass 是以“.sass”后缀为扩展名，而 SCSS 是以“.scss”后缀为扩展名
- 语法书写方式不同，Sass 是以严格的缩进式语法规则来书写，不带大括号({})和分号(;)，而 SCSS 的语法书写和我们的 CSS 语法书写方式非常类似。

先来看一个示例：

## Sass 语法 ##

	$font-stack: Helvetica, sans-serif  //定义变量
	$primary-color: #333 //定义变量
	
	body
	  font: 100% $font-stack
	  color: $primary-color

## SCSS 语法 ##

	$font-stack: Helvetica, sans-serif;
	$primary-color: #333;
	
	body {
	  font: 100% $font-stack;
	  color: $primary-color;
	}

## 编译出来的 CSS ##

	body {
	  font: 100% Helvetica, sans-serif;
	  color: #333;
	}


<a href="http://www.imooc.com">资源来源：慕课网</a>