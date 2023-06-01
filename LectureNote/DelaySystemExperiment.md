# 五、

## __解__

### 解题过程

记
$$
y(t)=
\begin{bmatrix}
    y_1(t) \\
    y_2(t)
\end{bmatrix},
$$
$$
f(t,y(t),y(t-\tau))=
\begin{bmatrix}
    \frac{1.1}{1+\sqrt{10}[y_1(t-\tau)]^{\frac{5}{4}}}-\frac{10y_1(t)}{1+40y_2(t)} \\
    \frac{100y_1(t)}{1+40y_2(t)}-2.43y_2(t)
\end{bmatrix},
$$
$$
\varphi(t)=
\begin{bmatrix}
    \varphi_1(t) \\
    \varphi_2(t)
\end{bmatrix},
\varphi_0=
\begin{bmatrix}
    1.057670270/3 \\
    1.030713491/3
\end{bmatrix},
$$
其中$\tau = 20$。则原方程可以写为
$$
\begin{cases}
    y'(t)=f(t,y(t),y(t-\tau)), & t \in [0,100], \\
    \varphi(t)=\varphi_0, & t\in [-20,0]. \\
\end{cases}
$$
对于此类方程可以给出其一般的Runge-Kutta方法(A,b,c)的计算格式如下：
$$
\begin{cases}
    y_i^{(n)}=y_{n}+h\sum\limits_{j=1}^sa_{ij}f(t_n+c_jh,y_j^{(n)},z_j^{(n)}), i=1,2,\cdots, s, \\
    y_{n+1}=y_{n}+h\sum\limits_{j=1}^sb_jf(t_n+c_jh,y_j^{(n)},z_j^{(n)}), n \geq 0, \\
\end{cases}
$$
其中
$$
A=(a_{ij})_{s\times s},b=[b_1,\cdots,b_s]^\top,c=[c_1,\cdots,c_s]^\top,
$$
$$
y_n \approx y(t_n), y_j^{(n)} \approx y(t_n+c_jh),
$$
$z_j^{(n)}\approx y(t_{n-m}+c_jh)$是对于延迟项的插值逼近，如果使用$y_j^{(n)}$进行插值，则
$$
z_j^{(n)} =\sum\limits_{k=-r}^sL^k y_j^{(n-m+k)}(m\geq s+1), L^k=\prod\limits_{l=-r,l \neq k}^s\frac{-l}{k-l},
$$
如果使用$y_n$进行插值，则
$$
z_j^{(n)} =\sum\limits_{k=-r}^sL_j^k y_{n-m+k}(m\geq s+1), L_j^k=\prod\limits_{l=-r,l \neq k}^s\frac{c_j-l}{k-l}.
$$

### 计算格式

记
$$
Y^n=[{y_1^{(n)}}^\top,{y_2^{(n)}}^\top,\cdots,{y_s^{(n)}}^\top]^\top,
$$
$$
F^n=[f(t_n+c_1h,y_1^{(n)},z_1^{(n)})^\top,f(t_n+c_2h,y_2^{(n)},z_2^{(n)})^\top,\cdots,f(t_n+c_sh,y_s^{(n)},z_s^{(n)})^\top]^\top,
$$
$$
Z^n=[{z_1^{(n)}}^\top,{z_2^{(n)}}^\top,\cdots,{z_s^{(n)}}^\top]^\top,
$$
则
$$
\begin{cases}
    Y^n=y_n\otimes e_s + h (A\otimes I_d)F_n, \\
    y_{n+1}=y_n+h(b^\top \otimes I_d)F_n,
\end{cases}
$$
$$
z_j^{(n)}=G_j^nL_j,
$$
若使用$y_j^{(n)}$进行插值，则
$$
G_j^n=[y_j^{(n-m-r)}; y_j^{(n-m-r+1)}; \cdots; y_j^{(n-m+s)}],
$$
$$
L_j=[L^{-r},L^{-r+1},\cdots,L^{s}]^\top,
$$
若使用$y_n$进行插值，则
$$
G_j^n=[y_{n-m-r}; y_{n-m-r+1}; \cdots; y_{n-m+s}],
$$
$$
L_j=[L_j^{-r},L_j^{-r+1},\cdots,L_j^{s}]^\top.
$$
因此基本步骤如下：
__Step1__:
计算延迟项$z_j^{(n)}$，这一步要用到$Y^{n-m-r},\cdots,Y^{n-m+s}$或者$y_{n-m-r},\cdots,y_{n-m+s}$；
__Step2__:
利用式子$$Y^n=y_n\otimes e_s + h (A\otimes I_d)F_n$$计算$Y^n$，显式Runge-Kutta方法可以直接推出，隐式Runge-Kutta方法可以采用Newton迭代法进行求解，这一步要用到$y_n,z_j^{(n)}$；
__Step3__:
利用式子$$y_{n+1}=y_n+h(b^\top \otimes I_d)F_n$$得到$y_{n+1}$，这一步要用到$y_n,z_j^{(n)}$；

### 计算结果

运行```main.m```（见后面）得到如下结果：

$$
\tilde{y}(100)=
\begin{bmatrix}
0.087680110742627 \\
0.293768594329476
\end{bmatrix},
$$

$$
\Vert y(100)-\tilde{y}(100) \Vert_{\infty} = 5.103873990108809\times 10^{-9} .
$$

### 程序代码

本代码使用Matlab编写，选择使用$y_j^{(n)}$去插值逼近$z_j^{(n)}$：

#### Runge-Kutta方法类 ImplicitRungeKutta1.m

