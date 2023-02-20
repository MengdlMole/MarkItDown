## 方程
$$
\begin{cases}
-\Delta\phi=f \ in \ \Omega, \\
\phi|_{\Gamma_1} = z, \\
\frac{\partial \phi}{\partial n}|_{\Gamma_2} = a. \\
\end{cases}
$$
## 基本代码
### $z = x, a = 0, f = 1$:
```
bool debug = false;
real theta = 4.*pi/3.;
real a=2., b=1.;
func z = x;
border Gamma1(t = 0, theta){x = a*cos(t); y = b*sin(t);}
border Gamma2(t = theta, 2*pi){x = a*cos(t); y = b*sin(t);}
mesh Th = buildmesh(Gamma1(100) + Gamma2(50));

fespace Vh(Th, P2);
Vh phi, w, f=1;

problem Laplace(phi, w) = int2d(Th)(dx(phi)*dx(w) + dy(phi)*dy(w))
                            - int2d(Th)(f*w)
                            + on(Gamma1, phi = z);

Laplace;

plot(phi, wait = debug, ps = "D:\\CodeDevelopment\\MyCode\\Freefem++Code\\Projects\\membrane\\membrane.eps");
plot(Th, wait = debug, ps = "D:\\CodeDevelopment\\MyCode\\Freefem++Code\\Projects\\membrane\\membraneTh.eps");

savemesh(Th, "D:\\CodeDevelopment\\MyCode\\Freefem++Code\\Projects\\membrane\\Th.msh");

```
### $z = x, a = 2, f = 1$:
```
bool debug = true;
real theta = 4.*pi/3.;
real a = 2., b = 1.; // the length of the semimajor axis and semiminor axis
func z = x;
border Gamma1(t = 0, theta){x = a*cos(t); y = b*sin(t);}
border Gamma2(t = theta, 2*pi){x = a*cos(t); y = b*sin(t)}
mesh Th = buildmesh(Gamma1(100) + Gamma2(50));
fespace Vh(Th, P2); // P2 conforming triangular FEM
Vh phi, w, f = 1;
solve Laplace(phi, w) = int2d(Th)(dx(phi)*dx(w) + dy(phi)*dy(w))
                        - int2d(Th)(f*w) + on(Gamma1, phi = z);
plot(phi, wait = debug, ps = "D:\\CodeDevelopment\\MyCode\\Freefem++Code\\Projects\\membraneError\\membrane.eps");
plot(Th, wait = debug, ps = "D:\\CodeDevelopment\\MyCode\\Freefem++Code\\Projects\\membraneError\\membraneTh.eps");

savemesh(Th, "D:\\CodeDevelopment\\MyCode\\Freefem++Code\\Projects\\membraneError\\Th.msh");
```
