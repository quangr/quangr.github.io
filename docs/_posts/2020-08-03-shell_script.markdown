---
layout: post
title:  "Shell Scripting"
date:   2020-08-03 18:09:14 +0800
categories: CS
---

由于要读偏计算机的研究生了，现在开始恶补cs。:>


## Bash Shell

总的来说，Linux Shell将字符串作为基本单元。这是他与powershell的巨大不同。编程中主要理解的概念有：1.I/O. 2.正则表达式 

# I/O

关于Linux下的I/O可以看CSAPP的第十章，大概要理解文件的概念，C中的标准read,write函数，以及如何再其之上写出Robust的读写函数。

# Regular Expression

因为Linux Shell将字符串作为基本单元，正则表达式在处理输出方面扮演着很重要的角色。注意的是一些内置命令只实现了BRE，没有实现拓展的正则表达式。


反正在linux下的shell编程就是像个原始人一样整各种字符操作。

## Powershell



而Powershell支持对象，并且巨硬提供了完整的Help文档，利用各种Cmdlet可以方便愉快的进行编程。需要注意的有：


pipe中的两种传输方式：By Value 和 By Propertyname。这里还有个关于Select-String的Input_object的小坑，可以去看看[GitHub上的源码](https://github.com/PowerShell/PowerShell/blob/4b9b0788ed28ea6d463ce857d1ed81bd4a977a59/src/Microsoft.PowerShell.Commands.Utility/commands/utility/MatchString.cs)

powershell里还有一些和windows纠缠在一起的特性，我也没时间看那些了。。。


## 参考书籍

读这种类型的书就像读小说一样，还是得读中文译本，读的快。。。

Linux命令行与shell脚本编程大全. Blum,Bresnahan

Windows PowerShell实战指南. Don Jones, Jeffery Hicks.