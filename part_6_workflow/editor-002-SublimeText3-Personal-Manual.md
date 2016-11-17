title: Sublime Text 3 私人手册
date: 2015-06-20 11:20:03
tags: sublime text 3
---


# 值得考虑
http://www.sitepoint.com/10-essential-sublime-text-plugins-full-stack-developer/
http://bubkoo.com/2014/01/04/sublime-text-3-plugins/

## 包管理器(Package Control)
1. ST3安装Package Control
通过ctrl + ` 打开console窗口，输入如下的python代码，回车。

```python
import urllib.request,os,hashlib; h = 'eb2297e1a458f27d836c04bb0cbaf282' + 'd0e7a3098092775ccb37ca9d6b2e4b7d'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```
<!-- more -->

更多细节，参考[Package Control Installation](https://packagecontrol.io/installation)

2. 通过Package Control安装、卸载软件


## Markdown支持
我最需要的就是markdown语法高亮，同时能够预览。

* 高亮：
[How to Set Up Sublime Text for a Vastly Better Markdown Writing Experience](https://blog.mariusschulz.com/2014/12/16/how-to-set-up-sublime-text-for-a-vastly-better-markdown-writing-experience)


简单来所就是：安装Monokai Extend和MarkdownExtend 两个插件，要注意的是，安装->重新打开ST3的过程中不要打开markdown文档，否则就会报 
> Error loading syntax file "Packages/Markdown/Markdown.tmLanguage": Unable to open Packages/Markdown/Markdown.tmLanguage

错误，解决思路查看[Issues with installation on ST3 for OSX](https://github.com/SublimeText-Markdown/MarkdownEditing/issues/115)


* 预览：
安装[Markdown HTML Prewview](https://packagecontrol.io/packages/Markdown%20HTML%20Preview)插件，通过ctrl+shift+m就可以在浏览器中预览了

## 通过Build System快捷方式在浏览器中打开当前编辑的HTML
参考：
* [How to Configure Sublime Text to Open HTML File in Chrome on Build](http://www.c-sharpcorner.com/UploadFile/370e35/how-to-configure-sublime-text-to-open-html-file-in-chrome-on/)
* [Getting Sublime 3 To Launch your HTML page in a Browser with a Key Combo](http://michaelcrump.net/getting-sublime-3-to-launch-your-html-page-in-a-browser-with-a-key-combo/)

## 注释的快捷键
ctrl + /
ctrl + shift + /

## Go编程支持
* Package: Gosublime

## Brogrammer Theme
Reference: https://github.com/kenwheeler/brogrammer-theme
在安装Package Manager之后，直接通过Installer搜索Brogrammer，安装完成后，打开Preferences -> Settings - User
在Preferences.sublime-settings文件中添加：

```json
{
  "theme": "Brogrammer.sublime-theme",
  "color_scheme": "Packages/Theme - Brogrammer/brogrammer.tmTheme"
}
```

比如我的设置内容为：

```json
{
	"theme": "Brogrammer.sublime-theme",
	"color_scheme": "Packages/Theme - Brogrammer/brogrammer.tmTheme",
	"ignored_packages":
	[
		"Vintage"
	]
}

```


## Try the Color ?
http://colorsublime.com/
https://github.com/daylerees/colour-schemes/blob/master/Hyrule.tmTheme

## How to modify the color or add new color ?
http://stackoverflow.com/questions/9807324/sublime-text-2-how-do-i-change-the-color-that-the-row-number-is-highlighted

## How to cancel the update notification ?
Proferences -> Settings-User
add "update-check" : false
Note: it's json file, be aware of the comma.


## Emmet update lang from en to zh-cn
Preference > Emmet > Settings- User:
```json
{
 "snippets": {
  "variables": {
   "lang": "zh-CN"
  }
 }
}
```

## Update Tab size to 4

http://www.ruanyifeng.com/blog/2013/06/emmet_and_haml.html