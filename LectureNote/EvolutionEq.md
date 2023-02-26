# 从Euler方法到Runge- Kutta方法

## Euler方法
考虑初值问题
$$
\begin{cases}
    \frac{dy}{dt} = f(t,y(t)), & 0 \leq t \leq T, \\
    y(0)=y_0.
\end{cases}
$$  

### 显式Euler方法
$$
y_{n+1}-y_n=hf(t_n,y_n),n=0,1,\cdots,N.
$$  

### 局部截断误差  
利用Taylor展开可知，
$$
\begin{split}
    y(t_{n+1})-y(t_n)
    = & y(t_n)+hy^{'}(t_n)+\mathcal{O}(h^2)-y
    (t_n) \\
    = & hf(t_n,y(t^n))+\mathcal{O}(h^2) .\\
\end{split}
$$  
*Hint：* 是从精确解考虑。  
因此，局部截断误差$R_n = \mathcal{O}(h^2)$。  

### 整体误差
对于精确解有
$$
y(t_{n+1})-y(t_n)=hf(t_n,y(t_n))+R_n.
$$  
对于数值解有
$$
y_{n+1}-y_n=hf(t_n,y_n).
$$  
两式做差可得
$$
e_{n+1}-e_{n} = h[f(t_n,y(t_n))-f(t_n,y_n)]+R_n.
$$  
设函数$f$满足如下Lipshitz条件：
$$
|f(t,y_1)-f(t,y_2)| \leq L |y_1-y_2|.
$$  
则有
$$
\begin{split}
    |e_{n+1}|
    \leq & |e_n| + Lh|e_n| + R \\
    \leq & \cdots \\
    \leq & (1+Lh)^n|e_0| + R \sum_{j=0}^{n-1} (1+Lh)^j \\
    \leq & e^{L(T-t_0)}|e_0| + \frac{R}{Lh}(e^{L(T-t0)}-1).
\end{split}
$$
其中$T=t_0+Nh, R=Ch^2, e_0=0$。因此整体误差为$\mathcal{O}(h)$。

### 数值算例
$$
\begin{cases}
    y^{'}=y-x^2+1, & x \in [0,2], \\
    y(0)=0.5. & \\
\end{cases}
$$

## 梯形方法
$$
y_{n+1}-y_n=\frac{h}{2}[f(t_n,y_n)+f(t_{n+1},y_{n+1})].
$$

## 改进的Euler方法到二级二阶显式Runge-Kutta方法
将显式Euler方法和梯形方法组合得到
$$
y_{n+1}-y_n=\frac{h}{2}[f(t_n,y_n)+f(t_{n+1},y_n+hf(t_n,y_n))].
$$  
类似显式Euler方法的讨论，知其局部截断误差为$\mathcal{O}(h^3)$，整体误差为$\mathcal{O}(h^2)$。  
重写计算格式，得到
$$
\begin{cases}
    K_{n,1}=f(t_n,y_n), \\
    K_{n,2}=f(t_{n+1},y_n+hK_{n,1})=f(t_{n+1},y_n+hf(t_n,y_n)), \\
    y_{n+1}=y_n+\frac{h}{2}(K_{n,1}+K_{n,2}).
\end{cases}
$$  
等价于
$$
\begin{cases}
    Y_{n,1}=y_n, \\
    Y_{n,2}=y_n+hf(t_n,Y_{n,1}), \\
    y_{n+1}=y_n+\frac{h}{2}[f(t_n,Y_{n,1})+f(t_{n+1},Y_{n,2})].
\end{cases}
$$  
这就是一个二级二阶显式Runge-Kutta方法。并且其Butcher表如下：
$$
\begin{array}{c|c}
    c & A \\
    \hline
    & b^{T} \\
\end{array},
A=\left[
\begin{matrix}
    0 & 0 \\
    1 & 0 \\
\end{matrix}
\right],
c=\left[
\begin{matrix}
    0 \\
    1 \\
\end{matrix}
\right],
b=\left[
\begin{matrix}
    \frac{1}{2} \\
    \frac{1}{2} \\
\end{matrix}
\right].
$$

# Runge- Kutta方法

## 三级显式
$$
\begin{cases}
    Y_{n,1}=y_n, \\
    Y_{n,2}=y_n + h a_{21}f(t_n,Y_{n,1}), \\
    Y_{n,3}=y_n + h a_{31}f(t_n,Y_{n,1}) + h a_{32}f(t_n+c_2h,Y_{n,2}) , \\
    y_{n+1}=y_n + h b_1f(t_n,Y_{n,1}) + h b_2f(t_n+c_2h,Y_{n,2}) + h b_3f(t_n+c_3h,Y_{n,3}) , \\
\end{cases}
$$
或等价于
$$
\begin{cases}
    K_{n,1}=f(t_n,y_n) \\
    K_{n,2}=f(t_n+c_2h,y_n+hc_2K_{n,1})\\
    K_{n,3}=f(t_n+c_3h,y_n+h(c_3-a_{32})K_{n,1}+ha_{32}K_{n,2})\\
    y_{n+1}=y_n + h b_1K_{n,1} + h b_2K_{n,2} + h b_3K_{n,3} , \\
\end{cases}
$$

### 阶相容条件
将上式的$y_n$视为精确解$y(t_n)$并将各项都在$(t_n,y(t_n))$处使用Taylor展开，对比系数知若使计算格式三阶相容，需要满足条件
$$
\begin{cases}
    b_1+b_2+b_3=1, \\
    b_2c_2+b_3c_3=\frac{1}{2}, \\
    b_2c_2^2+b_3c_3^2=\frac{1}{3}, \\
    b_3c_2a_{31}=\frac{1}{6}. \\
\end{cases}
$$
1. 一级一阶显式需满足
$$ b_1+b_2+b_3=1,$$
即
$$ b_1=1,$$
可以看到这就是显式Euler方法。  

2. 二级二阶显式需满足
$$
\begin{cases}
    b_1+b_2+b_3=1, \\
    b_2c_2+b_3c_3=\frac{1}{2}, \\
\end{cases}
$$
即
$$
\begin{cases}
    b_1+b_2=1, \\
    b_2c_2=\frac{1}{2}, \\
\end{cases}
$$
可以看到有无穷多个解。
如$c_2=1,b_2=\frac{1}{2},b_1=\frac{1}{2}$为改进的Euler方法，$c_2=\frac{1}{2},b_2=1,b_1=1$也是一个二级二阶显式方法。  
用三阶相容条件可知二级方法不会超过二阶。  

3. 三级三阶显式需满足
$$
\begin{cases}
    b_1+b_2+b_3=1, \\
    b_2c_2+b_3c_3=\frac{1}{2}, \\
    b_2c_2^2+b_3c_3^2=\frac{1}{3}, \\
    b_3c_2a_{31}=\frac{1}{6}. \\
\end{cases}
$$
考虑四阶相容条件可知三级方法不会超过三阶。  

4. 四级显式方法（求解八个方程）
