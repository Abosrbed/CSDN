> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_53099212/article/details/132452987?spm=1001.2014.3001.5502)

#### Linux 系统编程目录

*   [Linux 开发环境](#Linux_2)
*   [GCC](#GCC_4)
*   *   [什么是 GCC](#GCC_5)
    *   [GCC 工作流程](#GCC_22)
    *   [GCC 常用命令](#GCC_34)
*   [静态库与动态库](#_76)
*   *   [什么是库](#_77)
    *   [静态库](#_82)
    *   *   [静态库的命名规则](#_83)
        *   [静态库的制作](#_86)
        *   [静态库的使用](#_98)
    *   [动态库](#_125)
    *   *   [动态库的命名规则](#_126)
        *   [动态库的制作](#_129)
        *   [动态库的使用](#_139)
    *   [静态库和动态库的区别](#_231)
    *   *   [静态库优缺点](#_233)
        *   [动态库优缺点](#_243)
*   [Makefile](#Makefile_254)
*   *   [什么是 Makefile](#Makefile_255)
    *   [Makefile 文件的命名规则](#Makefile__261)
    *   [Makefile 工作原理](#Makefile__286)
    *   [Makefile 变量](#Makefile__306)
    *   *   [自定义变量](#_307)
        *   [常用预定义变量](#_312)
        *   [获取变量值](#_321)
        *   [变量使用](#_326)
        *   [变量匹配](#_338)
    *   [Makefile 常用函数](#Makefile__356)
*   [GDB](#GDB_379)
*   *   [什么是 GDB](#GDB_380)
    *   [调试前准备工作](#_386)
    *   [GDB 常用命令及使用](#GDB_441)
    *   *   [基础命令](#_442)
        *   [断点命令](#_514)
        *   [调试命令](#_542)
        *   [变量自动操作](#_567)
*   [标准 C 库 IO 函数和 Linux 系统 IO 函数对比](#_C__IO__Linux__IO__577)
*   *   [标准 C 库 IO 函数](#_C__IO__587)
    *   [标准 C 库 IO 函数和 Linux 系统 IO 函数工作流程](#_C__IO__Linux__IO__590)
    *   [详细对比](#_592)
*   [虚拟地址空间](#_607)
*   [文件描述符](#_612)
*   [open、close 函数](#openclose__618)
*   [read、write 函数](#readwrite__703)
*   [lseek 函数](#lseek__760)
*   [stat、lstat 函数](#statlstat__814)
*   *   [stat 结构体](#stat__860)
    *   [st_mode 变量](#st_mode__880)
    *   [软链接与硬链接](#_884)
    *   [软链接文件的创建](#_905)
    *   [模拟实现 ls -l 命令](#_ls_l__922)
*   [文件属性操作函数](#_1038)
*   *   [access 函数](#access_1039)
    *   [chomd 函数](#chomd__1066)
    *   [chown 函数](#chown__1096)
    *   [truncate 函数](#truncate__1114)
*   [目录操作函数](#_1142)
*   *   [mkdir 函数](#mkdir__1143)
    *   [rmdir 函数](#rmdir__1169)
    *   [rename 函数](#rename__1176)
    *   [chdir 函数](#chdir__1200)
    *   [getcwd 函数](#getcwd__1207)
*   [目录遍历函数](#_1254)
*   *   [opendir 函数](#opendir__1255)
    *   [readdir 函数](#readdir__1262)
    *   *   [dirent 结构体](#dirent_1268)
        *   [d_type 变量](#d_type__1279)
    *   [closedir 函数](#closedir__1283)
*   [dup、dup2 函数](#dupdup2__1362)
*   [fcntl 函数](#fcntl__1461)
*   [结语](#_1524)

Linux 开发环境
----------

略

[GCC](https://so.csdn.net/so/search?q=GCC&spm=1001.2101.3001.7020)
------------------------------------------------------------------

### 什么是 GCC

> **GCC（GNU Compiler Collection）是一套由 GNU 项目开发的开源编译器集合。**

**安装命令**

```
sudo apt install gcc g++

```

**查看版本**

```
gcc -v #g++ -v
gcc --version #g++ --version

```

**注意**：gcc/g++ 版本需要 4.8.5 以上，否则无法编译 C++11。

### GCC 工作流程

GCC 的工作流程与 C/C++ 的编译过程相同，流程图如下：

启动代码 链接器 库代码 源代码  
.h/.c/.cpp 预处理器 预处理后源代码  
.i 编译器 汇编代码  
.s 汇编器 目标代码  
.o 可执行程序  
.exe/.out 其他目标代码

### GCC 常用命令

**语法**

```
gcc [选项] 
g++ [选项] 

```

**常用选项**

<table><thead><tr><th>选项</th><th>说明</th></tr></thead><tbody><tr><td><code>-E</code></td><td>只预处理指定源文件，不编译</td></tr><tr><td><code>-S</code></td><td>编译指定源文件，不汇编</td></tr><tr><td><code>-c</code></td><td>编译、汇编指定源文件，不链接</td></tr><tr><td><code>-o</code></td><td>输出到</td></tr><tr><td><code>-On</code></td><td>n 的范围是 1~3，数字越大优化级别越高编译时间越长（O 是大写 o）</td></tr><tr><td><code>-I</code></td><td>编译时指定使用的头文件</td></tr><tr><td><code>-l</code></td><td>编译时指定使用的库</td></tr><tr><td><code>-L</code></td><td>指定编译时搜索库的路径</td></tr><tr><td><code>-g</code></td><td>编译时生成调试信息，表示该程序可以被调试器调试</td></tr><tr><td><code>-D</code></td><td>在编译时指定一个宏</td></tr><tr><td><code>-fpic</code></td><td>生成与位置无关的代码</td></tr><tr><td><code>-shared</code></td><td>生成共享目标文件</td></tr><tr><td><code>-std=</code></td><td>指定语言标准</td></tr><tr><td><code>-w</code></td><td>不生成任何警告</td></tr><tr><td><code>-Wall</code></td><td>生成所有警告</td></tr></tbody></table>

**代码示例**

```
# 分步编译
gcc -E main.c -o main.i
gcc -S main.i -o main.s
gcc -c main.s -o main.o
gcc main.o -o main

# 一步到位
gcc main.c -o main

#多文件编译
gcc test.c main.c -o main

```

静态库与动态库
-------

### 什么是库

> **库是计算机上的一类提供直接使用的变量、函数、类的文件。**  
> 库算是一种特殊的程序但不能单独运行可以看成一种代码仓库。  
> 库具有**保密代码**、**方便部署和分发**的作用。

### 静态库

#### 静态库的命名规则

1.  Linux：`libxxx.a`
2.  Windows：`libxxx.lib`

#### 静态库的制作

1.  `gcc` 获得 `.o` 文件
2.  使用 `ar` 工具（archive）将 `.o` 文件打包

**代码示例**  
`r` - 将文件插入备存文件中  
`c` - 建立备存文件  
`s` - 索引

```
# 可以打包多个.o 文件
ar rcs libxxx.a xxx.o

```

#### 静态库的使用

链接时须注意头文件的展开和库文件的加载，另外还需注意目录层级。

**代码示例**  
现有一个以打包的静态库文件 library ，其包含以下文件：

```
.
├─ include
│	└─ head.h
├─ lib
│	└─ libcalculate.a
├─ main.c
└─ src
	├─ add.c
	├─ div.c
	├─ mult.c
	└─ sub.c

```

使用语法如下：

```
#处理
gcc main.c -o app -I ./include/ -l calculate -L ./lib/
#使用
./app

```

### 动态库

#### 动态库的命名规则

*   Linux：`libxxx.so` （Linux 下是一个可执行文件）
*   Windows：`libxxx.dll`

#### 动态库的制作

1.  `gcc` 获得 `.o` 文件，得到和位置无关的代码
2.  `gcc` 获得动态库

**代码示例**  
`-fpic` 用于汇编阶段，产生的目标文件没有绝对地址，全部用相对地址，这正好满足了共享库的要求，共享库被加载时地址不是固定的。如果不加 `-fpic` ，那么生成的目标文件就会与位置有关，当进程使用该 `.so` 文件时都需要重定位，且会产生成该文件的副本，每个副本都不同，不同点取决于该文件代码段与数据段所映射内存的位置。

```
gcc -c -fpic test.c
gcc -shared test.o -o libcalculate.so

```

#### 动态库的使用

在 linux 目录下，动态库文件字体颜色为绿色，经过处理后的动态库会在生成的可执行程序名添加一个 * 号。  
由于 GCC 进行链接时无法将动态库代码打包到可执行程序中。启动程序后动态库会被加载到内存中，通过 `lld` 命令检查动态库依赖关系。  
**如何定位共享库文件**  
当系统加载可执行代码时，能够知道所依赖库的名字，但还是需要知道绝对路径。系统的动态载入器可以获取该绝对路径。  
elf 格式的可执行程序是由 ld-linux.so 来完成的，它先后搜索 elf 文件的 `DT_RPATH 段` → `环境变量LD_LIBRARY_PATH` → `/etc/ld.so.cache 文件列表` → `/lib/，/usr/lib 目录`找到库文件后将其载入内存。

**代码示例**  
现有一个以打包的静态库文件 library ，其包含以下文件：

```
.
├─ include
│	└─ head.h
├─ lib
│	└─ libcalculate.so
├─ main.c
└─ src
	├─ add.c
	├─ div.c
	├─ mult.c
	└─ sub.c

```

**使用语法如下**：

*   临时配置（终端配置后切换 Xshell 链接会报错）

```
# 处理生成app文件（app非必定名字）
gcc main.c -o app -I ./include/ -l calculate -L ./lib/

# 配置环境变量，值为lib文件的绝对路径（lib文件夹下用pwd指令输出绝对路径）
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:lib文件的绝对路径

# 在处理后生成的app文件下用lld指令，如果libcalculate.so以分配内存且路径在lib文件夹下则链接成功
ldd app

```

*   永久配置 1（用户级）

```
# 处理生成app文件（app非必定名字）
gcc main.c -o app -I ./include/ -l calculate -L ./lib/

# 切入home文件下找到.bashrc文件修改
cd home
ll
vim .bashrc

# 在.bashrc文件最后一行插入以下指令
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:lib文件的绝对路径

# 生效更新
. .bashrc # source .bashrc

# 在处理后生成的app文件下用lld指令，如果libcalculate.so以分配内存且路径在lib文件夹下则链接成功
ldd app

```

*   永久配置 2（系统级）

```
# 处理生成app文件（app非必定名字）
gcc main.c -o app -I ./include/ -l calculate -L ./lib/

# 用管理员身份进入系统变量设置文件
sudo vim /etc/profile

# 在profile文件最后一行插入以下指令
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:lib文件的绝对路径

# 生效更新
. /etc/profile # source /etc/profile

# 在处理后生成的app文件下用lld指令，如果libcalculate.so以分配内存且路径在lib文件夹下则链接成功
ldd app

```

*   永久配置 3（系统级，便捷）

```
# 处理生成app文件（app非必定名字）
gcc main.c -o app -I ./include/ -l calculate -L ./lib/

# 由于/etc/ld.so.cache文件是二进制文件，所以我们间接修改/etc/ld.so.conf文件：插入lib文件的绝对路径保存即可
sudo vim /etc/ld.so.conf

# 生效更新
sudo ldconfig

# 在处理后生成的app文件下用lld指令，如果libcalculate.so以分配内存且路径在lib文件夹下则链接成功
ldd app

```

*   永久配置 4（系统级，但是 / lib/，/usr/lib 目录下太多文件不建议配置）

### 静态库和动态库的区别

静态库、动态库区别来自链接阶段如何处理链接成可执行程序。分为静态链接方式和动态链接方式。

#### 静态库优缺点

*   **优点**
    
    *   静态库被打包到应用程序中加载速度快。
    *   发布程序无需额外提供静态库，移殖方便。
*   **缺点**
    
    *   消耗系统资源，浪费内存。
    *   更新、部署、发布麻烦。

#### 动态库优缺点

*   **优点**
    
    *   可以实现进程间资源共享（共享库）。
    *   更新、部署、发布简单。
    *   加载动态库时间可控。
*   **缺点**
    
    *   加载速度相对于静态库慢。
    *   发布程序时需要提供依赖的动态库。

Makefile
--------

### 什么是 Makefile

> **Makefile 是一种用于管理和自动化软件项目编译、构建和部署过程的文本文件。**  
> Makefile 的好处就是 “自动化编译”，只需一个 make 命令整个工程完全自动编译极大地提高了软件开发效率。  
> make 是一个解释 Makefile 文件中指令的命令工具。

### Makefile 文件的命名规则

*   **命名**：makefile 或 Makefile
*   **规则**：一个 Makefile 文件中可以有一个或多个规则

**代码示例**

**目标**：最终要生成的文件（伪目标文件不算）  
**伪目标**：一种特殊目标且不生成文件，而是表示一组命令的集合  
**依赖**：生成目标所需文件或是目标  
**命令**：通过执行命令对依赖操作生成目标（命令行前必须 Tab 缩进）

```
# 目标文件:依赖文件
#     命令(shell)
#     ...
# .PHONY:伪目标

app:sub.c add.c mult.c div.c main.c
	gcc sub.c add.c mult.c div.c main.c -o app
.PHONY:clean
clean:
    rm -f *.o my_program

```

在当前目录下键入 `make` 指令执行 Makefile 文件。如果没有指定目标， `make` 默认会执行 Makefile 中的第一个目标。

### Makefile 工作原理

**1. 执行命令前检查规则**

是 否 否 是 执行命令前 检查规则 规则中  
依赖是否存在 执行命令 向下检查规则 是否有其他规则  
用来生成依赖 执行该规则命令

**2. 执行命令时检测更新**

是 否 执行命令时 比较目标和依赖的时间 目标是否比依赖晚 不更新目标  
对应规则命令不执行 重新生成目标

### Makefile 变量

#### 自定义变量

**语法**：`变量名 = 变量值`

```
var = hello

```

#### 常用预定义变量

<table><thead><tr><th>预定义变量名</th><th>含义</th><th>默认值</th></tr></thead><tbody><tr><td><code>AR</code></td><td>归档维护程序的名称</td><td>ar</td></tr><tr><td><code>CC</code></td><td>C 编译器的名称</td><td>cc</td></tr><tr><td><code>CXX</code></td><td>C++ 编译器的名称</td><td>g++</td></tr><tr><td><code>$@</code></td><td>目标文件的完整名称</td><td></td></tr><tr><td><code>$&lt;</code></td><td>第一个依赖文件的名称</td><td></td></tr><tr><td><code>$^</code></td><td>所有的依赖文件</td><td></td></tr></tbody></table>

#### 获取变量值

**语法**：`$(变量名)`

```
$(var)

```

#### 变量使用

自动变量只能在规则的命令中使用

```
app:main.c a.c b.c
	gcc -c main.c a.c b.c -o app

# 以上代码等同于以下代码
src=main.c a.c b.c
target=app
$(target):$(src)
	$(CC) -c $^ -o $@

```

#### 变量匹配

**常用匹配规则**

<table><thead><tr><th>通配符</th><th>含义</th></tr></thead><tbody><tr><td><code>*</code></td><td>匹配零个或多个字符</td></tr><tr><td><code>?</code></td><td>匹配一个字符</td></tr><tr><td><code>%</code></td><td>匹配一个字符串（两个 <code>%</code> 匹配的是同一个字符串）</td></tr><tr><td><code>[...]</code></td><td>匹配方括号内的任何一个字符</td></tr><tr><td><code>[^...]</code></td><td>匹配除方括号内字符之外的任何一个字符</td></tr></tbody></table>

**代码示例**

```
# 将所有 .c 文件编译为相应的 .o 文件
%.o: %.c
    $(CC)  -c $< -o $@

```

### Makefile 常用函数

**1.`$(wildcard PATTERN)`**

*   **作用**：获取指定目录下指定类型的文件列表。
*   **参数**：PATTERN 指一个或多个（空格隔开）对应某种类型的文件。
*   **返回**：得到对应匹配的文件列表。

**代码示例**

```
$(wildcard *.c ./lib/*.c)

```

**2.`$(patsubst PATTERN,REPLACEMENT,TEXT)`**

*   **作用**：如果 TEXT 与 PATTERN 匹配，则用 REPLACEMENT 对应替换 TEXT 。
*   **参数**：PATTERN 是指匹配规则，REPLACEMENT 是指替换后字符串，TEXT 待替换字符串。
*   **返回**：被替换后的字符串。

**代码示例**

```
$(patsubst %.c,%.o,add.c sub.c mult.c div.c)

```

GDB
---

### 什么是 GDB

> **GDB(GNU Debugger) 是一种用于调试程序的开源调试工具。**  
> GDB 同 GCC 配套组成了一套完整的开发环境，是 Linux 和许多类 Unix 系统中的标准开发环境。  
> GDB 主要有以下功能：自定义启动和运行程序、在断点处暂停运行并检查、改变程序修正 BUG。

### 调试前准备工作

关掉[编译器优化](https://so.csdn.net/so/search?q=%E7%BC%96%E8%AF%91%E5%99%A8%E4%BC%98%E5%8C%96&spm=1001.2101.3001.7020)选项 `-On` ，并打开调试选项 `-g` ，另外尽量在不影响程序行为的情况下打开选项`-Wall`，显示所有 warning。

**代码示例**  
源文件 test.c

```
//test.c
#include <stdio.h>
#include <stdlib.h>
 
int test(int a);
 
int main(int argc, char* argv[]) {
    int a, b;
    printf("argc = %d\n", argc);
 
    if(argc < 3) {
        a = 10;
        b = 30;
    } else {
        a = atoi(argv[1]);
        b = atoi(argv[2]);
    }
    printf("a = %d, b = %d\n", a, b);
    printf("a + b = %d\n", a + b);
 
    for(int i = 0; i < a; ++i) {
        printf("i = %d\n", i);
        // 函数调用
        int res = test(i);
        printf("res value: %d\n", res);
    }
 
    printf("THE END !!!\n");
    return 0;
}
int test(int a){
	int num = 0;
	for (int i = 0;i < a;++i){
		num += 1;
	}
    return num;
}



```

对 test.c 进行调试前编译

```
gcc -g -Wall test.c -o test

```

注意：`-g` 选项的作用是在可执行文件中加入源代码的信息，比如可执行文件中第几条机器指令对应源代码的第几行，但并不是把整个源文件嵌入到可执行文件中，所以在调试时必须保证 gdb 能找到源文件。

### GDB 常用命令及使用

#### 基础命令

**启动命令**  
`gdb 可执行程序` ：进入可执行程序调试文件

```
gdb test

```

![](https://img-blog.csdnimg.cn/c1a94c5972a447ee823087351300ee41.png)

**退出命令**  
`quit` 或 `q` ：退出调试

```
quit
# q

```

![](https://img-blog.csdnimg.cn/22f66f2e7d2a40b19182e82dc08e8af7.png)

**参数命令**  
`set args 参数值...`：给程序设置参数  
`show args`：获取设置参数

```
set args 10 20
show args

```

![](https://img-blog.csdnimg.cn/9bd0026e5c704ea3adbef428b26baa2e.png)

**帮助命令**  
`help (具体命令)` ：查看调试帮助或具体指令的相关文档

```
help
# help 具体命令

```

![](https://img-blog.csdnimg.cn/6857e6928cb44e83bb30cf37397d5212.png)

**查看文件代码命令**  
**查看当前文件**  
`list` 或 `l` ：从默认位置显示 (默认显示 10 行，一直 list 会继续生成 10 行直到)  
`list 行号` 或 `l 行号` ：从指定的行显示（行号为中间位置，上下一并显示）  
`list 函数名` 或 `l 函数名`：从指定的函数显示（函数名在中间，上下一并显示）

```
list
list 32
list test

```

![](https://img-blog.csdnimg.cn/84279a7973b34507b7ee23413f603083.png)  
**查看非当前文件代码**  
`list 文件名:行号` 或 `l 文件名:行号` ：从指定文件中指定的行显示（行号为中间位置，上下一并显示）  
`list 文件名:函数名` 或 `l 文件名:函数名`：从指定文件中指定的函数显示（函数名在中间，上下一并显示）  
注意：非当前文件也有限制（需在链接范围内否则会报文件找不到的错误），查看非当前文件代码时也需要生成 GDB 调试文件

```
g++ bubble.cpp main.cpp select.cpp -o main -g

```

```
list bubble.cpp:1
list select.cpp:selectSort

```

![](https://img-blog.csdnimg.cn/b6c83fb3ee754a2e8b184cc521336efd.png)![](https://img-blog.csdnimg.cn/f0644adda1574d56a542556f5d79708f.png)  
**行数命令**

`show listsize` 或 `show list` ：输出当前能一次性显示的代码行数（一般默认显示行数为 10 行）  
`set listsize 行数` 或 `set list 行数`：设置当前能一次性显示的代码行数

```
show list
set list 20

```

![](https://img-blog.csdnimg.cn/9075cd676edf4fe1acca585b02ba0b21.png)

#### 断点命令

**设置断点**  
`break 行号` 或 `b 行号`  
`break 函数名` 或 `b 函数名`  
`break 文件名:行号` 或 `b 文件名:行号`  
`break 文件名:函数` 或 `b 文件名:函数`  
![](https://img-blog.csdnimg.cn/3bfc7498b00148dcad35356db9ab9599.png)

**查看断点**  
`info break` 或 `i b`  
![](https://img-blog.csdnimg.cn/d454dc2d720f413fbbd1c1228c1ee1f6.png)

**删除断点**  
`delete 断点编号` 或 `del 断点编号` 或 `d 断点编号`  
![](https://img-blog.csdnimg.cn/9852063f28404be9946df3002df2c7f1.png)

**设置断点无效**  
`disable 断点编号` 或 `dis 断点编号`  
![](https://img-blog.csdnimg.cn/0b37e3e5998e4d5aaf8586b79258e176.png)

**设置断点生效**  
`enable 断点编号` 或 `ena 断点编号`  
![](https://img-blog.csdnimg.cn/8d681a3fc0c54dfd9f26764929c7670d.png)

**设置条件断点**  
一般用于循环体，条件中等号应为 `==` 。  
`break 断点编号 if 条件` 或 `b 断点编号 if 条件`  
![](https://img-blog.csdnimg.cn/dcc52e8a2fb04ec696beeef78b2e5f27.png)

#### 调试命令

**运行 GDB 程序**  
以下两个命令运行均可，个人使用感觉没啥区别  
`start`：运行程序并停止在第一行  
`run`：遇到断点才停  
![](https://img-blog.csdnimg.cn/916da5abc11d4f1291e8e69a34e3e336.png)

**继续运行命令**  
`continue` 或 `c`：继续运行到下一个断点停  
![](https://img-blog.csdnimg.cn/d1e681d39ebb409fb655c01ea29bb7cc.png)

**向下执行命令**  
`next` 或 `n`：向下执行一行代码（不会进入函数体）  
![](https://img-blog.csdnimg.cn/cade7d8f428444a19b58209fae2a88bb.png)

**变量操作命令**  
`print 变量名` 或 `p 变量名`：打印变量值  
`ptype 变量名`：打印变量类型  
![](https://img-blog.csdnimg.cn/5cd15667b57e45fe9bf14d7cbca72e88.png)

**单步调试命令**  
`step` 或 `s`：向下单步调试遇到函数进入函数体  
`finish`：跳出函数体  
![](https://img-blog.csdnimg.cn/47be96ce114342e5870266559d41ab9b.png)

#### 变量自动操作

`display 变量名`：自动打印指定变量的值  
`info display` 或 `i display`：继续调试时就会自动显示 display 的变量  
`undisplay 编号`：不显示此编号的 display 变量  
![](https://img-blog.csdnimg.cn/658e5537411c4dacaefab26a14d38216.png)

**其他操作**  
`set var 变量名 = 变量值`：设置变量，循环体用得多  
`until`：跳出循环  
![](https://img-blog.csdnimg.cn/924f1d8544ee44d8ab77636f0b88a74e.png)

标准 C 库 IO 函数和 Linux 系统 IO 函数对比
------------------------------

标准 C 库的函数文档在 `man` 的第三章，可以使用以下命令来查看详细文档（以`fopen`为例）

```
man 3 fopen

```

Linux 系统函数在 `man` 的第二章，可以使用以下命令来查看详细文档（以 open` 为例）

```
man 2 open

```

### 标准 C 库 IO 函数

![](https://img-blog.csdnimg.cn/5e592ad4163749849d9d1d5f45db4c3a.png)  
每个标准 C 库的 IO 函数都带有缓冲区。

### 标准 C 库 IO 函数和 Linux 系统 IO 函数工作流程

![](https://img-blog.csdnimg.cn/dfaf92454a164ccbbf337d1151686857.png)

### 详细对比

<table><thead><tr><th>特性</th><th>标准 C 库 IO 函数</th><th>Linux 系统 IO 函数</th></tr></thead><tbody><tr><td>头文件</td><td><code>&lt;stdio.h&gt;</code></td><td><code>&lt;unistd.h&gt;</code></td></tr><tr><td>缓冲 IO</td><td>有缓冲</td><td>无缓冲</td></tr><tr><td>缓冲模式</td><td>可设置缓冲模式</td><td>无</td></tr><tr><td>文件指针</td><td><code>FILE*</code> 类型的文件指针</td><td>无</td></tr><tr><td>阻塞 IO</td><td>阻塞</td><td>阻塞或非阻塞</td></tr><tr><td>文件描述符</td><td>通过 <code>fileno()</code> 函数获取</td><td>直接使用整数类型的文件描述符</td></tr><tr><td>适用范围</td><td>文件、文本</td><td>文件、文本、管道、套接字</td></tr><tr><td>数据格式</td><td>格式化输入输出</td><td>无</td></tr><tr><td>并发和异步支持</td><td>有限</td><td>支持非阻塞 IO、异步 IO</td></tr><tr><td>使用场景</td><td>通常用于常规 IO 操作</td><td>更底层、高性能、网络编程</td></tr></tbody></table>

虚拟地址空间
------

> 此内存空间是不存在的是用来方便解释代码的执行逻辑，在内核通过逻辑管理单元 mmu 映射到物理内存。

![](https://img-blog.csdnimg.cn/c62dd0c10d5248d0ae5e3e28814ae655.png)

文件描述符
-----

> 文件描述符表本质是一个数组，前三个数字 0、1、2 固定后面可看作为文件编号方便打开文件，默认大小为 1024byte。

![](https://img-blog.csdnimg.cn/7ef031d176d54038854da03637c537af.png)  
注意：一个文件可以打开多次，但是每次打开的文件描述符不同。**后面介绍的函数均为 Linux 系统 IO 函数**。

open、close 函数
-------------

**`int open(const char *pathname, int flags);`**

*   **作用**：打开一个已经存在的文件
*   **参数**：
    *   `pathname`：要打开的文件路径
    *   `flags`：对文件操作的权限设置（还有其他设置）
        *   **必选项**：`O_RDONLY` 只读， `O_WRONLY` 只写， `O_RDWR` 读写
        *   **可选项**：`O_CREAT` 文件不存在，创建新文件
*   **返回值**：如果成功返回一个新的文件描述符；如果失败返回 - 1

**`void perror(const char *s);`**

*   **作用**：打印 errno 对应的错误描述
*   **参数**：`s`：用户描述，比如 hello，最终输出的内容是 hello:xxx(实际的错误描述）
*   **返回值**：errno 属于 Linux 系统函数库，库里面的一个全局变量，记录的是最近的错误号，返回对应的 errno 错误描述

**代码示例**

```
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>

int main(){
    int fd = open("a.txt",O_RDONLY);
    if(fd == -1){
    	//参数一般为调用函数
        perror("open");
    }
    //关闭
    close(fd);
    return 0;
}

```

![](https://img-blog.csdnimg.cn/9c77c2a6cc2547f18f2bd3651c7c6226.png)

**`int open(const char *pathname,int flags, mode_t mode);`**

*   **作用**：打开一个已经存在的文件
*   **参数**：
    *   `pathname`：要打开的文件路径
    *   `flags`：对文件操作的权限设置（还有其他设置）
        *   **必选项**：`O_RDONLY` 只读， `O_WRONLY` 只写， `O_RDWR` 读写
        *   **可选项**：`O_CREAT` 文件不存在，创建新文件
    *   `mode`：八进制的数，表示创建出的新的文件的操作权限，最终权限为 `mode & ~umask`  
        ，`umask` 的作用就是抹去某些权限，调用`umask` 函数可设定
*   **返回值**：如果成功返回一个新的文件描述符，如果失败返回 - 1

**代码示例**

```
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>

int main(){
	//创建一个新文件
	//flags参数是一个int类型的数据，占4个字节，32位flags 32个位，每一位就是一个标志位。
	//使用按位或：| 原因是每个flag都是互斥的，只能通过或来进行权限的增添。
    int fd = open("a.txt", O_RDONLY | O_CREAT, 0777);
    if(fd == -1){
    	//参数一般为调用函数
        perror("open");
    }
    //关闭
    close(fd);
    return 0;
}

```

![](https://img-blog.csdnimg.cn/2f4a9adb0c5d47a3944d722931ee5572.png)

**`int close(int fd);`**

*   **作用**：关闭文件描述符（养成每打开一次文件匹配一个此函数的习惯）
*   **参数**：`fd`：文件描述符
*   **返回值**：如果成功返回 0，如果失败返回 - 1

read、write 函数
-------------

> 两者搭配一般用于拷贝文件内容

**`ssize_t read(int fd, void *buf, size_t count);`**

*   **作用**：读取指定文件
*   **参数**：
    *   `fd`：文件描述符，open 得到的，通过这个文件描述符操作某个文件
    *   `buf`：需要读取数据存放的地方，数组的地址（传出参数)
    *   `count`：要读的数据的实际的大小
*   **返回值**：如果成功大于 0 返回实际读取到的字节数，等于 0 表示文件已经读取完毕；如果失败返回 - 1 并设置 errno

**`ssize_t write(int fd, const void *buf, size_t count);`**

*   **作用**：写入指定文件
*   **参数**：
    *   `fd`：文件描述符，open 得到的，通过这个文件描述符操作某个文件
    *   `buf`：要往磁盘写入的数据，数组的地址（传入参数)
    *   `count`：要写的数据的实际的大小
*   **返回值**：如果成功大于 0 返回实际读取到的字节数，等于 0 表示没有任何内容写入文件；如果失败返回 - 1 并设置 errno

```
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>

int main(){
    //1. 通过 open 打开 source.txt 文件
    int source_fd = open("source.txt", O_RDONLY);
    if(source_fd == -1){
        perror("open");
        return -1;
    }

    //2. 创建一个新的文件（拷贝文件）
    int copy_fd = open("copy.txt", O_WRONLY | O_CREAT, 0777);
    if(copy_fd == -1){
        perror("open");
        return -1;
    }

    //3. 频繁的读写操作，注意buf是一个数组需先分配和初始化，循环条件注意>优先级大于=需要左边表达式加上括号
    char buf[1024]={0};
    int len = 0;
    while((len = read(source_fd, buf, sizeof(buf)))>0){
        write(copy_fd, buf, len); 
    }
    //4. 关闭文件
    close(source_fd);
    close(copy_fd);

    return 0;
}

```

lseek 函数
--------

**`off_t lseek(int fd, off_t offset, int whence);`**

*   **作用**：1. 移动文件指针到文件头`lseek(fd,0，SEEK_SET);`  
               2. 获取当前文件指针的位置`lseek(fd，0，SEEK_CUR);`  
               3. 获取文件长度`lseek(fd,0，SEEK_END);`  
               4. 拓展文件的长度（如：当前文件 10b，110b，增加了 100 个字节）`lseek(fd,100,SEEK_END);`
    
*   **参数**：
    
    *   `fd`：文件描述符，open 得到的，通过这个文件描述符操作某个文件
    *   `offset`：偏移量
    *   `whence`：
        *   `SEEK SET` 设置文件指针的偏移量
        *   `SEEK CUR` 设置偏移量：当前位置 + 第二个参数 offset 的值
        *   `SEEK END` 设置偏移量：文件大小 + 第二个参数 offset 的值
*   **返回值**：返回文件指针的位置
    

**代码示例**

```
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>

int main()
{
    int fd = open("hello.text", O_RDWR);
    if (fd == -1)
    {
        perror("open");
        return -1;
    }

    // 扩展文件的长度
    lseek(fd, 100, SEEK_END);

    // 为方便显示录入数据后的变化，写入空字符填满并增加1字节
    write(fd, " ", 1);
    
    // 关闭文件
    close(fd);
    return 0;
}

```

**代码执行前**  
![](https://img-blog.csdnimg.cn/3e03bc0f22bf4a08bc7db8574c4f5aac.png)

**代码执行后**  
![](https://img-blog.csdnimg.cn/e60ce0577693498184ef755bcbab10c5.png)  
注意：`lseek` 拓展文件相当于：**先占坑，再拉💩**，免得正脱裤子的时候别人把你坑占了直接拉。

stat、lstat 函数
-------------

**`int stat(const char *pathname, struct stat statbuf);`**

*   **作用**：获取一个文件相关的一些信息
*   **参数**：
    *   `pathname`：操作的文件的路径
    *   `statbuf`：结构体变量，传出参数，用于保存获取到的文件的信息
*   **返回值**：如果成功返回 0；如果失败返回 - 1 并设置 errno

**代码示例**

```
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>

int main(){

    struct stat statbuf;
    int ret = stat("hello.txt", &statbuf);
    if (ret == -1)
    {
        perror("stat");
        return -1;
    }
    printf( "size: %ld\n", statbuf.st_size);


    return 0;
}

```

![](https://img-blog.csdnimg.cn/8d28d7171c7e48f1ae919c645d825071.png)

![](https://img-blog.csdnimg.cn/ad502c50fdba4f50824379e68a7945b3.png)

**`int lstat(const char *pathname,struct stat statbuf);`**

*   **作用**：获取一个软链接文件指向的文件的相关的一些信息
*   **参数**：
    *   `pathname`：操作的文件的路径
    *   `statbuf`：结构体变量，传出参数，用于保存获取到的文件的信息
*   **返回值**：如果成功返回 0；如果失败返回 - 1 并设置 errno

### stat 结构体

```
struct stat
{
    dev_t      st _dev; // 文件的设备编号
    ino_t      st_ino; // 节点
    mode_t     st_mode; // 文件的类型和存取的权限
    nlink_t    st_nlink; // 连到该文件的硬连接数目
    uid_t      st_uid; // 用户ID
    gid_t      st_gid; // 组ID
    dev_t      st_rdev; // 设备文件的设备编号
    off_t      st_size; // 文件字节数(文件大小)
    blksize_t  st_blksize; // 块大小
    blkcnt_t   st_blocks; // 块数
    time_t     st_atime; // 最后一次访问时间
    time_t     st_mtime; // 最后一次修改时间(指内容)
    time_t     st_ctime; // 最后一次改变时间(指属性)
};

```

### st_mode 变量

![](https://img-blog.csdnimg.cn/9735ca5b95644c92a9885f599b23953a.png)

### 软链接与硬链接

> **软链接是一种特殊的文件，它包含指向目标文件或目录的路径。** 软链接通常用于跨文件系统的链接或者需要在文件系统中保留一些特殊结构的情况。  
> **硬链接是在同一文件系统上的同一文件或目录的多个名称。** 硬链接通常用于在同一文件系统内共享文件内容而不占用额外空间的情况。

下面是关于软链接和硬链接的区别的表格总结：

<table><thead><tr><th>特性</th><th>软链接<br>（Symbolic Link）</th><th>硬链接<br>（Hard Link）</th></tr></thead><tbody><tr><td>文件类型</td><td>文件和目录</td><td>仅限文件</td></tr><tr><td>跨文件系统</td><td>可以</td><td>不可以</td></tr><tr><td>存在目标删除后</td><td>是，但指向 “死链接”</td><td>否</td></tr><tr><td>占用额外磁盘空间</td><td>是</td><td>否</td></tr><tr><td>共享 inode</td><td>否</td><td>是</td></tr><tr><td>适用性</td><td>跨文件系统、目录、文件</td><td>仅限同一文件系统内的文件</td></tr></tbody></table>

### 软链接文件的创建

**代码示例**

```
ln -s a.txt b.txt

```

**执行代码**  
![](https://img-blog.csdnimg.cn/fd63f109f3c543fe9743bcd137c8b849.png)  
**生成软链接**  
![](https://img-blog.csdnimg.cn/41aa7220e6b646299dfa6da49538f284.png)

**删除软链接**  
如果删除 a.txt 文件会成为 “死链接”，无法打开 b.txt 文件  
![](https://img-blog.csdnimg.cn/87701d8ec14c4b77a7d1841585445a53.png)  
注意：当创建软链接后使用 vim 查看 b.txt 文件时会进入 a.txt 文件，对 b.txt 使用`stat` 函数会获取到 a.txt 文件信息，要获取软链接文件 b.txt 信息应该使用 `lstat` 函数。

### 模拟实现 ls -l 命令

`ls -l 文件名` ：用于列出文件和目录详细信息的命令，包括文件的权限、所有者、大小、创建日期等。

![](https://img-blog.csdnimg.cn/800efc65317e485cb9bc6176aa602b71.png)

```
//模拟实现 ls -l 命令
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>
#include <pwd.h>
#include <grp.h>
#include <time.h>
#include <string.h>


int main(int argc, char* argv[]){

    //判断输入的参数是否正确，不正确则提示
    if (argc>2)
    {
        printf("%s filename\n",argv[0]);
        //exit();
        return -1;
    }

    //通过stat函数获取用户传入的文件信息
    struct stat st;
    int ret = stat(argv[1],&st);
    if (ret == -1)
    {
        perror("stat");
        return -1;
    }

    // 获取文件类型和文件权限
    char perms[11] = {0}; // 用于保存文件类型和文件权限的字符串
    switch (st.st_mode & __S_IFMT)
    {
    case __S_IFLNK:
        perms[0] = 'l';
        break;
    case __S_IFDIR:
        perms[0] = 'd';
        break;
    case __S_IFREG:
        perms[0] = '-';
        break;
    case __S_IFBLK:
        perms[0] = 'b';
        break;
    case __S_IFCHR:
        perms[0] = 'c';
        break;
    case __S_IFSOCK:
        perms[0] = 's';
        break;
    case __S_IFIFO:
        perms[0] = 'p';
        break;
    default:
        perms[0] = '?';
        break;
    }

    //判断文件的访问权限

    //文件所有者访问权限
    perms[1] = (st.st_mode & S_IRUSR)? 'r' : '-' ;
    perms[2] = (st.st_mode & S_IWUSR)? 'w' : '-' ;
    perms[3] = (st.st_mode & S_IXUSR)? 'x' : '-' ;
    
    //文件所在组访问权限
    perms[4] = (st.st_mode & S_IRGRP)? 'r' : '-' ;
    perms[5] = (st.st_mode & S_IWGRP)? 'w' : '-' ;
    perms[6] = (st.st_mode & S_IXGRP)? 'x' : '-' ;
    
    //其他人访问权限
    perms[7] = (st.st_mode & S_IROTH)? 'r' : '-' ;
    perms[8] = (st.st_mode & S_IWOTH)? 'w' : '-' ;
    perms[9] = (st.st_mode & S_IXOTH)? 'x' : '-' ;
    
    //硬链接数
    int linkNum = st.st_nlink;

    //文件所有者名称
    char* fileUsr = getpwuid(st.st_uid)->pw_name;

    //文件所在组名称
    char* fileGrp = getgrgid(st.st_gid)->gr_name;
    
    //文件大小
    off_t fileSize = st.st_size;
    
    //获取修改时间
    char* time = ctime(&st.st_mtime);
    
    //删除time带来的换行
    char mtime[512];
    strncpy(mtime, time, strlen(time)-1);

    //输出
    char buf[1024];
    sprintf(buf,"%s %d %s %s %ld %s %s", perms, linkNum, fileUsr, fileGrp, fileSize, mtime, argv[1]);

    printf("%s\n", buf);

    return 0;
}


```

![](https://img-blog.csdnimg.cn/95359cf2c2c04064ac06590d98551022.png)  
注意：此代码巩固了 st_mode 编码的运用，多多品味一些细节。`off_t` 表示 `long int` 。

文件属性操作函数
--------

### access 函数

**`int access(const char *pathname, int mode);`**

*   **作用**：判断某个文件是否有某个权限，或者判断文件是否存在参数
*   **参数**：
    *   `pathname`：判断的文件路径
    *   `mode`：`R_OK`判断是否有读权限，`w_OK`判断是否有写权限，`X_OK`判断是否有执行权限，`F_OK`判断文件是否存在
*   **返回值**：如果成功返回 0；如果失败返回 - 1 并设置 errno

**代码示例**

```
#include <unistd.h>
#include <stdio.h>

int main(){
    int ret = access("c.txt", F_OK);
    if (ret == -1)
    {
        perror("access");
    }
    printf("文件不存在！\n");
    return 0;
}

```

![](https://img-blog.csdnimg.cn/f90c0c66a2ea4357bebfe8883ed6e495.png)

### chomd 函数

**`int chmod(const char *pathname, mode_t mode);`**

*   **作用**：修改文件的权限
*   **参数**：
    *   `pathname`：需要修改的文件的路径
    *   `mode`：需要修改的权限值，八进制的数
*   **返回值**：如果成功返回 0；如果失败返回 - 1 并设置 errno

**代码示例**

```
#include <sys/stat.h>
#include <stdio.h>

int main(){
    int ret = chmod("a.txt",0777);
    if (ret == -1){
        perror("chmod");
        return -1;
    }
    return 0;
}

```

**代码执行前**  
![](https://img-blog.csdnimg.cn/89b995e3ff5546ef986eaa25aae2bdfb.png)  
**代码执行后**  
![](https://img-blog.csdnimg.cn/0adf6ff2b7fb4e05988634402ff11ec9.png)

### chown 函数

**`int chown (const char *pathname, uid_t owner, gid_t group);`**

*   **作用**：修改文件的所有者与所有组
*   **参数**：
    *   `pathname`：需要修改的文件的路径
    *   `owner`：所有者的 ID
    *   `group`：所有组的 ID
*   **返回值**：如果成功返回 0；如果失败返回 - 1 并设置 errno

**所有者 ID 查看**

```
vim /etc/passwd

```

**所有组 ID 查看**

```
vim /etc/group

```

### truncate 函数

**`int truncate(const char *path, off_t length);`**

*   **作用**：缩减或者扩展文件的尺寸至指定的大小
*   **参数**：
    *   `path`：需要修改的文件的路径
    *   `length`：需要最终文件变成的大小
*   **返回值**：如果成功返回 0；如果失败返回 - 1 并设置 errno

**代码示例**

```
#include <unistd.h>
#include <sys/types.h>
#include <stdio.h>

int main(){
    int ret = truncate("b.txt", 20);
    if (ret == -1)
    {
        perror("truncate");
        return -1;
    }
    return 0;
}

```

注意：`truncate` 函数可以通过改变文件的大小来删除或添加文件内容，而 `lseek` 函数只是用于移动文件指针的位置。

目录操作函数
------

### mkdir 函数

**`int mkdir(const char *pathname, mode_t mode);`**

*   **作用**：创建一个目录
*   **参数**：
    *   `pathname`：创建的目录的路径
    *   `mode`：权限，八进制的数
*   **返回值**：如果成功返回 0；如果失败返回 - 1 并设置 errno

**代码示例**

```
#include <sys/stat.h>
#include <sys/types.h>
#include <stdio.h>
int main()
{
    int ret = mkdir("aaa", 0777);
    if (ret == -1)
    {
        perror("mkdir");
        return -1;
    }
    return 0;
}

```

### rmdir 函数

**`int rmdir (const char *pathname);`**

*   **作用**：删除一个空目录（只能是空目录含文件会报错）
*   **参数**：`pathname`：需删除的目录的路径
*   **返回值**：如果成功返回 0；如果失败返回 - 1 并设置 errno

### rename 函数

**`int rename(const char *oldpath,const char *newpath);`**

*   **作用**：创建一个目录
*   **参数**：
    *   `oldpath`：当前目录的路径名
    *   `newpath`：改后目录的路径名
*   **返回值**：如果成功返回 0；如果失败返回 - 1 并设置 errno

**代码示例**

```
#include <stdio.h>
int main()
{
    int ret = rename("aaa", "bbb");
    if (ret == -1)
    {
        perror("rename");
        return -1;
    }
    return 0;
}

```

### chdir 函数

**`int chdir(const char *path);`**

*   **作用**：修改进程的工作目录
*   **参数**：`path`：需修改的工作目录的路径
*   **返回值**：如果成功返回 0；如果失败返回 - 1 并设置 errno

### getcwd 函数

**`char *getcwd(char *buf, size_t size);`**

*   **作用**：获取当前的工作目录
*   **参数**：
    *   `buf`：存储的路径，指向的是一个数组
    *   `size`：数组的大小
*   **返回值**：返回指向的一块内存，这块内存的数据就是第一个参数

**代码示例**

```
#include <unistd.h>
#include <stdio.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <fcntl.h>
int main(){
    // 获取当前的工作目录
    char buf[128];
    getcwd(buf, sizeof(buf));
    printf("当前的工作目录是:%s\n", buf);

    // 修改工作目录
    int ret = chdir("/home/zxz/open_file_excise/change_direction");
    if (ret == -1)
    {
        perror("chdir");
        return -1;
    }

    // 创建一个新的文件
    int fd = open("chdir.txt", O_CREAT | O_RDWR, 0664);
    if (fd == -1)
    {
        perror("open");
        return -1;
    }
    close(fd);

    // 获取修改后当前的工作目录
    char buf1[128];
    getcwd(buf1, sizeof(buf1));
    printf("当前的工作目录是:%s\n", buf1);
    return 0;
}

```

![](https://img-blog.csdnimg.cn/ccb088fb70704909bc20bb964aaa55b3.png)

目录遍历函数
------

### opendir 函数

**`DIR *opendir(const char *name);`**

*   **作用**：打开一个目录
*   **参数**： `name`：需要打开的目录的名称
*   **返回值**：返回 `DIR*` 类型的目录流

### readdir 函数

**`struct dirent *readdir(DIR *dirp);`**

*   **作用**：读取目录中的信息
*   **参数**： `dirp`：opendir 返回的结果
*   **返回值**：`struct dirent*` 类型表示如果读取成功返回 dirent 结构体；如果读取到的文件的信息读取到了末尾或者失败了，返回 NULL

#### dirent 结构体

```
struct dirent
{
    ino_t d_ino;                 // 此目录进入点的inode
    off_t d_off;                 // 目录文件开买至此目录进入点的位移
    unsigned short int d_reclen; // d_name的长度，不包含NULL字符
    unsigned char d_type;        // d_name所指的文件类型
    char d_name[256];            // 文件名
};

```

#### d_type 变量

![](https://img-blog.csdnimg.cn/ef5bc4c21d03403fb5553e4c3d4f41e0.png)

### closedir 函数

**`int closedir(DIR *dirp);`**

*   **作用**：关闭目录指定目录
*   **参数**：`dirp`：opendir 返回的结果
*   **返回值**：如果成功返回 0；如果失败返回 - 1 并设置 errno

**代码示例**

```
#define _DEFAULT_SOURCE
#include <sys/types.h>
#include <dirent.h>
#include <unistd.h>
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

// 读取某个目录下所有的普通文件的个数
int getFileNum(const char *path)
{
    // 打开目录
    DIR *dir = opendir(path);
    if (dir == NULL)
    {
        perror("opendir");
        exit(0);
    }

    struct dirent *ptr;

    // 记录普通文件个数
    int total = 0;

    while ((ptr = readdir(dir)) != NULL)
    {
        // 获取名称
        char *dname = ptr->d_name;
        // 忽略掉．和..
        if (strcmp(dname, ".") == 0 || strcmp(dname, "..") == 0)
        {
            continue;
        }
        // 判断是否是普通文件还是目录
        if (ptr->d_type == DT_DIR)
        {
            // 目录,需要继续读取这个目录
            char newpath[256];
            sprintf(newpath, "%s/%s", path, dname);
            total += getFileNum(newpath);
        }

        if (ptr->d_type == DT_REG)
        {
            // 普通文件
            total++;
        }
    }
    // 关闭目录
    closedir(dir);
    return total;
}

int main(int argc, char *argv[1])
{
    if (argc < 2)
    {
        printf("%s path\n", argv[0]);
        return -1;
    }
    int num = getFileNum(argv[1]);
    printf("普通文件的个数为:%d\n", num);

    return 0;
}


```

![](https://img-blog.csdnimg.cn/47dfe00209704be8b4e7afb41aaaca77.png)

dup、dup2 函数
-----------

**`int dup (int oldfd);`**

*   **作用**：复制文件描述符（原文件描述符和复制文件描述符指向同一个文件）
*   **参数**： `oldfd`：需要复制的文件描述符
*   **返回值**：如果成功返回文件描述符；如果失败返回 - 1 并设置 errno

**代码示例**

```
#include <unistd.h>
#include <stdio.h>
#include <fcntl.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <string.h>

int main()
{
    int fd = open("a.txt", O_RDWR | O_CREAT, 0664);
    int fd1 = dup(fd);
    if (fd1 == -1)
    {
        perror("dup");
        return -1;
    }
    printf("fd：%d\nfd1：%d\n", fd, fd1);
    close(fd);
    char *str = "hello,world";

    int ret = write(fd1, str, strlen(str));
    if (ret == -1)
    {
        perror("write");
        return -1;
    }
    close(fd1);
    return 0;
}

```

![](https://img-blog.csdnimg.cn/c3cf8db68fef497c9ab946cfeeda93b8.png)

**`int dup2 (int oldfd, int newfd);`**

*   **作用**：重定向文件描述符（如：`oldfd` 指向 a.txt， `newfd` 指向 b.txt；调用函数成功后：`newfd` 和 b.txt 做 `close`，`newfd` 指向了 a.txt）
*   **参数**：
    *   `oldfd`：原文件描述符（必须是有效的）
    *   `newfd`：可以重定向的文件描述符
*   **返回值**：如果成功返回重定向的文件描述符；如果失败返回 - 1 并设置 errno

**代码示例**

```
#include <unistd.h>
#include <stdio.h>
#include <fcntl.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <string.h>
int main()
{
    int fd = open("1.txt", O_RDWR | O_CREAT, 0664);
    if (fd == -1)
    {
        perror("open");
        return -1;
    }

    int fd1 = open("2.txt", O_RDWR | O_CREAT, 0664);
    if (fd1 == -1)
    {
        perror("open");
        return -1;
    }

    printf("fd：%d\nfd1：%d\n", fd, fd1);

    int fd2 = dup2(fd, fd1);
    if (fd2 == -1)
    {
        perror("dup2");
        return -1;
    }

    // 通过fd1去写数据，实际操作的是1.txt，而不是2.txt
    char *str = "hello, dup2";
    int len = write(fd1, str, strlen(str));

    printf("fd：%d\nfd1：%d\nfd2：%d\n", fd, fd1, fd2);

    close(fd);
    close(fd1);
    // close(fd2); fd1、fd2文件描述符相同可选一个关

    return 0;
}

```

![](https://img-blog.csdnimg.cn/7c841caffd6c4acc966c93719c8a3d8a.png)

fcntl 函数
--------

`int fcntl(int fd, int cmd, ...);`

*   **作用**：复制文件描述符、设置和获取文件状态标志
*   **参数**：
    *   `fd`：表示需要操作的文件描述符
    *   `cmd`：表示对文件描述符进行如何操作
        *   `F_DUPFD`：复制文件描述符，复制的是第一个参数 `fd`
        *   `F_GETFL`：获取指定的文件描述符文件状态 flag  
            获取的 flag 和我们通过`open`函数传递的 flag 是一个东西
        *   `F_SETFL`：设置文件描述符文件状态 flag  
            **必选项**：`O_RDONLY`， `O_WRONLY` ，`O_RDWR` （不可以被修改）  
            **可选项**：`O_APPEND` 追加数据，`O_NONBLOCK` 设置非阻塞（可以被修改）
*   **返回值**：如果成功返回重定向的文件描述符；如果失败返回 - 1 并设置 errno

**代码示例**

```
#include <unistd.h>
#include <fcntl.h>
#include <stdio.h>
#include <string.h>
int main()
{
    // 1.复制文件描述符
    int fd = open("1.txt", O_RDWR);
    // 第三个参数为0，则系统会自动选择一个未使用的最小文件描述符作为复制后的文件描述符。
    int fd1 = fcntl(fd, F_DUPFD, 0);

    printf("fd：%d\nfd1：%d\n", fd, fd1);
    close(fd1);

    // 2.修改或者获取文件状态flag
    if (fd == -1)
    {
        perror("open");
        return -1;
    }

    // 2.1.获取文件描述符状态flag
    int flag = fcntl(fd, F_GETFL);
    flag |= O_APPEND; // flag = flag | O_APPEND

    // 2.2.修改文件描述符状态的flag，给flag加入O_APPEND这个标记
    int ret = fcntl(fd, F_SETFL, flag);
    if (ret == -1)
    {
        perror("fcntl");
        return -1;
    }

    char *str = "nihao";

    write(fd, str, strlen(str));

    close(fd);

    return 0;
}


```

![](https://img-blog.csdnimg.cn/29829ec083cb42eb97f2fd1a2f63ff8c.png)

结语
--

课程笔记源于牛客 C++ 求职项目：[https://www.nowcoder.com/courses/cover/live/504](https://www.nowcoder.com/courses/cover/live/504) 的[第 1 章 Linux 系统编程入门](https://www.nowcoder.com/study/live/504/1/1)。  
此笔记相对课程内容有增删仅个人复习用，若有需要仅供参考。以上所有代码和图片均为课程自带以及网络资源，欢迎各位大佬提出问题和建议，此笔记实时更新。