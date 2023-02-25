# 延迟模型
## 基于PDEs的DDEs
$$
\begin{cases}
    y^{'}(t)=f(t,y(t),y(t-\tau),\int_{t-\tau}^{t}g(t,v,y(v))dv), & t \in [t_0,T], \\
    y(t)=\phi(t),& t \in [t_0-\tau,t_0],
\end{cases}
$$
其中$\tau$可以是常数，也可以依赖于时间$t$。  

称$y(t-\tau)$为离散型延迟项（discrete delay），称$\int_{t-\tau}^tg(t,v,y(v))dv$为分布型延迟项（distribute delay）。此外，也有其他形式的延迟项如$\int_{0}^tg(t,v,y(v))dv$。  

*Hint*：延迟项与时间t及时间t之前相关，称为Volterra型延迟项。  

模型举例：
* 捕食-被捕食模型
* 环境污染模型
* 血液生成模型

# 步方法（Step Method）求解延迟系统
在区间$[t_0+(i-1)\tau, t_0+i\tau], i=1,2,\cdots,N$上依此求解相应的常微分方程。
## 利用实际算例理解步方法
考虑如下形式的方程：
$$
\begin{cases}
    x^{'}(t)=-x(t-1), & x \in [0,2], \\
    x(t)=t, & x \in [-1,0]. \\
\end{cases}
$$
1. 在$[0,1]$上，方程等价于
   $$
   \begin{cases}
    x^{'}(t)=-(t-1), & ,x \in [0,1], \\
    x(0)=0.
   \end{cases}
   $$
   求解得到$x(t)=-\frac{1}{2}(t-1)^2+\frac{1}{2}, t \in [0,1]$。  
   *Hint:* $x(t-1)=t-1,t \in [0,1]$。
2. 在$[1,2]$上，方程等价于
   $$
   \begin{cases}
    x^{'}(t)=-\left[-\frac{1}{2}(t-2)^2+\frac{1}{2}\right], & x \in [1,2], \\
    x(1)=\frac{1}{2}.
   \end{cases}
   $$
   求解得到$x(t)=\frac{1}{6}(t-2)^3-\frac{t}{2}+\frac{7}{6}$。  
这样便得到了方程的解。
*Hint:* 回顾常微分方程的求解方法。
*Remark:* 若$t_0 + N\tau \leq T < t_0 + (N+1)\tau$，可采用插值的方法得到$T$时刻的近似值。

# Runge-Kutta方法求解延迟系统
## 由无延迟到有延迟
首先要求解的方程：
$$
\begin{cases}
    y^{'}(t)=f(t,y(t),y(t-\tau),\int_{t-\tau}^{t}g(t,v,y(v))dv), & t \in [t_0,T], \\
    y(t)=\phi(t),& t \in [t_0-\tau,t_0],
\end{cases}
$$
其中$\tau$为常数。实质上要考虑的是如何对$y(t-\tau)$和$\int_{t-\tau}^tg(t,v,y(v))dv$进行近似。取步长$h=\tau/m$,得到时间离散节点$t_n=t_0+nh,n=0,1,\cdots$，且在每个区间$[t_n,t_{n+1}]$上，类似无延迟的Runge-Kutta方法，可以得到辅助网格点$t_j^{(n)}=t_n+c_jh,j=1,2,\cdots,s$。  
定义
$$y_j^{(n)} \approx y(t_j^{(n)}),$$
$$z_j^{(n)} \approx z(t_j^{(n)}) := \int_{t_j^{(n-m)}}^{t_j^{(n)}} g(t_j^{(n)},v,y(v))dv,$$
$$y_n \approx y(t_n).$$
则可以将$f(t_j^{(n)},y_j^{(n)},y_j^{(n-m)},z_j^{(n)})$看作$f(t,y(t),t(t-\tau),\int_{t-\tau}^tg(t,v,y(v))dv)$在$t=t_j^{(n)}$时的近似。  
*Hint:* $t_j^{(n)}-\tau = t_n+c_jh - mh=t_{n-m}+c_jh=t_j^{(n-m)}$。  
*Remark:* $z_j^{(n)}$可以选取$z(t_j^{(n)})$的复合型求积公式。  
这样就得到如下形式的Runge-Kutta计算格式：
$$
\begin{cases}
    y_i^{(n)}=y_n + h\sum_{j=1}^s a_{ij} f(t_j^{(n)},y_j^{(n)},y_j^{(n-m)},z_j^{(n)}), & i=1,2,\cdots,s, \\
    z_j^{(n)} = \sum_{q=0}^m \omega_q g(t_j^{(n)},t_j^{(n-q)},y_j^{(n-q)}), & j=1,2,\cdots,s, \\
    y_{n+1}=y_n + h \sum_{j=1}^s b_j f(t_j^{(n)},y_j^{(n)},y_j^{(n-m)},z_j^{(n)}), & n \geq 0.
\end{cases}
$$
其中对于$z_j^{(n)}$，若采用不同的符合型求积公式则有不同的$\omega_q,q=0,1,\cdots,m$。  
若使用显式的Runge-Kutta方法，则有如下格式：
$$
\begin{cases}
    y_i^{(n)}=y_n + h\sum_{j=1}^{i-1} a_{ij} f(t_j^{(n)},y_j^{(n)},y_j^{(n-m)},z_j^{(n)}), & i=1,2,\cdots,s, \\
    z_j^{(n)} = \sum_{q=0}^m \omega_q g(t_j^{(n)},t_j^{(n-q)},y_j^{(n-q)}), & j=1,2,\cdots,s, \\
    y_{n+1}=y_n + h \sum_{j=1}^{i-1} b_j f(t_j^{(n)},y_j^{(n)},y_j^{(n-m)},z_j^{(n)}), & n \geq 0.
\end{cases}
$$
显式方法的计算步骤：$\cdots \rightarrow y_n\rightarrow y_1^{(n)}\rightarrow z_1^{(n)}\rightarrow y_2^{(n)}\rightarrow z_2^{(n)}\rightarrow \cdots \rightarrow y_s^{(n)}\rightarrow z_s^{(n)}\rightarrow y_{n+1}\rightarrow\cdots$。
同时对于上述方法，有一个简化的表示格式如下：
$$
\begin{array}{c|c}
    c & A \\
    \hline 
      & b^T \\
\end{array},
\omega=[\omega_0,\omega_1,\cdots,\omega_m]^T.
$$
## 一些具体的Runge-Kutta方法
### 二级二阶Runge-Kutta方法与复合梯形求积公式
$$
\begin{array}{c|cc}
    0 & 0 & 0 \\
    1/2 & 1/2 & 0 \\
    \hline 
      & 0 & 1 \\
\end{array},
\omega=\frac{1}{2}[1,2,2,\cdots,2,1]^T.(m-1个2)
$$
### 三级三阶Runge-Kutta方法与复合Gregory求积公式
$$
\begin{array}{c|ccc}
    0 & 0 & 0 & 0 \\
    1/2 & 1/2 & 0 & 0 \\
    1 & -1 & 2 & 0 \\
    \hline 
      & 1/6 & 2/3 & 1/6 \\
\end{array},
\omega=\frac{1}{12}[5,13,12,12,\cdots,12,13,5]^T.(m-3个12)
$$
### 四级四阶Runge-Kutta方法与复合Simpson求积公式
$$
\begin{array}{c|cccc}
    0 & 0 & 0 & 0 & 0 \\
    1/2 & 1/2 & 0 & 0 & 0 \\
    1/2 & 0 & 1/2 & 0 & 0 \\
    1 & 0 & 0 & 1 & 0 \\
    \hline 
      & 1/6 & 1/3 & 1/3 & 1/6 \\
\end{array},
\omega=\frac{1}{3}[1,4,2,4,2,\cdots,4,2,4,1]^T, m 为偶数.
$$

# 有限差分法求解延迟系统
