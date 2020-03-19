# 实验室相关技术要求

该篇文档主要给大家一个学习内容上的简单指引。

---

以下**主要内容**以及**次要内容**的分类是为了让大家有一个学习的先后顺序。主要是根据重要性排列。这些内容的学习有可能是**非顺序独立**的。该篇内容全为**基础内容**，实验室所开发的具体内容将不在此列出。请参考文档`robocup3d.pdf`

---

## 主要内容

实验室开发所用的基本内容，如果对这些内容不了解，就**不可能**参与到实验室的开发中。

### C++

> C++是个什么玩意我就不说了。实验室的开发所用的主要语言是C++。

1. C++的基础语法，相似于C语言的那部分语法必须相当熟悉。
2. C++中的Class相关内容。
3. C++标准库的使用，主要是容器类的使用。

> 推荐网课:[C++程序设计（面向对象进阶）](https://www.icourse163.org/course/BUPT-1003564002)
> 推荐参考书籍(书本身很好，但是可能对新手不是很友好）：C++ Primer

### Linux

> Linux是一套免费使用和自由传播的操作系统内核，是一个基于POSIX和Unix的多用户、多任务、支持多线程和多CPU的操作系统内核。

一般来说：“我在用Linux”，那么我的意思是我在用某个Linux的发行版。常见的Linux发行版有：Ubuntu, Debian GNU/Linux, Arch Linux, Manjaro Linux。这些发行版确实有相当的差异，不过使用起来大同小异。实验室主要使用Ubuntu来进行开发。

1. 简单的Linux的使用。
2. 简单的Linux命令的使用。
3. 了解简单的Linux Shell脚本

关于虚拟机器的安装请参考本目录下的`vminstall.pdf`，

> 推荐网课:[零基础学Linux操作系统](https://www.icourse163.org/course/CCZU-1449599161)
> 推荐入门书籍：Linux就该这么学
> 推荐参考书籍（书本身很好，但是可能对新手不是很友好）：鸟哥的Linux私房菜
---

### 次要内容

开发中也会用到内容，次要是相较于**主要内容**而言的。

### Git

> Git（读音为/gɪt/）是一个开源的分布式版本控制系统，可以有效、高速地处理从很小到非常大的项目版本管理。

我们使用git来进行版本控制与协作。

1. Git的的基本了解与使用
2. Github的使用

> 教程推荐：[廖雪峰Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)
> 教程推荐：[菜鸟教程](https://www.runoob.com/git/git-tutorial.html)
> 书籍推荐（强烈推荐）：[Pro Git中文版](https://gitee.com/progit/)

### CMake

请学习Linux之后再来学习CMake

> CMake是一个跨平台的安装（编译）工具，可以用简单的语句来描述所有平台的安装(编译过程)。

我们在开发中会一直用到CMake。

1. 了解CMake
2. 可以使用CMake来进行配置，编译多文件C++工程。

> 暂无中文推荐教程，建议google或者bing来进行搜索，找到一个自己看得懂的。
> 英文推荐教程：[Modern CMake](https://cliutils.gitlab.io/modern-cmake/)

---