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

# 3.3 语义分析方法流程图

## 3.3.2 语义动作执行流程图

```mermaid
flowchart TD
    开始([开始执行语义动作]) --> 获取产生式[获取产生式信息]
    获取产生式 --> 检查语义动作{产生式有语义动作?}
    检查语义动作 -->|否| 直接传递[直接传递第一个子节点属性值<br/>newVal = rhsVals第0个元素]
    检查语义动作 -->|是| 调用语义函数[调用语义动作函数<br/>newVal = semanticAction(rhsVals)]
    调用语义函数 --> 提取属性值[从rhsVals中提取子节点属性值]
    提取属性值 --> 计算属性值[计算父节点的属性值]
    计算属性值 --> 生成中间代码[生成中间代码四元式]
    生成中间代码 --> 返回结果[返回新的语义值]
    直接传递 --> 返回结果
    返回结果 --> 结束([语义动作执行完成])
```

## 3.3.3 属性值传递流程图

```mermaid
flowchart TD
    开始([开始归约]) --> 获取产生式[获取产生式编号和长度]
    获取产生式 --> 检查栈元素{语义栈元素足够?}
    检查栈元素 -->|否| 报错栈不足[报错: 语义栈元素不足]
    检查栈元素 -->|是| 弹出元素[从语义栈中弹出产生式长度个元素<br/>保存为rhsVals]
    弹出元素 --> 反转顺序[反转rhsVals顺序<br/>使其与产生式右部顺序一致]
    反转顺序 --> 执行语义动作[执行语义动作<br/>计算父节点属性值]
    执行语义动作 --> 压入新值[将新的语义值压入语义栈]
    压入新值 --> 结束([属性值传递完成])
    报错栈不足 --> 结束
```

## 3.3.4 中间代码生成流程图

```mermaid
flowchart TD
    开始([需要生成四元式]) --> 判断操作类型{操作类型}
    判断操作类型 -->|算术运算| 生成算术四元式[生成算术运算四元式<br/>op, arg1, arg2, result]
    判断操作类型 -->|赋值| 生成赋值四元式[生成赋值四元式<br/>=, value, , target]
    判断操作类型 -->|跳转| 生成跳转四元式[生成跳转四元式<br/>j/jz/j<等, arg1, arg2, target]
    生成算术四元式 --> 添加到列表[将四元式添加到quads列表]
    生成赋值四元式 --> 添加到列表
    生成跳转四元式 --> 添加到列表
    添加到列表 --> 结束([四元式生成完成])
```

## 3.3.5 临时变量生成流程图

```mermaid
flowchart TD
    开始([需要生成临时变量]) --> 增加计数器[tempCount++]
    增加计数器 --> 生成变量名[生成变量名<br/>name = "t" + to_string(tempCount)]
    生成变量名 --> 返回变量名[返回临时变量名]
    返回变量名 --> 结束([临时变量生成完成])
```

## 3.3.6 赋值语句语义动作流程图

```mermaid
flowchart TD
    开始([归约Assign产生式]) --> 提取标识符[提取id的属性值<br/>id_place = rhs第0个元素.name]
    提取标识符 --> 提取表达式[提取E的属性值<br/>E_place = rhs第2个元素.name]
    提取表达式 --> 生成赋值四元式[生成赋值四元式<br/>GEN=, E_place, , id_place]
    生成赋值四元式 --> 记录开始位置[记录表达式开始位置<br/>result.beginLabel = E.beginLabel]
    记录开始位置 --> 返回结果[返回语义值<br/>result.name = id_place]
    返回结果 --> 结束([赋值语句语义动作完成])
```

## 3.3.7 算术表达式语义动作流程图

```mermaid
flowchart TD
    开始([归约算术表达式产生式]) --> 提取左操作数[提取左操作数属性值<br/>E1_place = rhs第0个元素.name]
    提取左操作数 --> 提取右操作数[提取右操作数属性值<br/>T_place = rhs第2个元素.name]
    提取右操作数 --> 生成临时变量[生成临时变量<br/>E_place = Newtemp]
    生成临时变量 --> 生成算术四元式[生成算术运算四元式<br/>GEN+, E1_place, T_place, E_place]
    生成算术四元式 --> 记录开始位置[记录表达式开始位置<br/>result.beginLabel = E1.beginLabel]
    记录开始位置 --> 返回结果[返回语义值<br/>result.name = E_place]
    返回结果 --> 结束([算术表达式语义动作完成])
```

## 3.3.8 比较表达式语义动作流程图

```mermaid
flowchart TD
    开始([归约比较表达式产生式]) --> 提取左操作数[提取左操作数<br/>result.left = rhs第0个元素.name]
    提取左操作数 --> 提取运算符[提取运算符<br/>result.op = rhs第1个元素.name]
    提取运算符 --> 提取右操作数[提取右操作数<br/>result.right = rhs第2个元素.name]
    提取右操作数 --> 设置空名称[设置name为空<br/>result.name = ""]
    设置空名称 --> 返回结果[返回语义值]
    返回结果 --> 结束([比较表达式语义动作完成])
```

## 3.3.9 DO-WHILE语句语义动作流程图

```mermaid
flowchart TD
    开始([归约DoWhile产生式]) --> 获取循环起始[获取循环体起始行号<br/>stmtBeginQuad = rhs第1个元素.beginLabel]
    获取循环起始 --> 提取条件表达式[提取条件表达式E<br/>E_val = rhs第4个元素]
    提取条件表达式 --> 判断表达式类型{E是比较表达式?}
    判断表达式类型 -->|是| 生成条件跳转[生成条件跳转四元式<br/>GENj + E.op, E.left, E.right, stmtBeginQuad]
    判断表达式类型 -->|否| 计算退出位置[计算退出位置<br/>exitQuad = quads.size + 2]
    计算退出位置 --> 生成零跳转[生成零跳转四元式<br/>GENjz, E.name, , exitQuad]
    生成零跳转 --> 生成无条件跳转[生成无条件跳转四元式<br/>GENj, , , stmtBeginQuad]
    生成条件跳转 --> 记录开始位置[记录循环开始位置<br/>result.beginLabel = stmtBeginQuad]
    生成无条件跳转 --> 记录开始位置
    记录开始位置 --> 返回结果[返回语义值]
    返回结果 --> 结束([DO-WHILE语句语义动作完成])
```

