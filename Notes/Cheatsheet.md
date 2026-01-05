# Cheatsheet

## 基础公理、条件概率、随机变量

### 概率公理与集合运算

**概率空间三元组**：$(\Omega, \mathcal{F}, P)$ 

**基本公理**：

1. 非负性：$P(A)\ge0$
2. 规范性：$P(\Omega)=1$
3. 可列可加性：若$A_1,A_2,\dots$互斥，则$P(\cup A_i)=\sum P(A_i)$

**常用性质**：

1. $P(A^c)=1-P(A)$
2. **容斥原理**：$P(A\cup B)=P(A)+P(B)-P(AB)$
3. **单调性**：若$A\sub B$，则$P(B-A)=P(B)-P(A)$

### 条件概率、全概率与贝叶斯

**条件概率定义**：$P(A\mid B)=\frac{P(AB)}{P(B)}$

**全概率公式**：设$B_1,B_2,\dots$构成样本空间$\Omega$的一个划分，则对任意事件$A$：$P(A)=\sum_iP(A\mid B_i)P(B_i)$

**贝叶斯公式——逆概率**：$P(B_i\mid A)=\frac{P(A\mid B_i)P(B_i)}{P(A)}=\frac{P(A\mid B_i)P(B_i)}{\sum_jP(A\mid B_j)P(B_j)}$

> 经典例题：疾病检测：
>
> 已知：
>
> - 先验概率：$P(D)=0.02$（患病率）
> - 敏感性：$P(T\mid D)=0.95$（有病检测出阳性）
> - 特异性：$P(T^c\mid D^c)=0.98\;\Rightarrow\;P(T\mid D^c)=0.02$（误诊率）
>
> 问题：检测为阳性$T$，实际患病的概率$P(D\mid T)$是多少？
>
> 解题步骤：
>
> 1. 用全概率公式求分母$P(T)=P(T\mid D)P(D)+P(T\mid D^c)P(D^c)$
> 2. 求贝叶斯公式的分子$P(T\mid D)P(D)$
> 3. 贝叶斯公式：$P(D\mid T)=\frac{P(T\mid D)P(D)}{P(T)}$
>
> 最终求解发现即使检测为阳性，实际患病概率不到50%，反直觉。

### 独立性

**事件独立性定义**：$A\perp B\;\Longleftrightarrow\;P(AB)=P(A)P(B)$

**条件独立性**：$A\perp B\mid C\;\Longleftrightarrow\;P(AB\mid C)=P(A\mid C)P(B\mid C)$ *注意：$A,B$独立不代表在$C$发生的条件下也独立，反之亦然。*

**三个事件相互独立**：需要同时满足两两独立(3个等式)且$P(ABC)=P(A)P(B)P(C)$ *注意：即使$P(ABC)=P(A)P(BC)$且$P(AB)=P(A)P(B)$，也不能推出三者相互独立，更不能推出$P(ABC)=P(A)P(B)P(C)$。*

### 随机变量

**累积分布函数(CDF)**：$F_X(x)=P(X\le x)$

**性质**：

- 单调不减：$x_1<x_2\Rightarrow F(x_1)\le F_(x_2)$
- 右连续：$\lim_{y\to x^+}F(Y)=F(X)$
- 两个极限：$\lim_{x\to-\infin}F(x)=0$ 和 $\lim_{x\to\infin}F(x)=1$

**离散型变量**：

- PMF：$p_X(k)=P(X=k)$
- CDF与PMF的关系：$F(x)=\sum_{x\le k}p_X(k)$

**连续性变量**：

- PDF：$f_X(x)=\frac{P(x\le X\le x+dx)}{dx}$
- PDF与CDF的关系：$F(X)=\int_{-\infin}^xf(t)dt$，$P(a<X\le b)=F(b)-F(a)$

> 经典例题：混合型随机变量的CDF
>
> 场景：投硬币觉醒坐火车还是汽车：硬币正面则火车，到达时间$X\sim\mathcal{U}(20,25)$；硬币反面则汽车，到达时间$X\sim\mathcal{U}(15,30)$。求$X$的CDF$F_X(x)$
> $$
> F_X(x)=0.5\cdot F_{\text{Train}}(x)+0.5\cdot F_{\text{Car}}(x)
> $$
> 问：CDF总是连续吗？不一定。这里$F_X(x)$是一条连续的曲线，因为两个均匀分布覆盖了区间，且概率权重平滑过渡，但是如果一种情况是离散的点质量，CDF会出现阶梯。

