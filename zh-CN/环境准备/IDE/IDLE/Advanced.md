---
title: IDLE进阶使用
---

虽然IDLE并不适合开发者，但对于轻度使用（例如编写一些小文件，进行Debug？shell等）也是不错的选择。整个IDLE的大小不超过3M，所以你并不需要将其卸载。

！重要的是，一些竞赛禁止使用除IDLE以外的编辑器。


好吧，这就没办法了。  
所以配置好一个适合自己的IDLE，也能提高开发效率。

适合
可以根据自己的习惯进行配置


介绍
1. Python shell

shell 俗称壳
WB Python shell 是一种CLI shell。

WB CLI GUI

打开IDLE，默认打开的是 shell window （Python shell 窗口）
由于，国人也称为交互模式

可以干什么

与之相对应的就是文件编辑模式
打开：`Ctrl+N`ew （或File -> New File）


IDLE版本问题？

代码自动补齐
Debug模式
python文档

行号
自动保存

注释Alt
Ctrl+]
F5
自己探索
相较于VScode，额
你可以花点精力配置VScode以获得一个无比舒适的 可以同步？


# 配置外观，高亮颜色

问题：中文输入过程中
窗口被任务栏遮盖
提示保存
zoom height
Ctrl+F6


快捷键自己探索？

1 打开IDLE Shell
1)Win+R(打开运行窗口)
2)输入：cmd(进入dos命令窗口)
3)输入：python -m idlelib.idle （打开IDLE Shell）

2 Alt+p或Alt+n快捷键：
在IDLE的提示符下：>>>
输入：
>>>a=100
>>>b=200
>>>a+b
300
这时按快捷键Alt+p可以出现上一次键入的a+b,按Alt+n可以出现a=100，如果连续按则可依次循环出现上面按过的键（Alt+p逆序出现键值，Alt+n正序再现键值）

3 在提示符下输入：qu，然后按Tab
>>>qu  (按Tab,则会自动补全)
>>>quit
你可以修改成：
>>>quit()
按回车就退出IDLE了。
如果在提示符>>>输入的不是qu,而是he，然后按Tab键，则会弹出一个列表，你可以选help,然后输入括号，见下面
>>>help()   #输入回车后，可进入帮助页面状态
help> print    #输入print,然后按回车键，可以看到print的用法。退出可以输出Ctrl+ｚ
这时可以重新回到python界面。

4 在IDLE中按Ｃtrl+F6,清空导入记录，重启Shell
5 更多的快捷键：
F1	打开 Python 帮助文档	Python文件窗口和Shell 均可用
Alt+P	浏览历史命令（上一条）	仅 Python Shell 窗口可用
Alt+N	浏览历史命令（下一条）	仅 Python Shell 窗口可用
Alt+/	自动补全前面曾经出现过的单词，如果之前有多个单词具有相同前缀，可以连续按下该快捷键，在多个单词中间循环选择	Python 文件窗口和 Shell 窗口均可用
Alt+3	注释代码块	仅 Python 文件窗口可用
Alt+4	取消代码块注释	仅 Python 文件窗口可用
Alt+g	转到某一行	仅 Python 文件窗口可用
Ctrl+Z	撤销一步操作	Python 文件窗口和 Shell 窗口均可用
Ctrl+Shift+Z	恢复上—次的撤销操作	Python 文件窗口和 Shell 窗口均可用
Ctrl+S	保存文件	Python 文件窗口和 Shell 窗口均可用
Ctrl+]	缩进代码块	仅 Python 文件窗口可用
Ctrl+[	取消代码块缩进	仅 Python 文件窗口可用
Ctrl+F6	重新启动 Python Shell	仅 Python Shell 窗口可用



# Debug

Go表示运行完相当于eclipse的F8，不过按F5后先要go一下才能往下走，默认是不运行的

Step表示一步一步相当于eclipse的F5

Over表示跳过函数方法相当于eclipse的F6

Out表示跳出本函数相当于eclipse的F7

IDLE编辑器快捷键

自动补全代码 Alt+/（查找编辑器内已经写过的代码来补全)

补全提示 Ctrl+Shift+space(默认与输入法冲突，修改之)

(方法：Options->configure IDLE…->Keys-> force-open-completions

提示的时候只要按空格就出来对于的，否则翻上下键不需要按其他键自动就补全了)

后退 Ctrl+Z

重做 Ctrl+Shift+Z