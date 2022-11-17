### (TCNS2022) Distributed Resilent Oberver-based Fault-Tolerant Control for Heterogenneous Multiagent Systems Under Actuator Faults and DoS Attacks, Chao Deng and Changyun Wen

### 论文特点与研究内容

* 研究了执行器故障和DoS攻击下 **异质线性多智能体系统（heterogeneous MASs）** 的容错控制问题；
* 提出了一种弹性自适应的分布式观测器来估计系统矩阵和外系统状态；
* 使用驻留时间技术和李雅普诺夫稳定性理论证明了即使是在DOS攻击下，观测误差系统依然是指数稳定的；
* 提出了一种对攻击抵御性最强的观测器参数设计算法；
* 提出了一种不会引起震颤行为（chattering behaviors）的容错控制器来抵御执行器故障；
* **解决了协同容错输出调节问题**；
  
### 现有研究

* 多智能体系统的分布式状态反馈协同输出调节在TAC2012中已经研究；
* 更一般的输出反馈协同输出调节在[1][2]中有研究；
* 鲁棒协同输出调节、自适应协同输出调节都有广泛研究；
* **网络攻击的因素未能考虑在系统的协同输出调节控制问题中，特别是只有部分智能体与外系统有联系的情形**；
* 多智能体系统的网络安全问题已有广泛研究：包括分布式一致性、安全协同事件触发控制问题等；
* 有向图连接下的多智能体系统的分布式故障观测器设计已有研究；
* 文献[3] (Auto2019Yang)给出了保证调节方程可解性的充分条件，并设计了带有容错函数的控制器来抵御执行器 loss-of-effectiveness 故障和outage故障（中断故障）。但所得结果仅适用于同质多智能体系统(homogeneous MASs)。同时，在分布式容错控制器中采用的 **$\sigma$ 修正技术** 会产生震颤行为（这会造成控制所需能量增加，在实际应用中应该避免）。

### 存在的问题  
* 已有的容错控制方法并不能用以解决系统的**容错输出调节问题**，主要难点在于：1）多智能体的调节方程（regulator equations）可解性会被故障影响；2）来抵御执行器故障的基于容错函数的控制器的设计是否可行？
* 

### 主要难点
* 自适应分布式观测器互相耦合，且被DoS攻击影响 ；

### 主要工作与贡献
* 首次考虑了物理层发生故障、网络层发生DoS攻击的异质多智能体的弹性容错控制问题，提出了一种分布式弹性观测器依赖的容错控制方法；
* 使用一个预报器（predictor）来记录图的边是否被攻击，在此基础上设计了弹性自适应分布式控制器，基于LMI技术提出了一种能够最大化抵御攻击的算法；
* 设计了一种无震颤行为的容错控制器，证明了基于所提出的引理所给算法能够解决**协同容错输出调节问题**。

### 网络攻击的概念
* **攻击更容易发生在网络层**；
* **欺骗攻击：** 伪造通信数据，包括零动态攻击(zero-dynamic attacks)、偏差注入攻击(bias injection attacks)；   
* **DoS攻击：** 阻断传输通道，研究更为广泛，因为更容易实现（they invovle more reachable patterns）；

### 容错控制的概念
* **故障往往发生在物理层**

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
[3] Deng C, Yang G H. Distributed adaptive fault-tolerant control approach to cooperative output regulation for linear multi-agent systems[J]. Automatica, 2019, 103: 62-68.