## 常用分布

### 常用离散分布

| 分布名称 | 符号                    | PMF $P(X=k)$                        | 期望 $\mathbb{E}[X]$ | 方差 $\mathrm{Var}(X)$ | 备注                                |
| -------- | ----------------------- | ----------------------------------- | -------------------- | ---------------------- | ----------------------------------- |
| 伯努利   | $\mathrm{Ber}(p)$       | $p^k(1-p)^k$                        | $p$                  | $p(1-p)$               | 一次实验，成功为1                   |
| 二项     | $\mathrm{Bin}(n,p)$     | ${n\choose k}p^k(1-p)^{n-k}$        | $np$                 | $np(1-p)$              | $n$次独立$\mathrm{Ber}$实验成功次数 |
| 几何     | $\mathrm{Geo}(p)$       | $(1-p)^{k-1}p^k$                    | $\frac{1}{p}$        | $\frac{1-p}{p^2}$      | 第1次成功所需试验次数               |
| 负二项   | $\mathrm{NB}(r,p)$      | ${k-1\choose r-1}p^r(1-p)^{k-r}$    | $\frac{r}{p}$        | $\frac{r(1-p)}{p^2}$   | 第$r$次成功所需试验次数             |
| 泊松     | $\mathrm{Poi}(\lambda)$ | $\frac{\lambda^k e^{-\lambda}}{k!}$ | $\lambda$            | $\lambda$              | 稀有事件计数                        |

**几何分布的无记忆性**：$P(X>m+n\mid X>m)=P(X>n)$。这意味着“如果你已经失败了$m$次，再失败$n$次的概率就像重新开始一样”。指数分布也有这个性质。

**泊松近似**：当$n\to\infin,\;p\to0,\;np=\lambda$时，二项分布可以用泊松分布近似。

### 常用连续分布

| 分布名称 | 符号                        | PDF $f_X(x)$                                                 | 期望 $\mathbb{E}[X]$ | 方差 $\mathrm{Var}(X)$ | 备注                                               |
| -------- | --------------------------- | ------------------------------------------------------------ | -------------------- | ---------------------- | -------------------------------------------------- |
| 均匀     | $\mathcal{U}(a,b)$          | $\frac{1}{b-a}$                                              | $\frac{a+b}{2}$      | $\frac{(b-a)^2}{12}$   | 概率在区间内平均分布                               |
| 指数     | $\mathrm{Exp}(\lambda)$     | $\lambda e^{-\lambda x}$                                     | $\frac{1}{\lambda}$  | $\frac{1}{\lambda^2}$  | 等待时间模型                                       |
| 正态     | $\mathcal{N}(\mu,\sigma^2)$ | $\frac{1}{\sqrt{2\pi}\sigma}e^{-\frac{(x-\mu)^2}{2\sigma^2}}$ | $\mu$                | $\sigma^2$             | 中心极限定理的基础；标准化$Z=\frac{x-\mu}{\sigma}$ |

如果随机变量$T$有恒定的失效率$h(t)=\lambda$，则$T$必定服从指数分布。$P(T>t)=e^{-\lambda t}$

### 泊松过程

记$N_t$为$[0,t]$时间内的到达数，速率为$\lambda$。

1. **计数分布**：$N_t\sim\mathrm{Poi}(\lambda t)$

2. **间隔时间**：到达之间的时间间隔$T_1,T_2,\dots$是i.i.d的$\mathrm{Exp}(\lambda)$随机变量。

3. **条件分布**：给定$N_t=n$（即在时间$t$内发生了$n$次到达），这$n$个到达的时间点在$[0,t]$上是**独立同分布且均匀分布**的顺序统计量。即对于$0<s<t$，给定$N_t=n$，在$[0,s]$内到达的数量$k$服从二项分布$\mathrm{Bin}(n,\frac{s}{t})$
   $$
   P(N_s=k\mid N_t=n)={n\choose k}\left( \frac{s}{t} \right)^k\left( 1-\frac{s}{t} \right)^{n-k}
   $$

