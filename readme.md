# 说明文件

## 安装指南

基本安装准备

```powershell
安装 python 3.7 +
更新 pip
安装 poetry
```

准备虚拟环境

```powershell
poetry.exe init
# 下面默认回车就好
poetry.exe install
# 这里只安装虚拟环境，不安装任何库文件
poetry.exe shell
python -m pip install -U pip
```

准备 vscode python 插件

```powershell
poetry.exe add -D flake8 pylint mypy yapf
```

准备 python 插件

```powershell
poetry.exe add sphinx sphinx-rtd-theme
```

准备 Sphinx 文档

```powershell
sphinx-quickstart.exe
```

```
Welcome to the Sphinx 1.8.2 quickstart utility.

Please enter values for the following settings (just press Enter to
accept a default value, if one is given in brackets).

Selected root path: .

You have two options for placing the build directory for Sphinx output.
Either, you use a directory "_build" within the root path, or you separate
"source" and "build" directories within the root path.
> Separate source and build directories (y/n) [n]: y

Inside the root directory, two more directories will be created; "_templates"
for custom HTML templates and "_static" for custom stylesheets and other static
files. You can enter another prefix (such as ".") to replace the underscore.
> Name prefix for templates and static dir [_]:

The project name will occur in several places in the built documentation.
> Project name: sphinx-tutorial
> Author name(s): john
> Project release []:

If the documents are to be written in a language other than English,
you can select a language here by its language code. Sphinx will then
translate text that it generates into that language.

For a list of supported codes, see
http://sphinx-doc.org/config.html#confval-language.
> Project language [en]:

The file name suffix for source files. Commonly, this is either ".txt"
or ".rst".  Only files with this suffix are considered documents.
> Source file suffix [.rst]:

One document is special in that it is considered the top node of the
"contents tree", that is, it is the root of the hierarchical structure
of the documents. Normally, this is "index", but if your "index"
document is a custom template, you can also set this to another filename.
> Name of your master document (without suffix) [index]:
Indicate which of the following Sphinx extensions should be enabled:
> autodoc: automatically insert docstrings from modules (y/n) [n]: y
> doctest: automatically test code snippets in doctest blocks (y/n) [n]: y
> intersphinx: link between Sphinx documentation of different projects (y/n) [n]: y
> todo: write "todo" entries that can be shown or hidden on build (y/n) [n]: n
> coverage: checks for documentation coverage (y/n) [n]:
> imgmath: include math, rendered as PNG or SVG images (y/n) [n]: y
> mathjax: include math, rendered in the browser by MathJax (y/n) [n]: y
> ifconfig: conditional inclusion of content based on config values (y/n) [n]: y
> viewcode: include links to the source code of documented Python objects (y/n) [n]:
> githubpages: create .nojekyll file to publish the document on GitHub pages (y/n) [n]: y
Note: imgmath and mathjax cannot be enabled at the same time. imgmath has been deselected.

A Makefile and a Windows command file can be generated for you so that you
only have to run e.g. `make html' instead of invoking sphinx-build
directly.
> Create Makefile? (y/n) [y]:
> Create Windows command file? (y/n) [y]:

Creating file .\source\conf.py.
Creating file .\source\index.rst.
Creating file .\Makefile.
Creating file .\make.bat.

Finished: An initial directory structure has been created.

You should now populate your master file .\source\index.rst and create other documentation
source files. Use the Makefile to build the docs, like so:
   make builder
where "builder" is one of the supported builders, e.g. html, latex or linkcheck.
```

接下来修改 make.bat

```bat
set SOURCEDIR=source
set BUILDDIR=build
```

修改为

```bat
set SOURCEDIR=source
set BUILDDIR=docs
```

修改 conf.py

```python
html_theme = 'alabaster'
```

修改为

```python
html_theme = 'sphinx_rtd_theme'

html_theme_options = {
    'collapse_navigation': True,
    'display_version': True,
    'navigation_depth': 3,
}
```

在 source\\\_templates 添加文件 layout.html

```html
{% extends "!layout.html" %} {% block extrahead %} <link href="{{
pathto("_static/style.css", True) }}" rel="stylesheet" type="text/css"> {%
endblock %}
```

在 source\\\_static 添加文件 style.css

```css
.wy-nav-content {
  max-width: none;
}
```

在 docs 目录添加 index.html

```html
<html>
  <head>
    <meta http-equiv="refresh" content="0; url=html/index.html" />
  </head>
  <body></body>
</html>
```

在 docs 目录添加 \_config.yml

```yml
include:
  - html/_images
  - html/_sources
  - html/_static
  - html/_modules
  - html/_templates
```

初次建立以后将 docs\\html\\.nojekyll 复制到 docs 目录

```powershell
make.bat html
copy docs\html\.nojekyll docs
```

至此初始化完成
