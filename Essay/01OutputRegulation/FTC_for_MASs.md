### (TCNS2022) Distributed Resilent Oberver-based Fault-Tolerant Control for Heterogenneous Multiagent Systems Under Actuator Faults and DoS Attacks, Chao Deng and Changyun Wen

### 论文特点与研究内容

* 研究了执行器故障和DoS攻击下 异质线性多智能体系统的容错控制问题；
* 提出了一种弹性自适应的分布式观测器来估计系统矩阵和外系统状态；
* 使用驻留时间技术和李雅普诺夫稳定性理论证明了即使是在DOS攻击下，观测误差系统依然是指数稳定的；
* 提出了一种对攻击抵御性最强的观测器参数设计算法；
* 提出了一种不会引起震颤行为（chattering behaviors）的容错控制器来抵御执行器故障；
* 协同容错输出调节问题；
  
### 文献调研

* 分布式状态反馈协同输出调节在TAC2012中已经研究；
* 更一般的输出反馈协同输出调节在[1][2]中有研究；
* 鲁棒协同输出调节、自适应协同输出调节都有广泛研究；

### 图论术语
* **有向图：** $\mathcal{G} = (\mathcal{V},\epsilon)$，其中 $\mathcal{V}=\left\{ 1,2,...,N\right\}$ 为节点集合，$\epsilon \subset \mathcal{V} \times \mathcal{V}$ 表示边集合，从节点 $i$ 到 $j$ 的边记为 $(i,j)$； 

* **有向树：** 一种有向图，图中除了根节点没有父节点，其余节点均有一个确定的父节点，且从根节点出发每个子节点都是可达的（reachable）；

* **节点 $i_1$ 到节点 $i_{k+1}$ 可达：** 存在一条路径 $(i_1,i_2)$, $(i_2,i_3)$, $\cdots $, $(i_k, i_{k+1})$；

* **子图：** $\mathcal{G}_s = (\mathcal{V}_s,\epsilon_s)$ 称作 $\mathcal{G} = (\mathcal{V},\epsilon)$ 的子图，如果 $\mathcal{V}_s \subset \mathcal{V}$ ，且 $\epsilon_s \subset \epsilon \cap \mathcal{V}_s \times \mathcal{V}_s$ ；

* **有向生成树：** 是子图，也是有向树，且 $\mathcal{V}_s = \mathcal{V}$；

* 有向图 $\mathcal{G}$ 包含一条有向生成树 当且仅当 $\mathcal{G}$ 至少有一个节点能够达到其余每一个节点。

* **加权邻接矩阵：** $\mathcal{A} = [a_{ij}] \in \mathbb{R}^{N\times N}$，其中 $a_{ii}=0$； $a_{ij}>0$ 当且仅当 $(j,i)\in \epsilon$；

* **入度矩阵：** $D=diag \left\{ D_1,\cdots,D_N \right\}$，其中 $D_i = \sum_{j=1}^Na_{ij}$；
·
* **拉普拉斯矩阵：** $\mathcal{L} = [l_{ij}] \in \mathbb{R}^{N\times N}$，其中 $l_{ii}=\sum_{j=1}^Na_{ij}$； $l_{ij}= - a_{ij}$， $\mathcal{L} = D - \mathcal{A}$；
* 拉普拉斯矩阵 $\mathcal{L} = [l_{ij}] \in \mathbb{R}^{N\times N}$ 至少有一个特征值为零，且非零特征值均具有正实部；
* 拉普拉斯矩阵 $\mathcal{L} = [l_{ij}] \in \mathbb{R}^{N\times N}$ 有一个特征值为零，其余 $N-1$ 个特征值均具有正实部 当且仅当有向图 $\mathcal{G}$ 包含一棵有向生成树[1]；
 
* 对任意一个矩阵 $\mathcal{A} = [a_{ij}] \in \mathbb{R}^{N\times N}$，其中 $a_{ii}=0$； $a_{ij}>0$ 总能定义一个有向图 $\mathcal{G} = (\mathcal{V},\epsilon)$ 使得 $\mathcal{A}$ 成为其邻接矩阵。


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



### 参考文献
[1] Li Z, Chen M Z Q, Ding Z. Distributed adaptive controllers for cooperative output regulation of heterogeneous agents over directed graphs[J]. Automatica, 2016, 68: 179-183.