> 条件分布的推导过程：假设$N_t=n$，要推导$P(N_s=k\mid N_t=n)$的公式：
> $$
> \begin{aligned}
> P(N_s=k\mid N_t=n)&=\frac{P(N_s=k\cap N_t=n)}{P(N_t=n)}
> \\[5pt]
> &=\frac{P(N_s=k)P(N_t-N_s=n-k)}{P(N_t=n)}
> \\[5pt]
> &=\frac{(\lambda s)^{k}e^{-\lambda s}}{k!}\cdot\frac{[\lambda(t-s)]^{n-k}e^{-\lambda(t-s)}}{(n-k)!}\cdot\frac{n!}{(\lambda t)^ne^{-\lambda t}}
> \\[5pt]
> &={n\choose k}\left( \frac{s}{t} \right)^k\left( 1-\frac{s}{t} \right)^{n-k}\sim\mathrm{Bin}\left( n,\frac{s}{t} \right)
> \end{aligned}
> $$

## 分布变换

### 线性变换法

如果$U\sim\mathcal{U}(0,1)$，生成任意区间$[a,b]$的均匀分布：$X=a+(b-a)U$

### 逆变换法

**原理**：如果目标是分布$X$，其CDF是$F(x)$。只要生成一个均匀分布$U\sim\mathcal{U}(0,1)$，然后令：$X=F^{-1}(U)$，那么$X$就会服从目标分布。

**直观理解**：CDF的纵坐标$F(x)$的取值范围正好是$[0,1]$。如果你在纵轴上均匀地随机撒点（生成$U$），然后水平投射到CDF曲线上，再垂直投影到横轴，得到的$X$密度就会正好落在CDF陡峭的地方（概率密度大）。

> 经典例题：生成指数分布$\mathrm{Exp}(\lambda)$
>
> 步骤：
>
> 1. 求CDF：$F(x)=1-e^{-\lambda x}$
> 2. 令$u=F(x)$，即$u=1-e^{-\lambda x}$。
> 3. 反解$x$：$x=-\frac{1}{\lambda}\ln(1-u)$

### 高斯分布

**标准正态**$\mathcal{N}(0,1)$：生成$U_1,U_2\sim\mathcal{U}(0,1)$：$Z=\sqrt{-2\ln U_1}\cos(2\pi U_2)$

**一般正态**$\mathcal{N}(\mu,\sigma^2)$：$X=\mu+\sigma Z$

## 多维随机变量

### 联合分布

**离散型**：

- 联合概率质量函数(Joint PMF)：$p_{X,Y}(x,y)=P(X=x,Y=y)$
- 边缘PMF：$P_X(x)=\sum_yp_{X,Y}(x,y)$（对固定$x$，$y$求和）

**连续型**：

- 联合概率密度函数(Joint PDF)：$f_{X,Y}(x,y)$
- 性质：$f(x,y)\ge0,\;\iint f(x,y)dxdy=1$
- 概率计算：$P((X,Y)\in A)=\iint_Af(x,y)dxdy$
- 边缘PDF：$f_X(x)=\int_{-\infin}^{\infin}f(x,y)dy$（对固定$x$，$y$积分）

### 独立性

**定义**：$X$与$Y$独立 $\Longleftrightarrow\; f_{X,Y}(x,y)=f_X(x)f_Y(y)$（对所有的$x,y$成立）

**判断技巧**：若联合PDF可以写成$g(x)h(y)$，且定义域是矩形区域，则独立。

### 条件分布

**离散型**：$p_{Y\mid X}(y\mid x)=\frac{p_{X,Y}(x,y)}{p_X(x)}$

**连续型**：$f_{Y\mid X}(y\mid x)=\frac{f_{X,Y}(x,y)}{f_X(x)}$ *注意，在计算时，先计算边缘分布$f_X(x)$，再作为分母。*

### 独立随机变量之和(卷积公式)

若$X,Y$独立，令$Z=X+Y$。

- **离散型**（和分布）：$p_Z(z)=\sum_kp_X(k)p_Y(z-k)$
- **连续型**（卷积）：$f_Z(z)=\int_{-\infin}^{\infin}f_X(x)f_Y(z-x)dx$ *技巧：确定$x$的取值范围，使得$f_X(x)>0$且$f_Y(z-x)>0$*

### 随机变量函数的联合分布

若$(X,Y)\to(U,V)$是一一对应变换，反函数为$x=g(u,v),y=h(u,v)$，则

