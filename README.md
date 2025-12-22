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









```mermaid
graph TD
    A[磁盘调度算法模拟程序] --> B[初始化模块]
    A --> C[参数配置模块]
    A --> D[输入处理模块]
    A --> E[算法执行模块]
    A --> F[结果显示模块]
    A --> G[程序控制模块]
    
    B --> B1[创建DiskScheduler对象]
    B --> B2[设置默认参数<br/>磁头=0,方向=向外,最大磁道=199]
    B --> B3[显示欢迎信息]
    
    C --> C1[设置磁头位置<br/>setCurrentHead]
    C --> C2[设置移动方向<br/>setDirection]
    C --> C3[设置最大磁道号<br/>setMaxTrack]
    
    C1 --> C1A[输入验证范围检查]
    C1 --> C1B[更新currentHead]
    C1 --> C1C[显示设置成功信息]
    
    C2 --> C2A[输入验证1或-1]
    C2 --> C2B[更新direction]
    C2 --> C2C[显示方向说明]
    
    C3 --> C3A[输入验证>0]
    C3 --> C3B[更新maxTrack]
    C3 --> C3C[显示设置成功信息]
    
    D --> D1[选择输入模式]
    D --> D2[输入验证子模块]
    
    D1 --> D1A[模式1:逐个输入]
    D1 --> D1B[模式2:一次性输入]
    
    D1A --> D1A1[输入请求数量]
    D1A --> D1A2[循环输入每个磁道号]
    D1A --> D1A3[实时验证和反馈]
    D1A --> D1A4[添加到请求序列]
    
    D1B --> D1B1[读取整行输入]
    D1B --> D1B2[解析空格分隔的磁道号]
    D1B --> D1B3[验证每个磁道号]
    D1B --> D1B4[处理无效输入询问重新输入]
    D1B --> D1B5[保持原始输入顺序]
    D1B --> D1B6[显示输入统计信息]
    
    D2 --> D2A[类型验证整数转换]
    D2 --> D2B[格式验证无多余字符]
    D2 --> D2C[范围验证0到maxTrack]
    
    E --> E1[FCFS算法]
    E --> E2[SSTF算法]
    E --> E3[SCAN算法]
    E --> E4[批量比较功能compareAll]
    
    E1 --> E1A[检查请求序列非空]
    E1 --> E1B[按顺序访问每个请求]
    E1 --> E1C[计算每步移动距离]
    E1 --> E1D[累计总移动距离]
    E1 --> E1E[调用displayResult显示结果]
    
    E2 --> E2A[检查请求序列非空]
    E2 --> E2B[初始化访问标记数组visited]
    E2 --> E2C[循环查找最近未访问请求]
    E2 --> E2D[更新访问标记和当前位置]
    E2 --> E2E[累计总移动距离]
    E2 --> E2F[调用displayResult显示结果]
    
    E3 --> E3A[检查请求序列非空]
    E3 --> E3B[排序请求序列sort]
    E3 --> E3C[分离左右两侧请求]
    E3 --> E3D[根据方向决定访问顺序]
    E3 --> E3E[累计总移动距离]
    E3 --> E3F[调用displayResult显示结果]
    
    E3D --> E3D1[方向=1:先右后左<br/>使用反向迭代器rbegin]
    E3D --> E3D2[方向=-1:先左后右<br/>使用反向迭代器rbegin]
    
    E4 --> E4A[依次调用FCFS]
    E4 --> E4B[依次调用SSTF]
    E4 --> E4C[依次调用SCAN]
    E4 --> E4D[显示对比结果]
    
    F --> F1[显示系统设置displaySettings]
    F --> F2[显示算法结果displayResult]
    
    F1 --> F1A[当前磁头位置]
    F1 --> F1B[磁头移动方向]
    F1 --> F1C[最大磁道号]
    F1 --> F1D[请求序列格式化显示每行8个]
    
    F2 --> F2A[算法名称和基本信息]
    F2 --> F2B[访问顺序箭头连接自动换行]
    F2 --> F2C[统计信息]
    F2 --> F2D[详细移动过程表]
    
    F2C --> F2C1[磁头移动总磁道数]
    F2C --> F2C2[平均寻道长度]
    
    F2D --> F2D1[步骤编号]
    F2D --> F2D2[起始磁道]
    F2D --> F2D3[目标磁道]
    F2D --> F2D4[移动距离]
    
    G --> G1[主循环while true]
    G --> G2[菜单显示displayMenu]
    G --> G3[用户选择处理switch-case]
    G --> G4[退出处理case 0]
    
    style A fill:#e1f5ff,stroke:#01579b,stroke-width:3px
    style B fill:#fff4e1,stroke:#e65100
    style C fill:#e8f5e9,stroke:#2e7d32
    style D fill:#e8f5e9,stroke:#2e7d32
    style E fill:#e8f5e9,stroke:#2e7d32
    style F fill:#e8f5e9,stroke:#2e7d32
    style G fill:#fce4ec,stroke:#880e4f
```					
