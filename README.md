# 中文 Manpages 手册翻译
----------------------

## 大纲

中文 Manpages 手册翻译项目的翻译流程有四步，包括预翻译、翻译、排版和发布。这里是翻译流程的第三步，排版 REPO。

本 REPO 从 <https://github.com/manpages-zh/Translate> 读取翻译好的中文 HTML并排版，因为 man 程序的问题，以及中文文档的特殊性，并没有可以直接生成排版良好的中文手册的工具，目前我们使用 docbook,ronn(Markdnwon 兼容）来进行手工排版。这是个枯燥的过程，但必不可少。您可以添加自己的排版工具，只要能最终生成格式良好，每行不超过 80 个字符的 Groff 手册文件即可。

groff 格式是手册页的基本格式，它是由一些标记对文本进行标记，然后通过专门的软件进行分析实现的。其符号和标记的详细信息可以参阅 man7目录中的roff.7, mdoc.samples.7, man.7.

## 项目结构

`docbook/` 是排版 docbook 格式所需的文件夹，`html_zh` 是从翻译流程中得到的中文 HTML 文件，ronn 是对 HTML 排版得到的 ronn 文件，man 是 ronn 生成的 groff 手册文件。 

本 REPO 还包括一些第三方模块，已满足不同人员使用不同排版工具的需求。如下：

```csv
├── man2ronn        		Convert man pages to ronn-format files
├── roff-processzh		process Chinese man roff document for better display 
└── rtomayko/ronn          		the opposite to roff
```

本 REPO 得到的中文手册最终会来到 <https://github.com/manpages-zh/manpages_zh> 发布。

# 排版
----------------------

## 使用 ronn 进行排版

ronn 程序大概已经在您系统的包管理器里面了，所以直接安装即可，如果没有，这里提供了一个子模块 `rtomayko/`，里面是从 Github 获取的 ronn 的源代码。您也可以在这里找到它的源文件：<https://github.com/rtomayko/ronn> 编译安装即可。

ronn 简单易学，可以生成手册和 HTML 两种格式文档。它包括 ronn 程序本身和 ronn-format 标记语法。该语法类似于 markdown。ronn 命令可以将符合 ronn-format 标记的 `*.ronn` 文件转化成man手册页，ronn-format 包含markdown格式的所有特性，同时也引入了一些其他在man手册中使用的约定和标记。ronn 简单轻便，如果您熟悉 Markdown,那么您可以很快上手，并排版生成 Groff 手册文件，因此是目前我们推荐的方式。

ronn-format 的语法请参考 `./ronn-format.html`。ronn 命令使用方法如下：

为一个或多个 ronn 文件一次性生成手册和 HTML 文档：

	$ ronn man/ronn.5.ronn
	roff: man/ronn.5
	html: man/ronn.5.html

只生成 HTML 文件：

	$ ronn --html man/markdown.5.ronn
	html: man/markdown.5.html

只生成手册文件：

	$ ronn --roff man/*.ronn
	
需要注意 ronn-format 并不包含所有的roff格式特性，因此如果您需要 ronn 不支持的格式，请参考 docbook。

## 使用 Docbook 排版

请参考 docbook 文件夹。
