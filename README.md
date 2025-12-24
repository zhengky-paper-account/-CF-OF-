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

# 4.1 程序实现流程图

## 4.1.3 主控流程图

```mermaid
flowchart TD
    开始([程序开始]) --> 初始化编码[设置控制台编码为UTF-8]
    初始化编码 --> 读取输入[读取标准输入到字符串input]
    读取输入 --> 检查输入{输入为空?}
    检查输入 -->|是| 报错输入为空[报错: 输入为空]
    检查输入 -->|否| 创建词法分析器[创建Lexer对象]
    创建词法分析器 --> 执行词法分析[执行词法分析lx.run<br/>生成Token序列]
    执行词法分析 --> 检查Token{Token序列为空?}
    检查Token -->|是| 报错无Token[报错: 没有识别到任何Token]
    检查Token -->|否| 执行语法分析[执行语法分析parseSLR<br/>同时进行语义分析]
    执行语法分析 --> 检查结果{分析成功?}
    检查结果 -->|是| 输出中间代码[输出中间代码四元式]
    检查结果 -->|否| 输出错误信息[输出错误信息]
    输出中间代码 --> 结束([程序结束])
    输出错误信息 --> 结束
    报错输入为空 --> 结束
    报错无Token --> 结束
```

## 4.1.4 语法分析与语义分析结合流程图

```mermaid
flowchart TD
    开始([开始语法分析]) --> 初始化分析表[初始化SLR分析表<br/>构建ACTION和GOTO表]
    初始化分析表 --> 初始化三栈[初始化三个栈<br/>状态栈: 0<br/>符号栈: 栈底标记<br/>语义栈: 栈底标记]
    初始化三栈 --> 设置Token索引[设置Token索引为0]
    设置Token索引 --> 循环判断{Token索引未越界?}
    循环判断 -->|否| 报错未处理[报错: 输入未完全处理]
    循环判断 -->|是| 获取Token[获取当前Token]
    获取Token --> 转换为符号[将Token转换为符号编码]
    转换为符号 --> 获取状态[获取状态栈栈顶状态]
    获取状态 --> 查ACTION表[查ACTION表<br/>action = ACTION状态, 符号]
    查ACTION表 --> 判断动作{ACTION值}
    判断动作 -->|0| 接受[分析成功接受]
    判断动作 -->|-999| 报错语法错误[报错: 语法错误<br/>输出期望符号]
    判断动作 -->|>0| 移进操作[执行移进操作]
    判断动作 -->|<0| 归约操作[执行归约操作]
    移进操作 --> 压入状态栈[将转移状态压入状态栈]
    压入状态栈 --> 压入符号栈[将输入符号压入符号栈]
    压入符号栈 --> 压入语义栈[将Token词法值压入语义栈<br/>保存属性值]
    压入语义栈 --> 移动Token索引[Token索引加1]
    移动Token索引 --> 循环判断
    归约操作 --> 获取产生式[获取归约产生式编号]
    获取产生式 --> 检查栈元素{栈中元素足够?}
    检查栈元素 -->|否| 报错栈不足[报错: 栈元素不足]
    检查栈元素 -->|是| 弹出栈元素[从三个栈中弹出产生式长度个元素<br/>保存为右部语义值rhsVals]
    弹出栈元素 --> 反转顺序[反转rhsVals顺序<br/>使其与产生式右部顺序一致]
    反转顺序 --> 检查语义动作{产生式有语义动作?}
    检查语义动作 -->|是| 执行语义动作[调用语义动作函数<br/>newVal = semanticAction调用rhsVals<br/>生成中间代码]
    检查语义动作 -->|否| 直接传递[直接传递第一个子节点属性值<br/>newVal = rhsVals第0个元素]
    执行语义动作 --> 查GOTO表[查GOTO表<br/>gotoState = GOTO当前状态, 产生式左部]
    直接传递 --> 查GOTO表
    查GOTO表 --> 压入新状态[将gotoState压入状态栈]
    压入新状态 --> 压入非终结符[将产生式左部压入符号栈]
    压入非终结符 --> 压入新属性值[将newVal压入语义栈<br/>保存父节点属性值]
    压入新属性值 --> 循环判断
    接受 --> 输出成功[输出分析成功信息]
    输出成功 --> 结束([语法分析完成])
    报错语法错误 --> 结束
    报错栈不足 --> 结束
    报错未处理 --> 结束
```

## 4.1.5 语义动作执行流程图

```mermaid
flowchart TD
    开始([归约时执行语义动作]) --> 获取右部语义值[从语义栈获取右部语义值序列rhsVals]
    获取右部语义值 --> 检查语义动作{产生式有语义动作?}
    检查语义动作 -->|否| 直接传递[直接传递rhsVals第0个元素]
    检查语义动作 -->|是| 调用语义函数[调用语义动作函数<br/>newVal = semanticAction调用rhsVals]
    调用语义函数 --> 提取属性值[从rhsVals中提取子节点属性值]
    提取属性值 --> 判断产生式类型{产生式类型}
    判断产生式类型 -->|赋值语句| 生成赋值四元式[生成赋值四元式<br/>GEN =, E.place, 空, id.place]
    判断产生式类型 -->|算术表达式| 生成临时变量[生成临时变量Newtemp调用]
    生成临时变量 --> 生成算术四元式[生成算术运算四元式<br/>GEN+, E1.place, T.place, E.place]
    判断产生式类型 -->|比较表达式| 记录比较信息[记录比较表达式信息<br/>result.left, result.right, result.op]
    判断产生式类型 -->|DO-WHILE| 生成跳转四元式[生成跳转四元式<br/>GEN j<等, E.left, E.right, stmtBeginQuad行号]
    生成赋值四元式 --> 计算父节点属性值[计算父节点属性值<br/>result.name, result.beginLabel]
    生成算术四元式 --> 计算父节点属性值
    记录比较信息 --> 计算父节点属性值
    生成跳转四元式 --> 计算父节点属性值
    直接传递 --> 返回新属性值[返回新的语义值newVal]
    计算父节点属性值 --> 返回新属性值
    返回新属性值 --> 结束([语义动作执行完成])
```

