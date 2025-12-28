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
graph
    A[请求页式管理缺页中断模拟程序] --> B[输入模块]
    A --> C[算法选择模块]
    A --> D[页面置换算法模块]
    A --> E[状态记录模块]
    A --> F[输出模块]
    
    B --> B1[手动输入子模块]
    B --> B2[示例数据子模块]
    B1 --> B11[物理页框数输入]
    B1 --> B12[页面访问序列输入]
    B2 --> B21[默认页框数设置]
    B2 --> B22[经典测试序列加载]
    
    C --> C1[菜单显示]
    C --> C2[用户选择处理]
    C --> C3[算法调用]
    
    D --> D1[FIFO算法]
    D --> D2[LRU算法]
    D --> D3[OPT算法]
    D --> D4[Random算法]
    D1 --> D11[循环队列管理]
    D1 --> D12[页面置换逻辑]
    D2 --> D21[双向链表维护]
    D2 --> D22[哈希表查找]
    D2 --> D23[页面更新逻辑]
    D3 --> D31[未来序列查找]
    D3 --> D32[最优页面选择]
    D4 --> D41[访问计数维护]
    D4 --> D42[最少访问页面选择]
    
    E --> E1[内存状态记录]
    E --> E2[缺页次数统计]
    E --> E3[淘汰页号记录]
    
    F --> F1[基本信息输出]
    F --> F2[内存状态表输出]
    F --> F3[淘汰页号输出]
```
