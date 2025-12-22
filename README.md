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





**主函数调用流程：**

```mermaid
graph TD
    A[主函数] --> B[显示菜单]
    B --> C[获取用户输入]
    C --> D[分支选择]
    D --> E1[参数配置]
    D --> E2[输入处理]
    D --> E3[算法执行]
    E1 --> F[调度器核心类]
    E2 --> F
    E3 --> F
    F --> G[显示结果]
    
    style A fill:#ffeb3b
    style F fill:#4caf50
    style G fill:#2196f3
```

**参数配置模块调用：**

```mermaid
graph LR
    A[菜单项1-3] --> B1[设置磁头位置]
    A --> B2[设置移动方向]
    A --> B3[设置最大磁道号]
    B1 --> C[调度器核心类]
    B2 --> C
    B3 --> C
    
    style C fill:#4caf50
```

**输入处理模块调用：**

```mermaid
graph TD
    A[菜单项4] --> B[输入请求序列]
    B --> C1[获取整数输入]
    B --> C2[获取磁道号输入]
    B --> D[添加请求]
    D --> E[调度器核心类]
    
    style E fill:#4caf50
```

**算法执行模块调用：**

```mermaid
graph LR
    A[菜单项6-9] --> B1[先来先服务算法]
    A --> B2[最短寻道时间优先算法]
    A --> B3[电梯算法]
    A --> B4[批量比较]
    B1 --> C[调度器核心类]
    B2 --> C
    B3 --> C
    B4 --> C
    C --> D[显示结果]
    
    style C fill:#4caf50
    style D fill:#2196f3
```

 3.3.4 典型操作流程示例

流程1：完整测试流程
```
1. 启动程序 → 显示欢迎信息
2. 选择菜单项1 → 设置磁头位置（如：53）
3. 选择菜单项2 → 设置移动方向（如：1，向外）
4. 选择菜单项4 → 输入请求序列（如：98 183 37 122 14 124 65 67）
5. 选择菜单项9 → 比较所有算法
6. 查看三种算法的详细结果对比
7. 选择菜单项0 → 退出程序
```

流程2：快速测试流程
```
1. 启动程序
2. 选择菜单项10 → 使用示例数据测试
3. 自动完成参数设置和算法执行
4. 查看对比结果
5. 选择菜单项0 → 退出程序
```

流程3：单独算法测试流程
```
1. 启动程序
2. 选择菜单项4 → 输入请求序列
3. 选择菜单项6 → 执行FCFS算法
4. 查看FCFS结果
5. 返回主菜单，选择菜单项7 → 执行SSTF算法
6. 查看SSTF结果
7. 继续测试其他算法或退出
```

 3.4 功能结构图

**顶层模块结构：**

```mermaid
graph TD
    A[磁盘调度算法模拟程序] --> B[初始化模块]
    A --> C[参数配置模块]
    A --> D[输入处理模块]
    A --> E[算法执行模块]
    A --> F[结果显示模块]
    A --> G[程序控制模块]
    
    style A fill:#e1f5ff,stroke:#01579b,stroke-width:3px
```

**参数配置模块结构：**

```mermaid
graph TD
    A[参数配置模块] --> B1[设置磁头位置]
    A --> B2[设置移动方向]
    A --> B3[设置最大磁道号]
    B1 --> C1[输入验证]
    B1 --> C2[更新currentHead]
    B1 --> C3[显示成功信息]
    B2 --> C4[输入验证]
    B2 --> C5[更新direction]
    B3 --> C6[输入验证]
    B3 --> C7[更新maxTrack]
    
    style A fill:#e8f5e9
```

**输入处理模块结构：**

```mermaid
graph TD
    A[输入处理模块] --> B1[模式1:逐个输入]
    A --> B2[模式2:一次性输入]
    A --> B3[输入验证子模块]
    B1 --> C1[输入数量]
    B1 --> C2[循环输入]
    B1 --> C3[实时验证]
    B2 --> C4[读取整行]
    B2 --> C5[解析token]
    B2 --> C6[位置保持]
    B3 --> C7[类型验证]
    B3 --> C8[格式验证]
    B3 --> C9[范围验证]
    
    style A fill:#e8f5e9
```

**算法执行模块结构：**

```mermaid
graph TD
    A[算法执行模块] --> B1[FCFS算法]
    A --> B2[SSTF算法]
    A --> B3[SCAN算法]
    A --> B4[compareAll]
    B1 --> C1[顺序访问]
    B1 --> C2[计算距离]
    B2 --> C3[查找最近]
    B2 --> C4[标记访问]
    B3 --> C5[排序分离]
    B3 --> C6[方向判断]
    B4 --> C7[批量执行]
    
    style A fill:#e8f5e9
```

**结果显示模块结构：**

```mermaid
graph TD
    A[结果显示模块] --> B1[displaySettings]
    A --> B2[displayResult]
    B1 --> C1[显示参数]
    B1 --> C2[显示请求序列]
    B2 --> C3[显示访问序列]
    B2 --> C4[显示统计信息]
    B2 --> C5[显示详细过程]
    
    style A fill:#e8f5e9
```