**联合PDF**：$f_{U,V}(u,v)=f_{X,Y}(g(u,v),h(u,v))\cdot|J|$

**Jacobian行列式**：$J=\det\begin{vmatrix} \frac{\partial x}{\partial u} & \frac{\partial x}{\partial v} \\ \frac{\partial y}{\partial u} & \frac{\partial y}{\partial v} \end{vmatrix}$，这里的偏导数是反函数对$u,v$求导，千万别反了！

> 经典例题：假设$X,Y$是独立且均服从$\mathcal{U}(0,1)$，求$Z=X+Y$的PDF。
>
> 利用卷积公式：$f_Z(z)=\int_{-\infin}^{\infin}f_X(x)f_Y(z-x)dx$。
>
> 分析非零区域：
>
> - $f_X(x)$非零需要$0\le x\le 1$
> - $f_Y(z-x)$非零需要$0\le z-x\le 1$，即$x\le z\le x+1$
>
> 分段讨论：
>
> - 当$0\le z\le 1$时，$0\le x\le z$即可，则$f_Z(z)=\int_0^z1\cdot1dx=z$
> - 当$1<z\le 2$时，$z-1\le x\le 1$即可，则$f_Z(z)=\int_{z-1}^11\cdot 1dx=2-z$

## 数字特征

### 期望与方差

**期望的线性性质**（无论是否独立都成立）：$\mathbb{E}[aX+bY+c]=a\mathbb{E}[X]+b\mathbb{E}[Y]+c$

**期望的乘积性质**（只有在各变量独立时成立）：$\mathbb{E}[XY]=\mathbb{E}[X]\mathbb{E}[Y]$

**方差的性质**：$\mathrm{Var}(aX+b)=a^2\mathrm{Var}(X)$

**方差的计算**：$\mathrm{Var}(X)=\mathbb{E}[X^2]-(\mathbb{E}[X])^2\ge0$

### 协方差

**定义**：$\mathrm{Cov}(X,Y)=\mathbb{E}[(X-\mu_X)(Y-\mu_Y)]=\mathbb{E}[XY]-\mathbb{E}[X]\mathbb{E}[Y]$

**性质**：

- 对称性：$\mathrm{Cov}(X,Y)=\mathrm{Cov}(Y,X)$，$\mathrm{Cov}(X,X)=\mathrm{Var}(X)$
- 线性性质：$\mathrm{Cov}(aX+b,cY+d)=ac\cdot\mathrm{Cov}(X,Y)$
- 和的方差：$\mathrm{Var}(X\pm Y)=\mathrm{Var}(X)+\mathrm{Var}(Y)\pm2\mathrm{Cov}(X,Y)$

只有当$\mathrm{Cov}(X,Y)=0$，即两个变量相互独立时，才有$\mathrm{Var}(X\pm Y)=\mathrm{Var}(X)\pm\mathrm{Var}(Y)$

推广到$n$个i.i.d.变量：若$X_1,X_2,\dots,X_n$相互独立，

- 令$S_n=\sum_{i=1}^{N}X_i$，则：$\mathrm{Var}(S_n)=n\cdot\mathrm{Var}(X_1)$
- 令$\bar{X}_n=\frac{1}{n}\sum_{i=1}^{N}X_i$，则：$\mathrm{Var}(\bar{X}_n)=\frac{\mathrm{Var}(X_1)}{n}$

### 相关系数

**定义**：$\rho_{XY}=\frac{\mathrm{Cov}(X,Y)}{\sigma_X\sigma_Y}$

**性质**：$|\rho_{XY}|\le 1$，若$|\rho_{XY}|=1$，则说明$Y$和$X$完全线性相关。

**不相关 vs 独立**：独立 $\Longrightarrow$ 不相关（$\rho=0$），反之不一定成立

