# -CF-OF-
1.无符号数：CF为cary flag进位/借位标记，当2个数相加产生了进位时或2个数相减产生了借位时，CF=1
<img width="267" height="49" alt="图片" src="https://github.com/user-attachments/assets/a35888a8-deb9-407d-8106-40af90001a7a" />
<img width="980" height="467" alt="图片" src="https://github.com/user-attachments/assets/95c99d11-e57f-4f69-a14a-3ef68aae4995" />
<img width="1657" height="294" alt="图片" src="https://github.com/user-attachments/assets/b6302168-3f5d-4677-86aa-ce1cfe4f6dd4" />

2.有符号数：OF为overflow flag溢出标记，当运算结果result溢出时，OF=1；未溢出时，OF=0
OF的计算方法：
<img width="1511" height="462" alt="图片" src="https://github.com/user-attachments/assets/389ff910-fd16-4b1d-9e8f-7e4ab2076d30" />
<img width="1581" height="782" alt="图片" src="https://github.com/user-attachments/assets/1190561f-652f-4e81-93dc-9603260590a7" />
<img width="1696" height="862" alt="图片" src="https://github.com/user-attachments/assets/8eae6b0a-9f3e-4874-b6f5-51984afaaa66" />
<img width="1695" height="787" alt="图片" src="https://github.com/user-attachments/assets/388784ad-84c9-438d-8b90-7429ea70023f" />
注：从图形上理解，为什么原码数值相加有进位，补码数值相加就没有进位：两个数原码相加大于360度，两个原码、补码相加一共720度，那么两个补码相加一定小于360度
<img width="440" height="236" alt="图片" src="https://github.com/user-attachments/assets/3c9e8351-a4b5-4a7d-b85e-c4cbeecf7667" />
<img width="1702" height="791" alt="图片" src="https://github.com/user-attachments/assets/e2928036-4d87-49f1-a149-93ea1b0e0dc9" />

# 作业/测练
> 导出时间：2026/1/8 14:29:22

### 1. 根据本章所介绍的简单代码生成算法和所假设的目标语言，试给下列三地址码语句序列所生成的目标代码。A=B\*CD=E\+FG=A\+DH=G\*2其中，H是基本块出口的活跃变量，R0和R1是可用寄存器。
根据本章所介绍的简单代码生成算法和所假设的目标语言，试给下列三地址码语句序列所生成的目标代码。

A=B\*C

D=E\+F

G=A\+D

H=G\*2

其中，H是基本块出口的活跃变量，R0和R1是可用寄存器。
答案：
MOV B, R0

MUL R0, C

MOV E, R1

ADD R1, F

ADD R0, R1

MUL R0, 2

ST R0, H

### 2. 一个编译程序的代码生成需考虑哪些问题?
答案：
1\. 指令选择（Instruction Selection）

- 目标： 为每条中间语言语句选择合适的目标机指令或指令序列。

- 原则：语义一致性： 确保生成的指令序列保持与中间代码语义一致。  
执行效率： 考虑时间和空间的代价，提高代码执行的效率（例如，选择成本较低的指令序列）。  
上下文相关： 目标指令的选择通常取决于中间代码的上下文以及目标机的体系结构特性（如流水线处理）。  


2\. 寄存器分配（Register Allocation）

- 目标： 充分且高效地利用寄存器，减少内存访问。

- 原则：尽可能让变量的值保留在寄存器中。  
优先引用寄存器中的变量值。  
在不再被引用的变量所占用的寄存器中释放资源。  


- 方法： 借助于“待用信息链”和“活跃信息链”，确保寄存器分配的动态优化。

3\. 指令调度（Code Scheduling）

- 目标： 选择合理的计算次序，充分利用目标机的硬件特点（如流水线和并行处理能力）。

- 策略：通过分析依赖关系（如数据依赖、控制依赖）调整指令顺序。  
避免资源冲突，最大化指令的执行并行度。  


4\. 基本块范围内的优化

- 变量待用和活跃信息：待用信息：确定变量是否会被再次引用。  
活跃信息：判断变量是否在后续基本块出口仍然活跃。  
对基本块从出口到入口扫描，动态更新每个变量的待用信息和活跃信息。  


- 寄存器分配优化：基于活跃变量和寄存器状态动态调整寄存器分配。  
在基本块结束时，将活跃变量的值写回内存。  


5\. 代码生成算法

- 简单代码生成算法：基于基本块内的中间代码（TAC语句）进行生成。  
通过RVALUE和AVALUE数组管理寄存器和变量的存储状态。  
依据寄存器可用性动态分配寄存器，生成指令序列。  


- 优化寄存器使用：清理不再引用的变量，释放被占用的寄存器。  
对基本块出口处的活跃变量，确保将寄存器中的值存入内存。  


6\. DAG（有向无环图）优化

- DAG 表示： 用 DAG 图表示基本块中的依赖关系，生成语句次序。

- 启发式排序： 通过遍历 DAG，优化指令顺序，减少寄存器使用和冗余操作。
