# PA-ysyx-学习日志

## Day1

（2024.1.29）

### 总体

将Linux安装在虚拟机中，系统为**ubuntu-22.04.3-desktop-amd64**，并且成功配置清华源，安装相应软件,[学习了github](https://zhuanlan.zhihu.com/p/369486197)以及[git](https://blog.csdn.net/qq_37772475/article/details/107140061)，和vim[的使用方法](https://zhuanlan.zhihu.com/p/68111471)

### 问题

1.Linux下切换root用户提示**Authentication failure**

2.下载vim时出现以下问题

~~~
下列软件包有未满足的依赖关系：
 vim : 依赖: vim-common (= 2:8.2.3995-1ubuntu2) 但是 2:8.2.3995-1ubuntu2.10 正要被安装
E: 无法修正错误，因为您要求某些软件包保持现状，就是它们破坏了软件包间的依赖关系。
~~~

3.使用git clone远端仓库时出现以下问题

```
$  Git clone https://github.com/cz0729zc/PA-ysyx.git
Cloning into 'PA-ysyx'...
fatal: unable to access 'https://github.com/cz0729zc/PA-ysyx.git/': Failed to connect to github.com port 443 after 21088 ms: Couldn't connect to server
```

4.对git branch 之间的关系有了更深入的了解：在分支下创建文件后，需要对其add和commit。

### 解决方法及原因

问题一：[解决方法](https://blog.csdn.net/renrenxu/article/details/82725659)

问题二：[解决方法](https://blog.csdn.net/qq_40748967/article/details/122040610)

问题三：[解决方法](https://zhuanlan.zhihu.com/p/636418854)

问题四：[解决方法](https://zhuanlan.zhihu.com/p/410255613)



## Day2

（2024.1.30）

### 总体

今天将git和vim的语法深入学习了解了一下，掌握了和常见的git命令，和vim指令。并且使用vundle插件管理工具配置vim编辑器，参考[文章一](https://blog.csdn.net/amoscykl/article/details/80616688)，在虚拟机中配置了ssh以达到远程连接github，参考[文章二](https://blog.csdn.net/Sapphire41/article/details/111514465)，但是ubuntu无法连接github，也无法ping通，查了很多资料也没有解决，但是有了解决方向：通过修改ubuntu中的hosts文件，同时了解了IP和DNS的相关概念。

**ssh存放路径：/home/zc/.ssh**

**host存放路径指令：sudo gedit /etc/hosts**

推荐视频：硬件茶谈，[DNS](https://www.bilibili.com/video/BV1Rp4y1a7xQ?spm_id_from=333.880.my_history.page.click)，[IP](https://www.bilibili.com/video/BV1DD4y127r4?spm_id_from=333.880.my_history.page.click)

### 问题

1. ubuntu无法连接github也无法ping通



### 解决方法及原因

1. 通过域名解析器实时获取github.com响应ip，并配置到hosts文件中，[文章一](https://blog.csdn.net/PPprogrammer/article/details/105817073)



## Day3

### 总体

今天成功ping通github并解决了：可以ping通但是不能clone的问题，参考[文章一](https://blog.csdn.net/dashi_lu/article/details/89641778)，

 

### 问题

1.在给vim配置插件时出现**依赖问题**导致无法下载成功

2.无法clone远程仓库

### 解决方法及原因

1.[解决方法](https://blog.csdn.net/m0_51684972/article/details/109171608)**aptitude **

2.步骤一：先用UHE获取GitHub网络ip地址，配置hosts文件，然后登陆ikuu获取clash，然后配置clash. 

（每次开启时进入Downloads文件夹执行**./clash -d .**）



## Day4

### 总结

这几天一直在解决这个问题，通过实现虚拟机共享主机代理，成功实现GitHub，youtube，等网站在ubuntu上流畅打开，但是git clone 小项目的时候可以，项目一大就不行了，发现是网速太慢，后来发现在使用git clone时http协议可以，但是ssh协议速度很慢，后来通过配置ssh.config文件在其中添加

```
ssh 方式 clone 代码
修改本机的 ~/.ssh/config，给里面添加一条记录。

vi ~/.ssh/config
Host github.com
  ProxyCommand nc -v -x 127.0.0.1:1086 %h %p
```

***注意这里的127.0.0.1是自己的主机ip，1086是自己代理端口***

同时我也做了如下修改

~~~
vim /etc/ssh/sshd_config

修改GSSAPIAuthentication参数为 no，默认是yes
~~~



### 问题

1. git clone 速度缓慢

2. 在调用bash init.sh nemu时clone时间过长导致失败
3. git clone时http协议速度很快，但是ssh协议速度很慢



### 解决方法及原因

1.[文章一](https://zhuanlan.zhihu.com/p/360121631)

2.[文章二](https://zhuanlan.zhihu.com/p/58006202)

3.[新增方法](https://gitclone.com)：使用国内镜像

**或者使用全局参数，更改 git 参数**

~~~shell
git config --global url."https://https://githubclone.com/github.com/".insteadOf "https://github.com/"
~~~

使用全局参数更改以后，使用 **vim ~/.gitconfig** 命令即可查看当前的配置文件，看到以下配置。

~~~
[url "https://https://githubclone.com/github.com/"]
        insteadOf = https://github.com/
~~~

## Day5

### 总结

### 问题

1.在执行make menuconfig时报错

~~~
make[1]: bison: No such file or directory
~~~

2.下完flex和bison后任然报错

~~~c
In file included from mconf.c:23:
lxdialog/dialog.h:19:10: fatal error: ncurses.h: 没有那个文件或目录
   19 | include <ncurses.h>
      |          ^~~~~~~~~~~
compilation terminated.
make[1]: *** [/home/zc/ics2022/nemu/scripts/build.mk:34：/home/zc/ics2022/nemu/tools/kconfig/build/obj-mconf/mconf.o] 错误 1
make: *** [/home/zc/ics2022/nemu/scripts/config.mk:39：/home/zc/ics2022/nemu/tools/kconfig/build/mconf] 错误 2
~~~

3.安装完ncurses库后又出现**依赖问题**解决方法参考之前

### 解决方法及原因

1.通过下载bison和flex

~~~
sudo apt-get install bison
sudo apt-get install flex
~~~

2.通过安装ncurses库

~~~
sudo apt-get install libncurses5-dev libncursesw5-dev
~~~

## Day6

### 总结

今天成功在ubuntu上运行马里奥程序，没有遇到什么大的问题，就是总出现**依赖项**需要对软件包进行降级处理，不知道这个操作对后面有没有影响，有可能埋坑了

![image-20240219155556621](C:\Users\32734\AppData\Roaming\Typora\typora-user-images\image-20240219155556621.png)



## Day7

### 总结

花了几天时间，成功调试成功并解决nemu报错，比较理解了，程序到底是如何在计算机上运行的，对于**“ 谁来指示程序的结束? ”**有了自己的一部分理解

### 问题

1. 出现以下报错

~~~
[src/monitor/monitor.c:20 welcome] Exercise: Please remove me in the source code and compile NEMU again.
risc64-nemu-interpreter: src/monitor/monitor.c:36: welcome: Assertion `0' failed.
~~~

2. 进行gitclone的时候发现又不行了，经过检查发现是本机ip发生改变

### 解决方法及原因

1. 在**nemu/src/monitor/monitor.c**文件中对36行的assert(0),进行注释就可以了，这里涉及[断言](https://blog.csdn.net/fan_h_l/article/details/99837393)
2. 通过手动配置代理将其修改就可以，还有config文件配置

## Day8

### 总结

今天成功搭建verilator仿真环境，并且成功运行双控开关,并且使用gtkwave查看波形图

运行命令：

~~~
verilator --cc --exe --build -j 0 -Wall test1_main.cpp top.v

obj_dir/Vtop
~~~

- `--cc`: 指定Verilator使用C++进行仿真
- `--exe`: 生成可执行文件
- `--build`: 生成仿真器可执行文件
- `-j 0`: 使用所有可用的处理器核心进行编译
- `-Wall`: 显示所有警告信息
- `sim_main.cpp`: C++仿真程序的入口文件
- `our.v`: Verilog文件，包含待仿真的设计代码



**gtkwave**运行命令：

~~~
iverilog -o counter_test counter_tb.v counter.v  //创建一个test测试文件，对源文件和仿真文件，进行语法规则检查和编译
~~~

```
vvp -n counter_test -lxt2  //生成.vcd波形文件
```

```
cp counter_test.vcd counter_test.lxt
```

```
gtkwave counter_test.lxt    //打开波形文件，可以在图形化界面中查看仿真的波形图
```

![image-20240226111428273](C:\Users\32734\AppData\Roaming\Typora\typora-user-images\image-20240226111428273.png)

## Day9

### 总结

系统了解了**[makefile](https://blog.csdn.net/qq_66197674/article/details/139365933#:~:text=Makefile%20%E6%98%AF)**相关语法及其命令，在examples/Mytest/test3目录下，参考[文章一]()，并成功实现FPGA模拟开发板使用，要将项目的目录设置为环境变量NVBOARD_HOME，可以按照以下步骤操作：

1. 打开终端窗口。

2. 使用以下命令找到项目的目录路径：

   ```
   cd nvboard
   pwd
   ```

3. 将项目的目录路径添加到环境变量NVBOARD_HOME中，可以通过编辑~/.bashrc文件（或者~/.bash_profile文件）来实现。使用以下命令打开~/.bashrc文件：

   ```
   nano ~/.bashrc
   ```

4. 在文件末尾添加以下行，将项目的目录路径替换为实际路径：

   ```
   export NVBOARD_HOME=/path/to/nvboard
   ```

5. 使用Ctrl + X保存并退出文件。

6. 使用以下命令使更改生效：

   ```
   source ~/.bashrc
   ```

7. 确保环境变量已经设置成功，可以使用以下命令检查：

   ```
   echo $NVBOARD_HOME
   ```

## Day10

### 总结

今天将vim中的代码自动补全插件安装成功，大致熟悉了nvboard中的example框架，正在学习FPGA的基本语法。

[文章一](https://blog.csdn.net/lgyLGY35/article/details/113930618)

## Day11

### 总结

今天成功依照样例代码，编写出了led流水灯和拨片开关，并且将verilog_OJ刷了一些基础题，理解了verilater的基础编程
![image-20240229154727527](C:\Users\32734\AppData\Roaming\Typora\typora-user-images\image-20240229154727527.png)

**激励代码**通常指的是在硬件描述语言（如Verilog）中用于仿真的测试激励。让我们来详细探讨一下：

**激励代码是什么意思**

1. **Verilog 仿真激励**：

   - 在数字电路设计中，我们使用硬件描述语言（HDL）如Verilog来描述电路的行为和结构。
   - 仿真激励是一种用于验证设计的测试方法。它允许我们在没有实际硬件的情况下模拟电路的功能。
   - **Testbench** 是一个Verilog文件，用于生成仿真激励信号，以对设计进行仿真测试。
   - Testbench 包含信号声明、激励生成和模块实例化等部分。
   - 通过编写合适的 testbench，我们可以模拟输入信号并对设计进行仿真，以确保其正常工作。

2. **激励的具体含义**：

   - 在Verilog中，激励是指为设计提供输入信号的数据或者行为模型。
   - 例如，如果你编写了一个代码，在时钟上升沿时让某个变量 `a` 加1，但没有实际时钟源，你就需要为这段代码添加激励。这个激励相当于你所需的时钟信号，使得代码能够产生相应的输出，例如观察 `a` 是否加1。

3. **Testbench 示例**：

   - 下面是一个简单的Verilog模块和对应的testbench示例：

     ```verilog
     // 一个 2bit 数据拼接成 8bit 数据的功能模块
     module data_consolidation (
         input clk,
         input rstn,
         input [1:0] din, // 数据输入
         input din_en,    // 数据输入使能
         output [7:0] dout, // 数据输出
         output dout_en    // 数据输出使能
     );
     // ... 模块功能实现 ...
     
     // 对应的 testbench
     module test;
         reg clk;
         reg rstn;
         reg [1:0] din;
         reg din_en;
         wire [7:0] dout;
         wire dout_en;
     
         // ... 时钟和复位生成 ...
     
         // 从文件读取数据并生成激励
         // ...
     endmodule
     ```

   - 在testbench中，我们可以模拟输入信号，例如从文件读取数据，并将其作为激励信号输入到被测试的设计中。

总之，激励代码是为了验证设计的正确性而编写的测试信号，它在仿真中起到关键作用

​              [如何查看波形](https://blog.csdn.net/qq_41763108/article/details/127965316)

## Day12 

### 总结

今天开始pa2的正式学习，今天在调试pa1.2的时候遇到处理负号的时候出现如下bug
~~~c
(nemu) p --1
[src/monitor/sdb/expr.c:189 make_token] match rules[5] = "-" at position 0 with len 1: -
[src/monitor/sdb/expr.c:189 make_token] match rules[5] = "-" at position 1 with len 1: -
[src/monitor/sdb/expr.c:189 make_token] match rules[3] = "[0-9]+" at position 2 with len 1: 1
Entering eval with p=0, q=2
Entering eval with p=0, q=-1
~~~

调试bug发现q的值竟然是负数

~~~c
// 更新 tokens 的数量 
for(int j = 0;j < tokens_len; j ++){ 
    if(tokens[j].type == TK_NOTYPE)
    {
      for(int k = j+1; k < tokens_len;k ++){
        tokens[k - 1] = tokens[k];
      }
      tokens_len --;
      nr_token--;   //全局变量也要减
    }
}
~~~



## Day13 

### 总结

今天成功调试成功代码，完成pa2.1阶段，
~~~shell
zc@zc-virtual-machine:~/ics2022/am-kernels/tests/cpu-tests$ make ARCH=riscv32-nemu ALL=dummy run
# Building dummy-run [riscv32-nemu]
# Building am-archive [riscv32-nemu]
+ CC src/platform/nemu/trm.c
+ AR -> build/am-riscv32-nemu.a
# Building klib-archive [riscv32-nemu]
+ LD -> build/dummy-riscv32-nemu.elf
# Creating image [riscv32-nemu]
+ OBJCOPY -> build/dummy-riscv32-nemu.bin
+ LD /home/zc/ics2022/nemu/build/riscv32-nemu-interpreter
[src/utils/log.c:28 init_log] Log is written to /home/zc/ics2022/am-kernels/tests/cpu-tests/build/nemu-log.txt
c[src/memory/paddr.c:56 init_mem] physical memory area [0x80000000, 0x87ffffff]
[src/monitor/monitor.c:61 load_img] The image is /home/zc/ics2022/am-kernels/tests/cpu-tests/build/dummy-riscv32-nemu.bin, size = 57
[src/monitor/monitor.c:28 welcome] Trace: ON
[src/monitor/monitor.c:29 welcome] If trace is enabled, a log file will be generated to record the trace. This may lead to a large log file. If it is not necessary, you can disable it in menuconfig
[src/monitor/monitor.c:32 welcome] Build time: 16:01:58, Sep 19 2024
Welcome to riscv32-NEMU!
For help, type "help"
[src/monitor/monitor.c:35 welcome] Exercise: Please remove me in the source code and compile NEMU again.
(nemu) c
[src/cpu/cpu-exec.c:121 cpu_exec] nemu: HIT GOOD TRAP at pc = 0x80000030
[src/cpu/cpu-exec.c:89 statistic] host time spent = 2,058 us
[src/cpu/cpu-exec.c:90 statistic] total guest instructions = 13
[src/cpu/cpu-exec.c:91 statistic] simulation frequency = 6,316 inst/s
(nemu) q
 dummy
[         dummy] PASS!
~~~

