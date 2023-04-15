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

## 一、
试用分步法求解下列中立型延迟系统
$$
\begin{cases}
    x^{'}(t)=2x(t-1)-x^{'}(t-1), & t \in [0,3], \\
    x(t)=t, & t \in[-1,0], \\
\end{cases}
$$
并给出其解的曲线图。
### 解：
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
### 证明：
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
