# [Sass]不同样式风格的输出方法 #

- 嵌套输出方式 nested
- 展开输出方式 expanded  
- 紧凑输出方式 compact 
- 压缩输出方式 compressed

## [Sass]嵌套输出方式 nested ##
Sass 提供了一种嵌套显示 CSS 文件的方式。例如

	nav {
	  ul {
	    margin: 0;
	    padding: 0;
	    list-style: none;
	  }
	
	  li { display: inline-block; }
	
	  a {
	    display: block;
	    padding: 6px 12px;
	    text-decoration: none;
	  }
	}

在编译的时候带上参数“ --style nested”:

	sass --watch test.scss:test.css --style nested

编译出来的 CSS 样式风格：

	nav ul {
	  margin: 0;
	  padding: 0;
	  list-style: none; }
	nav li {
	  display: inline-block; }
	nav a {
	  display: block;
	  padding: 6px 12px;
	  text-decoration: none; }

## [Sass]展开输出方式 expanded ##

	nav {
	  ul {
	    margin: 0;
	    padding: 0;
	    list-style: none;
	  }
	
	  li { display: inline-block; }
	
	  a {
	    display: block;
	    padding: 6px 12px;
	    text-decoration: none;
	  }
	}

在编译的时候带上参数“ --style expanded”:

	sass --watch test.scss:test.css --style expanded

这个输出的 CSS 样式风格和 nested 类似，<span style="color:red">只是大括号在另起一行</span>，同样上面的代码，编译出来：

	nav ul {
	  margin: 0;
	  padding: 0;
	  list-style: none;
	}
	nav li {
	  display: inline-block;
	}
	nav a {
	  display: block;
	  padding: 6px 12px;
	  text-decoration: none;
	}

## [Sass]紧凑输出方式 compact ##

	nav {
	  ul {
	    margin: 0;
	    padding: 0;
	    list-style: none;
	  }
	
	  li { display: inline-block; }
	
	  a {
	    display: block;
	    padding: 6px 12px;
	    text-decoration: none;
	  }
	}

在编译的时候带上参数“ --style compact”:

	sass --watch test.scss:test.css --style compact

该方式适合那些喜欢单行 CSS 样式格式的朋友，编译后的代码如下：

	nav ul { margin: 0; padding: 0; list-style: none; }
	nav li { display: inline-block; }
	nav a { display: block; padding: 6px 12px; text-decoration: none; }

## [Sass]压缩输出方式 compressed ##

	nav {
	  ul {
	    margin: 0;
	    padding: 0;
	    list-style: none;
	  }
	
	  li { display: inline-block; }
	
	  a {
	    display: block;
	    padding: 6px 12px;
	    text-decoration: none;
	  }
	}

在编译的时候带上参数“ --style compressed”:

	sass --watch test.scss:test.css --style compressed

压缩输出方式会去掉标准的 Sass 和 CSS 注释及空格。也就是压缩好的 CSS 代码样式风格：

	nav ul{margin:0;padding:0;list-style:none}nav li{display:inline-block}nav a{display:block;padding:6px 12px;text-decoration:none}
	
<a href="http://www.imooc.com">资源来源：慕课网</a>
