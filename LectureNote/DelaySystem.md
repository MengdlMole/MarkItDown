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

# 步方法（Step Method）
在区间$[t_0+(i-1)\tau, t_0+i\tau], i=1,2,\cdots,N$上依此求解相应的常微分方程。