```method
classdef ImplicitRungeKutta1
    properties
        A
        B % the last row of Butcher table(s-class row vector)
        C % the first column of Butcher table(s-class column vector)
        step % represents an s-class method
    end

    methods
        function obj = ImplicitRungeKutta1(ButcherTable)
            % initialize, input a Butcher table;
            obj.A = ButcherTable(1:end - 1, 2:end);
            obj.B = ButcherTable(end, 2:end);
            obj.C = ButcherTable(1:end - 1, 1);
            obj.step = size(ButcherTable, 1) - 1;
        end

        function [node, node_value] = solve(obj, right_func, interval, step_length, initial_value_function, tau_delay)
            initial_value=initial_value_function(0);
            dim = length(initial_value);
            m = tau_delay/step_length;
            
            t = zeros(1, obj.step);
            F = zeros(obj.step*dim,1);
            node = interval(1):step_length:interval(2);
            node_num = length(node);

            Y_mid = zeros(dim*obj.step, m+node_num);
            node_mid=-tau_delay:step_length:0;
            for col = 1:1:m+1
                for j = 1:1:obj.step
                    Y_mid((j-1)*obj.step+1:1:j*obj.step, col) = initial_value_function(node_mid(col)+obj.C(j)*step_length);
                end
            end
            node_value = zeros(dim, node_num);
            node_value(:, 1) = initial_value;
        
            t0 = interval(1);
            for iter = 2:1:node_num
                for s = 1:1:obj.step
                    t(s) = t0 + step_length*obj.C(s);
                end
                Y_step = kron(ones(obj.step, 1), node_value(:, iter-1));
                Y_delay = obj.Lagrange(iter, Y_mid);
                Y_step = obj.Newton(dim, right_func, step_length, Y_step, Y_delay, 10);
                Y_mid(:, m+iter) = Y_step;
                
                for s = 1:1:obj.step
                    F((s-1)*dim + 1:s*dim, 1) = right_func(Y_step((s-1)*dim + 1:s*dim, 1), Y_delay((s-1)*dim + 1:s*dim, 1));
                end
        
                node_value(:, iter) = node_value(:, iter-1) + step_length*kron(obj.B, eye(dim))*F;
                t0 = t0 + step_length;
            end
        end

        function y_delay = Lagrange(obj, iter, yj_already_know)
            s = 2; r = 2;
            L = ones(s+r+1, 1);
            for k = -r:1:s
                for l = -r:1:s 
                    if l ~= k
                        L(k+r+1) = L(k+r+1)*(l/(l-k));
                    end
                end
            end
            
            if iter-r >= 1
                y_delay = yj_already_know(:, iter-r:1:iter+s)*L;
            else
                y_delay = yj_already_know(:, 1);
            end
        end

        function X = Newton(obj, dim, right_func, step_length, Y_step, Y_delay, iter_max)
            x0 = Y_step; X1 = x0;
            errorNorm2 = 1; iter_num = 0; 

            while errorNorm2 > 10 ^ (-14)
                if iter_num > iter_max
                    disp("error!");
                    errorNorm2 = 0;
                else
                    F = zeros(obj.step*dim, 1);
                    JacobianMatrix = zeros(obj.step*dim);
                    for s = 1:1:obj.step
                        F((s-1)*dim + 1:s*dim, 1) = right_func(X1((s-1)*dim + 1:s*dim, 1), Y_delay((s-1)*dim + 1:s*dim, 1));
                    end
                    G = X1 - x0 - step_length*kron(obj.A, eye(dim))*F;
        
                    % get Jacobian matrix diffG which satisfies -diffG*delta=G
                    epsilon = step_length * 10^(-12);
                    I = eye(dim); J = zeros(dim);
                    for s = 1:1:obj.step
                        for iter = 1:1:dim
                            J(:, iter) = 
                            (
                            right_func(X1((s-1)*dim + 1:s*dim, 1) + epsilon*I(:, iter), Y_delay((s-1)*dim + 1:s*dim, 1)) 
                            - right_func(X1((s-1)*dim + 1:s*dim, 1), Y_delay((s-1)*dim + 1:s*dim, 1))
                            ) 
                            / epsilon;
                        end
                        JacobianMatrix((s-1)*dim + 1:s*dim, (s-1)*dim + 1:s*dim) = J;
                    end
        
                    diffG = eye(obj.step*dim) - step_length*kron(obj.A,eye(dim))*JacobianMatrix;
                    deltaX = -diffG \ G;
                    X2 = X1 + deltaX;
                    iter_num = iter_num + 1;
                    errorNorm2 = norm(X2 - X1, 2);
                    X1 = X2;
                end
            end
            X = X1;
        end
    end
    
end
```

#### 右端函数 right_function.m

```right_function
function y = right_function(y, y_delay)
    y = [1.1/(1+sqrt(10)*(y_delay(1))^(5/4))-10*y(1)/(1+40*y(2)); 100*y(1)/(1+40*y(2))-2.43*y(2)];
end
```

#### 初始值函数 initial_value_function.m

```initial_function
function y = initial_value_function(t)
    y=[1.057670270/3; 1.030713491/3];
end
```

#### 主函数 main.m

```main
% ButcherTable:
FOUR_ORDER_GAUSS_METHOD = [1/2-sqrt(3)/6, 1/4, 1/4-sqrt(3)/6; 1/2+sqrt(3)/6, 1/4+sqrt(3)/6, 1/4; 0, 1/2, 1/2];

% Initialize the method class:
Gauss = ImplicitRungeKutta1(FOUR_ORDER_GAUSS_METHOD);

% Define basic parameters:
interval=[0,100];
step_length=0.01;
tau = 20;
y_exact=[0.08768011074437;0.29376859943335];

% Calculate:
[t,y] = Gauss.solve(@right_function, interval, step_length, @initial_value_function, tau);

% Show result:
% plot(t,y);
y(:, end)
error = y(:,end) - y_exact;
max(abs(error))
```
