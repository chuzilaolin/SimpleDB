# SimpleDB
> “What I cannot create, I do not understand.” – Richard Feynman

### 一、 项目简介
本项目是参考自[db_tutorial](https://github.com/cstack/db_tutorial)，使用C语言从头克隆一个SQLite。目的是为了弄清楚以下几个问题：

- 数据在内存和磁盘上分别以什么格式保存？
- 它什么时候从内存移动到磁盘？
- 为什么一张表只能有一个主键？
- 回滚事务的操作是如何进行？
- 索引是如何格式化的？
- 全表扫描何时以及如何发生？
- 准备好的语句以什么格式保存？

### 二、SQLite简介

<img width="412" alt="image" src="https://github.com/chuzilaolin/SimpleDB/assets/82101835/528b7862-8a18-4358-968d-cc2f6b82d576">

SQLite的架构，可以分为前端和后端两个部分

**前端部分**：

- Tokenizer（分词器）
- Parser（解析器）
- Code Generator（代码生成器）

前端的输入是SQL文本，输出是sqlite虚拟机字节码。

**后端部分**：

- Virtual Machine（虚拟机）
- B-tree（B树）
- Pager（页管理器）
- OS Interface（操作系统接口）

虚拟机将前端生成的字节码作为指令，然后对1/n个表或者索引执行对应的操作，VM本质上是字节码指令类型上的一个大Switch语句。

每个表或索引都存储在称为B树中，它的每个节点的长度为一页，它可以通过向页管理器发出命令从磁盘检索页面或将其存回磁盘。

页管理器接受到读取或写入数据页的命令，它负责在数据库文件中适当的位置进行读写；同时，它还在内存中保留最近访问的页面的缓存，
并确定何时需要将这些页面写回磁盘。

OS接口是根据SQLite编译时操作系统的不同而有所不同的层，SQLite是使用了VFS抽象对象以提供跨操作系统的可移植性。（本项目仅做学习使用，所以优先采用POSIX标准的系统调用，即无缓冲IO。）





















