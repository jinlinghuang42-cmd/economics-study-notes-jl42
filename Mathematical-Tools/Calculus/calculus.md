# Calculus for Economics

This note summarizes several calculus tools that are frequently used in economics, especially in microeconomic theory and optimization problems.

The main topics include:

* Chain rule
* Gradients
* Directional derivatives
* Implicit functions
* Level curves

---

## 1. Chain Rule

### 1.1 One-Variable Composite Function

Suppose

```math
y = y(u), \quad u = u(x)
```

Then (y) depends on (x) indirectly through (u). By the chain rule,

```math
\frac{dy}{dx}
=
\frac{dy}{du}
\cdot
\frac{du}{dx}
```


### 1.2 Multi-Variable Composite Function

Suppose

```math
z = f(u,v)
```

where

```math
u = u(x,y), \quad v = v(x,y)
```

By the multi-variable chain rule,

```math
\frac{\partial z}{\partial x}
=
\frac{\partial z}{\partial u}
\frac{\partial u}{\partial x}
+
\frac{\partial z}{\partial v}
\frac{\partial v}{\partial x}
```

Similarly,

```math
\frac{\partial z}{\partial y}
=
\frac{\partial z}{\partial u}
\frac{\partial u}{\partial y}
+
\frac{\partial z}{\partial v}
\frac{\partial v}{\partial y}
```

Putting these two partial derivatives together, we get the column vector

```math
\begin{pmatrix}
\frac{\partial z}{\partial x} \\
\frac{\partial z}{\partial y}
\end{pmatrix}
=
\begin{pmatrix}
\frac{\partial z}{\partial u}
\frac{\partial u}{\partial x}
+
\frac{\partial z}{\partial v}
\frac{\partial v}{\partial x}
\\
\frac{\partial z}{\partial u}
\frac{\partial u}{\partial y}
+
\frac{\partial z}{\partial v}
\frac{\partial v}{\partial y}
\end{pmatrix}
```

This column vector is the gradient of \(z\) with respect to \((x,y)\) .

So the gradient is the column vector of all first-order partial derivatives.

---

## 2. Gradient

For a function

```math
u = u(x_1,x_2)
```

the gradient is the vector of all first-order partial derivatives:

```math
\nabla u(x_1,x_2)
=
\begin{pmatrix}
\frac{\partial u}{\partial x_1} \\
\frac{\partial u}{\partial x_2}
\end{pmatrix}
```

More generally, if

```math
u = u(x_1,x_2,\dots,x_n)
```

then

```math
\nabla u(x)
=
\begin{pmatrix}
\frac{\partial u}{\partial x_1} \\
\frac{\partial u}{\partial x_2} \\
\vdots \\
\frac{\partial u}{\partial x_n}
\end{pmatrix}
```

---

## 3. Directional Derivative

**The directional derivative is equal to the dot product of the gradient vector and the direction vector.**

It measures the rate of change of \(u(x1,x2)\) at a given point \(x*\) along a given direction \(v=(v1,v2)\).

Consider the path

```math
x = x^* + tv, \quad t \in \mathbb{R}
```

Define

```math
g(t)
=
u(x^*+tv)
=
u(x_1^*+tv_1,\ x_2^*+tv_2)
```

By the chain rule,

```math
g'(0)
=
\begin{pmatrix}
\frac{\partial u}{\partial x_1}(x^*) &
\frac{\partial u}{\partial x_2}(x^*)
\end{pmatrix}
\begin{pmatrix}
v_1 \\
v_2
\end{pmatrix}
=D_vu(x^*)
```

Using the dot product formula,

```math
D_vu(x^*)
=
\|\nabla u(x^*)\|\|v\|\cos\theta
```

> [!TODO]  
> Add figure: implicit function and level curve.  
> Path: `assets/images/calculus/implicit-function-level-curve.png`
---

## 4. Implicit Function: Dini's Theorem
We have
```math
\left\{
\begin{aligned}
u(x_1,x_2)=c\\
x_2=f(x_1)\\
\frac{\partial u}{\partial x_2}(x_1^0,x_2^0)\neq 0
\end{aligned}
\right.
```

then, by Dini's theorem / the implicit function theorem,

```math
f'(x_1^0)
=
-
\frac{
\frac{\partial u}{\partial x_1}(x_1^0,x_2^0)
}{
\frac{\partial u}{\partial x_2}(x_1^0,x_2^0)
}
```

---

## 5. Level Curve

A level curve is defined by

```math
u(x_1,x_2)=c
```

The gradient is perpendicular to the level curve:

```math
\nabla u
\perp
\{(x_1,x_2):u(x_1,x_2)=c\}
```

Equivalently, the gradient is perpendicular to the tangent direction of the level curve.

For a utility function, an indifference curve is a level curve.
