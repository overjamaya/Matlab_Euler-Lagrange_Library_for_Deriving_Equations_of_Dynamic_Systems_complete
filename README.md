# Matlab: Euler-Lagrange Library for Derving Equations of Dynamic Systems

Using the above library, one can derive differential equations for any dynamic systems and solve response of the system for a given conditions.

Functinality of the library has been demonstrated by the following examples:

1. Double Pendulum
2. Spring Pendulum

## Example 1: Double Pendulum

Just run the **EVAL1.m** to derive equations and solve intial condition problem:

### Usage:
``` Matlab
syms th1 th2  Dth1 Dth2 
syms l1 l2 m1 m2 J1 J2  g t 

%% Kinetic and Potential Energy
T1 = 1/2*J1*Dth1^2 +1/2*m1*(l1/2*Dth1)^2;

Vc2_x = l1*Dth1*cos(th1) + l2/2*(Dth1 + Dth2)*cos(th1+th2);
Vc2_y = l1*Dth1*sin(th1) + l2/2*(Dth1 + Dth2)*sin(th1+th2);
Vc2 = sqrt(Vc2_x^2 + Vc2_y^2); 
T2 = 1/2*J2*(Dth1+Dth2)^2+1/2*m2*Vc2^2;

T = T1 + T2;

V1 = m1*g*l1*(1-cos(th1))/2;
V2 = m2*g*(l1*(1-cos(th1))+l2*(1-cos(th1+th2))/2);
V = V1 + V2;

L = T - V;
%%
q  = [th1, th2];
Dq = [Dth1, Dth2];
tt = linspace(0,5,500);
Eq = LagrangeDynamicEqDeriver(L, q, Dq);
[SS, xx] = DynamicEqSolver(Eq, q, Dq, [l1 l2 m1 m2 J1 J2 g],...
                           [0.5 0.5 1 2 0.2 0.5 9.81], tt, [120,-90,0,0]/180*pi);
````

Anlges of double pendulum:
<p align="center">
  <img src="../master/Pic/Ex1.png" />
</p>

Animated Response:
<p align="center">
  <img src="../master/Pic/Anim1.gif" />
</p>
	
## Example 2: Spring Pendulum

Just run the **EVAL2.m** to derive equations and solve intial condition problem:

### Usage:
``` MATLAB
syms th Dth x Dx
syms m l k g t 

%% Kinetic and Potential Energy
T = 1/2*m*(Dx^2 + (l + x)^2*Dth^2);
V = -m*g*(l+x)*cos(th) + 1/2*k*x^2;

L = T - V;
%% Derive Equations
q = [th, x]; Dq = [Dth, Dx];
Eq = LagrangeDynamicEqDeriver(L, q, Dq);

%% Solve Equations

tt = linspace(0,30,500);
[SS, xx] = DynamicEqSolver(Eq, q, Dq, [m l k g],...
                           [1 1 10 9.81], tt, [45/180*pi,0.1, 0, 0]);
```

Angle and length of spring pendulum:
<p align="center">
  <img src="../master/Pic/Ex1.png" />
</p>
Animated Response:
<p align="center">
  <img src="../master/Pic/Anim2.gif" />
</p>