> WHY???
>
> 首先要明确，**不相关**的数学定义是$\mathrm{Cov}(X,Y)=0$，协方差以及相关系数本质上是在衡量$X$和$Y$之间是否存在**线性关系**，而**独立性**意味着$X$和$Y$毫无瓜葛。因此如果$X$和$Y$独立，就说明他们不可能有线性关系，也就不相关。但是$X$和$Y$不相关仅仅意味着他们没有直线关系，可能有二次关系，不能推断他们独立。
>
> 最经典的例子就是$Y=X^2$，假设$X\sim\mathcal{U}(-1,1)$，则$X$和$Y$显然不独立，但是通过计算协方差：
> $$
> \mathbb{E}[XY]=\mathbb{E}[X\cdot X^2]=\mathbb{E}[X^3]=0
> \\[5pt]
> \mathbb{E}[X]=0
> \\[5pt]
> \mathrm{Cov}(X,Y)=\mathbb{E}[XY]-\mathbb{E}[X]\mathbb{E}[Y]=0
> $$
> 他们协方差为0，不相关，但是有严格的函数关系$Y=X^2$，即不独立。

**对于联合高斯分布，不相关等价于独立**：因为高斯分布的所有信息都包含在均值和方差（协方差矩阵）里。如果协方差为0，联合PDF刚好可以分解成边缘PDF的乘积。

## 极限定理与推断统计

### 极限定理

**切比雪夫不等式**：对于任意$k>0$，$P(|X-\mu|\ge k\sigma)\le\frac{1}{k^2}$或$P(|X-\mu|<k\sigma)\ge1-\frac{1}{k^2}$

**大数定律**(LLN)：当$n\to\infin$时，样本均值依概率收敛与真实期望，即$\bar{X}_n=\frac{1}{n}\sum_{i=1}^{n}X_i\to\mu$

**中心极限定理**(CLT)：无论总体分布如何（只要方差存在），当$n$足够大时，样本和（或均值）近似服从正态分布，即$S_n=\sum_{i=1}^{n}X_i\approx\mathcal{N}(n\mu,n\sigma^2)$，并且$\bar{X}_n\approx\mathcal{N}(\mu,\frac{\sigma^2}{n})$。

### 估计基础

**随机样本**：$X_1,\dots,X_n$是独立同分布的样本

**估计量**：用于估计参数$\theta$的统计量，记为$\hat{\theta}$（例如$\bar{X}$估计$\mu$）。

**均方误差(MSE)**：衡量估计好坏的标准。
$$
\mathrm{MSE}(\hat{\theta})=\mathbb{E}\left[ (\hat{\theta}-\theta)^2 \right]=\mathrm{Var}(\hat{\theta})+[\mathrm{Bias}(\hat{\theta})]^2
$$
其中$\mathrm{Bias}(\hat{\theta})=\mathbb{E}[\hat{\theta}]-\theta$，如果$\mathrm{Bias}=0$（无偏），则$\mathrm{MSE}=\mathrm{Var}(\hat{\theta})$

**无偏估计量**：$\mathbb{E}[\hat{\theta}]=\theta$

### 参数估计方法

**似然函数**：是一个关于$\theta$的函数，对于每一个可能的$\theta$，它告诉我们：“如果$\theta$取这个值，那产生我手上这组数据的几率有多大？”

#### 最大似然估计（MLE）

找到参数$\theta$使“当前样本发生的概率最大”。

**步骤**：

- 写出似然函数$L(\theta)=\prod_{i=1}^{n}f(x_i;\theta)$
- 取对数$\ln L(\theta)$（变成加法，方便求导）
- 对$\theta$求导并令其为0，解出$\hat{\theta}_{\text{MLE}}$

#### 最小MSE估计（MMSE）

写出MSE关于$\hat{\theta}$的表达式，求导令其为0即可。

### 二元假设检验

**模型**：

- $H_0$（零假设）：观测$X$服从$f_0(x)$
- $H_1$（备择假设）：观测$X$服从$f_1(x)$

**决策规则**：根据观测值$x$，决定判决为$D_0$（选$H_0$）或$D_1$（选$H_1$）

**似然比检验**：比较$f_1(x)$和$f_0(x)$的大小。

- **最大似然(ML)**：不考虑先验概率。若$f_1(x)>f_0(x)$，判$H_1$
- **最大后验概率(MAP)**：考虑先验$P(H_0)$和$P(H_1)$。若$\frac{f_1(x)}{f_0(x)}>\frac{P(H_0)}{P(H_1)}$，即$P(H_1)f_1(x)>P(H_0)f_0(x)$，判$H_1$。

**错误类型**：

- **虚警**：$P(D_1\mid H_0)=\int_{R_1}f_0(x)dx$（没病判有病）
- **漏检**：$P(D_0\mid H_1)=\int_{R_0}f_1(x)dx$（有病判没病）