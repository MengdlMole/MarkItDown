<!-- ---
title: "Homework"
papersize: A4
author: 
date: 
output: 
    pdf_document:
        latex_engine: xelatex
        path: ./Homework.pdf
--- -->

# 延迟系统思考题

## 一、

试用分步法求解下列中立型延迟系统
$$
\begin{cases}
    x^{'}(t)=2x(t-1)-x^{'}(t-1), & t \in [0,3], \\
    x(t)=t, & t \in[-1,0], \\
\end{cases}
$$
并给出其解的曲线图。

__解__：

1. 当$t \in [0,1]$时，有$x(t-1)=t-1$，代入原方程得
$$
\begin{cases}
    x^{'}(t)=2t-3, & t \in [0,1], \\
    x(0)=0. \\
\end{cases}
$$
求解得到$x(t)=t^2-3t,x\in [0,1]$。

2. 当$t \in [1,2]$时，有$x(t-1)=(t-1)^2-3(t-1)$，代入原方程得
$$
\begin{cases}
    x^{'}(t)=2(t-1)^2-8(t-1)+3, & x \in [1,2], \\
    x(1)=-2. \\
\end{cases}
$$
求解得到$x(t)=(t-1)^3-4(t-1)^2+3(t-1)-2,x \in [1,2]$。

3. 当$t \in [2,3]$时，有$x(t-1)=(t-2)^3-4(t-2)^2+3(t-2)-2$，代入原方程得
$$
\begin{cases}
    x^{'}(t)=2(t-2)^3-10(t-2)^2+14(t-2)-7, & x \in [2,3], \\
    x(2)=-2. \\
\end{cases}
$$
求解得到$x(t)=\frac{1}{2}(t-2)^4-\frac{10}{3}(t-2)^3+7(t-2)^2-t(t-2)-2,x \in [2,3]$。

<!-- 4. 曲线图如下： -->

## 二、

试证明：当$|b|<-\mathfrak{Re}(a)$时，延迟微分方程
$$x^{'}(t)=ax(t)+bx(t-\tau),a,b\in \mathbb{C},\tau>0,$$
的精确解$x(t)$是渐近稳定的。

__证明__：
将$x=e^{\lambda t}$代入原方程得到相应的特征方程
$$\lambda=a+be^{-\lambda \tau}.$$
原方程精确解渐近稳定等价于$\mathfrak{Re}(\lambda)<0$。往证当$|b|<-\mathfrak{Re}(a)$时可以推出$\mathfrak{Re}(\lambda)<0$。  
反证：假设当$|b|<-\mathfrak{Re}(a)$时有$\mathfrak{Re}(\lambda)\geq0$。  
已知$0 \leq |b| < - \mathfrak{Re}(a)$，可得$\mathfrak{Re}(a) < 0$。对特征方程两边分别取实部得
$$
\begin{split}
    \mathfrak{Re}(\lambda)
    =& \mathfrak{Re}(a+be^{-\lambda \tau}) \\
    =& \mathfrak{Re}(a) + \mathfrak{Re}(be^{-\lambda \tau}) \\
    =& \mathfrak{Re}(a) + \mathfrak{Re}(|b|e^{iarg(b)-\tau \mathfrak{Re}(\lambda)- i \tau\mathfrak{Im}(\lambda)}) \\
    =& \mathfrak{Re}(a) + |b|e^{-\tau \mathfrak{Re}(\lambda)}\mathfrak{Re}(e^{i\theta}) \\
\end{split}
$$
其中$\theta=arg(b)-\tau\mathfrak{Im}(\lambda)$。  
可知  
$$
\begin{split}
    & |b| \geq 0, \\
    & 0 < e^{-\tau \mathfrak{Re}(\lambda)} \leq 1, \\
    & -1 \leq \mathfrak{Re}(e^{i\theta}) \leq 1, \\
\end{split}
$$
从而有
$$-|b| \leq |b|e^{-\tau \mathfrak{Re}(\lambda)}\mathfrak{Re}(e^{i\theta}) \leq |b|,$$
从而
$$
\mathfrak{Re}(\lambda)=\mathfrak{Re}(a) + |b|e^{-\tau \mathfrak{Re}(\lambda)}\mathfrak{Re}(e^{i\theta})
\leq \mathfrak{Re}(a) + |b| < 0,
$$
与假设$\mathfrak{Re}(\lambda) \geq 0$相矛盾。从而假设不成立，证毕。

## 三、

取步长$h=\frac{\tau}{m}(m \in N)$，将线性$\theta$-方法
$$y_{n+1}=y_{n}+h[\theta f(t_n,y_n)+(1-\theta)f(t_{n+1},y_{n+1})],\theta \in [0,1],$$
推广应用于延迟微分方程
$$x^{'}(t)=ax(t)+bx(t-\tau),a,b\in \mathbb{C},\tau>0,$$
试给出其计算格式，并证明：当$|b| < - \mathfrak{Re}(a)$，且$\theta \in [0,\frac{1}{2}]$时，该计算格式是渐进稳定的。

__解__：
对于延迟微分系统
$$
\begin{cases}
    y'(t)=f(t,y(t),y(\alpha(t))), & t > t_0, \\
    y(t) = \phi(t), & t \in [t_0-\tau, t_0], \\
\end{cases}
$$
其中$\alpha(t) = t-\tau < t, \tau = mh$，可以将线性$\theta$-方法推广为如下形式：
$$y_{n+1}=y_{n}+h[\theta f(t_n, y_n, y(\alpha(t_n)))+ (1-\theta)f(t_{n+1},y_{n+1},y(\alpha(t_{n+1})))], \theta \in [0,1].$$
对于延迟项使用Lagrange插值：
$$
\begin{split}
    y(t) = & \frac{t-t_{n+1}}{t_{n}-t_{n+1}}y_n + \frac{t-t_n}{t_{n+1}-t_n}y_{n+1} \\
         = & \frac{t-t_{n+1}}{-h}y_n + \frac{t-t_n}{h} y_{n+1} \\
         = & \frac{(n+1)h-t}{h}y_n + \frac{t-nh}{h}y_{n+1}, t \in (t_n, t_{n+1}] = (t_0+nh, t_0+(n+1)h].\\
\end{split}
$$
将推广的线性$\theta$-方法应用于上述延迟微分系统得到计算格式
$$x_{n+1}=x_n + h \theta [ax_n + bx(\alpha(t_n))] + h (1-\theta) [ax_{n+1} + bx(\alpha(t_{n+1}))],$$
其中$\alpha(t_n) = t_n-\tau = t_n - mh = t_{n-m}$, $\alpha(t_{n+1}) = t_{n+1}-\tau = t_{n+1} - mh = t_{n-m+1}$,从而有
$$x(\alpha(t_n))=x_{n-m},$$
$$x(\alpha(t_{n+1}))=x_{n-m+1},$$
则计算格式为
$$x_{n+1}=x_n + h \theta [ax_n + bx_{n-m}] + h (1-\theta) [ax_{n+1} + bx_{n-m+1}].$$

为证明计算格式渐进稳定，设$x_n = \xi z^n$,带入计算格式得到
$$\left[[1-(1-\theta)ha]z^{n+1}-(1+\theta ha)z^n -(1-\theta)hbz^{n-m+1}-\theta hbz^{n-m} \right]\xi =0.$$
设
$$P_m(z)= [1-(1-\theta)ha]z^{m+1}-(1+\theta ha)z^m -(1-\theta)hbz-\theta hb,$$
则有
$$P_m(z)\xi =0,m\geq 1.$$
证明计算格式渐进稳定即证在题设条件下$P_m(z)$的根$z$满足$\mathop{lim}\limits_{n \rightarrow \infty}z^n=0$，为此只需证明$P_m(z)$为Schur多项式，即根$z$的模$|z| \leq 1$。
对于此类问题有如下引理：

__Theorom__：
对于多项式$P_m(z)=z^{m+1} -c z^m -p(z)$，其中$m \geq max(1, k-1)$，$c$为给定复常数，$p(z)$是任意次数$k \geq 0$的给定多项式。则对于任意$m \geq max(1,k-1)$，$P_m(z)$为Schur多项式，当且仅当如下条件成立：
$$
\begin{cases}
    |p(z)| \leq |z-c|, \forall |z|=1, \\
    |c| < 1 , \\
    P_m(z) \neq 0, \forall m \geq max(1,k-1) ,|z|=1 .\\
\end{cases}
$$

但是在这里我们不使用此定理，而是直接使用Rouche定理进行证明。设
$$f(z)=\{[1-(1-\theta)x]z-(1+\theta x)\}z^m,$$
$$g(z)=-y[(1-\theta)z+\theta],$$
其中$x=ha,y=hb$。
则$P_m(z)=f(z)+g(z)$。

令$f(z)=0$，可知$z=0$或$z=\frac{1+\theta x}{1-(1-\theta)x}$。若能证明
$$|\frac{1+\theta x}{1-(1-\theta)x}| < 1,$$
则$f(z)$的全部零点均满足$|z|<1$。在这个基础上，若能证明
$$|g(z)|<|f(z)|. \forall |z|=1,$$
则由Rouche定理可知$f(z)+g(z)$在$|z| < 1$上有着与$f(z)$相同个数的零点，因此$P_m(z)=f(z)+g(z)$的全部零点均在复平面的单位圆内部。
~~在此基础上若能说明$\sout{f(z)+g(z)\neq 0, \forall |z|=1}$，则可知$\sout{P_m(z)=f(z)+g(z)}$的全部零点在复平面的单位圆内部。~~

事实上，在满足条件$|b| < - \mathfrak{Re}(a)$且$\theta \in [0,\frac{1}{2}]$时，

(1)由$|b| < - \mathfrak{Re}(a)$知$|y| < -\mathfrak{Re}(x)$，进而有$\mathfrak{Re}(x)<0$，
由$\theta \in [0,\frac{1}{2}]$知$\theta \leq 1-\theta$。
那么显然有$|1+\theta x| < |1-(1-\theta)x|$（在复平面上作图可轻易看出此结果），此即$|\frac{1+\theta x}{1-(1-\theta)x}| < 1$。

(2)在$|z|=1$上，设$z=e^{i\psi}=\cos{\psi}+i\sin{\psi}, \psi \in [0, 2\pi]$，$x=x_1+i x_2$。则有
$$f(e^{i \psi}) = [1-(1-\theta)x_1]\cos{\psi}+(1-\theta)x_2\sin{\psi}-(1+\theta x_1)+i\{[1-(1-\theta)x_1]\sin{\psi}-(1-\theta)x_2\cos{\psi}-\theta x_2\},$$
$$g(e^{i \psi})=-y[(1-\theta)\cos{\psi}+\theta +i(1-\theta)\sin{\psi}].$$
那么有
$$
\begin{split}
    |f(e^{i \psi})|^2
    = & [1-2(1-\theta)x_1+(1-\theta)^2|x|^2]+1+2\theta x_1 + \theta^2 |x|^2 \\
    & \quad + 2\cos{\psi}\{-[1-(1-\theta)x_1](1+\theta x_1)+\theta(1-\theta)x_2^2\} \\
    & \quad + 2\sin{\psi}\{-[1-(1-\theta)x_1]\theta x_2 - (1+\theta x_1)(1-\theta)x_2\} \\
    = & 2-2(1-2\theta)x_1 + [1-2\theta(1-\theta)]|x|^2 \\
    & \quad + 2[\theta(1-\theta)|x|^2+(1-2\theta)x_1-1]\cos{\psi} - 2x_2\sin{\psi} \\
    \xlongequal{\eta=1-2\theta} & 2-2\eta x_1 + \frac{1+\eta^2}{2} |x|^2 + (-2+2\eta x_1 +\frac{1-\eta^2}{2}|x|^2)\cos{\psi}-2x_2\sin{\psi},
\end{split}
$$
$$
\begin{split}
    |g(e^{i \psi}|^2
    = & |y|^2 [(1-\theta)^2+2\theta(1-\theta)\cos{\psi}+\theta^2] \\
    = & |y|^2 [1-2\theta(1-\theta)+2\theta(1-\theta)\cos{\psi}] \\
    = & |y|^2 (\frac{1+\eta^2}{2}+\frac{1-\eta^2}{2}\cos{\psi}).
\end{split}
$$
我们将$|g(e^{i \psi}|<|f(e^{i \psi})|$进一步化简得到不等式
$$
2-2\eta x_1 + \frac{1+\eta^2}{2}(|x|^2-|y|^2)+[-2 + 2\eta x_1 +\frac{1-\eta^2}{2}(|x|^2-|y|^2)]\cos{\psi} > 2x_2 \sin{\psi},
$$
设
$$
\begin{split}
    & \alpha = 2-2\eta x_1 + \frac{1+\eta^2}{2}(|x|^2-|y|^2), \\
    & \beta = 2 + 2\eta x_1 +\frac{1-\eta^2}{2}(|x|^2-|y|^2), \\
    & \gamma = 2x_2 , \\
\end{split}
$$
则有不等式
$$\alpha + \beta \cos{\psi} > \gamma \sin{\psi}.$$
为证明此不等式成立，我们使用如下引理：

__Lemma__:
设$a,b,c \in \mathbb{R}$，那么对于$w\in [-1,1]$有
$$a+bw > |c|(1-w^2)^{\frac{1}{2}}\iff a>0,a^2-b^2>c^2.$$
_证明_：

1)$\Rightarrow$：设$w=0$，则有$a>|c|\geq 0$。设$r(w)=a+bw,s(w)=|c|(1-w^2)^{\frac{1}{2}},P(w)=r^2-s^2>0$，则
$$P(w)=(b^2+c^2)w^2+2abw+a^2-c^2, \forall w \in [-1,1].$$
根据对一元二次多项式极小值的分析可知必要性成立；

2)$\Leftarrow$：根据1)知条件成立时有$P(w)>0$。又由$a>0$可推出$r(w)>s(w)$。

利用上述引理，我们证明$\alpha + \beta \cos{\psi} > \gamma \sin{\psi}$。

对于$\alpha = 2-2\eta x_1 + \frac{1+\eta^2}{2}(|x|^2-|y|^2)$，已知$\eta=1-2\theta \geq 0$，且由$|b|<-\mathfrak{Re}(a)$知$-\mathfrak{Re}(a)=-a_1>|b|\geq 0$，进而有$a_1^2>|b|^2$，从而有$|a|^2>|b|^2$，即 $|x|^2>|y|^2$。因此有$\alpha > 0$。

通过计算并使用条件$x_1<0$和$x_1^2 > |y|^2$可得
$$
\begin{split}
    \alpha^2-\beta^2
    = & (2-2\eta x_1)^2 + 2(2-2\eta x_1)\frac{1+\eta^2}{2}(|x^2|-|y^2|)+(\frac{1+\eta^2}{2})^2(|x|^2-|y|^2)^2 \\
    & \quad - [(2-2\eta x_1)^2 - 2(2-2\eta x_1)\frac{1-\eta^2}{2}(|x^2|-|y^2|)+(\frac{1-\eta^2}{2})^2(|x|^2-|y|^2)^2 ] \\
    = & 4(1-\eta x_1)(|x|^2-|y|^2)+\eta^2(|x|^2-|y|^2)^2 \\
    > & 4 (x_1^2+x_2^2-|y|^2)>4x_2^2=\gamma^2.
\end{split}
$$
至此已证明$\alpha + \beta \cos{\psi} > \gamma \sin{\psi}$，即$|f(z)| > |g(z)|,|z|=1$。
综合(1)和(2)，证毕。

## 四、

将基本线性多步法推广应用于延迟微分方程
$$
\begin{cases}
    x'(t)=Lx(t) + Mx(t-\tau), & t \geq 0 , \\
    x(t) = \varphi(t), & t\in [-\tau, 0].\\
\end{cases}
$$
试取步长$h=\frac{\tau}{m}(m \in \mathbb{N})$给出其计算格式，并证明该格式为$NGP(\alpha)$稳定的充要条件是相应的基本线性多步法为$A(\alpha)$稳定的。

__证明__:

首先给出线性多步法的计算格式：

基本线性多步法的计算格式为
$$\sum\limits_{j=0}^k\alpha_j x_{n+j}=h\sum\limits_{j=0}^k \beta_j f_{n+j},$$
将其推广至延迟微分方程
$$
    y'(t)=f(t,y(t),y(t-\tau)), \tau = mh
$$
的计算格式为
$$\sum\limits_{j=0}^k\alpha_j x_{n+j}=h\sum\limits_{j=0}^k \beta_j f(t_{n+j},y_{n+j},y_{n-m+j}).$$
则对于延迟微分方程
$$
\begin{cases}
    x'(t)=Lx(t) + Mx(t-\tau), & t \geq 0 , \\
    x(t) = \varphi(t), & t\in [-\tau, 0],\\
\end{cases}
$$
其线性多步法的计算格式为
$$\sum\limits_{j=0}^k\alpha_j x_{n+j}=h\sum\limits_{j=0}^k \beta_j (Lx_{n+j}+Mx_{n-m+j}).$$
接下来我们通过引入一种一般线性方法格式来研究线性多步法的$NGP(\alpha)$稳定。对于 $p$维常微分系统
$$
\begin{cases}
    y'(t)=f(t,y(t)), t>0, \\
    y(0)=y_0,
\end{cases}
$$
其一般线性方法的格式如下：
$$
\begin{cases}
  Y_i^{(n)}  = h \sum\limits_{j=1}^uc_{ij}^{11}f(t_n+\mu_jh,Y_j^{(n)})
  +\sum\limits_{j=1}^v c_{ij}^{12}y_j^{(n-1)}, & i=1,2,\cdots,u, \\
  y_i^{(n)} = h\sum\limits_{j=1}^uc_{ij}^{21} f(t_n+\mu_jh,Y_j^{(n)})
  +\sum\limits_{j=1}^v c_{ij}^{22}y_j^{(n-1)}, & i=1,2,\cdots,v, \\
\end{cases}
$$
其中$h>0$为计算步长，$Y_i^{(n)} \approx y(t_n+\mu_jh)(i=1,2,\cdots,u)$为内部逼近值，$y_i^{(n)}$为外部逼近值。将其推广至$p$维延迟微分系统
$$
\begin{cases}
    y'(t)=f(t,y(t),y(t-\tau)), t>0, \\
    y(t)=y_0(t), t \in [-\tau, 0], \\
\end{cases}
$$
其中$\tau = mh$，则有计算格式
$$
\begin{cases}
  Y_i^{(n)}  = h \sum\limits_{j=1}^uc_{ij}^{11}f(t_n+\mu_jh,Y_j^{(n)},Y_j^{(n-m)})
  +\sum\limits_{j=1}^v c_{ij}^{12}y_j^{(n-1)}, & i=1,2,\cdots,u, \\
  y_i^{(n)} = h\sum\limits_{j=1}^uc_{ij}^{21} f(t_n+\mu_jh,Y_j^{(n)},Y_j^{(n-m)})
  +\sum\limits_{j=1}^v c_{ij}^{22}y_j^{(n-1)}, & i=1,2,\cdots,v, \\
\end{cases}
$$
可以将上述计算格式写成等价形式
$$
\begin{cases}
  Y_i^{(n)}  = h \sum\limits_{j=1}^uc_{ij}^{11} f_j^{(n)}
  +\sum\limits_{j=1}^v c_{ij}^{12}y_j^{(n-1)}, & i=1,2,\cdots,u, \\
  f_i^{(n)} = f(t_n+\mu_i h,Y_i^{(n)},Y_i^{(n-m)}), & i=1,2,\cdots,u, \\
  y_i^{(n)} = h\sum\limits_{j=1}^uc_{ij}^{21} f_j^{(n)}
  +\sum\limits_{j=1}^v c_{ij}^{22}y_j^{(n-1)}, & i=1,2,\cdots,v, \\
\end{cases}
$$
记
$$
\begin{split}
    & y^{(n)}=(y_1^{(n)},y_2^{(n)},\cdots,y_v^{(n)})\in \mathbb{C}^v, \\
    & C_{11}=(c_{ij}^{11})\in \mathbb{R}^{u \times u},
        C_{12}=(c_{ij}^{12})\in \mathbb{R}^{u \times v}, \\
    & C_{21}=(c_{ij}^{21})\in \mathbb{R}^{v \times u},
        C_{22}=(c_{ij}^{22})\in \mathbb{R}^{v \times v}, \\
\end{split}
$$
对于基本线性多步法，将其写为上述格式
$$
\begin{cases}
  Y_1^{(n)}  = h \frac{\beta_k}{\alpha_k}f(t_n, Y_1^{(n)})
  +\sum\limits_{j=1}^{2k} c_{ij}^{12}y_j^{(n-1)}, & \\
  y_i^{(n)} = hc_{i1}^{21} f(t_n, Y_1^{(n)})
  +\sum\limits_{j=1}^{2k} c_{ij}^{22}y_j^{(n-1)}, & i=1,2,\cdots,2k, \\
\end{cases}
$$
其中
$$C_{11}=\frac{1}{\alpha_k}
\left[\begin{array}{}
    \beta_k
\end{array}\right],
$$
$$C_{12}=\frac{1}{\alpha_k}
\left[\begin{array}{cccc|cccc}
    \alpha_{k-1} & \alpha_{k-1} & \cdots & \alpha_{0}
    & \beta_{k-1} & \beta_{k-2} & \cdots & \beta_{0} \\
\end{array}\right],
$$
$$C_{21}=\frac{1}{\alpha_k}
\left[\begin{array}{cccc|cccc}
    \alpha_{k} & 0 & \cdots & 0
    & 1 & 0 & \cdots & 0 \\
\end{array}\right]^T,
$$
$$C_{22}=\frac{1}{\alpha_k}
\left[\begin{array}{cccc|cccc}
    \alpha_{k-1} & \alpha_{k-1} & \cdots & \alpha_1 & \alpha_{0}
    & \beta_{k-1} & \beta_{k-2} & \cdots & \beta_1 & \beta_{0} \\
    1 & 0 & \cdots & 0 & 0
    & 0 & 0 & \cdots & 0 & 0 \\
    0 & 1 & \cdots & 0 & 0
    & 0 & 0 & \cdots & 0 & 0 \\
    \vdots & \vdots &  & \vdots & \vdots
    & \vdots & \vdots &  & \vdots & \vdots \\
    0 & 0 & \cdots & 1 & 0
    & 0 & 0 & \cdots & 0 & 0 \\
    \hline
    0 & 0 & \cdots & 0 & 0
    & 0 & 0 & \cdots & 0 & 0 \\
    0 & 0 & \cdots & 0 & 0
    & 1 & 0 & \cdots & 0 & 0 \\
    \vdots & \vdots &  & \vdots & \vdots
    & \vdots & \vdots &  & \vdots & \vdots \\
    0 & 0 & \cdots & 0 & 0
    & 0 & 0 & \cdots & 1 & 0 \\
\end{array}\right],
$$
$$
\begin{split}
    & y_1^{(n)}=y_{n},y_2^{(n)}=y_{n-1},\cdots,y_k^{(n)}=y_{n-k+1}, \\
    & y_{k+1}^{(n)}=hf(t_{n},y_{n}),y_{k+2}^{(n)}=hf(t_{n-1},y_{n-1}),\cdots,y_{2k}^{(n)}=hf(t_{n-k+1},y_{n-k+1}).
\end{split}
$$
在此基础上，我们给出关于$A(\alpha)$稳定和$NGP(\alpha)$的定义。将基本线性方法应用于任意标量测试问题
$$
\begin{cases}
    y'(t)=\lambda y(t), \mathfrak{R}(\lambda) < 0, \\
    y(0)=y_0, \\
\end{cases}
$$
可以得到
$$
y^{(n)}=\left[\hat{h}C_{21}(I_u-\hat{h}C_{11})^{-1}C_{12}+C_{22}\right]y^{(n-1)},
$$
其中$\hat{h}=h\lambda$。

__Defination__: 对于某一常数$\alpha\in(0,\frac{\pi}{2})$，一般线性方法成为$A(\alpha)$稳定的，当且仅当其稳定域
$$
\mathbb{S}:=\left\{\hat{h}\in \mathbb{C}: 将其应用于测试问题后得到的的解序列\{y^{(n)}\}满足\mathop{lim}\limits_{n\rightarrow\infty}y^{(n)}=0\right\}
$$
包含区域$\hat{\mathbb{S}}:=\left\{\hat{h}\in \mathbb{C}: |arg(-\hat{h}) < \alpha\right\}$。此外，若对于所有$\alpha\in(0,\frac{\pi}{2})$方法都是$A(\alpha)$稳定的，那么称方法是$A$稳定的。
此外关于$A(\alpha)$有如下定理：

__Theorem__: 一般线性方法是$A(\alpha)$稳定的当且仅当$(I_u-\hat{h}C_{11})$是非奇异的且对任意的$|arg(-\hat{h})|<\alpha$有$\rho[R(\hat{h})]<1$，其中
$$R(\hat{h})=\hat{h}C_{21}(I_u-\hat{h}C_{11})^{-1}C_{12}+C_{22}).$$

对于延迟微分系统
$$
\begin{cases}
    \frac{d}{dt}[x(t)-Nx(t-\tau)]=Lx(t) + Mx(t-\tau), & t \geq 0 , \\
    x(t) = \varphi(t), & t\in [-\tau, 0], \\
\end{cases}
$$
对其使用一般线性方法可得到如下计算格式：
$$
\begin{cases}
  f_i^{(n)} = L(h \sum\limits_{j=1}^uc_{ij}^{11} f_j^{(n)}
  +\sum\limits_{j=1}^v c_{ij}^{12}x_j^{(n-1)})
  +M(h \sum\limits_{j=1}^uc_{ij}^{11} f_j^{(n-m)}
  +\sum\limits_{j=1}^v c_{ij}^{12}x_j^{(n-m-1)})
  +Nf_i^{(n-m)} , & i=1,2,\cdots,u,\\
  x_i^{(n)} = h\sum\limits_{j=1}^uc_{ij}^{21} f_j^{(n)}
  +\sum\limits_{j=1}^v c_{ij}^{22}x_j^{(n-1)}, & i=1,2,\cdots,v, \\
\end{cases}
$$
其中
$$
\begin{split}
    & x_j^{(n-m)}=\sum\limits_{q=-r}^sL_qx_j^{(n-m+q)}, \\
    & f_j^{(n-m)}=\sum\limits_{q=-r}^sL_qf_j^{(n-m+q)}, f_i^{(n)} \approx x'(t_n+c_ih), \\
    & L_q=\prod\limits_{l=-r,l\neq q}^s \frac{-l}{q-l}. \\
\end{split}
$$
设
$$
\begin{split}
    & \bar{L}=hL, \bar{M}=hM,
    F^{(n)}=\left({f_1^{(n)}}^\top,{f_2^{(n)}}^\top,\cdots,{f_u^{(n)}}^\top\right)^\top, \\
    & x^{(n)}=\left({x_1^{(n)}}^\top,{x_2^{(n)}}^\top,\cdots,{x_v^{(n)}}^\top\right)^\top, Z_n=\left({F^{(n)}}^\top, {x^{(n)}}^\top\right)^\top, \\
\end{split}
$$
那么上述计算格式可以写为向量形式
$$
\begin{bmatrix}
    I_u\otimes I_p-C_{11}\otimes \bar{L} & 0 \\
    -h(C_{21}\otimes I_p) & I_v\otimes I_p \\
\end{bmatrix}Z_n
=\begin{bmatrix}
    0 & C_{12}\otimes L \\
    0 & C_{22}\otimes I_p \\
\end{bmatrix}Z_{n-1}\\
+\begin{bmatrix}
    C_{11}\otimes \bar{M} + I_u \otimes N & 0 \\
    0 & 0 \\
\end{bmatrix}\sum\limits_{1=-r}^sL_q Z_{n-m+q}
+\begin{bmatrix}
    0 &  C_{12}\otimes M \\
    0 & 0 \\
\end{bmatrix}\sum\limits_{q=-r}^sL_qZ_{n-m+1-1}
$$
下面给出该方法$NGP(\alpha)$稳定的定义。

__Defination__:一般线性方法应用于上述延迟微分方程后，对于某一$\alpha\in (0,\frac{\pi}{2})$，称其是$NGP(\alpha)$稳定的，当且仅当该方法在条件
$$
\begin{split}
    & (\tilde{a})\quad |arg(-\lambda_i)|<\alpha,|\lambda_i|\neq 0\quad (1\leq i\leq p. |\zeta|\leq 1), \\
    & (b)\quad \rho(N)<1, \\
\end{split}
$$
下得到的数值解$x^{(n)}$满足
$$
\mathop{lim}\limits_{n\rightarrow \infty}x^{(n)}=0,
$$
其中
$$
\lambda_i=\lambda_i[(I_p-\zeta N)^{-1}(L+\zeta M)].
$$
除此之外我们这里给出其他一些关于稳定性的性质。对于延迟微分系统
$$
\begin{cases}
    \frac{d}{dt}[x(t)-Nx(t-\tau)]=Lx(t)+Mx(t-\tau), & t>0, \\
    x(t)=\varphi(t), & -\tau\leq t \leq 0, \\
\end{cases}
$$

__Proposition__:称上述系统为渐近稳定的，如果其满足如下条件：
$$
\begin{split}
    & (a) \mathfrak{R}\left\{\lambda_i[(I_p-\zeta N)^{-1}(L+\zeta M)] \right\}<0, \forall \ i \ and \ \zeta \in \mathbb{C}:|\zeta|\leq1, \\
    & (b) \rho(N)<1.
\end{split}
$$
由于条件$(\tilde{a})$可以推出条件$(a)$，因此

__Proposition__:上述系统是渐近稳定的如果存在某一$\alpha\in (0, \frac{\pi}{2})$使得条件$(\tilde{a})$和$(b)$成立。

对于向量形式的方程，取$z_n=z^n\xi$，可得到
$$
\begin{bmatrix}
    Q_1(z) & Q_2(z) \\
    Q_3(z) & Q_4(z) \\
\end{bmatrix}\zeta=0,
$$
因此我们可以考虑特征方程
$$
det\begin{bmatrix}
    Q_1(z) & Q_2(z) \\
    Q_3(z) & Q_4(z) \\
\end{bmatrix} = 0, z \in \mathbb{C},
$$
其中
$$
\begin{split}
    & Q_1(z)=z^{m+1}[I_u\otimes (I_p-N\theta(z))-C_{11}\otimes(\bar{L}+\bar{M}\theta(z))], \\
    & Q_2(z)=-z^m[C_{12}\otimes(L+M\theta(z))], \\
    & Q_3(z)=-h(C_{21}\otimes I_p)z^{M+1}, \\
    & Q_4(z)=z^m[(I_v\otimes I_p)z-(C_{22}\otimes I_p)], \\
    & \theta(z) =\sum\limits_{q=-r}^sL_qz^{q-m}. \\
\end{split}
$$
如果上述行列式能推出$|z|<1$，那么可以得到$\mathop{lim}\limits_{n\rightarrow \infty}Z_n=0$，进一步可以得到$\mathop{lim}\limits_{n\rightarrow \infty}x^{(n)}=0$。

为此有如下引理：

__Lemma__:假设$r\leq s\leq r+2$，则一般线性方法是$A(\alpha)$稳定的，如果条件$(\tilde{a})$和$(b)$成立。那么，对于$|z|\geq 1$~~和$\sout{\delta\in [0,1)}$~~，$Q_1(z)$是非奇异的。

__Lemma__:若$Q_1(z)$是非奇异的，那么有
$$
det\begin{bmatrix}
    Q_1(z) & Q_2(z) \\
    Q_3(z) & Q_4(z) \\
\end{bmatrix} = 0
\Leftrightarrow
det[Q_1(z)]det[Q_4(z)-Q_3(z)Q_1(z)^{-1}Q_2(z)]=0.
$$
在此基础上有如下定理：

__Theorom__:假设$r\leq s\leq r+2$，则推广到延迟微分系统的一般线性方法是$NGP(\alpha)$稳定的当且仅当一般线性方法是$A(\alpha)$稳定的。

_证明_:

$\Leftarrow$：只需证明可以由$A(\alpha)$稳定推出特征方程为零时有$|z|<1$。采用反证法，假设存在$\tilde{z}\geq1$使得当特征方程为零。那么由上述引理知
$$det[Q_4(\tilde{z})-Q_3(\tilde{z})Q_1(\tilde{z})^{-1}Q_2(\tilde{z})]=0.$$
而这将推出矛盾。（见文章3.$NGP(\alpha)$稳定的Page1110）。
事实上，可以推出存在$i$使得
$$det[\tilde{z}I_v-R(\hat{\lambda_i})]=0.$$
结合条件$(\tilde{a})$可以得到
$$|\tilde{z}|\leq \rho[R(\hat{\lambda_i})]<1,$$
因此矛盾。

$\Rightarrow$：
选取$p=1,M=N=0$便可直接由$NGP(\alpha)$稳定推出$A(\alpha)$稳定。

## 五、

设复N维分布型延迟微分系统
$$
\begin{cases}
    y'(t)=f(t,y(t),\int_{t-\tau}^tg(t,s,y(s))ds), & t\in [t_0,\infty], \\
    y(t)=\varphi(t), & t\in [t_0-\tau, t_0]
\end{cases}
$$
满足
$$
\begin{cases}
    & \mathfrak{Re}\left\langle f(t,x,y)-f(t,\tilde{x},\tilde{y}),x-\tilde{x}\right\rangle \leq \alpha \Vert x-\tilde{x}\Vert^2 + \beta \Vert y-\tilde{y} \Vert^2, \forall t\geq t_0, x,\tilde{x},y,\tilde{y}\in \mathbb{C}^N, \\
    & \Vert g(t,s,x)-g(t,s,\tilde{x})\Vert \leq \gamma \Vert x-\tilde{x}\Vert, \forall t\geq t_0-\tau, x,\tilde{x}\in \mathbb{C}^N, \\
    & 0 \leq \beta (\gamma \tau)^2 <-\alpha. \\
\end{cases}
$$
试证明该系统满足下列稳定性质：

(1) $\Vert y(t)-\tilde{y}(t)\Vert \leq \mathop{max}_{t_0-\tau\leq t\leq t_0}\Vert \varphi(t)-\psi(t)\Vert, \forall t\leq t_0$，

(2) $\mathop{lim}\limits_{t\rightarrow \infty}\Vert y(t)-\tilde{y}(t)\Vert=0$，

其中$\tilde{y}(t)$为上述系统取不同初始函数$\psi(t)$的解。

__证明__:

使用Halanay不等式证明。记$Y(t)=y(t)-\tilde{y}(t)$，可以得到
$$
\begin{cases}
    Y'(t)=f(t,y(t),\int_{t-\tau}^tg(t,s,y(s))ds)-f(t,\tilde{y}(t),\int_{t-\tau}^tg(t,s,\tilde{y}(s))ds) & t\in [t_0,\infty], \\
    Y(t)=\varphi(t)-\psi(t), & t\in [t_0-\tau, t_0]. \\
\end{cases}
$$
<!-- 首先证明其右导数存在：
$$
\begin{split}
    D_{+}(\Vert Y(t)\Vert)
    =&\mathop{lim}\limits_{x\rightarrow 0^{+}}\frac{\Vert Y(t+x)\Vert-\Vert Y(t)\Vert}{x} \\
    =&\mathop{lim}\limits_{x\rightarrow 0^{+}}
    \frac{\Vert Y(t+x)\Vert-\Vert Y(t)+xY'(t)\Vert}{x}
    +\mathop{lim}\limits_{x\rightarrow 0^{+}}
    \frac{\Vert Y(t)+xY'(t)\Vert-\Vert Y(t)\Vert}{x} ,\\
\end{split}
$$
(1):
$$
0\leq \left|\frac{\Vert Y(t+x)\Vert-\Vert Y(t)+xY'(t)\Vert}{x}\right| 
\leq \frac{\Vert Y(t+x)-Y(t)-xY'(t)\Vert}{x}=\frac{o(x)}{x},
$$
(2)
$$
H(x):=\frac{\Vert Y(t)+xY'(t)\Vert-\Vert Y(t)\Vert}{x}
$$
非减且有界（对于$x>0$）。设$0<x_1<x_2$，有
$$
\begin{split}
    H(x_1)-H(x_2)
    =& \frac{\Vert Y(t)+x_1Y'(t)\Vert-\Vert Y(t)\Vert}{x_1}
    -\frac{\Vert Y(t)+x_2Y'(t)\Vert-\Vert Y(t)\Vert}{x_2} \\
    =& \frac{x_2\Vert Y(t)+x_1Y'(t)\Vert-x_1\Vert Y(t)+x_2Y'(t)\Vert-x_2\Vert Y(t)\Vert-x_2\Vert Y(t)}{x_1x_2} \\
    \leq & \frac{\Vert x_2[Y(t)+x_1Y'(t)]-x_1[Y(t)+x_2Y'(t)]\Vert+(x_1-x_2)\Vert Y(t)\Vert}{x_1x_2} \\
    =& \frac{\Vert x_2Y(t)-x_1Y(t)\Vert+(x_1-x_2)\Vert Y(t)\Vert}{x_1x_2} \\
    =& \frac{\Vert (x_2-x_1)Y(t)\Vert+(x_1-x_2)\Vert Y(t)\Vert}{x_1x_2}=0, \\
\end{split}
$$
即$H(x_1)\leq H(x_2)$。
$$
|H(x)|=\left|\frac{\Vert Y(t)+xY'(t)\Vert-\Vert Y(t)\Vert}{x}\right|
\leq \frac{\Vert Y(t)+xY'(t)-Y(t)\Vert}{x}=\Vert Y'(t)\Vert, \forall x>0.
$$ -->

__Lemma__:
$$
\frac{d}{dt}\langle Y(t),Y(t)\rangle=2\mathfrak{Re}\langle Y(t),Y'(t)\rangle
=2\mathfrak{Re}\langle Y'(t),Y(t)\rangle.
$$

那么对于$\Vert Y(t)\Vert$有
$$
\begin{split}
    \frac{d}{dt}(\Vert Y(t)\Vert^2)
    =&2\mathfrak{Re}\langle Y'(t),Y(t)\rangle \\
    =&2\mathfrak{Re}\langle f(t,y(t),\int_{t-\tau}^tg(t,s,y(s))ds)-f(t,\tilde{y}(t),\int_{t-\tau}^tg(t,s,\tilde{y}(s))ds),Y(t)\rangle \\
    \leq& \alpha\Vert Y(t)\Vert^2
    +\beta \left\Vert \int_{t-\tau}^t[g(t,s,y(s))-g(t,s,\tilde{y}(s))]ds\right\Vert^2 \\
    \leq& \alpha\Vert Y(t)\Vert^2
    +\beta \left[\int_{t-\tau}^t\Vert g(t,s,y(s))-g(t,s,\tilde{y}(s))\Vert ds\right]^2 \\
    \leq& \alpha\Vert Y(t)\Vert^2
    +\beta \left[\int_{t-\tau}^t\gamma\Vert Y(s)\Vert ds\right]^2 \\
    \leq& \alpha\Vert Y(t)\Vert^2
    +\beta \gamma^2\left[\tau\mathop{sup}\limits_{t-\tau\leq s\leq t}\Vert Y(s)\Vert \right]^2 \\
    \leq& \alpha\Vert Y(t)\Vert^2+\beta (\gamma \tau)^2\mathop{sup}\limits_{t-\tau\leq s\leq t}\Vert Y(s)\Vert^2 \\
\end{split}
$$
那么有
$$
\begin{split}
    & \frac{d}{dt}(\Vert Y(t)\Vert^2)\leq\alpha\Vert Y(t)\Vert^2+\beta (\gamma \tau)^2\mathop{sup}\limits_{t-\tau\leq s\leq t}\Vert Y(s)\Vert^2,  \forall t \in [t_0, +\infty), \\
    & \Vert Y(t)\Vert^2 = \Vert \varphi(t)-\psi(t)\Vert^2, t\in [t_0-\tau, t_0],
\end{split}
$$
且有$\alpha+\beta(\gamma\tau)^2<0$，因此利用Halanay不等式可得
$$
\Vert Y(t)\Vert^2\leq \mathop{max}\limits_{s\in[t_0-\tau,t_0]}\Vert \varphi(t)-\psi(t)\Vert^2,\forall t \geq t_0 \ and \ \mathop{lim}\limits_{t\rightarrow \infty} \Vert Y(t)\Vert^2 = 0.
$$
证毕。

## 六、

取步长$h=\frac{\tau}{m}(m\in \mathbb{N})$，试写出Runge-Kutta方法$(A,b,c)$应用于$RI(\alpha,\beta,0,0)$类非线性离散型延迟系统
$$
\begin{cases}
    y'(t)=f(t,y(t),y(t-\tau)), & t\in[t_0,+\infty), \\
    y(t)=\varphi(t), & t\in [t_0-\tau,t_0], \\
\end{cases}
$$
的计算格式。并证明：当该方法代数稳定时，其数值解$y_n(n\geq 1)$满足如下扰动估计：
$$
\Vert y_n-\tilde{y}_n\Vert^2\leq\Vert y_0-\tilde{y}_0\Vert^2
+2h(\alpha+\beta)\sum\limits_{i=0}^{n-1}\sum\limits_{j=1}^sb_j\Vert y_j^{(i)}-\tilde{y}_j^{(i)}\Vert^2+\beta\tau\sum\limits_{j=1}^sb_j\mathop{max}\limits_{-m\leq i \leq -1}\Vert y_j^{(i)}-\tilde{y}_j^{(i)}\Vert^2,
$$
其中$y_j^{(i)},\tilde{y}_j^{(i)}$分别为数值解$y_n,y_j^{(i)}$的相应扰动解，$b_j$为方法权向量$b$的第$j$个分量。

__解__:

计算格式为
$$
\begin{cases}
    y_i^{(n)}=y_n+h\sum\limits_{j=1}^sa_{ij}f(t_j^{(n)},y_j^{(n)},y_j^{(n-m)}), & i=1,2,\cdots,s, \\
    y_{n+1}=y_n+h\sum\limits_{j=1}^sb_jf(t_j^{(n)},y_j^{(n)},y_j^{(n-m)}), & n\geq 0,
\end{cases}
$$
其中
$$
t_n=t_0+nh, t_j^{(n)}=t_n+c_jh,y_i^{(n)}\approx y(t_i^{(n)}), y_n\approx y(t_n).
$$
代数稳定即$(1,0)$-代数稳定，这里给出$(k,l)$-代数稳定的定义：

__Definaton__:称s级Runge-Kutta方法是$(k,l)$-代数稳定的，如果存在实数$k>0$及非负定对角矩阵$D=diag(d_1,d_2,\cdots,d_s)\in \mathbb{R}^{s\times s}$使得矩阵$M$是非负定的，这里
$$M=
\begin{bmatrix}
    k-1-2le^\top De & e^\top D -b^\top -2le^\top DA \\
    De-b-2lA^\top De & DA+A^\top D-bb^\top -2lA^\top DA \\
\end{bmatrix}\in \mathbb{R}^{(s+1)\times (s+1)},
$$
$A=(a_{ij})\in\mathbb{R}^{s\times s}, b=(b_1,b_2,\cdots,b_s)^\top\in \mathbb{R}^s,e=(1,1,\cdots,1)^\top \in\mathbb{R}^s$。

对于$RI(\alpha,\beta,0,0)$类非线性离散型延迟系统，其满足如下条件：
$$
\begin{split}
    & \mathfrak{Re}\left\langle f(t,x,y)-f(t,\tilde{x},y),x-\tilde{x}\right\rangle\leq \alpha\Vert x-\tilde{x}\Vert^2, \\
    & \Vert f(t,x,y)-f(t,x,\tilde{y}) \Vert\leq \beta\Vert y-\tilde{y}\Vert^2.
\end{split}
$$
记
$$
\begin{split}
    Y_n=y_n-\tilde{y}_n,Y_j^{(n)}=y_j^{(n)}-\tilde{y}_j^{(n)},\sout{Z_j^{(n)}=z_j^{(n)}-\tilde{z}_j^{(n)}}, \\
    F_j^{(n)}=f(t_j^{(n)},y_j^{(n)},y_j^{(n-m)})-f(t_j^{(n)},\tilde{y}_j^{(n)},\tilde{y}_j^{(n-m)}).
\end{split}
$$

如果Runge-Kutta方法是$(k,l)$-渐近稳定的，那么对于$RI(\alpha,\beta,\sigma,\gamma)$类型的延迟微分系统有如下引理(Burrage & Butcher,1980)：

__Lemma__:
$$
\Vert Y_{n+1}\Vert^2-k\Vert Y_{n}\Vert^2-2\sum\limits_{j=1}^sd_j\mathfrak{Re}\langle Y_j^{(n)}, h F_j^{(n)}-l Y_j^{(n)}\rangle
=-\sum\limits_{i=1}^{s+1}\sum\limits_{j=1}^{s+1}m_{ij}<\omega_i,\omega_j>\leq 0,
$$
其中$M=(m_{ij}),\omega_1=Y_n,\omega_{i+1}=hF_i^{(n)}(i=1,2,\cdots,s)$，进而有
$$
\Vert Y_{n+1}\Vert^2 \leq k\Vert Y_n\Vert^2 +2\sum\limits_{j=1}^s\mathfrak{Re}\langle Y_j^{(n)},hF_j^{(n)}-lY_j^{(n)}\rangle.
$$

下面证明题目要求的结果，由上面的定义和引理，可以得到对于$(1,0)$-代数稳定的Runge-Kutta方法，存在$D=diag(d_1,d_2,\cdots,d_s)$非负定使得
$$
\Vert Y_{n+1}\Vert^2 \leq \Vert Y_n\Vert^2 +2\sum\limits_{j=1}^sd_j\mathfrak{Re}\langle Y_j^{(n)},hF_j^{(n)}\rangle,
$$
且有
$$M=
\begin{bmatrix}
    0 & e^\top D-b^\top \\
    De-b & DA+A^\top D-bb^\top \\
\end{bmatrix}
$$
非负定。
如果当$d_j=b_j\geq 0$时有$DA+A^\top D-bb^\top$非负定，那么显然
$$M=
\begin{bmatrix}
    0 & 0 \\
    0 & DA+A^\top D-bb^\top \\
\end{bmatrix}
$$
也非负定，此时可以选取$d_j=b_j$。
利用条件
$$
\begin{split}
    & \mathfrak{Re}\left\langle f(t,x,y)-f(t,\tilde{x},y),x-\tilde{x}\right\rangle\leq \alpha\Vert x-\tilde{x}\Vert^2, \\
    & \Vert f(t,x,y)-f(t,x,\tilde{y}) \Vert\leq \beta\Vert y-\tilde{y}\Vert^2.
\end{split}
$$
可以推出；
$$
\begin{split}
    2\mathfrak{Re}\langle Y_j^{(n)}, hF_j^{(n)}\rangle
    =& 2h\mathfrak{Re}\langle Y_j^{(n)}, f(t_j^{(n)},y_j^{(n)},y_j^{(n-m)})-f(t_j^{(n)},\tilde{y}_j^{(n)},\tilde{y}_j^{(n-m)})\rangle \\
    =& 2h\mathfrak{Re}\langle Y_j^{(n)}, f(t_j^{(n)},y_j^{(n)},y_j^{(n-m)})-f(t_j^{(n)},\tilde{y}_j^{(n)},{y}_j^{(n-m)})\rangle  \\
    &  + 2h\mathfrak{Re}\langle Y_j^{(n)}, f(t_j^{(n)},\tilde{y}_j^{(n)},{y}_j^{(n-m)})-f(t_j^{(n)},\tilde{y}_j^{(n)},\tilde{y}_j^{(n-m)})\rangle \\
    \leq & 2h\alpha\Vert Y_j^{(n)}\Vert^2
    + 2h\Vert Y_j^{(n)}\Vert\Vert f(t_j^{(n)},\tilde{y}_j^{(n)},{y}_j^{(n-m)})-f(t_j^{(n)},\tilde{y}_j^{(n)},\tilde{y}_j^{(n-m)})\Vert \\
    \leq & 2h\alpha\Vert Y_j^{(n)}\Vert^2+2h\beta\Vert Y_j^{(n)}\Vert\Vert y_j^{(n-m)}-\tilde{y}_j^{(n-m)}\Vert \\
    \leq & 2h\alpha\Vert Y_j^{(n)}\Vert^2+h\beta(\Vert Y_j^{(n)}\Vert^2+\Vert Y_j^{(n-m)}\Vert^2) \\
    \leq & h(2\alpha+\beta)\Vert Y_j^{(n)}\Vert^2 + h\beta\Vert Y_j^{(n-m)}\Vert^2,
\end{split}
$$
那么有
$$
\Vert Y_{n+1}\Vert^2 \leq \Vert Y_n\Vert^2 +h\sum\limits_{j=1}^sd_j[(2\alpha+\beta)\Vert Y_j^{(n)}\Vert^2 + \beta\Vert Y_j^{(n-m)}\Vert^2].
$$
从$k=0$到$k=n$求和得到
$$
\Vert Y_n\Vert^2\leq\Vert Y_0\Vert^2
+h(2\alpha+\beta)\sum\limits_{k=0}^{n-1}\sum\limits_{j=1}^s d_j\Vert Y_j^{(k)}\Vert^2
+h\beta\sum\limits_{k=0}^{n-1}\sum\limits_{j=1}^s d_j\Vert Y_j^{(k-m)}\Vert^2,
$$
其中
$$
\begin{split}
    h\sum\limits_{k=0}^{n-1}\sum\limits_{j=1}^s d_j\Vert Y_j^{(k-m)}\Vert^2
    = & h\sum\limits_{i=-m}^{n-m-1}\sum\limits_{j=1}^s d_j\Vert Y_j^{(i)}\Vert^2 \\
    = & h\sum\limits_{i=0}^{n-m-1}\sum\limits_{j=1}^s d_j\Vert Y_j^{(i)}\Vert^2
    +h\sum\limits_{i=-m}^{-1}\sum\limits_{j=1}^s d_j\Vert Y_j^{(i)}\Vert^2 \\
    \leq & h\sum\limits_{i=0}^{n-1}\sum\limits_{j=1}^s d_j\Vert Y_j^{(i)}\Vert^2
    +mh\sum\limits_{j=1}^s d_j\mathop{max}\limits_{-m\leq i\leq -1}\Vert Y_j^{(i)}\Vert^2 \\
    = & h\sum\limits_{i=0}^{n-1}\sum\limits_{j=1}^s d_j\Vert Y_j^{(i)}\Vert^2
    +\tau\sum\limits_{j=1}^s d_j\mathop{max}\limits_{-m\leq i\leq -1}\Vert Y_j^{(i)}\Vert^2 \\.
\end{split}
$$
从而有
$$
\begin{split}
    \Vert Y_n\Vert^2
    \leq& \Vert Y_0\Vert^2
    +h(2\alpha+\beta)\sum\limits_{k=0}^{n-1}\sum\limits_{j=1}^s d_j\Vert Y_j^{(k)}\Vert^2
    +h\beta\sum\limits_{k=0}^{n-1}\sum\limits_{j=1}^s d_j\Vert Y_j^{(k-m)}\Vert^2 \\
    \leq& \Vert Y_0\Vert^2
    +h(2\alpha+\beta)\sum\limits_{k=0}^{n-1}\sum\limits_{j=1}^s d_j\Vert Y_j^{(k)}\Vert^2 \\
    & + \beta h\sum\limits_{i=0}^{n-1}\sum\limits_{j=1}^s d_j\Vert Y_j^{(i)}\Vert^2
    +\beta\tau\sum\limits_{j=1}^s d_j\mathop{max}\limits_{-m\leq i\leq -1}\Vert Y_j^{(i)}\Vert^2 \\
    \leq& \Vert Y_0\Vert^2
    +h(2\alpha+2\beta)\sum\limits_{i=0}^{n-1}\sum\limits_{j=1}^s d_j\Vert Y_j^{(k)}\Vert^2
    +\beta\tau\sum\limits_{j=1}^s d_j\mathop{max}\limits_{-m\leq i\leq -1}\Vert Y_j^{(i)}\Vert^2.
\end{split}
$$
当$d_j=b_j$时则有
$$
\begin{split}
    \Vert Y_n\Vert^2
    \leq& \Vert Y_0\Vert^2
    +h(2\alpha+2\beta)\sum\limits_{i=0}^{n-1}\sum\limits_{j=1}^s b_j\Vert Y_j^{(k)}\Vert^2
    +\beta\tau\sum\limits_{j=1}^s b_j\mathop{max}\limits_{-m\leq i\leq -1}\Vert Y_j^{(i)}\Vert^2,
\end{split}
$$
即
$$
\begin{split}
    \Vert y_n-\tilde{y}_n\Vert^2
    \leq& \Vert y_0-\tilde{y}_0\Vert^2
    +h(2\alpha+2\beta)\sum\limits_{i=0}^{n-1}\sum\limits_{j=1}^s b_j\Vert y_n^{(i)}-\tilde{y}_n^{(i)}\Vert^2
    +\beta\tau\sum\limits_{j=1}^s b_j\mathop{max}\limits_{-m\leq i\leq -1}\Vert y_n^{(i)}-\tilde{y}_n^{(i)}\Vert^2.
\end{split}
$$

## 七、

试将延迟抛物型方程
$$
\begin{cases}
    \frac{\partial u(x,t)}{\partial t}=a\frac{\partial^2 u(x,t)}{\partial x^2}+bu(x,t-\tau), & t>0, 0\leq x \leq 1, \\
    u(x,t)=\varphi(x,t), & -\tau\leq t\leq 0, 0\leq x \leq 1,
\end{cases}
$$
变换为常微分延迟系统（其中$a>0$为扩散系数），然后给出该延迟系统的线性多步法，其时间离散步长可取为$h=\frac{\tau}{m}$，$m$为给定常数。

__解__：

对空间使用中心差分格式，得到
$$
\frac{\partial u(x_j,t)}{\partial t}\approx a\frac{u(x_{j+1},t)-2u(x_j,t)+u(x_{j-1},t)}{h_s^2}+bu(x_j,t-\tau), j=1,2,\cdots,N-1,
$$
其中$h_s=\frac{1}{N}$为空间离散步长。
对于延迟微分系统
$$
y'=f(t,y,y(t-\tau))
$$
有如下线性多步法的计算格式：
$$
\sum\limits_{j=1}^k\alpha_j y_{n+j}=h\sum\limits_{j=0}^k\beta_j f(t_{n+j},y_{n+j},y_{n-m+j}).
$$
将其类似的推广到到上面的空间离散格式可以得到
$$
\sum\limits_{j=0}^k \alpha_j u_{n+j}^{l}=h\sum\limits_{j=0}^k\beta_j
\left[a\frac{u_{n+j}^{(l+1)}-2u_{n+j}^{(l)}+u_{n+j}^{(l-1)}}{h_s^2}+bu_{n-m+j}^{(l)}\right],
$$
其中$u_j^{(l)}=u(x_l,t_j )$。
