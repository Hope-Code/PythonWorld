---
lang: zh-CN
title: 『fun』实现单行输出
description: Python如何实现单行|一行输出
---

>>@Micheal @李沛霖 @刘老师 and 看到这篇文章所有我的朋友：
>
>第一次写没有任何经验，想把每种方法解释清楚一点，这使我篇幅过长了。
>可能会有冗余或者没解释清楚的地方，Error肯定会有的。
>要是有任何需要修改的地方请直接划到底部，通过评论指出谢谢:pray:
>
>and more...  
>代码框里的内容没有调试，不知道是否正确。  
>里面的一些链接可能不会跳转到理想位置，~~原因是我还没开始写呢~~

**让我们来看一个有意思的现象：**

当执行这一段代码的时候：

```python
print('Hello, World!')
print('From Cody')
```

你会得到这样的输出：
```
Hello, World!  
From Cody
```
Cody: 这不是很正常吗？  

Hopecode: 是的，让我们来看看别的语言：

:::tabs
@tab C++
```cpp
printf("Hello, World!");
printf("From Cody");
```
@tab Java
```java
System.out.printf("Hello, World!");
System.out.printf("From Cody");
```
:::

:::::details More...
::::tip
许多编程语言的行尾有分号`;`，是语句结束的标志。  
在Python中，分号`;`也可以作为语句结束，主要用于分隔语句。  
例如下面的语句可以顺次给a，b赋值。
:::tabs

@tab 示例
```python
a=1;b=2
```
等同于
```python
a=1
b=2
```

@tab 错误的写法
```python
a=1 b=2
```
会得到 Syntax Error 的报错。

:::
`;`用来分隔语句使代码更易于阅读。
::::
:::tip
printf是这两种语言的常用格式化输出之一。其中f表示format。
:::
:::::
代码是不是很相似？来让我们看看这两种语言的输出结果：
```
Hello, World!From Cody
```
Cody：:question:为什么输出只有一行？

### 默认换行

Hopecode：是的，对比这三种语言，会发现Python的`print()` 默认换行。

这很方便。因为更多情况下，我们并不想让信息粘在一起。这样让你在输出的时候，不需要注意是否需要换行。  
但在大部分语言中，并没有这样的设定，你需要手动添加换行。

:::tip
你应该把「换行」当做像a,b,c,d一样的字符。  
几乎所有语言中，字符串`\n`等于一个换行。例如：
```python
print('a\nb')
```
输出：
```
a
b
```
:::

### 不默认换行

不过不默认换行也有好处：如果我需要换行就换行，不需要就不换。  
比如这个情况：
<div class="language-text line-numbers-mode" data-ext="text">
    <button class="copy-code-button" aria-label="复制代码" data-copied="已复制" data-balloon-pos="left">
        <div class="copy-icon"></div>
    </button>
    <pre class="language-text" copy-code-registered="">
<code>Cody去Hope Store买了两样物品。<br>一件是1024核8192位处理器，花费n<sub>1</sub>；<br>另一件是3D超全息空气显示屏，花费n<sub>2</sub>。<br>请计算他的花费总额N。<br>
※输入格式：两行，一行一个整数，表示n<sub>1</sub>和n<sub>2</sub>。         
※输出格式：总计花费N</code></pre>
    <div class="line-numbers" aria-hidden="true">
        <div class="line-number"></div>
        <div class="line-number"></div>
        <div class="line-number"></div>
        <div class="line-number"></div>
        <div class="line-number"></div>
        <div class="line-number"></div>
        <div class="line-number"></div>
    </div>
</div>

