# 基本求解过程
## 1.求解区域
```
border Gamma1(s = 0, 1) {x=s; y=0; label=C}
border Gamma2(s = 0, 1) {x=1; y=s; label=C}
border Gamma3(s = 0, 1) {x=1-s; y=1; label=C}
border Gamma4(s = 0, 1) {x=0; y=1-s; label=C}
```
## 2.网格剖分
生成三角单元，边界网格点个数为50。
```
mesh Th = buildmesh (C(50));
```

## 3.生成有限元空间

```
fespace Vh(Th, P1);
```
### The elemnts
P0: piecewise constant,
P1: continuous piecewise linear,
P2: continuous piecewise quadratic,
P3: continuous piecewise cubic,(need load "Element_P3")
P4: continuous piecewise quartic,(need load "Element_P4")
RT0: Raviart-Thomas piecewise constant,
$\cdots$
#### The elements in 3d:
P03d: piecewise constant,
P13d: continuous piecewise linear,
P23d: continuous piecewise quadratic,
RT03d: Raviart-Thomas piecewise constant.

TODO:Think about 2d?

## 4.设置求解问题并求解
```
Vh u, v;  // defines u and v as piecewise-P1 continuous functions
func f = x*y;  // definition of a called f function
problem Possion(u, v, solver = LU) =  //defines the PDE
    int2d(Th)(dx(u)*dx(v) + dy(u)*dy(v))  // bilinear part
    - int2d(Th)(f*v)  // right hand side
    + on(C, u = 0);  // Dirichlet boundary condition
Possion;
```
solver:
LU: LU method;
CG: Conjugate Gradient method;

## 5.求解线性方程：
定义变分函数：
```
varf a(u, v) = int2d(Th)(dx(u)*dx(v) + dy(u)*dy(v))
             + on(C, u = 0);
```
生成刚度矩阵：
```
matrix A = a(Vh, Vh); 
```
右端函数：
```
varf l(unused, v) = int2d(Th)(f*v) + on(C, unused = 0);
Vh F;
F[] = l(0, Vh);
```
线性方程求解：
```
u[] = A^-1*F[];
```


# 其他一些命令

## debug
```
bool debug = true;
plot(Th, wait = debug);  // wait = true 时需要鼠标点击后进行 plot；
```


## plot
```
plot(phi, wait = true, fill = true);
```
