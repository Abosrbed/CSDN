> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_53099212/article/details/132551062?spm=1001.2014.3001.5502)

#### Linux 多进程开发目录

*   [进程](#_2)
*   *   [程序和进程](#_3)
    *   *   [什么是程序](#_4)
        *   [什么是进程](#_17)
    *   [单道、多道程序设计](#_27)
    *   *   [什么是单道程序设计](#_28)
        *   [什么是多道程序设计](#_31)
    *   [时间片](#_39)
    *   *   [什么是时间片](#_40)
    *   [并行和并发](#_49)
    *   *   [什么是并行](#_50)
        *   [什么是并发](#_55)
    *   [进程控制块（PCB）](#PCB_69)
*   [进程状态转换](#_102)
*   *   [进程的状态](#_104)
    *   [进程相关命令](#_122)
    *   *   [查看进程](#_123)
        *   [实时显示进程动态](#_142)
        *   [杀死进程](#_165)
    *   [进程号和相关函数](#_189)
    *   *   [进程号](#_190)
        *   [父进程号](#_192)
        *   [进程组号](#_194)
        *   [相关函数](#_197)
*   [进程创建](#_211)
*   *   [fork 函数](#fork__213)
*   [父子进程虚拟地址空间情况](#_285)
*   *   [父子进程运行区别](#_286)
    *   [父子进程虚拟地址空间](#_293)
    *   [写时拷贝技术（Copy-On-Write）](#CopyOnWrite_357)
*   [父子进程关系及 GDB 多进程调试](#GDB_374)
*   *   [父子进程关系](#_375)
    *   [GDB 多进程调试](#GDB_395)
    *   *   [设置调试子进程或父进程](#_443)
        *   [设置调试模式](#_460)
        *   [查看调试的进程](#_476)
        *   [切换当前调试的进程](#_484)
        *   [使进程脱离 GDB 调试](#GDB_492)
*   [exec 函数族](#exec__501)
*   *   [什么是 exec 函数族](#_exec__502)
    *   [exec 函数族](#exec__510)
*   [进程控制](#_586)
*   *   [进程退出](#_587)
    *   [孤儿进程](#_634)
    *   [僵尸进程](#_674)
    *   [进程回收](#_726)
    *   *   [wait 函数](#wait__730)
        *   [退出信息相关宏函数](#_797)
        *   [waitpid 函数](#waitpid__880)
*   [进程间通信](#_978)
*   *   [什么是进程间通信](#_979)
    *   [Linux 进程间通信的方式](#Linux__990)
*   [匿名管道](#_992)
*   *   [管道的特点](#_1003)
    *   [为什么可以使用管道进行进程间通信](#_1017)
    *   [管道的数据结构](#_1024)
*   [父子进程通过匿名管道通信](#_1029)
*   *   [创建匿名管道](#_1030)
    *   [管道缓冲大小](#_1110)
    *   [匿名管道通信三种情况](#_1158)
    *   [第二种情况遇到的问题以及解决办法](#_1162)
*   [匿名管道通信案例](#_1235)
*   [管道读写特点和管道设置为非阻塞](#_1314)
*   *   [管道读写特点](#_1315)
    *   [管道设置为非阻塞](#_1335)
*   [有名管道](#_1420)
*   *   [有名管道与匿名管道的区别](#_1425)
    *   [有名管道的使用](#_1431)
*   [有名管道实现简单版聊天功能](#_1551)
*   *   [基本框架](#_1552)
    *   [写一读一聊天](#_1555)
*   [内存映射](#_1725)
*   *   [什么是内存映射](#_1726)
    *   [内存映射相关系统调用](#_1732)
    *   [使用内存映射实现进程间通信](#_1763)
    *   [内存映射相关问题](#_1834)
    *   [通过内存映射实现文件拷贝功能](#_1858)
    *   [匿名映射](#_1934)
*   [信号](#_1996)
*   *   [什么是信号](#_1997)
    *   [Linux 信号一览表](#Linux__2031)
    *   [信号的 5 种默认处理动作](#5_2070)
*   [kill、raise、abort 函数](#killraiseabort__2132)
*   [alarm 函数](#alarm__2190)
*   [setitimer 定时器函数](#setitimer__2242)
*   [signal 信号捕捉函数](#signal__2307)
*   [信号集及相关函数](#_2376)
*   *   [什么是信号集](#_2377)
    *   [阻塞信号集和未决信号集](#_2383)
    *   [信号集相关函数](#_2408)
*   [sigprocmask 函数使用](#sigprocmask__2510)
*   [sigaction 信号捕捉函数](#sigaction__2596)
*   *   [内核实现信号捕捉的过程](#_2689)
*   [SIGCHLD 信号](#SIGCHLD__2693)
*   [共享内存](#_2783)
*   *   [什么是共享内存](#_2785)
    *   [共享内存使用步骤](#_2792)
    *   [共享内存相关函数](#_2801)
    *   [共享内存操作命令](#_2924)
    *   *   [ipcs 用法](#ipcs__2925)
        *   [ipcrm 用法](#ipcrm__2948)
    *   [共享内存相关问题](#_2982)
*   [守护进程](#_3007)
*   *   [什么是控制终端](#_3008)
    *   [什么是进程组](#_3019)
    *   [什么是会话](#_3032)
    *   [进程组、会话、控制终端之间的关系](#_3040)
    *   [进程组、会话操作函数](#_3067)
    *   [什么是守护进程](#_3086)
    *   [守护进程的创建步骤](#_3099)
*   [结语](#_3202)

进程
--

### 程序和进程

#### 什么是程序

> **程序是包含一系列信息的文件**，这些信息描述了如何在运行时创建一个进程。

**信息文件**

*   **二进制格式标识**：每个程序文件都包含用于描述可执行文件格式的元信息。内核利用此信息来解释文件中的其他信息。 (ELE 可执行连接格式)
*   **机器语言指令**：对程序算法进行编码
*   **程序入口地址**：标识程序开始执行时的起始指令位置。
*   **数据**：程序文件包含的变量初始值和程序使用的字面量值 (比如字符串)。
*   **符号表及重定位表**：描述程序中函数和变量的位置及名称。这些表格有多重用途，其中包括调试和运行时的符号解析 (动态链接)。
*   **共享库和动态链接信息**：: 程序文件所包含的一些字段，列出了程序运行时需要使用的共享库，以及加载共享库的动态连接器的路径名。
*   **其他信息**：程序文件还包含许多其他信息，用以描述如何创建进程。

#### 什么是进程

> **进程是正在运行的程序的实例**，是一个具有一定独立功能的程序关于某个[数据集合](https://so.csdn.net/so/search?q=%E6%95%B0%E6%8D%AE%E9%9B%86%E5%90%88&spm=1001.2101.3001.7020)的一次运行活动，是**操作系统动态执行的基本单元**，在传统的[操作系统](https://so.csdn.net/so/search?q=%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F&spm=1001.2101.3001.7020)中，进程既是基本的执行单元，也是基本的分配单元。**进程是系统资源分配的最小单位，一个进程可以有多个线程。**

**进程与内核的关系**  
可以用一个程序来创建多个进程，进程是由内核定义的抽象实体，并为该实体分配用以执行程序的各项系统资源。  
**从内核的角度看，进程由用户内存空间和一系列内核数据结构组成，其中用户内存空间包含了程序代码及代码所使用的变量，而内核数据结构则用于维护进程状态信息。**  
记录在内核数据结构中的信息包括许多与进程相关的标识号 (IDs)、虚拟内存表、打开文件的描述符表、信号传递及处理的有关信息、进程资源使用及限制、当前工作目录和大量的其他信息。

### 单道、多道程序设计

#### 什么是单道程序设计

> **单道程序设计是指在一个时间段内，计算机内存中只允许一个的程序运行**，一旦一个程序开始执行，直到它执行完毕或者发生错误，其他程序都无法执行。

#### 什么是多道程序设计

> **多道程序设计是指在一个时间段内，计算机可以同时加载和执行多个程序**，使多个程序在管理程序控制下**相互穿插运行**并在计算机系统中同处于开始到结束之间的状态，这些程序共享计算机系统资源，从而提高系统资源和 CPU 的利用率。

**CPU 处理程序**  
对于一个单 CPU 系统来说，程序同时处于运行状态只是一种宏观上的概念，他们虽然都已经开始运行，但就微观而言，任意时刻，**CPU 上运行的程序只有一个**。在多道程序设计模型中，多个进程轮流使用 CPU。而当下常见 CPU 为纳秒级，1 秒可以执行大约 10 亿条指令。由于人眼的反应速度是毫秒级，所以看似同时在运行。

### 时间片

#### 什么是时间片

> **时间片 (time slice) 是操作系统分配给每个正在运行的进程微观上的一段 CPU 时间**。  
> 在只考虑一个 CPU 的情况下，这些进程 “看起来像” 同时运行的，实则是轮番穿插地运行。由于时间片通常很短(在 Linux 上一般为几 ms 到几十 ms)，用户不会感觉到。

**时间片在内核中的作用**  
**时间片由操作系统内核的调度程序分配给每个进程**。首先，内核会给每个进程分配相等的初始时间片，然后每个进程轮番地执行相应的时间，当所有进程都处于时间片耗尽的状态时，内核会重新为每个进程计算并分配时间片，如此往复。

### 并行和并发

#### 什么是并行

> **并行 (parallel) 指在同一时刻，有多条指令在多个处理器上同时执行。**

![](https://img-blog.csdnimg.cn/902d3e33671949a7b23d5d204a6fca0b.png)

#### 什么是并发

> **并发 (concurrency) 指在同一时刻只能有一条指令执行，但多个进程指令被快速的轮换执行，使得在宏观上具有多个进程同时执行的效果**，但在微观上并不是同时执行的只是把时间分成若干段，使多个进程快速交替的执行。

![](https://img-blog.csdnimg.cn/bdb826d2746f4afebc43f0f41eba9cd2.png)

**理解例子**

并行是两个队列同时使用两台咖啡机：  
![](https://img-blog.csdnimg.cn/62b7d895b843490886f64ba58679878e.png)

并发是两个队列交替使用一台咖啡机：  
![](https://img-blog.csdnimg.cn/a049ca0a799d4f16bfa0c88a420c2c8b.png)

### 进程控制块（PCB）

为了管理进程，内核必须对每个进程所做的事情进行清楚的描述。内核为每个进程分配一个 PCB(Processing Control Block) 进程控制块，维护进程相关的信息 Linux 内核的进程控制块是 `task_struct` 结构体。

在以下文件中可以查看 `task_struct` 结构体定义：

```
/usr/src/linux-headers-xxx/include/linux/sched.h

```

![](https://img-blog.csdnimg.cn/c72a73de2c174f0b80002e760baf2824.png)

**需要了解的 `task_struct` 结构体内容**

*   进程 id：系统中每个进程有唯一的 id，用 pid t 类型表示，其实就是一个非负整数
*   进程的状态：有就绪、运行、挂起、停止等状态
*   进程切换时需要保存和恢复的一些 CPU 寄存器
*   描述虚拟地址空间的信息
*   描述控制终端的信息
*   当前工作目录 (Current Working Directory)
*   umask 掩码
*   文件描述符表，包含很多指向 file 结构体的指针
*   和信号相关的信息
*   用户 id 和组 id
*   会话 (Session) 和进程组
*   进程可以使用的资源上限 (Resource Limit)

**查看资源上限的命令**

```
ulimit -a

```

![](https://img-blog.csdnimg.cn/9e2388afd8d64d8fbc20ccb3a7e836d8.png)

进程状态转换
------

### 进程的状态

**进程状态反映进程执行过程的变化**。这些状态随着进程的执行和外界条件的变化而转换。

在三态模型中进程状态分为三个基本状态：

*   **运行态**：进程占有处理器正在运行。
*   **就绪态**：进程具备运行条件，等待系统分配处理器以便运行。当进程已分配到除 CPU 以外的所有必要资源后，只要再获得 CPU，便可立即执行。在一个系统中处于就绪状态的进程可能有多个，通常将它们排成一个队列，称为就绪队列。
*   **阻塞态**：又称为等待 (wait) 态或睡眠 (sleep) 态，指进程不具备运行条件，正在等待某个事件的完成。

![](https://img-blog.csdnimg.cn/70deddb2360c4e3a94ddc2864b2a9fe0.png)

在五态模型中，进程状态在三个基本状态上添加了新建态、终止态

*   **新建态**：进程刚被创建时的状态，尚未进入就绪队列。
*   **终止态**：进程完成任务到达正常结束点，或出现无法克服的错误而异常终止，或被操作系统及有终止权的进程所终止时所处的状态。进入终止态的进程以后不再执行，但依然保留在操作系统中等待善后。一旦其他进程完成了对终止态进程的信息抽取之后，操作系统将删除该进程。

![](https://img-blog.csdnimg.cn/4ae85f50f7c34b11a3282bf591da15ba.png)

### 进程相关命令

#### 查看进程

`a` - 显示终端上的所有进程，包括其他用户的进程  
`u` - 显示进程的详细信息  
`x` - 显示没有控制终端的进程  
`j` - 列出与作业控制相关的信息

```
ps aux

```

![](https://img-blog.csdnimg.cn/c91ccf21cc81430eb5442d1182c8f6ce.png)

```
ps ajx

```

![](https://img-blog.csdnimg.cn/0a255c1b22ef4d18a4cc0d1d617cf7ac.png)

**STAT 参数含义**  
![](https://img-blog.csdnimg.cn/0b128eadd2634d298dd4fc891b0be73a.png)

#### 实时显示进程动态

```
top

```

可以在使用 `top` 命令时加上 `-d n`来指定显示信息更新的时间间隔

```
top -d 5

```

![](https://img-blog.csdnimg.cn/1b0864633fbc43cf8992f127787c2b52.png)

**更新排序**  
进入 top 后界面键入以下键盘按键可按规则显示

*   `M`：根据内存使用量排序
*   `P`：根据 CPU 占有率排序
*   `T`：根据进程运行时间长短排序
*   `U`：根据用户名来筛选进程
*   `K`：输入指定的 PID 杀死进程
*   `Q`：退出 top 界面

#### 杀死进程

**语法**：`kill 信号选项 pid`

**列出所有信号**

```
kill -l

```

![](https://img-blog.csdnimg.cn/eab3e5ff15b74a03b49a5334aa980575.png)

```
# 强制终止进程的命令
kill -9 pid #kill -SIGKILL pid

# 建议先向进程发送一个终止请求，允许进程执行清理工作并正常退出（15是kill默认信号）。别直接一来就9，除非出现严重问题。
kill -15 pid #kill -SIGTERM pid

```

**根据进程名杀死进程**

```
killall name

```

### 进程号和相关函数

#### 进程号

每个进程都由 **进程号 (PID)** 来标识，其类型为 `pid_t` (整型) 进程号的范围: 0~32767。进程号是唯一的，但可以重复使用。当一个进程终止后，其进程号就可以再次使用。

#### 父进程号

任何进程 (除 init 进程) 都是由另一个进程创建，该进程称为被创建进程的父进程对应的进程号称为 **父进程号 (PPID)** 。

#### 进程组号

进程组是一个或多个进程的集合。他们之间相互关联，进程组可以接收同一终端的各种信号，关联的进程有一个 **进程组号 (PGID)** 。默认情况下，当前的进程号会当做当前的进程组号。

#### 相关函数

**`pid_t getpid(void);`**

*   **作用**：用于获取调用进程的进程号
*   **返回值**：如果成功子进程中返回 0，父进程中返回子进程 ID 调用进程的进程号；如果失败返回 - 1 并设置 errno

**`pid_t getppid(void);`**

*   **作用**：用于获取调用进程的父进程号
*   **返回值**：如果成功子进程中返回 0 调用进程的父进程号；如果失败返回 - 1 并设置 errno

**`pid_t getpgid(void);`**

*   **作用**：用于获取调用进程的进程组号
*   **返回值**：如果成功子进程中返回进程组号；如果失败返回 - 1 并设置 errno

进程创建
----

系统允许一个进程创建新进程，新进程即为子进程，子进程还可以创建新的子进程，形成进程树结构模型。

### fork 函数

**`pid_t fork(void);`**

*   **作用**：用于创建一个新的进程（子进程）
*   **返回值**：如果成功子进程中返回 0，父进程中返回子进程 ID；如果失败返回 - 1 并设置 errno

**失败的两个主要原因**

1.  当前系统的进程数已经达到了系统规定的上限，这时 errno 的值被设置为 EAGAIN
2.  系统内存不足，这时 errno 的值被设置为 ENOMEM

**代码示例**

```
#include <sys/types.h>
#include <unistd.h>
#include <stdio.h>

int main()
{

    // 创建子进程
    pid_t pid = fork();

    // 判断是父进程还是子进程
    if (pid > 0)
    {
        printf("pid : %d\n", pid);
        // 如果大于0，返回的是创建的子进程的进程号，当前是父进程
        printf("i am parent process, pid : %d, ppid : %d\n", getpid(), getppid());
    }
    else if (pid == 0)
    {
        // 当前是子进程
        printf("i am child process, pid : %d, ppid : %d\n", getpid(), getppid());
    }

    for (int i = 0; i < 5; i++)
    {
        printf("i : %d, pid : %d\n", i, getpid());
        sleep(2);
    }

    return 0;
}

```

![](https://img-blog.csdnimg.cn/cc01427fb2e54cfc923687996ae9cb8e.png)

ps：在这放一道有争议的题，题目源于七牛云的笔试题，18 年的题至  
今都还有人讨论答案，欢迎各位大佬前来探讨。

> 以下程序输出（）个 “-”
> 
> ```
> int main(void) {
>     int i;
>     for (i = 0; i < 2; i++) {
>         fork();
>         printf("-");
>     }
>     return 0; 
> } 
> 
> ```
> 
> A. 2        B. 4        C. 6        D. 8

linux 环境下 GCC 编译后运行一共打印 8 个  
![](https://img-blog.csdnimg.cn/825d550e1a3a4feb98c2c7bbc2bdc145.png)

将 `printf("-");` 改为 `printf("-\n");` 后同环境下打印 6 个  
![](https://img-blog.csdnimg.cn/727b01f163ce4e1993b6b7f63294a107.png)

父子进程虚拟地址空间情况
------------

### 父子进程运行区别

1.  父进程执行到 `fork()` 时，创建一个子进程
2.  子进程创建完后 `fork()` 会给父进程返回子进程的 PID ，会给子进程返回 0
3.  系统会为父进程的复制资源生成一段新的虚拟地址空间供子进程使用
4.  父进程执行条件判断，子进程执行条件判断（子进程只执行 `fork()` 之后的代码）
5.  通过循环和 `sleep()` 显式体现 cpu 交替处理父子进程  
    ![](https://img-blog.csdnimg.cn/f701f5a316b64b2faaa965f1360ba116.png)

### 父子进程虚拟地址空间

扩充上一小节第 3 步。  
调用`fork()` 后，子进程的用户区数据与父进程相同但是 `fork()` 返回值不同，核区数据也会拷贝过来但是 pid 不同。  
![](https://img-blog.csdnimg.cn/0ec9530a6a2b4f5da8c937842c447995.png)

**代码示例**

```
#include <sys/types.h>
#include <unistd.h>
#include <stdio.h>

int main()
{
    int num = 10;
    // 输出num原定义值
    printf("original num: %d\n", num);

    // 输出num原地址
    printf("Address of original num: %p\n", &num);

    // 创建子进程
    pid_t pid = fork();

    // 判断是父进程还是子进程
    if (pid > 0)
    {
        // printf("pid : %d\n", pid);
        //  如果大于0，返回的是创建的子进程的进程号，当前是父进程
        printf("i am parent process, pid : %d, ppid : %d\n", getpid(), getppid());

        printf("parent num: %d\n", num);
        num += 10;
        printf("parent num += 10: %d\n", num);

        // 输出父进程中num的地址
        printf("Address of num in parent precess: %p\n", &num);
    }
    else if (pid == 0)
    {
        // 当前是子进程
        printf("i am child process, pid : %d, ppid : %d\n", getpid(), getppid());
        printf("child num: %d\n", num);
        num += 100;
        printf("child num += 100: %d\n", num);

        // 输出子进程中num的地址
        printf("Address of num in child precess: %p\n", &num);
    }

    // for (int i = 0; i < 5; i++)
    // {
    //     printf("i : %d, pid : %d\n", i, getpid());
    //     sleep(2);
    // }

    return 0;
}

```

![](https://img-blog.csdnimg.cn/3b4d0aff07144e2791255473f6c09d95.png)  
最终打印结果发现两地址进程相同，这是因为我们所理解的是虚拟内存地址，**虚拟内存地址每个进程都是共享的，而 mmu 所映射的物理内存地址是不一样的**，通过写操作会拷贝数据到新的物理内存地址。  
从操作系统来理解，每个进程有自己的页表，父进程 fork 出新的子进程时，子进程拷贝一份父进程的页表，且父子进程将页表状态修改为写保护。当父进程或子进程发生写操作时将会发生缺页异常，缺页异常处理函数将会为子进程分配新的物理地址。**由于不同的进程的页表不同，因此访问同样的逻辑地址对应的物理地址才不同**。

### 写时拷贝技术（Copy-On-Write）

> **当一个进程或线程想要修改共享数据时，会先创建该数据的副本，然后再进行修改。**  
> 原始数据保持不变，其他进程或线程仍可读取原始数据的副本。这个策略避免了多个进程同时修改数据时的竞争条件，从而提高了并发性能。

上面的`fork()`的实现就是**读时共享，写时拷贝**，当资源读取的时候内核此时并不复制整个进程的地址空间，而是让父子进程共享同一个地址空间。只有在需要写入的时候才会复制到新的地址空间，从而使各个进行拥有各自的地址空间。

STL 标准模板库中的 `string` 类，就是一个具有写时拷贝技术的类。  
通常 `string` 类中必有一个私有成员，其是一个 `char*` ，用户记录从堆上分配内存的地址，其在构造时分配内存，在析构时释放内存。  
因为是从堆上分配内存，所以 `string` 类在维护这块内存上是格外小心的，`string` 类在返回这块内存地址时，只返回 `const char*` ，也就是只读的，如果需要写，只能通过 `string` 提供的方法进行数据的改写。

注意：

1.  fork 之后父子进程共享文件，产生的子进程与父进程相同的文件文件描述符指向相同的文件表，增加 引用计数，共享 文件偏移指针。
2.  不同的 gcc 编译器对共享内存有不同的处理策略。有的环境可能直接是深拷贝，有的环境是共享内容。

父子进程关系及 GDB 多进程调试
-----------------

### 父子进程关系

**区别**

*   `fork()` 的返回值不同
    *   父进程中：>0 返回子进程的 ID
    *   子进程中：=0
*   PCB 中的一些数据
    *   当前的进程的 id：pid
    *   当前的进程的父进程的 id：ppid
    *   信号集

**共同**  
当子进程刚被创建出来，还没有执行任何的写数据的操作，以下对象父子进程共享

*   用户区的数据
*   文件描述符表

**父子进程对变量是不是共享的?**  
刚开始是共享的，一旦修改数据共享不了。读时共享，写时拷贝。

### GDB 多进程调试

工作一般不用，面试较多。

使用 GDB 调试的时候，GDB 默认只能跟踪一个进程，可以在 `fork()` 调用之前，通过指令设置 GDB 调试工具跟踪父进程或者是跟踪子进程，默认跟踪父进程。

**代码示例**

```
#include <sys/types.h>
#include <unistd.h>
#include <stdio.h>

int main(){
    printf("begin\n");
    if (fork()>0)
    {
        printf("我是父进程: pid = %d, ppid = %d\n", getpid(), getppid());
        int i;
        for(i = 0; i< 10; i++){
            printf("i = %d\n", i);
            sleep(1);
        }
    }else{
        printf("我是子进程: pid = %d, ppid = %d\n", getpid(), getppid());
        int j;
        for(j = 0; j< 10; j++){
            printf("j = %d\n", j);
            sleep(1);
        }
    }
    return 0;
}

```

进行 GDB 调试

```
# 查看源代码
l
# 设置父进程打印断点
b 9
# 设置子进程打印断点
b 16
# 运行
r

```

![](https://img-blog.csdnimg.cn/25163b29ac2b4016ba95f9c8f996be47.png)

#### 设置调试子进程或父进程

**设置调试父进程（默认）**

```
set follow-fork-mode parent

```

![](https://img-blog.csdnimg.cn/d4f0968da7b64cf7b4b7223253eb98a6.png)

**设置调试子进程**

```
set follow-fork-mode child

```

![](https://img-blog.csdnimg.cn/06dc4e553b94455e9e6861d798d809c3.png)  
进行 GDB 调试  
![](https://img-blog.csdnimg.cn/a04da54c8af54a7594ecac67c82014a0.png)

#### 设置调试模式

**调试当前进程，其他进程继续运行（默认）**

```
set detach-on-fork on

```

![](https://img-blog.csdnimg.cn/5502842a29104d4ea42156f625910fbf.png)

**调试当前进程，其他进程被 GDB 挂起**

```
set detach-on-fork off

```

![](https://img-blog.csdnimg.cn/d4e8ae1fe09145ba8ea974d57293cba8.png)  
进行 GDB 调试  
![](https://img-blog.csdnimg.cn/02776db764f74a62b76943462268a746.png)

#### 查看调试的进程

```
info inferiors

```

![](https://img-blog.csdnimg.cn/b3eba5a746f348d0a1d2f7946d653849.png)

#### 切换当前调试的进程

```
inferiors id

```

![](https://img-blog.csdnimg.cn/fbf8a00ef248410a9d8ec556dc79fff6.png)  
![](https://img-blog.csdnimg.cn/f5f54974c8f84ac987da86d2f60d71fb.png)

#### 使进程脱离 GDB 调试

```
detach inferiors id

```

![](https://img-blog.csdnimg.cn/eaf16799774b4341bfd1aff661a3ea38.png)

exec 函数族
--------

### 什么是 exec 函数族

> 在调用进程内部执行一个可执行文件。

exec 函数族的作用是根据指定的文件名找到可执行文件，并用它来取代调用进程的内容。  
exec 函数族的函数执行成功后不会返回，因为调用进程的实体，包括代码段、据段和堆栈等都已经被新的内容取代，只留下进程 ID 等一些表面上的信息仍保持原样；只有调用失败了才会返回 -1 并从原程序的调用点接着往下执行。  
调用 exec 函数族并不是新建一个进程而是只替换用户区的数据

### exec 函数族

```
#include <unistd.h>
extern char **environ;

int execl(const char *path, const char *arg, ...);
int execlp(const char *file, const char *arg, ...);
int execle(const char *path, const char *arg,..., char * const envp[]);
int execv(const char *path, char *const argv[]);
int execvp(const char *file, char *const argv[]);
int execvpe(const char *file, char *const argv[],char *const envp[]);

```

**含义区分**

*   带`l`：调用程序每个命令行参数需单独写成列表形式并以空指针结束
*   带`p`：如果函数参数 `file` 含 `/` 就视为路径名，否则按 PATH 环境变量指定的目录搜索可执行文件
*   带`v`：需先构造一个命令行参数的指针数组，然后将数组地址作为调用程序参数
*   带`e`：需先构造环境字符串指针数组，然后将数组地址传给函数使用新的环境变量代替调用进程的环境变量

**参数**  
`path`：可执行文件的路径名字  
`file` ：按 PATH 环境变量指定的目录搜索可执行文件  
`arg` ：可执行程序所带的命令行参数，第一个参数为可执行文件的名字（没什么用，一般写这个），从第二个参数开始就是程序所需参数列表，最后必须以 NULL 结束  
`argv[]` ：命令行参数的指针数组  
`envp[]` ：环境字符串指针数组

**返回值**  
执行**成功后不会返回**，因为调用进程的实体，包括代码段、据段和堆栈等都已经被新的内容取代，只留下进程 ID 等一些表面上的信息仍保持原样；只有调用**失败了才会返回 -1 并设置 erron** 从原程序的调用点接着往下执行。

**代码示例**  
hello.c

```
#include <stdio.h>

int main(){
    printf("helloworld!\n");
    return 0;
}

```

编译后为 hello 可执行文件

execl.c

```
#include <sys/types.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main()
{
    // 创建一个子进程，在子进程中执行exec函数族中的函数
    pid_t pid = fork();
    if (pid > 0)
    {
        // 父进程
        printf("i am parent process, pid : %d\n", getpid());
        sleep(1);
    }
    else if (pid == 0)
    {
        // 子进程
        // 建议绝对路径
        execl("/home/zxz/open_file_excise/exec_process/hello", "hello", NULL);
        printf("i am child process, pid : %d\n", getpid());
    }
    for (int i = 0; i < 3; i++)
    {
        printf("i = %d, pid = %d\n", i, getpid());
    }
    return 0;
}

```

![](https://img-blog.csdnimg.cn/ae211b1797184f9180483ae94adbd38e.png)

进程控制
----

### 进程退出

![](https://img-blog.csdnimg.cn/0fc1ddd8ec6b4805a7bc533be6e82097.png)  
`status`：是进程退出时的一个状态信息。父进程回收子进程资源的时候可以获取到。

**代码示例**

1.  标准 C 库函数 `exit()`

```
#include <sys/types.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main()
{
    printf("hello\n");
    printf("world");

    exit(0);
    // exit(0) 等价于 return 0，于是不再执行以下代码
    printf("byebye");

    return 0;
}

```

![](https://img-blog.csdnimg.cn/b5edb5e5f5834cc0a64fe06761654029.png)

2.  标准 Linux 系统库函数 `_exit()`

```
#include <sys/types.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main()
{
    printf("hello\n");
    printf("world");

    _exit(0);
    // exit(0) 等价于 return 0，于是不再执行以下代码
    printf("byebye");
    return 0;
}

```

![](https://img-blog.csdnimg.cn/b3bd7a271cea4ee09b1b946cd751ecb7.png)  
注意：`exit()` 在调用 `_exit()` 之前会进行刷新 I/O 缓冲，由于当 `std::endl` 或者 `\n` 被输出时，缓冲区会被刷新，所以数据会被立即显示在屏幕上，而直接调用 `_exit()` 不会进行刷新 I/O 缓冲，所以当 `std::endl` 或者 `\n` 未被输出时数据不会被显示在屏幕上。

### 孤儿进程

> 父进程运行结束，但子进程还在运行（未运行结束)，这样的子进程就称为孤儿进程 (Orphan Process) 。

**代码示例**

```
#include <sys/types.h>
#include <unistd.h>
#include <stdio.h>

int main()
{
    // 创建子进程
    pid_t pid = fork();

    // 判断是父进程还是子进程
    if (pid > 0)
    {
        //  如果大于0，返回的是创建的子进程的进程号，当前是父进程
        printf("i am parent process, pid : %d, ppid : %d\n", getpid(), getppid());
    }
    else if (pid == 0)
    {
        sleep(1);
        // 当前是子进程
        printf("i am child process, pid : %d, ppid : %d\n", getpid(), getppid());
    }

    for (int i = 0; i < 5; i++)
    {
        printf("i : %d, pid : %d\n", i, getpid());
    }

    return 0;
}

```

![](https://img-blog.csdnimg.cn/612d0e335c5c45a79786ff2d949026cc.png)  
孤儿进程没有什么危害，已领养孤儿进程的父进程（内核的 init 进程）会循环地 `wait()` 已经退出的子进程，最终会处理子进程直到其结束生命周期。

### 僵尸进程

> 每个进程结束之后，都会释放自己地址空间中的用户区数据， 内核区的 PCB 没有办法自己释放掉，需要父进程去释放。进程终止时，父进程尚未回收，子进程残留资源（PCB）存放于内核中，变成僵尸进程 (Zombie Process)。

**代码示例**

```
#include <sys/types.h>
#include <unistd.h>
#include <stdio.h>

int main()
{
    // 创建子进程
    pid_t pid = fork();

    // 判断是父进程还是子进程
    if (pid > 0)
    {
        while (1)
        {
            //  如果大于0，返回的是创建的子进程的进程号，当前是父进程
            printf("i am parent process, pid : %d, ppid : %d\n", getpid(), getppid());
            sleep(1);
        }
        
    }
    else if (pid == 0)
    {
        // 当前是子进程
        printf("i am child process, pid : %d, ppid : %d\n", getpid(), getppid());
    }

    for (int i = 0; i < 5; i++)
    {
        printf("i : %d, pid : %d\n", i, getpid());
    }

    return 0;
}

```

父进程执行完，子进程还在执行未释放内核资源（无限循环）  
![](https://img-blog.csdnimg.cn/5854dfc25a89444da4ed1d5029dc4369.png)  
新建一个终端输入 `ps aux` 查看僵尸进程  
![](https://img-blog.csdnimg.cn/b0f13e7045f047d8b7cc408f2293807b.png)  
一般调试使用 `Ctrl + C` 杀掉僵尸进程（`kill -9`杀不死）  
![](https://img-blog.csdnimg.cn/b889022e59af4c669528ea172bf9170b.png)

ps：如果父进程不调用 `wait()` 或 `waitpid()` 的话，那么保留的那段信息就不会释放，其进程号就会一直被占用，但是系统所能使用的进程号是有限的，如果大量的产生僵尸进程，将因为没有可用的进程号而导致系统不能产生新的进程，此即为僵尸进程的危害，应当避免。

### 进程回收

在每个进程退出的时候，内核释放该进程所有的资源、包括打开的文件、占用的内存等。但是仍然为其保留一定的信息，这些信息主要主要指进程控制块 PCB 的信息 (包括进程号、退出状态、运行时间等)。  
父进程可以通过调用 `wait()` 或 `waitpid()` 得到它的退出状态同时彻底清除掉这个进程。

#### wait 函数

**`pid_t wait(int *wstatus);`**

*   **作用**：等待任意一个子进程结束，如果任意一个子进程结束了，则此函数会回收子进程的资源。
*   **参数**：`wstatus`：退出时的状态信息，传入的是一个 int 类型的地址，传出参数
*   **返回值**：如果成功返回被回收的子进程的 id；如果失败返回 - 1（所有的子进程都结束，调用函数失败）

调用 `wait()` 的进程会被挂起（阻塞），直到它的一个子进程退出或者收到一个不能被忽略的信号才被唤醒（相当于继续往下执行）。如果没有子进程或子进程都结束了，会立即返回 -1 。

**代码示例**

```
#include <sys/types.h>
#include <unistd.h>
#include <stdio.h>
#include <sys/wait.h>

int main()
{
    // 有一个父进程，创建5个子进程（兄弟）
    pid_t pid;
    for (int i = 0; i < 5; i++)
    {
        pid = fork();
        if (pid == 0)
        {
            break;
        }
    }
    if (pid > 0)
    {
        // 父进程
        while (1)
        {
            printf("parent, pid = %d\n", getpid());

            int ret = wait(NULL);
            if (ret == -1)
            {
                break;
            }

            printf("child die, pid = %d\n", ret);

            sleep(1);
        }
    }
    else if (pid == 0)
    {
        // 子进程
        while (1)
        {
            printf("child, pid = %d\n", getpid());
            sleep(1);
        }
    }

    return 0;
}

```

执行代码后 ps aux 查看创建的 5 个子进程都处于阻塞状态  
![](https://img-blog.csdnimg.cn/ad5880dd77a149539696cc5c1b024e4b.png)  
选择第一个子进程杀掉

```
kill -9 84790

```

![](https://img-blog.csdnimg.cn/a0c0936e52fa416eb71ec54f326b7f61.png)

#### 退出信息相关宏函数

**退出**

*   `WIFEXITED(status)`：非 0，进程正常退出
*   `WEXITSTATUS (status)`：如果上面宏为真，获取进程退出的状态（ `exit()` 的参数）

**终止**

*   `WIFSIGNALED(status)`：非 0，进程异常终止
*   `WTERMSIG(status)`：如果上面宏为真，获取使进程终止的信号编号

**暂停**

*   `IFSTOPPED (status)`：非 0，进程处于暂停状态
*   `WSTOPSIG(status)`：如果上面宏为真，获取使进程暂停的信号的编号
*   `WIFCONTINUED (status)`：非 0，进程暂停后已经继续运行

**代码示例**

```
#include <sys/types.h>
#include <unistd.h>
#include <stdio.h>
#include <sys/wait.h>
#include <stdlib.h>

int main()
{
    // 有一个父进程，创建5个子进程（兄弟）
    pid_t pid;
    for (int i = 0; i < 5; i++)
    {
        pid = fork();
        if (pid == 0)
        {
            break;
        }
    }
    if (pid > 0)
    {
        // 父进程
        while (1)
        {
            printf("parent, pid = %d\n", getpid());

            // int ret = wait(NULL);
            int st;
            int ret = wait(&st);
            
            if (ret == -1)
            {
                break;
            }
            if (WIFEXITED(st))
            {
                // 是不是正常退出
                printf("退出的状态码:%d\n", WEXITSTATUS(st));
            }
            if (WIFSIGNALED(st))
            {
                // 是不是异常终止
                printf("被哪个信号干掉了：%d\n", WTERMSIG(st));
            }
            printf("child die, pid = %d\n", ret);
            sleep(1);
        }
    }
    else if (pid == 0)
    {
        // 子进程
        while (1)
        {
            printf("child, pid = %d\n", getpid());
            sleep(1);
        }
        exit(0);
    }

    return 0;
}

```

使用信号杀掉子进程  
![](https://img-blog.csdnimg.cn/74681f9026c44153bd1ac143ec537769.png)  
![](https://img-blog.csdnimg.cn/85755238608e413ab9025bc06096d206.png)

#### waitpid 函数

**`pid_t waitpid(pid_t pid, int *wstatus, int options);`**

*   **作用**：回收一个指定进程号的子进程，可以设置是否阻塞。
*   **参数**：
    *   `pid`：
        *   `pid > 0`：某个子进程的 pid
        *   `pid = 0` ：回收当前进程组的任意子进程
        *   `pid = -1`：回收所有的子进程，相当于 wait()
        *   `pid < -1` ：某个进程组的组 id 的绝对值，回收指定进程组中的子进程
    *   `wstatus`：退出时的状态信息，传入的是一个 int 类型的地址，传出参数
    *   `options`：设置阻塞或者非阻塞
        *   `0`：阻塞
        *   `WNOHANG` ：非阻塞
*   **返回值**：
    *   `>0`: 返回子进程的 id
    *   `=0` : `options` = `WNOHANG`，表示还有子进程活着
    *   `= -1` : 错误，或者没有子进程了

**代码示例**

```
#include <sys/types.h>
#include <unistd.h>
#include <stdio.h>
#include <sys/wait.h>
#include <stdlib.h>

int main()
{
    // 有一个父进程，创建5个子进程（兄弟）
    pid_t pid;
    for (int i = 0; i < 5; i++)
    {
        pid = fork();
        if (pid == 0)
        {
            break;
        }
    }
    if (pid > 0)
    {
        // 父进程
        while (1)
        {
            printf("parent, pid = %d\n", getpid());
            sleep(1);

            // int ret = wait(NULL);
            int st;
            // int ret = waitpid(-1, &st, 0);
            // 非阻塞，父进程不用挂起还可以执行
            int ret = waitpid(-1, &st, WNOHANG);
            if (ret == -1)
            {
                break;
            }
            if (ret == 0)
            {
                // 说明还有子进程存在
                continue;
            }
            else if (ret > 0)
            {
                if (WIFEXITED(st))
                {
                    // 是不是正常退出
                    printf("退出的状态码:%d\n", WEXITSTATUS(st));
                }
                if (WIFSIGNALED(st))
                {
                    // 是不是异常终止
                    printf("被哪个信号干掉了：%d\n", WTERMSIG(st));
                }
            }

            printf("child die, pid = %d\n", ret);
                }
    }
    else if (pid == 0)
    {
        // 子进程
        while (1)
        {
            printf("child, pid = %d\n", getpid());
            sleep(1);
        }
        exit(0);
    }

    return 0;
}

```

![](https://img-blog.csdnimg.cn/a59d1801830448a596369885bd1abc9e.png)  
使用信号杀死子进程  
![](https://img-blog.csdnimg.cn/78941ce0d516453fb9ab83362d73bbf2.png)  
![](https://img-blog.csdnimg.cn/96c0c8ec3ec24a03aec276ebffbf774c.png)

进程间通信
-----

### 什么是进程间通信

> **进程间通信（Inter-Process Communication，IPC）是指不同执行的进程之间进行数据交换和信息共享的机制**。  
> 进程是一个独立的资源分配单元，不同进程（这里所说的进程通常指的是用户进程）之间的资源是独立的，没有关联．不能在一个进程中直接访问另一个进程的资源。但是，进程不是孤立的，不同的进程需要进行信息的交互和状态的传递等，因此需要进程间通信。

**进程间通信目的**

*   **数据传输**：一个进程需要将它的数据发送给另一个进程。
*   **通知事件**：一个进程需要向另一个或一组进程发送消息，通知它 (它们) 发生了某种事件（如进程终止时要通知父进程)。
*   **资源共享**：多个进程之间共享同样的资源。为了做到这一点，需要内核提供互斥和同步机制。
*   **进程控制**：有些进程希望完全控制另一个进程的执行 (如 Debug 进程)，此时控制进程希望能够拦截另一个进程的所有陷入和异常，并能够及时知道它的状态改变。

### Linux 进程间通信的方式

![](https://img-blog.csdnimg.cn/c52857a54caf4adcb517e05adfea18e7.png)

匿名管道
----

> 管道也叫无名（匿名）管道，它是 UNIX 系统 IPC(进程间通信）的最古老形式，所有的 UNIX 系统都支持这种通信机制。 **匿名管道是一种单向通信管道，允许一个进程将数据写入管道的一端，另一个进程从管道的另一端读取数据**。

**代码示例**  
统计一个目录文件的数目，为了执行该命令 shell 创建了两个进程来分别执行 `ls` 和 `wc`

```
ls | wc -l

```

![](https://img-blog.csdnimg.cn/23f9ad2417504e1da1c4cb743acf166a.png)

### 管道的特点

*   管道其实是一个**在内核内存中维护的缓冲器**，这个缓冲器的存储能力是有限的，不同的操作系统大小不一定相同
*   管道拥有文件的特质：读操作、写操作，匿名管道没有文件实体，有名管道有文件实体，但不存储数据，可以按照操作文件的方式对管道进行操作
*   一个管道是一个字节流，使用管道时不存在消息或者消息边界的概念，从管道读取数据的进程可以读取任意大小的数据块，而不管写入进程写入管道的数据块的大小是多少
*   通过管道传递的数据是顺序的, 从管道中读取出来的字节的顺序和它们被写入管道的顺序是完全一样的
*   在管道中的数据的**传递方向是单向的**，一端用于写入，一端用于读取，**管道是半双工的**
*   从管道读数据是一次性操作，数据一旦被读走，它就从管道中被抛弃，释放空间以便写更多的数据，在管道中无法使用 `lseek()` 来随机的访问数据
*   匿名管道只能在具有公共祖先的进程（父进程与子进程，或者两个兄弟进程，具有亲缘关系）之间使用

![](https://img-blog.csdnimg.cn/54b9a6a23b8541d8bc61bff628cb24d9.png)

### 为什么可以使用管道进行进程间通信

或者说匿名管道只能在具有公共祖先的进程之间使用。  
其实管道类似于文件，管道读写端获取数据类似于文件的读写。  
![](https://img-blog.csdnimg.cn/313930a0830d4affaa50463fec540f8a.png)

### 管道的数据结构

底层为线性队列，逻辑类似循环队列，读写顺序相同。![](https://img-blog.csdnimg.cn/de58b8a778444ad080e3324bfbdfa3e7.png)

父子进程通过匿名管道通信
------------

### 创建匿名管道

**`int pipe(int pipefd[2]);`**

*   **作用**：创建一个匿名管道，用来进程间通信
*   **参数**：`int pipefd[2]`：这个数组是一个传出参数
    *   `pipefd[0]` ：对应的是管道的读端
    *   `pipefd[1]` ：对应的是管道的写端
*   **返回值**：如果成功返回 0；如果失败返回 -1

注意：匿名管道只能用于具有关系的进程之间的通信（父子进程、兄弟进程）。管道中如果没有信息时 read 操作是阻塞的，管道中如果信息已满 write 操作是阻塞，不能够同时进行读写，否则会一直阻塞。 `sleep()` 不能放在 `read()` 下面否则会造成自写自读（注释掉 `sleep()` 也会发生）。

**代码示例**  
不停读写的父子进程

```
// 子进程发送数据给父进程，父进程读取到数据输出
#include <unistd.h>
#include <sys/types.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{

    // 在fork之前创建管道
    int pipefd[2];
    int ret = pipe(pipefd);
    if (ret == -1)
    {
        perror("pipe");
        exit(0);
    }

    // 创建子进程
    pid_t pid = fork();
    if (pid > 0)
    {
        // 父进程
        printf("i am parent processe, pid = %d\n", getpid());

        char buf[1024] = {0};
        while (1)
        {
            // 从管道中读取数据
            int len = read(pipefd[0], buf, sizeof(buf));
            printf("parent recv : %s, pid : %d\n", buf, getpid());

            // 向管道中写入数据
            char *str = "hello,i am parent";
            write(pipefd[1], str, strlen(str));
            sleep(1);
        }
    }
    else if (pid == 0)
    {
        // 子进程
        printf("i am child process, pid = %d\n", getpid());

        char buf[1024] = {0};
        while (1)
        {
            // 向管道中写入数据
            char *str = "hello, i am child";
            write(pipefd[1], str, strlen(str));
            sleep(1);

            // 从管道中读取数据
            int len = read(pipefd[0], buf, sizeof(buf));
            printf("child pecv: %s, pid = %d\n", buf, getpid());
        }
    }

    return 0;
}

```

![](https://img-blog.csdnimg.cn/58fdce904bf74f50935ce494a94cec86.png)

### 管道缓冲大小

**查看大小**

```
ulimit -a

```

![](https://img-blog.csdnimg.cn/5c3671d1b4aa42f280084b5ed566a20a.png)

使用函数获取  
**`long fpathconf(int fd, int name);`**

*   **作用**：用于查询文件描述符相关属性
*   **参数**：
    *   `fd`：要查询的文件描述符
    *   `name` ：表示要查询的属性（以_PC_为前缀的常量）以下为常用属性：
        *   `_PC_LINK_MAX` ：文件的最大链接数
        *   `_PC_MAX_CANON` ：规范输入队列中的最大字节数
        *   `_PC_MAX_INPUT` ：输入队列中的最大字节数
        *   `_PC_NAME_MAX` ：文件名的最大长度
        *   `_PC_PATH_MAX` ：文件路径的最大长度
        *   `_PC_PIPE_BUF` ：管道缓冲区的最大大小
        *   `_PC_CHOWN_RESTRICTED` ：指示是否允许更改文件所有者
*   **返回值**：如果成功返回查询到的属性值（`long` 类型）；如果失败返回 -1 并设置 errno

**代码示例**

```
#include <unistd.h>
#include <stdio.h>

int main(){
    int pipefd[2];
    int ret = pipe(pipefd);

    // 获取管道的大小
    long size = fpathconf(pipefd[0],  _PC_PIPE_BUF);
    printf("pipe size : %ld\n", size);

    return 0; 
}

```

![](https://img-blog.csdnimg.cn/cdd28bc3a38140589da069390b842872.png)

**修改大小**

```
ulimit -p

```

### 匿名管道通信三种情况

![](https://img-blog.csdnimg.cn/bd66fe21f9434b17a947ab5c03e0514d.png)

### 第二种情况遇到的问题以及解决办法

**问题**  
接上一章节的代码。如果注释掉 `sleep()` 会直接转变成第一种自写自读情况：  
![](https://img-blog.csdnimg.cn/2fa9391e1aab4ad1b752aafd2d14a7b2.png)  
![](https://img-blog.csdnimg.cn/8eb774ba833f4d2ea9def9bdc2654081.png)

**解决办法**  
将代码改写成第三种情况

**代码示例**

```
// 子进程发送数据给父进程，父进程读取到数据输出
#include <unistd.h>
#include <sys/types.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{

    // 在fork之前创建管道
    int pipefd[2];
    int ret = pipe(pipefd);
    if (ret == -1)
    {
        perror("pipe");
        exit(0);
    }

    // 创建子进程
    pid_t pid = fork();
    if (pid > 0)
    {
        // 父进程
        printf("i am parent processe, pid = %d\n", getpid());

        // 关闭写端
        close(pipefd[1]);

        char buf[1024] = {0};
        while (1)
        {
            // 从管道中读取数据
            int len = read(pipefd[0], buf, sizeof(buf));
            printf("parent recv : %s, pid : %d\n", buf, getpid());
        }
    }
    else if (pid == 0)
    {
        // 子进程
        printf("i am child process, pid = %d\n", getpid());

        // 关闭读端
        close(pipefd[0]);

        char buf[1024] = {0};
        while (1)
        {
            // 向管道中写入数据
            char *str = "hello, i am child\n";
            write(pipefd[1], str, strlen(str));
        }
    }

    return 0;
}

```

![](https://img-blog.csdnimg.cn/1b6652877e6f4e71a3bcfbce4fe93203.png)

匿名管道通信案例
--------

实现 `ps aux | grep xxx` 父子进程间通信

*   子进程： ps aux，子进程结束后，将数据发送给父进程
*   父进程：获取到数据，过滤  
    `pipe()`、`execlp()`、`dup2()`（子进程将标准输出重定向到管道的写端）

```
#include <unistd.h>
#include <sys/types.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <wait.h>

int main(){
    // 创建一个管道
    int fd[2];
    int ret = pipe(fd);

    if (ret == -1)
    {
        perror("pipe");
        exit(0);
    }
    
    // 创建子进程
    pid_t pid = fork();

    if (pid > 0)
    {
        // 父进程

        // 关闭写端
        close(fd[1]);
        // 从管道中读取
        char buf[4096] = {0};
        int len = -1;
        // size-1 表示减去字符串结束符 "\0"
        while ((len = read(fd[0], buf, sizeof(buf)-1)) > 0)
        {
            // 过滤数据输出
            printf("%s", buf);
            memset(buf, 0, 4096);
        }

        // 回收子进程资源
        wait(NULL);

    }else if(pid == 0)
    {
        // 子进程

        // 关闭读端
        close(fd[0]);

        // 文件描述符的重定向 stdout_fileno -> fd[1]
        dup2(fd[1], STDOUT_FILENO);

        // 执行 ps aux
        int flag = execlp("ps", "ps", "aux", NULL);
        if (flag == -1)
        {
            perror("execlp");
            exit(0);
        }
    }else
    {
        perror("fork");
        exit(0);
    }

    return 0;
}

```

ps：暂未实现 grep 功能，后续更新。4096 其实并不是管道内存极限，而是超过 4096 的数据是会分包的也是保证其原子操作。  
如果想在终端输出真正所想的大小（< 4096），让 `len = read(fd[0], buf, sizeof(buf)-1)` 别在循环里就行。

管道读写特点和管道设置为非阻塞
---------------

### 管道读写特点

使用管道（包括匿名和有名）时，需注意以下几种特殊情况（假设都是阻塞 I/O 操作）

*   所有的指向管道写端的文件描述符都关闭了 (管道写端引用计数为 0），有进程从管道的读端读数据，那么管道中剩余的数据被读取以后，再次 read 会返回 0，就像读到文件末尾一样
*   如果有指向管道写端的文件描述符没有关闭 (管道的写端引用计数大于 0) ，而持有管道写端的进程也没有往管中写数据，这个时候有进程从管道中读取数据，那么管道中剩余的数据被读取后，再次 read 会阻塞，直到管道中有数据可以读了才读取数据并返回
*   如果所有指向管道读端的文件描述符都关闭了 (管道的读端引用计数为 0) ，这个时候有进程向管道中写数据，那么该进程会收到一个信号 SIGPIPE ，通常会导致进程异常终止
*   如果有指向管道读端的文件描述符没有关闭 (管道的读端引用计数大 0)，而持有管道读端的进程也没有从管道中读数据，这时有进程向管道中写数据，那么在管道被写满的时候再次 write 会阻塞，直到管道中有空位置才能写入数据并返回

总结：

*   读管道:
    *   管道中有数据：read 返回实际读到的字节数。
    *   管道中无数据:
        *   写端被全部关闭，read 返回 0(相当于读到文件的末尾)
        *   写端没有完全关闭，read 阻塞等待
*   写管道:
    *   管道读端全部被关闭，进程异常终止 (进程收到 SIGPIPE 信号)
    *   管道读端没有全部关闭:
        *   管道已满，write 阻塞
        *   管道没有满，write 将数据写入，并返回实际写入的字节数

### 管道设置为非阻塞

**代码示例**

```
// 子进程发送数据给父进程，父进程读取到数据输出
#include <unistd.h>
#include <sys/types.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <fcntl.h>
/*
    设置管道非阻塞
    fcntl
*/ 

int main()
{

    // 在fork之前创建管道
    int pipefd[2];
    int ret = pipe(pipefd);
    if (ret == -1)
    {
        perror("pipe");
        exit(0);
    }

    // 创建子进程
    pid_t pid = fork();
    if (pid > 0)
    {
        // 父进程
        printf("i am parent processe, pid = %d \n", getpid());

        // 关闭写端
        close(pipefd[1]);

        char buf[1024] = {0};

        // 获取原来的flag
        int flags = fcntl(pipefd[0], F_GETFL); 

        // 修改flag的值
        flags |= O_NONBLOCK;
        
        // 设置新的flag
        fcntl(pipefd[0], F_SETFL,  flags);
        
        while (1)
        {
            // 从管道中读取数据
            int len = read(pipefd[0], buf, sizeof(buf));
            printf("len=%d \n", len);
            printf("parent recv : %s , pid : %d \n", buf, getpid());
            memset(buf, 0, 1024);
            sleep(1);
        }
    }
    else if (pid == 0)
    {
        // 子进程
        printf("i am child process, pid = %d \n", getpid());

        // 关闭读端
        close(pipefd[0]);

        char buf[1024] = {0};
        while (1)
        {
            // 向管道中写入数据
            char *str = "hello, i am child \n";
            write(pipefd[1], str, strlen(str));
            sleep(3);
        }
    }

    return 0;
}


```

![](https://img-blog.csdnimg.cn/dbe3dd4801c24ac393f5b9a855d0ec68.png)

有名管道
----

> **有名管道（FIFO）又称 FIFO 文件，它提供了一个路径名与之关联，只要可以访问该路径就能够通过 FIFO 相互通信**。  
> 有名管道打开方式同打开普通文件一样，一旦打开就能在它上面使用与操作匿名管道和其他文件的系统调用一样的 I/O 系统函数了。

### 有名管道与匿名管道的区别

*   FIFO 在文件系统中作为一个特殊文件存在，但 FIFO 中的内容却存放在内存中
*   使用 FIFO 的进程退出后，EIFO 文件将继续保存在文件系统中以便以后使用
*   FIFO 有名字，不相关的进程可以通过打开有名管道进行通信

### 有名管道的使用

**命令创建**  
一旦使用 mkfifo 创建了一个 FIFO，就可以使用 `open()` 打开它，常见的文件 I/0 函数都可用于 FIFO。如: `close()` 、`read()` 、`write()` 、`unlink()` 等

```
mkfifo filename

```

**函数创建**  
**`int mkfifo(const char *pathname， mode t mode);`**

*   **作用**：创建 FIFO 文件
*   **参数**：
    *   `pathname`：管道名称的路径
    *   `mode`：文件的权限（和 `open()` 的 `mode` 是一样的）

**代码示例**

write.c

```
#include <stdio.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <string.h>
//  向管道中写数据

int main(){

    // 1. 判断文件是否存在
    int flag = access("fifo_test", F_OK);
    if (flag == -1)
    {
        printf("管道不存在！请创建管道\n");

        // 1.1 不存在则创建管道文件
        int ret = mkfifo("fifo_test", 0664);
        
        if (ret == -1)
        {
            perror("mkfifo");
            exit(0);
        }
    }

    // 2. 以只写方式打开管道
    int fifo_fd = open("fifo_test", O_WRONLY);
    if (fifo_fd == -1)
    {
        perror("open");
        exit(0);
    }

    // 3. 写数据
    for (int i = 0; i < 100; i++)
    {
        char buf[1024];
        sprintf(buf,"hello,%d\n", i);
        printf("write data：%s\n", buf);
        write(fifo_fd, buf, strlen(buf));
        sleep(1);
    }

    // 4. 关闭FIFO文件描述符
    close(fifo_fd);

    return 0;
}

```

read.c

```
#include <stdio.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <string.h>
//  从管道中读数据

int main(){
    // 1. 打开管道文件
    int fifo_fd = open("fifo_test", O_RDONLY);
    if(fifo_fd == -1){
        perror("open");
        exit(0);
    }

    // 2. 读取数据
    while (1)
    {
        char buf[1024] = {0};
        int len = read(fifo_fd, buf, sizeof(buf));
        if (len == 0)
        {
            printf("写端已断开连接...\n");
            break;
        }
        printf("recv buf：%s\n", buf);
    }
    
    // 3. 关闭文件描述符
    close(fifo_fd);

    return 0;
}

```

两个进程运行  
![](https://img-blog.csdnimg.cn/78cbde2a8dc848cb97ea653912832666.png)  
![](https://img-blog.csdnimg.cn/2185e19beb834e55b2618952d2ad6c0a.png)

注意：

*   一个为只读而打开一个管道的进程会阻塞，直到另外一个进程为只写打开管道
*   一个为只写而打开一个管道的进程会阻塞，直到另外一个进程为只读打开管道

有名管道实现简单版聊天功能
-------------

### 基本框架

![](https://img-blog.csdnimg.cn/d17296e53751403896ea73068cdc73bd.png)

### 写一读一聊天

**代码示例**  
chatA.c

```
#include <stdio.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <string.h>

int main(){
    // 1.判断有名管道是否存在
    int ret = access("fifo1", F_OK);
    if (ret == -1)
    {
        // 文件不存在
        printf("管道文件不存在，创建对应有名管道\n");
        ret = mkfifo("fifo1", 0664);
        if (ret == -1)
        {
            perror("mkfifo");
            exit(0);
        }
    }

    // 2.以只写的方式打开管道fifo1
    int w_fd = open("fifo1", O_WRONLY);
    if (w_fd == -1)
    {
        perror("open");
        exit(0);
    }
    printf("管道fifo1打开成功，等待写入...\n");

    // 3.以只读的方式打开管道fifo2
    int r_fd = open("fifo2", O_RDONLY);
    if (r_fd == -1)
    {
        perror("open");
        exit(0);
    }
    printf("管道fifo2打开成功，等待读取...\n");

    char buf[128];
    // 4.循环地写读数据
    while(1)
    {
        memset(buf, 0, 128);
        // 4.1.获取标准输入的数据
        fgets(buf, 128, stdin);
        // 4.2.写数据
        ret = write(w_fd, buf, strlen(buf));
        if (ret == -1)
        {
            perror("write");
            exit(0);
        }
        
        // 4.3.读数据
        memset(buf, 0, 128);
        ret = read(r_fd, buf, 128);
        if (ret == -1)
        {
            if (ret <= 0 )
            {
                perror("read");
                break;
            }
        }
        printf("chatB: %s\n",buf);
    }

    // 5.关闭读写文件描述符
        close(r_fd);
        close(w_fd);

    return 0;
}

```

chatB.c

```
#include <stdio.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <string.h>

int main(){
    // 1.判断有名管道是否存在
    int ret = access("fifo2", F_OK);
    if (ret == -1)
    {
        // 文件不存在
        printf("管道文件不存在，创建对应有名管道\n");
        ret = mkfifo("fifo2", 0664);
        if (ret == -1)
        {
            perror("mkfifo");
            exit(0);
        }
        
    }

    // 2.以只读的方式打开管道fifo1
    int r_fd = open("fifo1", O_RDONLY);
    if (r_fd == -1)
    {
        perror("open");
        exit(0);
    }
    printf("管道fifo1打开成功，等待读取...\n");

    // 3.以只写的方式打开管道fifo2
    int w_fd = open("fifo2", O_WRONLY);
    if (w_fd == -1)
    {
        perror("open");
        exit(0);
    }
    printf("管道fifo2打开成功，等待写入...\n");

    char buf[128];

    // 4.循环地读写数据
    while(1)
    {
        // 4.1.读数据
        memset(buf, 0, 128);
        ret = read(r_fd, buf, 128);
        if (ret == -1)
        {
            if (ret <= 0 )
            {
                perror("read");
                break;
            } 
        }
        printf("chatA: %s\n",buf);

        memset(buf, 0, 128);

        // 4.1.获取标准输入的数据
        fgets(buf, 128, stdin);

        // 4.2.写数据
        ret = write(w_fd, buf, strlen(buf));
        if (ret == -1)
        {
            perror("write");
            exit(0);
        }
    }

    // 5.关闭读写文件描述符
    close(w_fd);
    close(r_fd);
    
    return 0;
}

```

![](https://img-blog.csdnimg.cn/3e02f55d7d484ed2ac895bc4175d7190.png)  
![](https://img-blog.csdnimg.cn/c03a545746bc49dc85d04a0df5502488.png)

内存映射
----

### 什么是内存映射

> **内存映射 (Memory-mapped I/O) 是将磁盘文件的数据映射到内存，用户通过修改内存就能修改磁盘文件**。

![](https://img-blog.csdnimg.cn/e7268b6fa798471c8f9e746a7cbd0a14.png)

### 内存映射相关系统调用

**`void *mmap(void *addr, size t length, int prot, int flags, int fd, off_t offset);`**

*   **作用**：将一个文件或者设备的数据映射到内存中
    
*   **参数**：
    
    *   `addr`：NULL，由内核指定
    *   `length` ：要映射的数据的长度，这个值不能为 0。建议使用文件的长度，获取文件的长度：`stat()` 、`lseek()`
    *   `prot`：对申请的内存映射区的操作权限，要操作映射内存，必须要有读的权限（常用：`PROT_READ`、`PROT_READ | PROT_WRITE`）
        *   `PROT_EXEC`：可执行权限
        *   `PROT_READ`：读权限
        *   `PROT_WRITE`：写权限
        *   `PROT_NONE`：没有权限
    *   `flags`：
        *   `MAP_SHARED`：映射区的数据会自动和磁盘文件进行同步，**进程间通信必须要设置这个选项**
        *   `MAP_PRIVATE`：不同步，内存映射区的数据改变了，对原来的文件不会修改，会重新创建一个新的文件（copy-on-write）
    *   `fd`：需要映射的那个文件的文件描述符
        *   通过 open 得到，open 的是一个磁盘文件。
        *   注意：文件的大小不能为 0，open 指定的权限不能和`prot`有冲突  
            `prot`：`PROT_READ` 对应 open：只读 / 读写  
            `prot`：`PROT_READ | PROT_WRITE` 对应 open：读写
    *   `offset`：偏移量，一般不用。必须指定的是 4096 的整数倍，0 表示不偏移。
*   **返回值**：如果成功返回创建的内存的首地址；如果失败返回 `MAP_FAILED`（`(void*) -1` ），并设置 errno
    
    * * *
    

**`int munmap(void *addr, size t length);`**

*   **作用**：释放内存映射
*   **参数**：
    *   `addr`：要释放内存的首地址
    *   `length`：要释放的数据的长度（内存大小），这个值不能为 0。建议使用文件的长度，获取文件的长度：`stat()` 、`lseek()`
*   **返回值**：如果成功返回 0；如果失败返回 - 1，并设置 errno

### 使用内存映射实现进程间通信

**实现原理**

*   **有关系的进程间通信** (父子进程)
    *   还没有子进程的时候，通过唯一的父进程，先创建内存映射区
    *   有了内存映射区以后，创建子进程
    *   父子进程共享创建的内存映射区
*   **没有关系的进程间通信**
    *   准备一个大小不是 0 的磁盘文件
    *   `进程1`：通过磁盘文件创建内存映射区，得到一个操作这块内存的指针
    *   `进程2`：通过磁盘文件创建内存映射区，得到一个操作这块内存的指针
    *   使用内存映射区通信

注意：内存映射区通信是非阻塞的

**代码示例**  
有关系的进程间通信

```
#include <stdio.h>
#include <wait.h>
#include <sys/mman.h>
#include <sys/types.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <string.h>

int main()
{
    // 1.打开一个文件
    int fd = open("test.txt", O_RDWR);
    int size = lseek(fd, 0, SEEK_END); // 获取文件大小

    // 2.创建内存映射
    void *ptr = mmap(NULL, size, PROT_READ | PROT_WRITE, MAP_SHARED, fd, 0);
    if (ptr == MAP_FAILED)
    {
        perror("mmap");
        exit(0);
    }

    // 3.创建子进程
    pid_t pid = fork();
    if (pid > 0)
    {
        wait(NULL);
        // 父进程
        char buf[64];
        strcpy(buf, (char *)ptr);
        printf("read data : %s\n", buf);
    }
    else if (pid == 0)
    {
        // 子进程
        strcpy((char *)ptr, "nihao, this's son！！！");
    }
    else
    {
        perror("fork");
        exit(0);
    }

    // 4.释放内存映射区
    munmap(ptr, size);

    return 0;
}

```

![](https://img-blog.csdnimg.cn/7cbf45e9442d4f6eb958f7736956f684.png)

### 内存映射相关问题

**1. 如果对 `mmap()` 的返回值 `ptr` 做 ++ 操作 (`ptr++`)，`munmap()` 是否能够成功?**  
**答**：可以做 ++ 操作，但不能成功释放，必须传递首地址。

**2. 如果 `open()` 时 `O RDONLY`，`mmap()` 时 `prot` 指定 `PROT_READ | PROT_WRITE` 会怎样?**  
**答**：产生错误返回 `MAP_FAILED`，建议`open()`中权限和 `prot` 权限保持一致。

**3. 如果文件偏移量为 1000 会怎样?**  
**答**：偏移量必须是 4096 的整数倍，返回 `MAP_FAILED`

**4.`mmap()` 什么情况下会调用失败?**  
**答**：① `length` = 0；②`prot`只指定了写权限；③产生上述第二个问题

**5. 可以 `open()` 的时候 `O_CREAT` 一个新文件来创建映射区吗?**  
**答**：可以的，但创建的文件大小为 0 不行（可使用 `lseek()` 和 `truncate()` 进行扩展）。

**6.`mmap()` 后关闭文件描述符，对 `mmap()` 映射有没有影响?**  
**答**：没有影响，映射区还是存在，只是创建映射区的 `fd` 关闭了而已

**7. 对 `ptr` 越界操作会怎样?**  
**答**：越界操作操作的是非法内存，会产生段错误

### 通过内存映射实现文件拷贝功能

**思路步骤**

1.  对原始的文件进行内存映射
2.  创建一个新文件 (拓展该文件)
3.  把新文件的数据映射到内存中
4.  通过内存拷贝将第一个文件的内存数据拷贝到新的文件内存中
5.  释放资源

**代码示例**

```
#include <stdio.h>
#include <wait.h>
#include <sys/mman.h>
#include <sys/types.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <string.h>


int main(){
    // 1.对原始的文件进行内存映射
    int fd = open("english.txt", O_RDWR);
    if (fd == -1)
    {
        perror("open");
        exit(0);
    }

    // 获取源文件大小
    int len = lseek(fd, 0, SEEK_END);

    // 2.创建一个新文件(拓展该文件)
    int fd1 = open("cpy.txt", O_RDWR | O_CREAT, 0644);
    if (fd1 == -1)
    {
        perror("open");
        exit(0);
    }

    // 对新建文件进行拓展
    truncate("cpy.txt", len);
    write(fd1, " ", 1);

    // 3.把新文件的数据映射到内存中
    void *ptr = mmap(NULL, len, PROT_READ | PROT_WRITE, MAP_SHARED, fd, 0); 
    void *ptr1 = mmap(NULL, len, PROT_READ | PROT_WRITE, MAP_SHARED, fd1, 0);   
    
    if(ptr == MAP_FAILED)
    {
        perror("mmap");
        exit(0);
    }
    if(ptr1 == MAP_FAILED)
    {
        perror("mmap");
        exit(0);
    }

    //内存拷贝
    memcpy(ptr1, ptr, len);

    // 释放资源（谁先打开先释放）
    munmap(ptr1, len);
    munmap(ptr, len);

    // 关闭文件描述符
    close(fd1);
    close(fd);

    return 0;
}

```

注意：一般来讲这样不便拷贝太大文件，防止内存不够

### 匿名映射

> **不需要文件实体进程一个内存映射**。  
> 可以做有关系进程（父子进程）映射。

**代码示例**

```
#define _DEFAULT_SOURCE // MAP_ANONYMOUS

#include <stdio.h>
#include <wait.h>
#include <sys/mman.h>
#include <sys/types.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <string.h>

#define BUF_LEN 4096

int main()
{

    // 1.创建匿名映射区
    void *ptr = mmap(NULL, BUF_LEN, PROT_READ | PROT_WRITE, MAP_SHARED | MAP_ANONYMOUS, -1, 0);
    if (ptr == MAP_FAILED)
    {
        perror("mmap");
        exit(0);
    }

    // 2.父子间通信
    pid_t pid = fork();

    if (pid > 0)
    {
        // 父进程
        strcpy((char *)ptr, "hello, world");
        wait(NULL);
    }
    else if (pid == 0)
    {
        // 子进程
        sleep(1);
        printf("%s\n", (char *)ptr);
    }

    // 3.释放内存映射区
    int ret = munmap(ptr, BUF_LEN);
    if (ret == -1)
    {
        perror("munmap");
        exit(0);
    }

    return 0;
}

```

![](https://img-blog.csdnimg.cn/f7ebfdd173424439881969971a3479c7.png)

信号
--

### 什么是信号

> **信号是 Linux 进程间通信是事件发生时对进程的通知机制，有时也称之为软件中断**。  
> 信号是在软件层次上对中断机制的一种模拟，是一种异步通信的方式。  
> 信号可以导致一个正在运行的进程被另一个正在运行的异步进程中断，转而处理某一个突发事件。

**发往进程的诸多信号，通常都是源于内核**。引发内核为进程产生信号的各类事件如下：

*   对于前台进程，用户可以通过输入特殊的终端字符来给它发送信号。比如输入 ctrl+C 通常会给进程发送一个中断信号比如输入`Ctrl+C`通常会给进程发送一个中断信号。  
    
*   硬件发生异常，即硬件检测到一个错误条件并通知内核，随即再由内核发送相应信号给相关进程。比如执行一条异常的机器语言指令，诸如被 0 除，或者引用了无法访问的内存区域。  
    
*   系统状态变化。比如 `alarm()` 定时器到期将引起 `SIGALRM` 信号，进程执行的 CPU 时间超限，或者该进程的某个子进程退出。  
    
*   运行 kill 命令或调用 `kill()`
    
    * * *
    

**使用信号的两个目的**

*   让进程知道已经发生了一个特定的事情
    
*   强迫进程执行它自己代码中的信号处理程序
    
    * * *
    

**信号的特点**

*   简单
    
*   不能携带大量信息
    
*   满足某个特定条件才发送
    
*   优先级比较高
    
    * * *
    

**查看系统定义的信号列表**

```
kill -l

```

ps：前 31 个信号为常规信号，其余为实时信号

### Linux 信号一览表

<table><thead><tr><th>编号</th><th>信号名称</th><th>对应事件</th><th>默认动作</th></tr></thead><tbody><tr><td>1</td><td>SIGHUP</td><td>用户退出 shell 时由该 shell 启动的所有进程将收到这个信号</td><td>终止进程</td></tr><tr><td>2</td><td>SIGINT<br></td><td>当用户按下了 <code>Ctrl+C</code> 组合键时，用户终端向正在运行中的由该终端启动的程序发出此信号</td><td>终止进程</td></tr><tr><td>3</td><td>SIGQUIT<br></td><td>用户按下 <code>Ctrl+\</code> 组合键时产生该信号，用户终端向正在运行中的由该终端启动的程序发出些信号</td><td>终止进程</td></tr><tr><td>4</td><td>SIGIIL</td><td>CPU 检测到某进程执行了非法指令</td><td>终止进程并产生 core 文件</td></tr><tr><td>5</td><td>SIGTRAP</td><td>该信号由断点指令或其他 trap 指令产生</td><td>终止进程并产生 core 文件</td></tr><tr><td>6</td><td>SIGABRT</td><td>调用 <code>abort()</code> 时产生该信号</td><td>终止进程并产生 core 文件</td></tr><tr><td>7</td><td>SIGBUS</td><td>非法访问内存地址，包括内存对齐出错</td><td>终止进程并产生 core 文件</td></tr><tr><td>8</td><td>SIGFPE</td><td>在发生致命的运算错误时发出。不仅包括浮点运算错误，还包括溢出及除数为 0 等所有的算法错误</td><td>终止进程并产生 core 文件</td></tr><tr><td>9</td><td>SIGKILL<br></td><td>无条件终止进程。该信号不能被忽略，处理和阻塞</td><td>终止进程，可以杀死任何正常进程（僵尸进程等异常进程不算）</td></tr><tr><td>10</td><td>SIGUSE1</td><td>用户定义的信号。即程序员可以在程序中定义并使用该信号</td><td>终止进程</td></tr><tr><td>11</td><td>SIGSEGV<br></td><td>指示进程进行了无效内存访问 (段错误)</td><td>终止进程并产生 core 文件</td></tr><tr><td>12</td><td>SIGUSR2</td><td>另外一个用户自定义信号，程序员可以在程序中定义并使用该信号</td><td>终止进程</td></tr><tr><td>13</td><td>SIGPIPE<br></td><td>Broken pipe 向一个没有读端的管道写数据</td><td>终止进程</td></tr><tr><td>14</td><td>SIGALRM</td><td>定时器超时，超时的时间 由系统调用 <code>alarm()</code> 设置</td><td>终止进程</td></tr><tr><td>15</td><td>SIGTERM</td><td>程序结束信号，与 SIGKILL 不同的是，该信号可以被阻塞和终止。通常用来要示程序正常退出。执行 shell 命令 Kill 时，缺省产生这个信号</td><td>终止进程</td></tr><tr><td>16</td><td>SIGSTKFLT</td><td>Linux 早期版本出现的信号，现仍保留向后兼容</td><td>终止进程</td></tr><tr><td>17</td><td>SIGCHLD<br></td><td>子进程结束时，父进程会收到这个信号</td><td>忽略这个信号</td></tr><tr><td>18</td><td>SIGCONT<br></td><td>如果进程已停止，则使其继续运行</td><td>继续 / 忽略</td></tr><tr><td>19</td><td>SIGSTOP<br></td><td>停止进程的执行。信号不能被忽略，处理和阻塞</td><td>为终止进程</td></tr><tr><td>20</td><td>SIGTSTP</td><td>停止终端交互进程的运行。按下 &lt;ctrl+z&gt; 组合键时发出这个信号</td><td>暂停进程</td></tr><tr><td>21</td><td>SIGTTIN</td><td>后台进程读终端控制台</td><td>暂停进程</td></tr><tr><td>22</td><td>SIGTTOU</td><td>该信号类似于 SIGTTIN，在后台进程要向终端输出数据时发生</td><td>暂停进程</td></tr><tr><td>23</td><td>SIGURG</td><td>套接字上有紧急数据时，向当前正在运行的进程发出些信号，报告有紧急数据到达。如网络带外数据到达</td><td>忽略该信号</td></tr><tr><td>24</td><td>SIGXCPU</td><td>进程执行时间超过了分配给该进程的 CPU 时间，系统产生该信号并发送给该进程</td><td>终止进程</td></tr><tr><td>25</td><td>SIGXFSZ</td><td>超过文件的最大长度设置</td><td>终止进程</td></tr><tr><td>26</td><td>SIGVTALRM</td><td>虚拟时钊超时时产生该信号。类似于 SIGALRM，但是该信号只计算该进程占用 CPU 的使用时间</td><td>终止进程</td></tr><tr><td>27</td><td>SGIPROF</td><td>类似于 SIGVTALRM，它不公包括该进程占用 CPU 时间还包括执行系统调用时间</td><td>终止进程</td></tr><tr><td>28</td><td>SIGWINCH</td><td>窗口变化大小时发出</td><td>忽略该信号</td></tr><tr><td>29</td><td>SIGIO</td><td>此信号向进程指示发出了一个异步 IO 事件</td><td>忽略该信号</td></tr><tr><td>30</td><td>SIGPWR</td><td>关机</td><td>忽略这个信号</td></tr><tr><td>31</td><td>SIGSYS</td><td>无效的系统调用</td><td>终止进程并产生 core 文件</td></tr><tr><td>34<br>~<br>64</td><td>SIGRTMIN<br>~<br>SIGRTMAX</td><td>LINUX 的实时信号，它们没有固定的含义 (可以由用户自定义)</td><td>终止进程</td></tr></tbody></table>

ps：标红色的信号需要掌握。**SIGKILL 和 SIGSTOP 信号不能被捕捉、阻塞或者忽略，只能执行默认动作**。

### 信号的 5 种默认处理动作

**查看信号的详细信息**

```
man 7 signal

```

**信号的 5 中默认处理动作**

*   **Term**：终止进程
*   **Ign**：当前进程忽略掉这个信号
*   **Core**：终止进程，并生成一个 core 文件
*   **Stop**：暂停当前进程
*   **Cont**：继续执行当前被暂停的进程

ps：  
Core 文件保存进程异常退出的信息

```
#include <stdio.h>
#include <string.h>
int main() (
	// 没有指向合法内存
	char * buf;
	strcpy(buf,"hello");
	return 0;

```

编译生成目标文件报段错误

```
gcc core.c
./a.out

```

![](https://img-blog.csdnimg.cn/cf2d7253816c4611aaa6649b6272324e.png)  
生成 Core 文件

```
ulimit -a
ulimit -c 1024
./a.out

```

![](https://img-blog.csdnimg.cn/51cb4847849d41c6a5541c03b1790767.png)  
![](https://img-blog.csdnimg.cn/1aa78798202f42dda4d3f864f3ed81db.png)  
![](https://img-blog.csdnimg.cn/567220c271e34c379e18ae0ddcc7f7ce.png)  
调试 Core 文件

```
gdb a.out
# 进入GDB调试界面
(gdb) core-file core

```

![](https://img-blog.csdnimg.cn/7ac74453e6614de9b0e11b0963a937e6.png)  
![](https://img-blog.csdnimg.cn/fbeea8091c50487d975845c351a40a8c.png)

**信号的几种状态**

*   产生
*   未决
*   递达

kill、raise、abort 函数
-------------------

**`int kill(pid t pid, int sig);`**

*   **作用**：给任何的进程或者进程组 pid，发送任何的信号 `sig`
    
*   **参数**：
    
    *   `pid`：
        *   `> 0`：将信号发送给指定的进程
        *   `= 0`：将信号发送给当前的进程组
        *   `= -1`：将信号发送给每一个有权限接收这个信号的进程
        *   `<-1`：这个 pid = 某个进程组的 ID 取反 (如：-12345)
    *   `sig` : 需要发送的信号的编号或者是宏值，0 表示不发送任何信号
*   **返回值**：如果成功返回 0；如果失败返回 - 1，并设置 errno
    
    * * *
    

**`int raise(int sig);`**

*   **作用**：给当前进程发送信号
    
*   **参数**： `sig` : 需要发送的信号的编号或者是宏值，0 表示不发送任何信号
    
*   **返回值**：如果成功返回 0；如果失败返回 - 1，并设置 errno
    
    * * *
    

**`void abort(void);`**

*   **作用**：发送 SIGABRT 信号给当前的进程，杀死当前进程

**代码示例**

```
#include <stdio.h>
#include <sys/types.h>
#include <signal.h>
#include <unistd.h>
int main(){

    pid_t pid = fork();

    if (pid == 0)
    {
        //子进程
        for (int i = 0; i < 5; i++)
        {
            printf("child process\n");
            sleep(1);
        }
    }else if (pid > 0)
        {
            // 父进程
            printf("parent process\n");
            sleep(2);
            printf("kill child process now\n");
            kill(pid, SIGINT);
        }
    

    return 0;
}

```

![](https://img-blog.csdnimg.cn/30ed3a0ada524b75962ace607c60d5ee.png)

alarm 函数
--------

**`unsigned int alarm(unsigned int seconds);`**

*   **作用**：设置定时器 (闹钟) 。函数调用，开始倒计时，当倒计时为 8 的时候函数会给当前的进程发送一个信号: SIGALARM
*   **参数**：`seconds`：倒计时的时长，单位: 秒。如果参数为 0，定时器无效 (不进行倒计时，不发信号)，如取消一个定时器：`alam(0)`
*   **返回值**：如果之前没有计时器，返回 0；如果之前有计时器返回之前计时器剩余的时间

**SIGALARM** : 默认终止当前的进程，每一个进程都有且只有唯一的一个定时器。  
**例子**

```
alarm(10); //-> 返回0
//过了1秒
alarm(5); //-> 返回9

alam(100); //该函数不阻塞

```

**代码示例**

```
#include <stdio.h>
#include <unistd.h>
int main() {
    int seconds = alarm(5);
    printf("seconds = %d\n", seconds); // 0

    sleep(2);
    seconds = alarm(2); //不阻塞
    printf("seconds = %d\n", seconds);// 3
    //while(1){}第一个例子

	alarm(0);
    
    // 1s电脑能数多少数//第二个例子
    alarm(1);
    int i = 0;
    while (1)
    {
        printf("%i\n", i++);
    }

    return 0;
}

```

![](https://img-blog.csdnimg.cn/0536e05e04ce4954aa29850df04209ed.png)  
![](https://img-blog.csdnimg.cn/285767c25e514f24b492d697c9d2c02d.png)  
![](https://img-blog.csdnimg.cn/81eec59b22c84b8ea536078b144f0088.png)

ps：其实 1s 内计算机真实计数远远大于 2.txt 中的数。**实际的时间 = 内核时间 + 用户时间 + 消耗的时间**。进行文件 IO 操作的时候比较浪费时间。定时器与进程的状态无关（自然定时法），无论进程处于什么状态，`alarm()` 都会计时。

setitimer 定时器函数
---------------

**`int setitimer(int which, const struct itimerval *new_ value, struct itimerval *old value);`**

*   **作用**：设置定时器 (闹钟)。可以替代`alarm()` ，精度微秒：us，可以实现周期性定时
*   **参数**：
    *   `which`：定时器以什么时间计时
        *   `ITIMER_REAL`：真实时间，时间到达，发送 SIGALRM（常用）
        *   `ITIMER_VIRTUAL`：用户时间，时间到达，发送 SIGVTALRM
        *   `ITIMER_PROF`：以该进程在用户态和内核态下所消耗的时间来计算，时间到达，发送
    *   `new_value`：设置定时器的属性
    *   `old_value`：记录上一次定时器的时间参数，一般不用，指定 NULL
*   **返回值**：如果成功返回 0；如果失败返回 - 1，并设置 errno

```
// 定时器的结构体
struct itimerval {
	// 每个阶段的时间，间隔时间
	struct timeval it interval;
	
	// 延迟多长时间执行定时器
	struct timeval it_value;
};

// 时间的结构体
struct timeval {
	// 秒数
	time_ttv_sec;
	
	// 微秒
	suseconds t tv_usec;
};

```

**代码示例**  
过 3 秒以后，每隔 2 秒钟定时一次

```
#include <sys/time.h>
#include <stdio.h>
#include <stdlib.h>

int main(){

    struct itimerval new_value;

    // 设置间隔的时间
    new_value.it_interval.tv_sec = 2;
    new_value.it_interval.tv_usec = 0;

    // 设置延迟的时间，3秒后开始第一次定时
    new_value.it_value.tv_sec = 3;
    new_value.it_value .tv_usec = 0;
    int ret =setitimer(ITIMER_REAL, &new_value, NULL);// 非阻塞
    printf("定时器开始了...\n");
    if(ret == -1)
    {
        perror("setitimer");
        exit(0);    
    }

    getchar();
    return 0;
}


```

![](https://img-blog.csdnimg.cn/52deb5b496b246ed855b6a32ef087c94.png)

signal 信号捕捉函数
-------------

**`sighandler_t signal(int signum, sighandler_t handler);`**

*   **作用**：设置某个信号的捕捉行为
*   **参数**：
    *   `signum`：要捕捉的信号
    *   `handler`：捕捉到信号要如何处理
        *   `SIG_IGN`：忽略信号
        *   `SIG_DFL`：使用信号默认的行为
        *   回调函数：这个函数是内核调用，程序员只负责写，捕捉到信号后如何去处理信号
*   **返回值**：如果成功返回上一次注册的信号处理函数的地址，第一次调用返回 NULL；如果失败返回`SIG_ERR`，设置 errno

ps：SIGKILL、SIGSTOP 不能被捕捉，不能被忽略。  
回调函数需要程序员实现，提前准备好的，函数的类型根据实际需求，看函数指针的定义，不是程序员调用，而是当信号产生，由内核调用。函数指针是实现回调的函数实现之后，将函数名放到函数指针的位置就可以了。

**代码示例**

```
#include <sys/time.h>
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>

void myalarm(int num)
{
    printf("捕捉到了信号的编号是: %d\n", num);
    printf("xxxxxxx\n");
}

int main(){

    // 注册信号捕捉
    // signal(SIGALRM，SIG_IGN);
    // signa1(SIGALRM，SIG_DFL);
    // void (*sighandler_t)(int); 函数指针，int 类型的参数表示信号捕捉到的值

    __sighandler_t flag = signal(SIGALRM, myalarm);
    if (flag == SIG_ERR)
    {
        perror("signal");
        exit(0);
    }
    

    struct itimerval new_value;

    // 设置间隔的时间
    new_value.it_interval.tv_sec = 2;
    new_value.it_interval.tv_usec = 0;

    // 设置延迟的时间
    new_value.it_value.tv_sec = 3;
    new_value.it_value .tv_usec = 0;
    int ret =setitimer(ITIMER_REAL, &new_value, NULL);// 非阻塞
    printf("定时器开始了...\n");
    if(ret == -1)
    {
        perror("setitimer");
        exit(0);    
    }

    getchar();
    return 0;
}


```

![](https://img-blog.csdnimg.cn/ce1742d11b064eb28cc09d1a02b90d54.png)

信号集及相关函数
--------

### 什么是信号集

> 许多信号相关的系统调用都需要能表示一组不同的信号，**多个信号可使用一个称之为信号集的数据结构来表示**，其系统数据类型为 `sigset_t`。  
> 在 PCB 中有两个非常重要的信号集。一个称之为 “**阻塞信号集**”，另一个称之为 “**未决信号集**”。这两个信号集都是内核使用位图机制来实现的。但操作系统不允许我们直接对这两个信号集进行位操作。而需自定义另外一个集合，借助信号集操作函数来对 PCB 中的这两个信号集进行修改

### 阻塞信号集和未决信号集

> **信号的 “未决” 是一种状态，指的是从信号的产生到信号被处理前的这一段时间**。

> **信号的 “阻塞” 是一个开关动作，指的是阻止信号被处理，但不是阻止信号产生**。  
> 信号的阻塞就是让系统暂时保留信号留待以后发送。由于另外有办法让系统忽略信号所以一般情况下信号的阻塞只是暂时的，只是为了防止信号打断敏感的操作。

**工作原理**  
![](https://img-blog.csdnimg.cn/b5e651a290a34e2695d577e6a05dc4cc.png)

1.  用户通过键盘 ctrl + C，产生 2 号信号 SIGINT (信号被创建)
    
2.  信号产生但是没有被处理 (未决)
    
    *   在内核中将所有的没有被处理的信号存储在一个集合中 (未决信号集)
    *   SIGINT 信号状态被存储在第二个标志位上
        *   这个标志位的值为 0，说明信号不是未决状态
        *   这个标志位的值为 1，说明信号处于未决状态
3.  这个未决状态的信号，需要被处理，处理之前需要和另一个信号集（阻塞信号集），进行比较
    
    *   阻塞信号集默认不阻塞任何的信号
    *   如果想要阻塞某些信号需要用户调用系统的 API
4.  在处理的时候和阻塞信号集中的标志位进行查询，看是不是对该信号设置阻塞了
    
    *   如果没有阻塞，这个信号就被处理
    *   如果阻塞了，这个信号就继续处于未决状态，直到阻塞解除，这个信号就被处理

### 信号集相关函数

**`int sigemptyset(sigset_t *set);`**

*   **作用**：清空信号集中的数据, 将信号集中的所有的标志位置为 0
    
*   **参数**：`set`：传出参数，需要操作的信号集
    
*   **返回值**：成功返回 0，失败返回 - 1
    
    * * *
    

**`int sigfillset(sigset t *set);int sigaddset(sigset_t *set, int signum);`**

*   **作用**：将信号集中所有的标志位设为 1
    
*   **参数**：
    
    *   `set`：传出参数，需要操作的信号集
    *   `signum`: 需要设置阻塞的那个信号
*   **返回值**：成功返回 0，失败返回 - 1
    
    * * *
    

**`int sigaddset(sigset_t *set, int signum);`**

*   **作用**：设置信号集中的某一个信号对应的标志位为 1，表示阻塞这个信号
    
*   **参数**：
    
    *   `set`：传出参数，需要操作的信号集
    *   `signum`: 需要设置阻塞的那个信号
*   **返回值**：成功返回 0；失败返回 - 1
    
    * * *
    

**`int sigdelset(sigset t *set, int signum);`**

*   **作用**：设置信号集中的某一个信号对应的标志位为 0，表示不阻塞这个信号
    
*   **参数**： `set`：传出参数，需要操作的信号集
    
*   **返回值**：成功返回 0；失败返回 - 1
    
    * * *
    

**`int sigismember(const sigset_t *set, int signum);`**

*   **作用**：判断某个信号是否阻塞
    
*   **参数**：
    
    *   `set`：需要操作的信号集
    *   `signum`: 需要判断的那个信号
*   **返回值**：如果成功返回 1 表示 `signum`被阻塞，返回 0 表示`signum`不阻塞；如果失败返回 - 1
    
    * * *
    

**代码示例**

```
#define _DEFAULT_SOURCE
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>

int main(){

    // 创建一个信号集
    sigset_t set;

    // 清空信号集的内容
    sigemptyset(&set);

    // 判断 SIGINT 是否在信号集 set 里
    int ret = sigismember(&set, SIGINT);
    if (ret == 0)
    {
        printf("SIGINT 不阻塞\n");
    }else if (ret == 1)
    {
        printf("SIGINT 阻塞\n");
    }
    
    // 添加几个信号到信号集中
    sigaddset(&set, SIGINT);
    sigaddset(&set, SIGQUIT);

    // 判断SIGINT是否在信号集中
    ret = sigismember(&set, SIGINT);
    if(ret == 0) {
        printf("SIGINT 不阻塞\n");
    } else if(ret == 1) {
        printf("SIGINT 阻塞\n");
    }

    // 判断SIGQUIT是否在信号集中
    int jug = sigismember(&set, SIGQUIT);
    if(jug == 0){
        printf("SIGQUIT 不阻塞\n");
    } else if(ret == 1){
        printf("SIGQUIT 阻塞\n");
    }

    // 从信号集中删除一个信号
    sigdelset(&set, SIGQUIT);

    // 判断SIGQUIT是否在信号集中
    jug = sigismember(&set, SIGQUIT);
    if(jug == 0){
        printf("SIGQUIT 不阻塞\n");
    } else if(ret == 1){
        printf("SIGQUIT 阻塞\n");
    }


    return 0;
}

```

![](https://img-blog.csdnimg.cn/1a47acae42b94a498bf84d380129f726.png)

sigprocmask 函数使用
----------------

**`int sigprocmask(int how,const sigset_t *set, sigset_t *oldset);`**

*   **作用**：将自定义信号集中的数据设置到内核中（设置阻塞，解除阻塞，替换）
    
*   **参数**：
    
    *   `how`：如何对内核阻塞信号集进行处理
        *   `SIG_BLOCK`：将用户设置的阻塞信号集添加到内核中，内核中原来的数据  
            假设内核中默认的阻塞信号集是`mask`， `mask | set`
        *   `SIG_UNBLOCK`：根据用户设置的数据，对内核中的数据进行解除阻塞  
            `mask &= ~set`  
            `SIG_SETMASK`：覆盖内核中原来的值
    *   `set`：已经初始化好的用户自定义的信号集
    *   `oldset`：保存设置之前的内核中的阻塞信号集的状态，可以是 NULL
*   **返回值**：如果成功返回 0；如果失败返回 - 1，并设置错误号`EFAULT`、`EINVAL`
    
    * * *
    

**`int sigpending(sigset_t *set);`**

*   **作用**：获取内核中的未决信号集
    
*   **参数**：`set`：传出参数，保存的是内核中的未决信号集中的信息。
    
*   **返回值**：如果成功返回 0；如果失败返回 - 1，并设置 errno
    
    * * *
    

**代码示例**  
编写一个程序，把所有的常规信号（1-31）的未决状态打印到屏幕设置某些信号是阻塞的，通过键盘产生这些信号

```
#define _DEFAULT_SOURCE
#include <stdio.h>
#include <signal.h>
#include <stdlib.h>
#include <unistd.h>

int main()
{
    // 设置2、3号信号阻塞
    sigset_t set;
    sigemptyset(&set);

    // 将2号和3号信号添加到信号集中
    sigaddset(&set, SIGINT);
    sigaddset(&set, SIGQUIT);

    // 修改内核中的阻塞信号集
    sigprocmask(SIG_BLOCK, &set, NULL);

    int num = 0;
    while (1)
    {
        num++;
        // 获取当前的未决信号集的数据
        sigset_t pendingset;
        sigemptyset(&pendingset);
        sigpending(&pendingset);

        // 遍历前32位
        for (int i = 1; i <= 32; i++)
        {
            if (sigismember(&pendingset, i) == 1)
            {
                printf("1");
            }
            else if (sigismember(&pendingset, i) == 0)
            {
                printf("0");
            }
            else
            {
                perror("sigismember");
                exit(0);
            }
        }
        printf("\n");
        sleep(1);
        if (num == 10)
        {
            // 解除阻塞
            sigprocmask(SIG_UNBLOCK, &set, NULL);
        }
    }

    return 0;
}

```

![](https://img-blog.csdnimg.cn/cdf7768c57cb4154b17bc50fb781d6b8.png)

sigaction 信号捕捉函数
----------------

**`int sigaction(int signum, const struct sigaction *act, struct sigaction *oldact);`**

*   **作用**：检查或者改变信号的处理。信号捕捉
    
*   **参数**：
    
    *   `signum`：需要捕捉的信号的编号或者宏值（信号的名称)
    *   `act`：捕捉到信号之后的处理动作
    *   `oldact`：上一次对信号捕捉相关的设置，一般不使用，传递 NULL
*   **返回值**：如果成功返回 0；如果失败返回 - 1，并设置 errno
    
    * * *
    

**sigaction 结构体**

```
struct sigaction {
	//函数指针，指向的函数就是信号捕捉到之后的处理函数
	void (*sa_handler)(int);
	
	//不常用
	void (*sa_sigaction)(int, siginfo_t*, void *);
	
	//临时阻塞信号集，在信号捕捉函数执行过程中，临时阻塞某些信号。
	sigset_t sa_mask;
	
	//使用哪一个信号处理对捕捉到的信号进行处理
	
	//这个值可以是0，表示使用sa_handler，也可以是SA_SIGINFO表示sa_sigaction
	int sa_flags;
	// 已废弃
	void (*sa_restorer)(void);


```

**代码示例**

```
#define _DEFAULT_SOURCE
#include <sys/time.h>
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>

void myalarm(int num)
{
    printf("捕捉到了信号的编号是: %d\n", num);
    printf("xxxxxxx\n");
}

int main(){

    // 注册信号捕捉
    struct sigaction act;
    act.sa_flags = 0;
    act.sa_handler = myalarm;
    // 清空临时阻塞信号集
    sigemptyset(&act.sa_mask);

    sigaction(SIGALRM, &act, NULL);


    __sighandler_t flag = signal(SIGALRM, myalarm);
    if (flag == SIG_ERR)
    {
        perror("signal");
        exit(0);
    }
    

    struct itimerval new_value;

    // 设置间隔的时间
    new_value.it_interval.tv_sec = 2;
    new_value.it_interval.tv_usec = 0;

    // 设置延迟的时间
    new_value.it_value.tv_sec = 3;
    new_value.it_value .tv_usec = 0;
    int ret =setitimer(ITIMER_REAL, &new_value, NULL);// 非阻塞
    printf("定时器开始了...\n");
    if(ret == -1)
    {
        perror("setitimer");
        exit(0);    
    }

    getchar();
    return 0;
}


```

![](https://img-blog.csdnimg.cn/abe459ae7fd3436d908cbe1cf764d403.png)

### 内核实现信号捕捉的过程

![](https://img-blog.csdnimg.cn/e64fec1491d241a4a727f0ffe64cc0ca.png)

SIGCHLD 信号
----------

**SIGCHLD 信号产生的条件**

*   子进程终止时
*   子进程接收到 SIGSTOP 信号暂停时
*   子进程处在停止态，接受到 SIGCONT 后唤醒时（继续运行）

ps：以上三种条件都会给父进程发送 SIGCHLD 信号，父进程默认会忽略该信号。可以使用 SIGCHLD 信号解决僵尸进程的问题。

**代码示例**

```
#define _DEFAULT_SOURCE
#include <stdio.h> 
#include <unistd.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <signal.h>
#include <sys/wait.h>

void myFun(int num)
{
    printf("捕捉到的信号:%d\n", num); // 回收子进程PCB的资源
    // while(1) {
    // wait(NULL);
    // }
    while (1)
    {
        int ret = waitpid(-1, NULL, WNOHANG);
        if (ret > 0)
        {
            printf("child die , pid = %d\n", ret);
        }
        else if (ret == 0)
        {
            // 说明还有子进程或者
            break;
        }else if (ret == -1)
        {
            break;
        }
        
    }
}

int main() {

    // 提前设置好阻塞信号集，阻塞SIGCHLD，因为有可能子进程很快结束，父进程还没有注册完信号符
    sigset_t set;
    sigemptyset(&set);
    sigaddset(&set, SIGCHLD);
    sigprocmask(SIG_BLOCK, &set, NULL);

    //创建一些子进程
    pid_t pid;
    for(int i = 0; i < 20; i++) {
        pid = fork();
        if(pid == 0) {
            break;
        }
    }

    if(pid > 0) {
        //父进程

        //捕捉子进程死亡时发送的SIGCHLD信号
        struct sigaction act;
        act.sa_flags = 0;
        act.sa_handler = myFun;
        sigemptyset(&act.sa_mask);
        sigaction(SIGCHLD, &act, NULL);

        //注册完信号捕捉以后，解除阻塞
        sigprocmask(SIG_UNBLOCK, &set, NULL);

        while(1){
            printf("parent process pid : %d\n", getpid());
            sleep(2);
        }
    }
    else if(pid == 0){
        //子进程
        printf("child process pid : %d\n", getpid());
    }
	return 0;
}

```

![](https://img-blog.csdnimg.cn/704bb4a54da745ae9506f8d268217e26.png)

共享内存
----

### 什么是共享内存

> **共享内存是一种用于多进程或多线程之间共享数据的机制**，它允许不同的进程或线程在物理内存创建一个共享区域（段）。  
> 由于一个共享内存段会称为一个进程用户空间的一部分，因此这种 IPC 机制无需内核介入。所有需要做的就是让一个进程将数据复制进共享内存中，并且这部分数据会对其他所有共享同一个段的进程可用。  
> 与管道等要求发送进程将数据从用户空间的缓冲区复制进内核内存和接收进程将数据从内核内存复制进用户空间的缓冲区的做法相比，这种 IPC 技术的速度更快。

### 共享内存使用步骤

1.  **调用 `shmget()` 创建一个新共享内存段或取得一个既有共享内存段的标识符**（即由其他进程创建的共享内存段)。这个调用将返回后续调用中需要用到的共享内存标识符。
2.  **使用 `shmat()` 来附上共享内存段**，即使该段成为调用进程的虚拟内存的一部分。
3.  此刻在程序中可以像对待其他可用内存那样对待这个共享内存段。**为引用这块共享内存程序需要使用由 `shmat()` 调用返回的 `addr` 值**，它是一个指向进程的虚拟地址空间中该共享内存段的起点的指针。
4.  **调用 `shmdt()` 来分离共享内存段**。在这个调用之后，进程就无法再引用这块共享内存了。这一步是可选的, 并且在进程终止时会自动完成这一步。
5.  **调用`shmctl()`来删除共享内存段**。只有当当前所有附加内存段的进程都与之分离之后内存才会销毁。只有—个进程需要执行这一步

### 共享内存相关函数

**`int shmget(key_t key, size_t size, int shmflg);`**

*   **作用**：创建一个新的共享内存段，或者获取一个既有的共享内存段的标识  
    新创建的内存段中的数据都会被初始化为 0
    
*   **参数**：
    
    *   `key`：`key_t` 类型是一个整形，通过这个找到或者创建一个共享内存。  
        一般使用 16 进制表示，非 0 值
    *   `size`：共享内存的大小
    *   `shmflg`：属性
        *   访问权限
        *   附加属性: 创建 / 判断共享内存是不是存在
            *   创建：IPC_CREAT
            *   判断共享内存是否存在：IPC_EXCL，需要和 IPC_CREAT 一起使用 `IPC_CREAT | IPC_EXCL | 0664`
*   **返回值**：如果成功`>0`返回共享内存的引用的 ID（后面操作共享内存都是通过这个值）；如果失败返回 - 1，并设置 errno
    
    * * *
    

**`void *shmat(int shmid, const void *shmaddr, int shmflg);`**

*   **作用**：和当前的进程进行关联 - 参数
    
*   **参数**：
    
    *   `shmid`：- shmid : 共享内存的标识（ID）, 由`shmget` 返回值获取
    *   `shmaddr`：申请的共享内存的起始地址，指定 NULL，内核指定
    *   `shmflg`：对共享内存的操作
        *   读：SHM_RDONLY，必须要有读权限
        *   读写：0
*   **返回值**：如果成功`>0`返回共享内存的起始地址；如果失败返回 (void*)-1，并设置 errno  
    **`int shmdt(const void *shmaddr);`**
    
*   **作用**：解除当前进程和共享内存的关联
    
*   **参数**：`shmaddr`：共享内存的首地址
    
*   **返回值**：如果成功返回 0；如果失败返回 - 1
    
    * * *
    

**`int shmctl(int shmid, int cmd, struct shmid_ds *buf);`**

*   **作用**：对共享内存进行操作。删除共享内存，共享内存要删除才会消失，创建共
*   **参数**：
    *   `shmid`：共享内存的 ID
    *   `cmd`：要做的操作
        *   IPC_STAT：获取共享内存的当前的状态
        *   IPC_SET：设置共享内存的状态
        *   IPC_RMID：标记共享内存被销毁
    *   `buf`：需要设置或者获取的共享内存的属性信息
        *   IPC_STAT：buf 存储数据
        *   IPC_SET：buf 中需要初始化数据，设置到内核中
    *   IPC RMID：没有用，NULL
*   **返回值**：如果成功返回 0；如果失败返回 - 1

**代码示例**  
write_shm.c

```
#include <stdio.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <string.h>

int main()
{

    // 1.创建一个共享内存
    int shmid = shmget(100, 4096, IPC_CREAT | 0664);
    
    // 2.和当前进程进行关联
    void *ptr = shmat(shmid, NULL, 0);

    char *str = "helloworld";

    // 3.写数据
    memcpy(ptr, str, strlen(str) + 1);
    printf("按任意键继续\n");
    getchar();

    // 4.解除关联
    shmdt(ptr);

    // 5.删除共享内存
    shmctl(shmid, IPC_RMID, NULL);

    return 0;
}

```

read_shm.c

```
#include <stdio.h>
#include <sys/ipc.h>
#include <sys/shm.h>

int main()
{

    // 1.获取一个共享内存
    int shmid = shmget(100, 0, IPC_CREAT);
    printf("shmid: %d\n", shmid);

    // 2.和当前进程进行关联
    void *ptr = shmat(shmid, NULL, 0);

    // 3.读数据
    printf("%s\n", (char *)ptr);

    printf("按任意键继续\n");
    getchar();

    // 4.解除关联
    shmdt(ptr);

    // 5.删除共享内存
    shmctl(shmid, IPC_RMID, NULL);

    return 0;
}

```

![](https://img-blog.csdnimg.cn/a7754d8a4dad4b4691bf17c4567569ac.png)  
![](https://img-blog.csdnimg.cn/3bba686f620246d4b6dcb6b6d1c22bfa.png)

**`key_t ftok(const char *pathname, int proj_id);`**

*   **作用**：根据指定的路径名，和 `int` 值，生成一个共享内存的 key
*   **参数**：
    *   `pathname`：指定一个存在的路径
    *   `proj_id`： `int` 类型的值，但是这系统调用只会使用其中的 1 个字节  
        范围: 0-255 一般指定一个字符’a’
*   **返回值**：是一个 `key_t` 类型的键，表示关联到指定文件和项目 ID 的唯一键。

### 共享内存操作命令

#### ipcs 用法

打印当前系统中所有的进程间通信方式的信息

```
ipcs -a

```

打印出使用共享内存进行进程间通信的信息

```
ipcs -m

```

打印出使用消息队列进行进程间通信的信息

```
ipcs -q

```

打印出使用信号进行进程间通信的信息

```
ipcs -s

```

#### ipcrm 用法

移除用 shmkey 创建的共享内存段

```
ipcrm -M shmkey

```

移除用 shmid 标识的共享内存段

```
ipcrm -m shmid

```

移除用 msqkey 创建的消息队列

```
ipcrm -Q msgkey

```

移除用 msqid 标识的消息队列

```
ipcrm -q msqid

```

移除用 semkey 创建的信号

```
ipcrm -s semkey

```

移除用 semid 标识的信号

```
ipcrm -s semid

```

### 共享内存相关问题

**问题 1：操作系统如何知道一块共享内存被多少个进程关联?**  
**答**：共享内存维护了一个结构体`struct shmid_ds`这个结构体中有一个成员 `shm nattach` 记录了关联的进程个数  
  
**问题 2: 可不可以对共享内存进行多次删除 `shmctl` ？**  
**答**：可以的。因为 `shmctl` 标记删除共享内存，不是直接删除。**那什么时候真正删除呢?**  
**当和共享内存关联的进程数为 0 的时候，就真正被删除**。当共享内存的 key 为 0 的时候，表示共享内存被标记删除了。如果一个进程和共享内存取消关联，那么这个进程就不能继续操作这个共享内存。  
  
**共享内存和内存映射的区别**

1.  共享内存可以直接创建，内存映射需要磁盘文件（匿名映射除外)
    
2.  共享内存效果更高
    
3.  内存  
    所有的进程操作的是同一块共享内存。  
    内存映射，每个进程在自己的虚拟地址空间中有一个独立的内存。
    
4.  数据安全
    
    *   进程突然退出：共享内存还存在内存映射区消失
    *   运行进程的电脑死机，宕机了：数据存在在共享内存中，没有了。内存映射区的数据﹐由于磁盘文件中的数据还在，所以内存映射区的数据还存在。
5.  生命周期
    
    *   内存映射区：进程退出，内存映射区销毁
    *   共享内存：进程退出，共享内存还在，标记删除（所有的关联的进程数为 0）  
        如果一个进程退出，会自动和共享内存进行取消关联。

守护进程
----

### 什么是控制终端

> 在 UNIX 系统中，用户通过终端登录系统后得到一个 shell 进程，这个终端成为 shell 进程的**控制终端 (controlling Terminal)**，进程中，控制终端是保存在 PCB 中的信息，而 `fork()` 会复制 PCB 中的信息，因此由 shell 进程启动的其它进程的控制终端也是这个终端。

> 默认情况下（没有重定向)，每个进程的标准输入、标准输出和标准错误输出都指向控制终端，进程从标准输入读也就是读用户的键盘输入，进程往标准输出或标准错误输出写也就是输出到显示器上。

> 在控制终端输入一些特殊的控制键可以给前台进程发信号，例如 `Ctrl +C` 会产生 SIGINT 信号， `Ctrl +\` 会产生 SIGQUIT 信号。

![](https://img-blog.csdnimg.cn/0cb70c3549304f2f8debf365001ae242.png)

### 什么是进程组

> **进行组由一个或多个共享同一进程组标识符（PGID）的进程组成**。一个进程组拥有一个进程组首进程，该进程是创建该组的进程，其进程 ID 为该进程组的 ID，新进程会继承其父进程所属的进程组 ID。

> **进程组拥有一个生命周期，其开始时间为首进程创建组的时刻，结束时间为最后一个成员进程退出组的时刻**。一个进程可能会因为终止而退出进程组，也可能会因为加入了另外一个进程组而退出进程组。进程组首进程无需是最后一个离开进程组的成员。

进程组和会话在进程之间形成了一种两级层次关系：

*   进程组是一组相关进程的集合。
*   会话是一组相关进程组的集合。

进程组和会话是为支持 shell 作业控制而定义的抽象概念，用户通过 shell 能够交互式地在前台或后台运行命令。

### 什么是会话

> **会话是一组相关进程组的集合**。会话首进程是创建该新会话的进程，其进程 ID 会成为会话 ID。新进程会继承其父进程的会话 ID。

> **一个会话中的所有进程共享单个控制终端**。控制终端会在会话首进程首次打开一个终端设备时被建立。**一个终端最多可能会成为一个会话的控制终端**。  
> 在任一时刻，会话中的其中一个进程组会成为终端的前台进程组，其他进程组会成为后台进程组。**只有前台进程组中的进程才能从控制终端中读取输入**。当用户在控制终端中输入终端字符生成信号后，该信号会被发送到前台进程组中的所有成员。**当控制终端的连接建立起来之后，会话首进程会成为该终端的控制进程**。

### 进程组、会话、控制终端之间的关系

**关系示例**  
以下命令的作用是在根目录下搜索所有文件和目录，将标准错误输出（STDERR）重定向到 `/dev/null` 忽略任何错误消息，然后通过管道将搜索结果的行数（即文件和目录的数量）计数，并在后台运行这个任务，期间允许继续使用终端。

```
find / 2> / dev /null | wc -l &

```

以下命令的作用是将 `longlist` 中的内容按照字母顺序排序，然后统计每个唯一项出现的次数，并以 `次数 唯一项` 的格式输出。

```
sort < longlist | uniq -c

```

以上两组命令关系图  
![](https://img-blog.csdnimg.cn/f50f72c9b0914fdf98e47d89d97081b4.png)

终端显示  
![](https://img-blog.csdnimg.cn/1a3f987060bc4467a53fa69d04c81e7f.png)

ps：执行完第一组命令后输入 `fg` ，命令将回到前台运行，并且可以看到它的输出，也可以在需要时终止它。

### 进程组、会话操作函数

```
// 获取调用进程的进程组ID
pid_t getpgrp (void) ;

// 获取指定进程的进程组ID
pid_t getpgid(pid_t pid) ;

// 设置指定进程的进程组ID
int setpgid(pid_t pid, pid_t pgid) ;

// 获取指定进程的会话ID
pid_t getsid(pid_t pid) ;

// 创建一个新的会话，并返回其会话ID
pid_t setsid (void) ;

```

### 什么是守护进程

> **守护进程 (Daemon Process) ，也就是通常说的 Daemon 进程（精灵进程)，是 Linux 中的后台服务进程**。它是一个生存期较长的进程，通常独立于控制终端并且周期性地执行某种任务或等待处理某些发生的事件，虽然产生条件和孤儿进程类似但并不是孤儿进程。

> 守护进程一般采用以 d 结尾的名字。  
> Linux 的大多数服务器就是用守护进程实现的。比如， Internet 服务器 inetd，web 服务器 httpd 等。

**守护进程特征**

*   **生命周期很长**，守护进程会在系统启动的时候被创建并一直运行直至系统被关闭。
*   它在**后台运行并且不拥有控制终端**。没有控制终端确保了内核永远不会为守护进程自动生成任何控制信号以及终端相关的信号（如 SIGINT、SIGQUIT)。

### 守护进程的创建步骤

1.  执行一个 `fork()`，之后父进程退出，子进程继续执行。
2.  子进程调用 `setsid()` 开启一个新会话。
3.  清除进程的 `umask` 以确保当守护进程创建文件和目录时拥有所需的权限。
4.  修改进程的当前工作目录，通常会改为根目录 `/`。
5.  关闭守护进程从其父进程继承而来的所有打开着的文件描述符。
6.  在关闭了文件描述符 0、1、2 之后，守护进程通常会打开 `/dev /null` 并使用 `dup2()` 使所有这些描述符指向这个设备。
7.  核心业务逻辑。

**代码示例**  
写一个守护进程，每隔 2s 获取一下系统时间，将这个时间写入到磁盘文件中。

```
#define _DEFAULT_SOURCE
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <fcntl.h>
#include <sys/time.h>
#include <signal.h>
#include <time.h>
#include <string.h>
// 写一个守护进程，每隔2s获取一下系统时间，将这个时间写入到磁盘文件中。

void work(int num)
{
    // 捕捉到信号之后，获取系统时间，写入磁盘文件
    time_t tm = time(NULL);
    struct tm *loc = localtime(&tm);
    // char buf[1024];
    // sprintf(buf, "%d-%d-%d %d: %d : %d\n", loc->tm_year, loc->tm_mon, loc->tm_mday, loc->tm_hour, loc->tm_min, loc->tm_sec);
    // print("%s\n", buf);

    char* str = asctime(loc);
    int fd = open("time.txt", O_RDWR | O_CREAT | O_APPEND, 0664);
    write(fd, str, strlen(str));

    close(fd);
}

int main(){
    // 1.创建子进程,退出父进程
    pid_t pid = fork();
    if(pid > 0){
        exit(0);
    }

    // 2.将子进程重新创建一个会话
    setsid();

    // 3.设置编码
    umask(022);

    // 4.更改工作目录
    chdir("/home/zxz/");

    // 5．关闭、重定向文件描述符
    int fd = open("/dev/null", O_RDWR);
    dup2(fd, STDIN_FILENO);
    dup2(fd, STDOUT_FILENO);
    dup2(fd, STDERR_FILENO);

    // 6.业务逻辑

    // 6.1.捕捉定时信号
    struct sigaction act;
    act.sa_flags = 0;
    act.sa_handler = work;
    sigemptyset(&act.sa_mask);
    sigaction(SIGALRM, &act, NULL);

    struct itimerval val;
    val.it_value.tv_sec = 2;
    val.it_value.tv_usec = 0;
    val.it_interval.tv_sec = 2;
    val.it_interval.tv_usec = 0;

    // 6.2.创建定时器
    setitimer(ITIMER_REAL, &val, NULL);

    // 6.3.不让进程结束
    while (1)
    {
        sleep(10);
    }
    

    return 0;
}

```

![](https://img-blog.csdnimg.cn/eacd551ba5df403b86cd2bb037ca491f.png)  
![](https://img-blog.csdnimg.cn/6457aa6f42c8419b849a9903810f0ece.png)  
vim 进入 time 文件

```
vim time.txt

```

![](https://img-blog.csdnimg.cn/1effcd03e3434e889ae82c90d5d73ae6.png)  
键入 `:e` 重新加载文件![](https://img-blog.csdnimg.cn/5bf3be278629419782dbea943fd4ef24.png)

结语
--

课程笔记源于牛客 C++ 求职项目：[https://www.nowcoder.com/courses/cover/live/504](https://www.nowcoder.com/courses/cover/live/504) 的[第 2 章 Linux 多进程开发](https://www.nowcoder.com/study/live/504/2/1)。  
**由于并不是专门的进程学习课程，可能此章节老师的一些说法不太清晰或完全，我是结合《CSAPP》来学习的，多练习一下上面的题有时会醍醐灌顶，另外多使用 `man` 来查看系统 API 文档。**  
此笔记相对课程内容有增删仅个人复习用，若有需要仅供参考。以上所有代码和图片均为课程自带以及网络资源，欢迎各位大佬提出问题和建议，更完的笔记实时更新，后续为了能更加巩固相关知识可能会更新较慢望谅解。