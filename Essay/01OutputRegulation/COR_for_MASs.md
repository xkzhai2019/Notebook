### (TAC2012) Cooperative Output Regulation of Linear Multi-Agent Systems, Youfeng Su and Jie Huang

#### 1. 引言
**线性多智能体系统模型**：
$$ \begin{aligned}\dot{x}_i &=A_i x_i+B_i u_i+E_i \\
e_i &=C_i x_i+D_i u_i+F_i v . \quad i=1, \ldots, N
\end{aligned} $$

**外系统模型**：$$ \dot{v}=Sv $$

**协同输出调节控制的目的**： 设计分布式控制器，使得**闭环系统稳定（外部信号$v=0$时），且跟踪误差$e_i$渐近收敛到0**.

**输出调节控制问题的常用求解方法**：
* 前馈法(feedforward design)：对于一个
  
* 内模法(internal model design)