[点这里去测试](https://oj.hopecode.com.cn/problem/0010)

Cody的哥哥Codyy和Codyyy分别用Java和C++成功获得了AC。

:::info Word Bank
「AC」Accepted 通过
:::

Cody：我也写好了：
```python
n1=int(input())
n2=int(input())
N=n1+n2
print('总计花费')
print(N)
```
他兴奋地去提交了，结果获得了WA 100%。

:::info Word Bank
「WA」Wrong Answer 答案错误
:::


我们来看看他的运行结果：~~我还正在写交互模块呢，先贴个代码块糊弄一下~~
```
总计花费
99999999
```

:::tip
所以说，「立刻提交」是一个很不好的行为，一定要先验证一下是否正确。
:::

很明显，这是一个[「不需要（默认）换行」]()的情况。如何才能让默认换行的Python不换行呢？

#### 接下来，正文开始咯！

___

## [PartⅠ] 参数控制

:::details
要是下面不好理解或者太冗余，欢迎 ~~[提issue](https://issue.hopecode.com.cn)~~ [github issues](https://github.com/Hope-Code/PythonWorld/issues) 或[论坛](https://forum.hopecode.com.cn)，我会及时修改  
:::

首先，默认换行是在`print()`的[最后]()，Cody的输出就会像这样：

<pre>输出<sub>1</sub>+换行<sub>1</sub>+输出<sub>2</sub>+换行<sub>2</sub></pre>

其中换行~1~是多余的，因为它夹在了不需要换行两个输出之间。

那么我如果只用一个`print()`，输出就会像这样：

<pre>输出<sub>1</sub>+换行<sub>1</sub></pre>

中间就不会有换行了。

Cody 修改了他的输出：

```python
print('总计花费',N)
```

Cody：我先在本地测试一下。

:::tabs
@tab 输入
```
49999999 50000000
```
@tab 输出
```
总计花费 99999999
```
:::

嗯perfect，结果……

:::danger WA 100%
:::

Cody：这是什么情况？？？

我们来对比一下：

:::tabs
@tab 样例输出
```
总计花费99999999
```
@tab Cody的输出
```
总计花费 99999999
```
:::

Cody的输入多了一个空格……  
Hopecode：看来还是要仔细啊。

::::details More...

Online Judge中末尾空格/回车的数量不会影响题目正确与否。  
主要是因为不同语言输出的差异。

不同语言的写法：

:::tabs#1

@tab Python

```python
print('line 1')
print('line 2')
print('line 3')
```
@tab C++

```cpp
cout<<"line 1"<<endl;
cout<<"line 2"<<endl;
cout<<"line 3";
```
:::
输出：

:::tabs#1

@tab Python
```
line 1
line 2
line 3

```

@tab C++
```
line 1
line 2
line 3
```
:::

在很多情况中，如果严格限制行尾的空格或回车数量，则会大大增加编程难度。所以这种无伤大雅的误差就不做限制了。

:::danger 但如果输出的行首或行中空格数量不正确，则会得到WA。
:::
::::

为了消灭中间那个多余的空格，我们要引入一个神奇的东西：

### sep

sep是separator的缩写

:::info Word Bank
「separator」n.分隔符
:::

比如`print('a','b')` 得到了 `a b` 而不是 `ab` ，就是因为分隔符的存在。

**默认的分隔符是一个空格**

分隔符的存在很有价值。例如我想输出时间：

```python
hour=input()
minute=input()
second=input()
print('Now',hour,minute,second,sep=':')
```

当我输入时分秒后，输出如下：`Now:11:59:59`

分隔符变成了一个冒号。

现在你应该明白sep的作用了吧。

::::details More...
sep是函数print()中一个可变参数，默认为一个空格（sep=' ')。  
使用方法：在所有输出项的最后，加入一个项：`sep=str`str为你所需的分隔符，类型为`string`。
:::info
参数：你可以理解成**参考数值**，就像程序在执行的时候附加的一些参考。
:::
具体会在[参数]()部分讲解。
::::

Cody：那我只需要把sep的值设为空（什么也没有），就可以AC了？  
Hopecode：Bingo!

:::details 常见错误
```python
print('example_1','example_2',sep=)
```
很棒，你会收到一个报错。  
原因：参数必须传入值。
```python
print(sep='','example_1','example_2')
```
你会收到另一个报错。  
原因：双星可变参数必须位于最后。

详解请见[函数]()部分

:::

经过不懈的努力，他终于成功了：

```python
n1=int(input())
n2=int(input())
N=n1+n2
print('总计花费',N,sep='')
```
:clap: 恭喜Cody获得了第一次AC，我们接着看获取更多AC的方法。
___

刚介绍完sep，接下来是一个类似的参数：

### end

:::info Word Bank
应该不用我解释了吧……
:::

我们再来看看Cody的原始代码：
```python
n1=int(input())
n2=int(input())
N=n1+n2
print('总计花费')
print(N)
```
那有没有办法直接去掉这个换行符呢？  
当然可以！`end`参数就是这么设计的！

:::details More...
end也是函数print()里的一个可变参数，默认为一个换行（end='\n'）。  
和sep使用方法相同，都需要放在最后。
:::

Cody：我能同时使用sep和end两个参数吗？  
Hopecode：当然可以，而且顺序随意。只要它们都放在输出项后。

Cody：那么只需要把默认的`end='\n'`改成`end=''`？  
Hopecode：嗯，注意end的位置，应该在第一个print中。
```python
n1=int(input())
n2=int(input())
N=n1+n2
print('总计花费',end='')
print(N)
```
:::details 常见错误
```python
n1=int(input())
n2=int(input())
N=n1+n2
print('总计花费')
print(N,end='')
```
你会得到这样的输出：
```
总计花费
99999999
```
因为print()的默认换行是在该输出的行尾，如果把end写到第二个print()里，那么第一个print()还会照常输出默认换行。
:::
非常幸运，Cody获得了第二个AC。

___

## [PartⅡ] 格式化

要是忘记[格式化]()的意思，可以点击链接跳转。

### %格式化
>`%`不是屏幕上多出来的冗余字符。

百分号格式化是程序员最喜欢的格式化之一。  
%格式化有两个特点：通用（几乎所有语言都支持它）、简便。  
由于Cody学过（[若有所遗忘请Click here]()），这边Cody仅用了0.999秒便完成了。
```python
n1=int(input())
n2=int(input())
N=n1+n2
print('总计花费%d'%N)
```
Cody：虽然%格式化会让不懂编程的人望而生畏，但程序员们喜欢它也不是没有道理的。  
对比前两种方式sep和end，是不是简洁了不少呢？

### format()格式化

Cody：`格式化`的英文不就是`format`吗？  
Hopecode：是的，不过这里的`format`指内置函数format()

:::tip
`input()`,`print()`也是内置函数
:::

Cody：如何使用呢？

Hopecode：如
```python
'{}{}'.format(exam,ple)
```
会格式化成`'example'`
```python
'{0}{1}{1}{2}'.format('h','e','l','o')
```
会格式化成`'hello'`

Hopecode：这样明白了吗？


调用format()时，原字符串的大括号相当于占位符，里面的数字类似于[索引]()，format()里的元素则是索引访问的对象。
如果所有大括号内为空，则默认按照从左往右{0}{1}{2}…的顺序排列。

format()在格式化多个重复元素时尤为方便。比如下面的情况：

:::tabs

@tab %format
```python
name='Cody'
print('%s叫%s，%s爸爸的儿子叫%s，%s弟弟的哥哥叫%s。'%(name,name,name,name,name,name))
```

@tab %format_2
```python
print('%s叫%s，%s爸爸的儿子叫%s，%s弟弟的哥哥叫%s。'%('Cody','Cody','Cody','Cody','Cody','Cody'))
```
@tab format() format
```python
print('{0}叫{0}，{0}爸爸的儿子叫{0}，{0}弟弟的哥哥叫{0}。'.format('Cody'))
```
:::

`format()`是最强大的格式化方案。使用`format()`可以实现非常多的功能。代价是你需要背诵并理解许多难以记忆的组合（比如有时候会像这样`{:0>10.3f}`）。

但是在简单的格式化中，使用`format()`反而会令代码更长。因为`format()`本身就有8个字符。所以`format()`只会在少数复杂的情况下出现。

Cody的代码：
```python
n1=int(input())
n2=int(input())
N=n1+n2
print('总计花费{}'.format(N))
```

### f-string

>这名字一看就很高级。

:::info Word Bank
f是format，string应该不用解释了吧。
:::

f-string是最简单的。   
它的代码最少，也最直观，不像前两种难以阅读。  
举个例子：
```python
name='Cody'
age=2
print(f'{name} is {age} years old.')
```
是不是不看使用方法也能明白是什么意思？

:::info 当然还是贴个使用方法
可以看到，f-string是在普通字符串前加上`f`（或`F`）。字符串内的大括号里填写表达式。  
e.g. `a=1` `print(f'{-a}')`会得到-1。
:::

:::tip
「表达式」由数字、量、运算符、括号等组成的式子。  
具体请见[表达式]()
:::



f-string是最简便优美的格式化方式。不过由于功能较为局限，不适用于少数情况。

Cody格式化篇的最后一组代码：
```python
n1=int(input())
n2=int(input())
N=n1+n2
print(f'总计花费{N}')
```
Cody：果然，在简单的转义中，f-string真的好简洁！  
Hopecode：是的，我通常都会使用f-string来格式化。

***3_seconds_later......***

Cody：怎么报错了？  
Hopecode：你这次学聪明了，没往直接往OJ提交。

:::warning
Python 3.6以下的版本不支持`f-string`。如果出现了报错，请检查Python的版本。
:::

::::details More...
:::info Word Bank
Cody的错误是一个CE。  
「CE」Compilation Error 编译错误
:::

不过不用担心。各大OJ的Python版本都会≥3.6，你可以放心使用`f-string`。
::::

### 「格式化」说明

:::tip
[f-string]()应该成为最常用的格式化方案。  
如果有f-string不能实现的，请使用[%格式化]()；  
如果%格式化还不能实现或者太麻烦，就用[format()格式化]()
:::

「因地制宜」使你的程序保持最优解。

当然，如果你特别熟悉或喜欢某一种方法，也是没有问题的。
#### 条条大路通罗马

:::note For Advanced
不建议将[format()]()和[f-string]()里的大括号转义。如需，请自行Search。
:::

## [partⅢ] 字符串拼接
这是最后一种方法，但是我不太推荐。  
这种方式叫做[字符串拼接]()，做法是把两个字符串“加”在一起。
先看代码：
```python
n1=int(input())
n2=int(input())
N=n1+n2
print('总计花费'+str(N))
```
不同只有最后一行。  
知识点是[用算术运算符把两个字符串相加]()，获得一个长字符串。  
这里的'总计花费'是str类，但N是int类。[字符串和数字不可相加]()，所以需要将N转化成字符串型，就可以相加了。

Cody：不需要`sep=''`了吗？  
Hopecode：是的。这行`print()`里只有一项，所以没有间隔符。

:::details 详细解释
`print()`里项与项的之间是用`,`划分的。这里并没有`,`，所以只有一项。  
这一项是什么呢？  
例如当N=99时，  
`print('总计花费'+str(99))` => `print('总计花费'+'99')` => `print('总计花费99')`  
所以只有一项。
:::

太棒了Cody获得了第六个AC。

Cody：为什么不推荐这一种做法呢？  
Hopecode：一是程序员不习惯（可能出现表意不明），二是这种方式太局限了。举个例子你就明白了。

:::tabs

@tab 字符串拼接
```python
age1,age2,age3=2,3,4
print('Cody'+str(age1)+'岁，'+'Codyy'+str(age2)+'岁，'+'Codyyy'+str(age3)+'岁。')
```
@tab f-string
```python
age1,age2,age3=2,3,4
print('Cody{age1}岁，Codyy{age2}岁，Codyyy{age3}岁。')
```
:::

差别不仅在代码的长度上，还在`shift`的按动次数上，更在阅读调试的成本上。

所以你会选择[字符串拼接]()这种方法吗？

相信无论是写代码还是读代码的人都不习惯吧。

**但是！** 还是那句话「因地制宜」。如果不需要类型转化，又比较简短，字符串相加也是不错之选。  
比如往用户的输入中加上句点：

```python
print(input()+'.')
```
这时[字符串拼接]()也是不错的方式。

>有时间再贴创意图 Only One Line
>
>先假装这有个图片。。。

<center>「一行」「两行」「三行」 是算法工程师们的终身追求。</center>

___

### 写在最后

结束了。

9000字……一个简单的问题写了这么多，也是我没想到的。希望大家能够多多支持。

提[issue]() ~~（等会我还没开始搭建呢）~~

题目入口再放一遍：[Cody's Buying](https://oj.hopecode.com.cn/problem/0010)

答应我，AC这道题。

Cody：我都AC六遍了……

一道不错的题目 [Names](https://oj.hopecode.com.cn/problem/0011)  
如果你了解 [if判断]()，刷了上面那道题。

改天给Cody换上图片 ![Cody](/Cody.png "Cody" =120x100)

~~改天添加补充材料~~ 很有意思的哦

已经添加评论功能，欢迎留言！
___


<!--##补充材料

分割线深色
CRLF
\n
为什么要学习转义字符 包括%吗
转义字符都是\开头的吗？
win路径用/或\\

计算机语言发展史：二进制，汇编样子
!<--.format在后面？


Sep End 等必须在输出内容之后（双星可变参数）
字符串拼接省略加号

（sep end 顺序可变？）
题目：Cody's Buying 外国人名

#字符串拼接
#字符串填充
# print(f"{str:->15}")
# print(f"{str:-<15}")
# print(f"{str:-^15}")

>>> import datetime
>>> name = 'Fred'
>>> age = 50
>>> anniversary = datetime.date(1991, 10, 12)
>>> f'My name is {name}, my age next year is {age+1}, my anniversary is {anniversary:%A, %B %d, %Y}.'
'My name is Fred, my age next year is 51, my anniversary is Saturday, October 12, 1991.'
>>> f'He said his name is {name!r}.'
"He said his name is 'Fred'."

转义？
tip折叠？
-->