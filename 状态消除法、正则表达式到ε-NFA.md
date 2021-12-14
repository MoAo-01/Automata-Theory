#### 由DFA到正则表达式，状态消除法

- 从DFA中逐个删除状态
- 用标记了正则表达式的新路径替换被删掉的路径
- 保持"自动机"等价



```mermaid
stateDiagram-v2
 	A1-->B1 :a
 	B1-->C1 :b
 	A2-->C2 :ab 	
```



```mermaid
stateDiagram-v2
 	A1-->B1 :a
 	A1-->B1 :a
 	A2-->B2 :a+b 	
```

```mermaid
stateDiagram-v2
	A1-->B1 :a
	B1-->B1 :c
	B1-->C1 :b
	A2-->C2 :ac*b
```



```mermaid
stateDiagram-v2
	P-->S :p
	R-->S :r
	S-->S :s
	S-->Q :q
	S-->T :t
	P'-->Q' :ps*q
	P'-->T' :ps*t
	R'-->Q' :rs*q
	R'-->T' :rs*t
```

利用状态消除法，构造下图自动机的正则表达式.

```mermaid
stateDiagram-v2
[*]-->q0
q0-->q0 :1
q0-->q1 :0
q1-->q2 :1
q2-->q1 :0
q2-->q0 :1
q1-->q1 :0
q2-->[*]
```



添加起始和结束的空转移：

```mermaid
stateDiagram-v2
[*]-->q0 :ε
q0-->q0 :1
q0-->q1 :0
q1-->q2 :1
q2-->q1 :0
q2-->q0 :1
q1-->q1 :0
q2-->[*] :ε
```

消除状态q1，添加路径q0→q2和q2→q2：

```mermaid
stateDiagram-v2
[*]-->q0 :ε
q0-->q0 :1

q0-->q2 :00*1
q2-->q2 :00*1 

q2-->q0 :1

q2-->[*] :ε
```

消除状态q0，添加路径s→q2和q2→q2：

```mermaid
stateDiagram-v2
[*]-->q2 :1*00*1
q2-->q2 :00*1+1100*1
q2-->[*] :ε
```

消除状态q2，添加路径s→f：

```mermaid
stateDiagram-v2
[*]-->[*] :1*00*1(00*1+1100*1)*
```



正则表达式(0+1)*1(0+1)构造ε-NFA.

```mermaid
stateDiagram-v2
	[*]-->q0
	q0-->q1 :ε
	q0-->q7 :ε
	
	q1-->q2 :ε
	q2-->q3 :0 
	q3-->q6 :ε
	
	q1-->q4 :ε
	q4-->q5 :1
	q5-->q6 :ε
	
	q6-->q1 :ε
	
	q6-->q7 :ε 
	q7-->q8 :ε
	q8-->q9 :1
	q9-->q10 :ε
	
	q10-->q11 :ε
	q11-->q12 :0
	q12-->[*] :ε
	
	q10-->q13 :ε
	q13-->q14 :1
	q14-->[*] :ε		
```

**任何一个DFA存在一个正则表达式，任何一个正则表达式存在一个DFA。**

#### 由正则表达式构造ε-NFA

任何正则表达式e，都存在与其等价的ε-NFA A，即L(A)=L(e)，并且A满足：

1. 仅有一个接受状态；
2. 没有进入开始状态的边；
3. 没有离开接受状态的边。

**正则表达式定义的语言，都可以被又穷自动机识别。**

归纳法可以证明，略。