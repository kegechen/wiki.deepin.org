---
title: Wine开发中的常用命令介绍
description: 简单介绍Wine开发中的常用命令
published: true
date: 2022-10-25T02:37:05.431Z
tags: 
editor: markdown
dateCreated: 2022-07-07T08:08:45.024Z
---

# Wine开发中的常用命令介绍
## 编译相关
编译这个词我们大家经常在用，笼统的来说就是将源码变成可执行的程序。实际上在 Linux 中我们用的比较多的通常是编译套件，比如 GCC，它包括各种语言的编译器、汇编器、链接器等等。有了编译套件我们能够将源码变成可执行的程序，但是由于大的项目通常涉及成百上千的源文件，手动写脚本来完成这些繁琐的编译、链接工作太耗时，某个改动后想做到重新生成的代价最小则更是难上加难，所以出现了构建系统。

最基础和常见的构建系统是 Make，它拥有一套语法，可以定义文件生成的规则，以及文件之间的依赖关系，项目中的 `Makefile` 文件通常就是包含了这些规则的文件。对于大的项目来说 `Makefile` 文件的编写也不是太容易，所以人们总结出了一套准则，提供了更高一级的抽象，用更高级的工具来生成 `Makefile` 文件。这些更高级的构建工具包括 GNU autotools、CMake 等，以 autotools 为例：

开发人员通常编写 `configure.ac` 文件和 `Makefile.am` 文件，通过 autoconf 和 automake（autoreconf 可以全部生成），生成对应的 `configure` 脚本和 `Makefile.in` 文件。用户根据具体需求，通过不同的参数运行 `./configure` 脚本生成 `Makefile` 文件。最后再用 make 命令，生成最终的可执行程序。遵循标准的 `Makefile` 文件一般还会存在 `install` 、`uninstall` 等目标，用来实现安装和卸载等功能。

至此，我们完成了从源码到程序的构建。
## 打包相关
不同的操作系统，或者说 Linux 下不同的发行版，通常都有自己的一套标准的软件安装方式，可以用来追踪安装的软件，保证软件来源的一致性和可靠性。Deepin 系统基于 Debian 系统而来，使用了和 Debian 系统一样的包管理系统（Ubuntu 也是基于 Debian 的包管理系统）。

所谓打包就是将一系列的文件按照一致的规则收集到一起，以用于方便的安装、升级、卸载和配置的过程，打包最终生成的文件以 `.deb` 结尾，我们可以通过 `dpkg -i ` 命令来安装。复杂的安装包通常都存在依赖关系，使用 `dpkg` 系列命令时我们需要了解对应的依赖关系是否满足。而 `apt` 系列命令，是更高一级的包管理系统，它包含了对依赖的解析和自动解决依赖的功能，所以可以简单的认为，`dpkg` 系列命令是用来操作单个包的，而 `apt` 系列命令是用来和包管理系统交互的。常见的 `dpkg` 和 `apt` 系列命令如下：

dpkg，通过 `-i`、`-r`、`-l`、`-S` 参数可以安装、移除、查看安装包或者进行文件溯源。
dpkg-deb，用来查看、解开或者打包安装包。
`apt install/remove/purge/update/dist-upgrade`，来安装、移除软件包，以及系统的包索引更新和系统完整的升级。
`apt-cache show/policy/madison/depends/rdepends`，可以用来查看包、当前安装策略、可用安装包、依赖包和被依赖包等信息。
简单来说，在开发阶段通常都是先使用 `dpkg` 相关命令来测试，最终在用端一般只会使用 `apt` 相关命令。关于打包的具体过程，存在许多方法不同，这部分可以参考详细的文档，因此这里不在赘述。
## 运行相关
可执行程序在终端中可以直接执行运行，运行的结果或者日志，通常以标准输出或者标准错误输出的形式输出到控制台，我们可以灵活的使用 shell 中各种重定向功能将日志保存到文件中。比如：

wine xxx.exe &> log，将标准输出和标准错误都重定向到文件中。
其他可能常用的命令：

用 `ps` 命令来查看当前运行的进程。
用 `kill` 命令给指定进程发送信号。
用 `top` 命令查看当前系统的负载。
用 `netstat` 或者 `ss` 查看当面网络链接情况。
用 `tar`、`unzip`、`unrar`、`7z` 等命令来创建或者解压压缩文件。
用 `grep` 命令在指定文件或者文件夹中搜索字符串。
最重要的是，学会通过 `man` 命令来学习其他命令的使用。