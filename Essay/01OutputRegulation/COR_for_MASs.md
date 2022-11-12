### (TAC2012) Cooperative Output Regulation of Linear Multi-Agent Systems, Youfeng Su and Jie Huang

#### 1. 引言
**线性多智能体系统模型**：

$$ \begin{aligned}\dot{x}_i &=A_i x_i+B_i u_i+E_i \\
e_i &=C_i x_i+D_i u_i+F_i v . \quad i=1, \ldots, N\end{aligned} \tag{1.1} $$

**外系统模型**：

$$ \dot{v}=Sv \tag{1.2} $$

**协同输出调节控制的目的**： 设计分布式控制器，使得**闭环系统稳定（外部信号 $v=0$ 时），且跟踪误差 $e_i$ 渐近收敛到0**.

**输出调节控制问题的常用求解方法**：
* 前馈法(feedforward design)：对于一个含有 $N$ 个子系统的多智能体系统 $(1.1)$ ， 如果将子系统分为两类，一类是控制信号 $u_i$ 能够获取外部信号 $v$ ，另一类无法获取取外部信号 $v$ ，则**基于前馈设计的分散式控制方法**无法解决第二类子系统的OR问题。
  
* 内模法(internal model design)：基于内模法的OR问题的可解性要求满足传零条件（transmission zero condition）
      
    $$ \operatorname{rank}\left[\begin{array}{cc}
        A_i-\lambda I & B_i \\
        C_i & D_i
        \end{array}\right]=n_i+p_i, \quad \forall \quad \lambda \in \sigma(S) $$ 

    其中 $\sigma(S)$ 表示 $S$ 的谱(spectrum)。 