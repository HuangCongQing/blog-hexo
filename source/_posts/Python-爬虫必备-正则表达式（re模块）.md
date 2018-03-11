---
title: Python 爬虫必备-正则表达式（re模块）
date: 2017-08-19 17:50:33
tags: python
---

![正则表达式re模块](http://upload-images.jianshu.io/upload_images/4340772-8403f99919beba25.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 正则表达式须知
* 正则表达式是用来匹配字符串非常强大的工具，在其他编程语言中同样有正则表达式的概念，Python同样不例外，利用了正则表达式，我们想要从返回的页面内容提取出我们想要的内容就易如反掌了。
>正则表达式的大致匹配过程是：
1.依次拿出表达式和文本中的字符比较，
2.如果每一个字符都能匹配，则匹配成功；一旦有匹配不成功的字符则匹配失败。
3.如果表达式中有量词或边界，这个过程会稍微有一些不同。

## 正则表达式语法规则

下面是Python中正则表达式的一些匹配规则，图片资料来自CSDN
![正则表达式](http://upload-images.jianshu.io/upload_images/4340772-b0baf49f04744a80.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<!-- more -->

## 正则表达式特别强调

1.  python转义字符
    * 正则表达式使用反斜杠" \ "来代表特殊形式或用作转义字符，这里跟Python的语法冲突，因此，Python用" \\\\ "表示正则表达式中的" \ "，因为正则表达式中如果要匹配" \ "，需要用\来转义，变成" \\ "，而Python语法中又需要对字符串中每一个\进行转义，所以就变成了" \\\\ "。

     * Python里的原生字符串很好地解决了这个问题，这个例子中的正则表达式可以使用r”\\”表示。同样，匹配一个数字的”\\d”可以写成r”\d”。有了原生字符串，妈妈也不用担心是不是漏写了反斜杠，写出来的表达式也更直观勒。
2. 贪婪模式和非贪婪模式

正则表达式通常用于在文本中查找匹配的字符串。Python里数量词默认是贪婪的（在少数语言里也可能是默认非贪婪），总是尝试匹配尽可能多的字符；非贪婪则相反，总是尝试匹配尽可能少的字符。在"*","?","+","{m,n}"后面加上？,使贪婪变成非贪婪。

可参考： [python 正则表达式的贪婪匹配与非贪婪匹配](http://blog.csdn.net/zcc_0015/article/details/53671189)



## Python Re模块
Python 自带了re模块，它提供了对正则表达式的支持。主要用到的方法列举如下

```
#返回pattern对象
re.compile(string[,flag])  
#以下为匹配所用函数
re.match(pattern, string[, flags])
re.search(pattern, string[, flags])
re.split(pattern, string[, maxsplit])
re.findall(pattern, string[, flags])
re.finditer(pattern, string[, flags])
re.sub(pattern, repl, string[, count])
re.subn(pattern, repl, string[, count])
```
在介绍这几个方法之前，我们先来介绍一下pattern的概念，pattern可以理解为一个匹配模式，那么我们怎么获得这个**匹配模式**呢？很简单，我们需要利用re.compile方法就可以。例如
```
pattern = re.compile(r'hello')
```
另外大家可能注意到了另一个参数 flags，在这里解释一下这个参数的含义：

参数flag是匹配模式，取值可以使用按位或运算符’|’表示同时生效，比如re.I | re.M。

可选值有：
```
 • re.I(全拼：IGNORECASE): 忽略大小写（括号内是完整写法，下同）
 • re.M(全拼：MULTILINE): 多行模式，改变'^'和'$'的行为（参见上图）
 • re.S(全拼：DOTALL): 点任意匹配模式，改变'.'的行为
 • re.L(全拼：LOCALE): 使预定字符类 \w \W \b \B \s \S 取决于当前区域设定
 • re.U(全拼：UNICODE): 使预定字符类 \w \W \b \B \s \S \d \D 取决于unicode定义的字符属性
 • re.X(全拼：VERBOSE): 详细模式。这个模式下正则表达式可以是多行，忽略空白字符，并可以加入注释。
```
在刚才所说的另外几个方法例如 re.match 里我们就需要用到这个pattern了，下面我们一一介绍。

### （1）re.match(pattern, string[, flags])

这个方法将会从string（我们要匹配的字符串）的开头开始，尝试匹配pattern，一直向后匹配，如果遇到无法匹配的字符，立即返回None，如果匹配未结束已经到达string的末尾，也会返回None。两个结果均表示匹配失败，否则匹配pattern成功，同时匹配终止，不再对string向后匹配。下面我们通过一个例子理解一下
```

# 将正则表达式编译成Pattern对象，注意hello前面的r的意思是“原生字符串”
pattern = re.compile(r'hello')
 
# 使用re.match匹配文本，获得匹配结果，无法匹配时将返回None
result1 = re.match(pattern,'hello')
result2 = re.match(pattern,'helloo CQC!')
result3 = re.match(pattern,'helo CQC!')
result4 = re.match(pattern,'hello CQC!')
 
#如果1匹配成功
if result1:
    # 使用Match获得分组信息
    print(result1.group())
else:
    print ('1匹配失败！')
 
 
#如果2匹配成功
if result2:
    # 使用Match获得分组信息
    print(result2.group())
else:
    print( '2匹配失败！')
 
 
#如果3匹配成功
if result3:
    # 使用Match获得分组信息
    print( result3.group())
else:
    print('3匹配失败！')
 
#如果4匹配成功
if result4:
    # 使用Match获得分组信息
    print( result4.group())
else:
    print( '4匹配失败！')

```
我们还看到最后打印出了result.group()，这个是什么意思呢？下面我们说一下关于match对象的的属性和方法
Match对象是一次匹配的结果，包含了很多关于此次匹配的信息，可以使用Match提供的可读属性或方法来获取这些信息。

```
1.group([group1, …]):
获得一个或多个分组截获的字符串；指定多个参数时将以元组形式返回。group1可以使用编号也可以使用别名；编号0代表整个匹配的子串；不填写参数时，返回group(0)；没有截获字符串的组返回None；截获了多次的组返回最后一次截获的子串。
2.groups([default]):
以元组形式返回全部分组截获的字符串。相当于调用group(1,2,…last)。default表示没有截获字符串的组以这个值替代，默认为None。
```

### （2）re.search(pattern, string[, flags])
search方法与match方法极其类似，区别在于match()函数只检测re是不是在string的开始位置匹配，search()会扫描整个string查找匹配，match（）只有在0位置匹配成功的话才有返回，如果不是开始位置匹配成功的话，match()就返回None。同样，search方法的返回对象同样match()返回对象的方法和属性。我们用一个例子感受一下

```
# 将正则表达式编译成Pattern对象
pattern = re.compile(r'world')
# 使用search()查找匹配的子串，不存在能匹配的子串时将返回None
# 这个例子中使用match()无法成功匹配
match = re.search(pattern,'hello world!')
if match:
    # 使用Match获得分组信息
    print( match.group())

```

###  （3）re.split(pattern, string[, maxsplit])
按照能够匹配的子串将string分割后返回列表。maxsplit用于指定最大分割次数，不指定将全部分割。我们通过下面的例子感受一下。

```
pattern = re.compile(r'\d+')
print( re.split(pattern,'one1two2three3four4'))
 
### 输出 ###
# ['one', 'two', 'three', 'four', '']

```
### （4）re.findall(pattern, string[, flags])
搜索string，以列表形式返回全部能匹配的子串。我们通过这个例子来感受一下

```
pattern = re.compile(r'\d+')
print( re.findall(pattern,'one1two2three3four4'))
 
### 输出 ###
# ['1', '2', '3', '4']
```

### （5）re.finditer(pattern, string[, flags])

搜索string，返回一个顺序访问每一个匹配结果（Match对象）的迭代器。我们通过下面的例子来感受一下

```
pattern = re.compile(r'\d+')
for m in re.finditer(pattern,'one1two2three3four4'):
    print( m.group()),
 
### 输出 ###
# 1 2 3 4
```

### （6）re.sub(pattern, repl, string[, count])

使用repl替换string中每一个匹配的子串后返回替换后的字符串。
当repl是一个字符串时，可以使用\id或\g、\g引用分组，但不能使用编号0。
当repl是一个方法时，这个方法应当只接受一个参数（Match对象），并返回一个字符串用于替换（返回的字符串中不能再引用分组）。
count用于指定最多替换次数，不指定时全部替换。
```
pattern = re.compile(r'(\w+) (\w+)')
s = 'i say, hello world!'
 
print( re.sub(pattern,r'\2 \1', s))
 
def func(m):
    return m.group(1).title() + ' ' + m.group(2).title()
 
print( re.sub(pattern,func, s))
```


### （7）re.subn(pattern, repl, string[, count])

返回 (sub(repl, string[, count]), 替换次数)。
```
pattern = re.compile(r'(\w+) (\w+)')
s = 'i say, hello world!'
 
print( re.subn(pattern,r'\2 \1', s))
 
def func1(m):
    return m.group(1).title() + ' ' + m.group(2).title()
 
print( re.subn(pattern,func1, s))
 
### output ###
# ('say i, world hello!', 2)
# ('I Say, Hello World!', 2)


```



参考：[静觅](http://cuiqingcai.com/) » [Python爬虫入门七之正则表达式](http://cuiqingcai.com/977.html)
[python中re项目详解](http://lihuipeng.blog.51cto.com/3064864/1270525/)
