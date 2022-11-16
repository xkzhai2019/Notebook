### (TAC2012) Cooperative Output Regulation of Linear Multi-Agent Systems, Youfeng Su and Jie Huang

### 论文特点与研究内容

* 考虑了两类子系统：一类能够接触外系统，另一类无法接触外系统



### 全文梗概
#### 1. 引言
**线性多智能体系统模型**：

$$ \begin{aligned}\dot{x}_i &=A_i x_i+B_i u_i+E_i \\
e_i &=C_i x_i+D_i u_i+F_i v . \quad i=1, \ldots, N\end{aligned} \tag{1.1} $$

* $x_i\in \mathbb{R}^{n_i}$：子系统状态；
* $e_i\in \mathbb{R}^{p_i}$：跟踪误差；
* $u_i\in \mathbb{R}^{m_i}$：控制输入；
* $v\in \mathbb{R}^{q}$：外部参考信号或待抑制的干扰.

**外系统模型**：

$$ \dot{v}=Sv \tag{1.2} $$

**协同输出调节控制的目的**： 设计分布式控制器，使得**闭环系统稳定（外部信号 $v=0$ 时），且跟踪误差 $e_i$ 渐近收敛到0**.

**输出调节控制问题的常用求解方法**：
* 前馈法(feedforward design)：对于一个含有 $N$ 个子系统的多智能体系统 $(1.1)$ ， 如果将子系统分为两类，一类是控制信号 $u_i$ 能够获取外部信号 $v$ ，另一类无法获取取外部信号 $v$ ，则**基于前馈设计的分散式控制方法**无法解决第二类子系统的OR问题。
  
* 内模法(internal model design)：基于内模法的OR问题的可解性要求满足传零条件（transmission zero condition）
      
    $$ \operatorname{rank}\left[\begin{array}{cc}
        A_i-\lambda I & B_i \\
        C_i & D_i
        \end{array}\right]=n_i+p_i, \quad \forall \lambda \in \sigma(S) $$ 

    其中 $\sigma(S)$ 表示 $S$ 的谱(spectrum)。 当$p_i>m_i$时，传零条件不会成立，所以此时OR问题也不能使用基于内模法的分散式控制器来求解。

**本文的结果：** 
* 采用一种分布式控制手段来解决问题，克服了第二类子系统无法获取外部信号 $v$ 带来的设计困难；


