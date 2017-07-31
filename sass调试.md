# Sass 的调试 #

![](img/06.gif)

Sass 调试一直以来都是一件头痛的事情，使用 Sass 的同学都希望能在浏览器中直接调试 Sass 文件，能找到对应的行数。值得庆幸的是，现在实现并不是一件难事，只要你的浏览器支持“sourcemap”功能即可。早一点的版本，需要在编译的时候添加“--sourcemap”  参数：

	sass --watch --scss --sourcemap style.scss:style.css

在 Sass3.3 版本之上，不需要添加这个参数也可以：

	sass --watch style.scss:style.css

在命令终端，你将看到一个信息：

	>>> Change detected to: style.scss
	  write style.css
	  write style.css.map

这时你就可以像前面展示的 gif 图一样，调试你的 Sass 代码。