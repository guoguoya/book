# shell 入门

q:软件工具设计概念与原则是什么
q:unix 工具是什么
q:如何结合所有工具，完成工作

## 软件工具的原则

一次做好一件事
处理文本行，不要处理二进制数据
使用正则表达式
默认使用标准输入/输出
避免喋喋不休
输入格式必须与可接受的输入格式一致
让工具去做困难的部分
构建特定工具前先想一想

在工具程序的世界里，没有消息就是好消息。
你叫它做什么，你就会得到什么。

p:越低层次的语言，他们的行为（抽象形式的种类）就越单一。

## shell脚本的特性 p23

简单性，可移植性，开发容易。

## 基本知识

当Shell执行一个程序时，会要求unix内核启动一个新的进程。

```shell
    #!/bin/bash 用!#开头，后面的表示解释器的路径（这行的长度在在不同的系统是不同的）最好不要超过64个字符
```

## 参数

>命令名称是命令行的第一个项目。通常后面会跟着选项，任何额外的参数都会放在选项之后。
>选项的开头是一个破折号（或减号），后面接着一个字母。

用 **；**隔开同行中的多条命令。Shell会依次执行这些命令。如果你使用&隔开多条命令，则shell将在后台执行其前面的命令

shell三种基本命令：内建命令、Shell函数以及外部命令（p28）

## 变量

>Shell变量名称的开头是一个字母或下划线符号，
>变量赋值的方式为：名称=字符
>需要取出变量时，只需要在变量前加$字符

## command 

echo waring:在我的shell bash中 \n 没效果 “\n” -> \n

```shell
    echo "hello world";
```

printf

```
    printf "hello world %s %s %d \n" my sister 10 info:这个东西和c的有点像
```

tr(p34) tr命令可以对来自标准输入的字符进行替换、压缩和删除。它可以将一组字符变成另一组字符，经常用来编写优美

```
    tr -d '\r'
```

#

```
    #这个是注释
```

set 

```
    set -x /-x  命令追踪
    echo hello world
    echo hello world my sister
    set +x 


    set -- hello "hehe heihei" gege /调用此命令时而未给予任何选项，则它会设置位置参数的值，并将之前的存在的任何值丢弃。
```


unset 

```
    unset -v 删除变量
    unset -f 删除方法
```

sed sed [-n] 'address editing command' [file]
```
    sed 's/oldString/newString/; s/oldString/newString' ./text
    find /Users/yujiabin/learn/test | sed 's;/learn/;/he1/;' //先用find查出文件列表，将test目录下的learn修改成test q:这里为什么没法替换文件名？


    '/hello/ s/world/world !/' //匹配有hello的行 将world 改成world ！
```

cut 

```
    cut -c 1-10 /etc/pwd //剪切1-10的字符
    cut -d : -f 1,2  /etc/pwd //以:为界限符 裁剪 1,2字段
```

join (join [option] file1 file2)

```

```

awk 一般对字段进行处理

```
```

sort

```
```

uniq (用于sort以后)

```shell

```

fmt (重新格式化段落)

```
```

## 基本的I/O 重定向

>标准输入/输出
程序应该有数据的来源端和目的端，以及报告问题的地方。他们分别被称为标准输入、标准输出以及标准输出。

>默认的标准输入、标准输出、以及标准错误输出都是终端。
```
    cat 
    hello world 
    //hello world
    my sister 
    // my sister 
    view:这里shell启动了一个新的进程 该程序执行了cat命令，cat命令一直在等待标准输入，然后输出
```

默认的情况下，它们读取标准输入、写入输出，并将错误信息传递到标准错误输出。这类程序常叫做过滤器。

>在你登录时，UNIX便将默认的标准输入、输出以及错误输出安排成你的终端。I/O重定向就是你通过与终端交互，或是在Shell脚本里设置，重新安排在哪里输入或输出到哪里。

以 **<** program < file 改变标准输入

以 **>** program > file 该表表示输出

以 **>>** program >> file 附加到file的结尾处 

建立管道

program1 | program2 可将program1的标准输出修改为program2的标准输入

im:构造管道时，应该试着让每个阶段的数据量变得更加少。如果你有两个要完成的步骤与先后次序无关，你可以把会让数据量变少的那一个步骤放在管道的前面。这个做可以提升脚本的整体性能。

/dev/null 这个是位桶（bit bucket）， 传送到此文件的数据都将被系统丢弃。

## Shell基本命令查找

Shell会沿着查找路径$PATH来寻找命令。所找到的命令可能是编译后的可执行文件，也可能是Shell脚本。


## 访问Shell脚本的参数

所谓的位置参数指的也就是Shell脚本的命令行参数。在Shell函数里，他们同时也可以是函数的参数。各参数都由整数来命名。当它超过9时应该用 **{}** 把数字包裹起来。


## 正则表达式

了解行与字符串的差异是相当重要的。^ 与 $分别表示行的开头和结尾。


## 排序

以字段排序

## 管道

## 变量、判断、重复


**export** 

**readonly**

>参数展开 是Shell提供变量值在程序中使用的过程；例如，作为给新变量的值，或是作为命令行的部分或全部参数。

**替换运算符**（p128）

${varname: -word}
${varname: =word}
${varname: ?message}
${varname: +word}

**模式匹配运算符**

${variable#pattern}
${variable##pattern}
${variable%pattern}


**位置参数**

>位置参数指的是Shell脚本的命令行参数，同时也表示在Shell函数内的函数参数。当这个参数大于9时要用  **{}** 括起来。

**while** 

```shell
    while [ $# != 0 ]
    do
       echo $1
       shift
    done
```

$#, $*, $@, "$*", "$@"
