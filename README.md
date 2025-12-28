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

3.2.1 系统总体结构图

```mermaid
flowchart TB
    A[请求页式管理缺页中断模拟程序]
    A --> B[输入模块]
    A --> C[算法选择模块]
    A --> D[页面置换算法模块]
    A --> E[状态记录模块]
    A --> F[输出模块]
```

如图3.2.1所示，系统总体结构图展示了请求页式管理缺页中断模拟程序的五个主要功能模块：输入模块、算法选择模块、页面置换算法模块、状态记录模块和输出模块。

3.2.2 输入模块结构图

```mermaid
flowchart TB
    A[输入模块]
    A --> B[手动输入子模块]
    A --> C[示例数据子模块]
    B --> D[物理页框数输入]
    B --> E[页面访问序列输入]
    C --> F[默认页框数设置]
    C --> G[经典测试序列加载]
```

如图3.2.2所示，输入模块包含手动输入和示例数据两个子模块。手动输入子模块提供物理页框数输入和页面访问序列输入功能；示例数据子模块提供默认页框数设置和经典测试序列加载功能。

3.2.3 算法选择模块结构图

```mermaid
flowchart TB
    A[算法选择模块]
    A --> B[菜单显示]
    A --> C[用户选择处理]
    A --> D[算法调用]
```

如图3.2.3所示，算法选择模块负责菜单显示、用户选择处理和算法调用三个功能。菜单显示向用户展示可选的算法选项；用户选择处理获取并验证用户的选择；算法调用根据用户选择执行相应的页面置换算法。

3.2.4 页面置换算法模块结构图

```mermaid
flowchart TB
    A[页面置换算法模块]
    A --> B[FIFO算法]
    A --> C[LRU算法]
    A --> D[OPT算法]
    A --> E[Random算法]
    B --> B1[循环队列管理]
    B --> B2[页面置换逻辑]
    C --> C1[双向链表维护]
    C --> C2[哈希表查找]
    C --> C3[页面更新逻辑]
    D --> D1[未来序列查找]
    D --> D2[最优页面选择]
    E --> E1[访问计数维护]
    E --> E2[最少访问页面选择]
```

如图3.2.4所示，页面置换算法模块实现了四种算法。FIFO算法使用循环队列管理和页面置换逻辑；LRU算法使用双向链表维护、哈希表查找和页面更新逻辑；OPT算法使用未来序列查找和最优页面选择；Random算法使用访问计数维护和最少访问页面选择。

3.2.5 状态记录模块结构图

```mermaid
flowchart TB
    A[状态记录模块]
    A --> B[内存状态记录]
    A --> C[缺页次数统计]
    A --> D[淘汰页号记录]
```

如图3.2.5所示，状态记录模块负责记录内存状态、缺页次数统计和淘汰页号记录。内存状态记录记录每步的内存状态变化；缺页次数统计实时统计缺页次数；淘汰页号记录记录每次置换时被淘汰的页号。

3.2.6 输出模块结构图

```mermaid
flowchart TB
    A[输出模块]
    A --> B[基本信息输出]
    A --> C[内存状态表输出]
    A --> D[淘汰页号输出]
```
