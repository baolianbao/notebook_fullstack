---
title: Visual Studio Code Essentials
date: 2016-08-18 22:05:40
tags:
---


## 如何自动换行：
http://askubuntu.com/questions/622631/how-to-wrap-text-comments-in-visual-studio-code

File > Preferences > User Settings
Paste the following in settings.json

// Place your settings in this file to overwrite the default settings

{ "editor.wrappingColumn": 0 }
If you already have settings.json, just add

"editor.wrappingColumn": 0
As the settings is in JSON, last settings are without the comma "," as you see in Default settings and the "settings.json" overide all the Default settings

## 如何从终端打开VSC？
通过Command + P， 然后输入:`>shell command`选择`install 'code' command in PATH`，然后就可以在终端里直接使用code了：
* `code` 打开VSC
* `code .` 打开当前文件夹
* `code somefile`编辑某个文件
参考：https://code.visualstudio.com/docs/setup/osx


## 多行编辑
Windows： Shift+Alt+LeftMouse进行块选 或者 Alt + LeftMouse进行单行选择
* [Multiline editing in VSCode](http://stackoverflow.com/questions/30037808/multiline-editing-in-vscode)
* [Does Visual Studio Code have box select/multi-line edit?](http://stackoverflow.com/questions/30384442/does-visual-studio-code-have-box-select-multi-line-edit)
