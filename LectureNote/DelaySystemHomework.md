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

4. 曲线图如下：

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
