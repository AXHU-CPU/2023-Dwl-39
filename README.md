设计简介
---------------
    该设计是针对于 2023 年“龙芯杯”计算机系统能力培养大赛个人赛所设计的一个 32位 MIPS CPU，所设计的 CPU 采用了顺序单发射机制和经典的五级流水结构，可以运行实现8 条算术运算指令、7 条逻辑运算指令、6 条移位指令、10 条分支跳转指令、4 条访存指令，共计 35 条指令（具体指令见支持指令表 1）。本次设计的 CPU 在所有指令功能测试和性能测试满分通过的基础上，最高可以支持65MHz 的时钟频率，且 WNS、TNS 都为正值，满足时序要求。在数据相关问题上采用数据前推的方式进行解决，在 load 相关问题和指令数据访存冲突时通过暂停流水线进行解决。同时设计了一个 32 位的超前进位加法器用于加减法的运算。工程包含示例代码和所有引脚约束，可以直接编译。
![image](https://github.com/user-attachments/assets/b8c26b90-9657-4400-bb21-ef19085af65d)

模块结构图
---------------
![image](https://github.com/user-attachments/assets/082b4d72-05b2-4630-8380-196f15e6540a)

thinpad_top.srcs 目录层次
---------------
源代码的 thinpad_top.srcs 目录层次如下：
thinpad_top.srcs
├─ constrs_1 //约束文件，添加了部分输入的时序延时，
│ └─ new
│ └─ thinpad_top.xdc //管教约束文件，来源于发布包
├─ sim_1 //使用发布包的仿真文件，未列出
│ └─ new
└─ sources_1
├─ ip //所调用的 ip 核(通过调参，vivado 自动生成)
│ └─ pll_example //时钟分频模块,分频为 65MHz
└─ new //设计源文件
├─ ADD_SUB.v //超前进位加法器
├─ ALUModule.v //ALU 运算模块
├─ async.v //串口实例化模块
├─ bus_ctrl.v //总线控制模块
├─ DEFINES.v //宏定义
├─ D_BUFF5.v //缓存暂存模块(IF-ID、ID-EX、EX-MEM、MEM-WB)
├─ D_CPU.v //所设计的 DCPU 顶层模块
├─ pipe_ctrl.v //流水线控制模块
├─ regfile.v //寄存器模块
├─ SEG7_LUT.v //数码管模块（验证板卡是否启动，与 CPU 无关）
├─ state_ex.v //执行模块
├─ state_id.v //译码模块
├─ state_if.v //取值模块
├─ state_mem.v //访存模块
├─ thinpad_top.v //顶层文件
└─ vga.v //VGA 显示模块（验证板卡是否启动，与 CPU 无关）

代码中包含中文注释，Vivado下可能出现乱码问题，为了保证显示正确
Windows平台请使用GBK编码的文件，Linux平台请使用UTF-8编码的文件。  
