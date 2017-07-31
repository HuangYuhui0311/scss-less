# Sass 编译 #

- 命令编译
- GUI工具编译
- 自动化编译

## [Sass]命令编译 ##

命令编译是指使用你电脑中的命令终端，通过输入 Sass 指令来编译 Sass。这种编译方式是最直接也是最简单的一种方式。因为只需要在你的命令终端输入：

单文件编译：

	sass <要编译的Sass文件路径>/style.scss:<要输出CSS文件路径>/style.css

这是对一个单文件进行编译，如果想对整个项目所有 Sass 文件编译成 CSS 文件，可以这样操作：

多文件编译：

	sass sass/:css/

上面的命令表示将项目中“sass”文件夹中所有“.scss”(“.sass”)文件编译成“.css”文件，并且将这些 CSS 文件都放在项目中“css”文件夹中。

- 缺点及解决方法：

在实际编译过程中，你会发现上面的命令，只能一次性编译。每次个性保存“.scss”文件之后，都得重新执行一次这样的命令。如此操作太麻烦，其实还有一种方法，就是在编译 Sass 时，开启“watch”功能，这样只要你的代码进行任保修改，都能自动监测到代码的变化，并且给你直接编译出来：

	sass --watch <要编译的Sass文件路径>/style.scss:<要输出CSS文件路径>/style.css

当然，使用 sass 命令编译时，可以带很多的参数：![](img/04.png)


- watch 举例：

来看一个简单的示例，假设我本地有一个项目，我要把项目中“bootstrap.scss”编译出“bootstrap.css”文件，并且将编译出来的文件放在“css”文件夹中，我就可以在我的命令终端中执行：

	sass --watch sass/bootstrap.scss:css/bootstrap.css

一旦我的 bootstrap.scss 文件有任何修改，只要我重新保存了修改的文件，命令终端就能监测，并重新编译出文件：![](img/05.png)

## [Sass]GUI 界面工具编译 ##
对于 GUI 界面编译工具，目前较为流行的主要有：

- Koala (http://koala-app.com/)
- Compass.app（http://compass.kkbox.com/）
- Scout（http://mhs.github.io/scout-app/）
- CodeKit（https://incident57.com/codekit/index.html）
- Prepros（https://prepros.io/）

推荐使用前两个。

## [Sass]自动化编译 ##

- Grunt 配置 Sass 编译的示例代码

		module.exports = function(grunt) {
		    grunt.initConfig({
		        pkg: grunt.file.readJSON('package.json'),
		        sass: {
		            dist: {
		                files: {
		                    'style/style.css' : 'sass/style.scss'
		                }
		            }
		        },
		        watch: {
		            css: {
		                files: '**/*.scss',
		                tasks: ['sass']
		            }
		        }
		    });
		    grunt.loadNpmTasks('grunt-contrib-sass');
		    grunt.loadNpmTasks('grunt-contrib-watch');
		    grunt.registerTask('default',['watch']);
		}

想了解 Grunt 同学请单击这里学习《Grunt-beginner前端自动化工具》。


- Gulp 配置 Sass 编译的示例代码

		var gulp = require('gulp');
		var sass = require('gulp-sass');
		
		gulp.task('sass', function () {
		    gulp.src('./scss/*.scss')
		        .pipe(sass())
		        .pipe(gulp.dest('./css'));
		});
		
		gulp.task('watch', function() {
		    gulp.watch('scss/*.scss', ['sass']);
		});
		
		gulp.task('default', ['sass','watch']);

## [Sass]常见的编译错误 ##

- 最为常见的一个错误就是字符编译引起的。在Sass的编译的过程中，是不是支持“GBK”编码的。所以在创建 Sass 文件时，就需要将文件编码设置为“utf-8”。

- 另外一个错误就是路径中的中文字符引起的。建议在项目中文件命名或者文件目录命名不要使用中文字符。

- 而至于人为失误造成的编译失败，在编译过程中都会有具体的说明，大家可以根据编译器提供的错误信息进行对应的修改。

