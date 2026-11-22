# Optimization

This note summarizes basic optimization tools used in economics.

Main topics:

- Unconstrained optimization
- Constrained optimization
- Lagrangian Method and KKT conditions
- *Interior and corner solutions* (todo)
- Envelope theorem
- *Types of optimization* (todo)

---

## 1. Optimization Problem

An optimization problem is a problem of choosing variables to maximize or minimize an objective function.

```math
\max_x f(x)
```

```math
\min_x f(x)
```

In economics, optimization problems are used to model choices such as utility maximization, profit maximization, cost minimization, and welfare maximization.

---

## 2. Unconstrained Optimization
### 2.1 FOC
For an unconstrained maximization or minimization problem, the first-order condition is

```math
f'(x^*)=0
```

For a multi-variable function, the first-order condition is

```math
\nabla f(x^*)=0
```

The first-order condition is necessary, but not sufficient. 


### 2.2 SOC

For a one-variable function:

```math
f''(x^*)<0
```

implies a local maximum.

```math
f''(x^*)>0
```

implies a local minimum.

```math
f''(x^*)=0
```

is inconclusive. The point may be a maximum, a minimum, or a saddle point.

For a multi-variable function, the Hessian matrix is used to check the second-order condition.

---


## 3. Constrained Optimization

A constrained optimization problem has an objective function and one or more constraints.

A general form is

```math
\max_x f(x)
```

s.t.

```math
\left\{
\begin{aligned}
g(x) &= 0 \\
h(x) &\geq 0
\end{aligned}
\right.
```

There are two types of constraints:

```math
\left\{
\begin{aligned}
g(x)=0 &\quad \text{equality constraint} \\
h(x)\geq 0 &\quad \text{inequality constraint}
\end{aligned}
\right.
```

The basic principle is:

1. Change the constrained problem into an unconstrained problem with a **Lagrange formulation**.
2. Set all partial derivatives equal to zero **[FOC]**.
3. Check whether each **inequality constraint is binding**.



### 3.1 Lagrangian Method

For an equality-constrained problem,

```math
\max_x f(x)
```

s.t.

```math
g(x)=0
```

construct the Lagrangian:

```math
\mathcal{L}(x,\lambda)
=
f(x)+\lambda g(x)
```

Then solve the first-order conditions:

```math
\left\{
\begin{aligned}
\frac{\partial \mathcal{L}}{\partial x_i} &= 0 \\
\frac{\partial \mathcal{L}}{\partial \lambda} &=0
\end{aligned}
\right.
```

The Lagrange multiplier measures the marginal value of relaxing the constraint.



### 3.2 KKT Conditions

For inequality constraints, the key issue is whether the constraint is binding.

A constraint is binding if it holds with equality:

```math
h(x)=0
```

A constraint is non-binding if it is slack:

```math
h(x)>0
```

--

For the problem

```math
\max_x f(x)
```

s.t.

```math
h(x)\geq 0
```

construct the Lagrangian:

```math
\mathcal{L}(x,\lambda)
=
f(x)+\lambda h(x),
\quad
\lambda\geq 0
```

--

**The KKT conditions combine all required conditions**:

```math
\left\{
\begin{aligned}
\nabla_x \mathcal{L}(x,\lambda) &= 0 \\
\lambda h(x) &= 0\\
h(x) &\geq 0 \\
\lambda &\geq 0
\end{aligned}
\right.
```

--

Complementary slackness:

```math
\lambda h(x)=0
```

It means:

```math
\left\{
\begin{aligned}
h(x)>0 &\Rightarrow \lambda=0 \\
\lambda>0 &\Rightarrow h(x)=0
\end{aligned}
\right.
```

--

>Thus, KKT conditions are the combination of:
>```text
>FOC + complementary slackness + feasibility + non-negative multipliers
>```



### 3.3 Non-Negativity Constraints

In economics, choice variables are usually non-negative:

```math
x^*=(x_1^*,x_2^*,\dots,x_n^*)\geq 0
```

For example, consumption cannot be negative.

However, it can be cumbersome to put every non-negativity constraint into the Lagrangian. There are two common ways to deal with this.
<br>

#### Case 1: Put non-negativity constraints into the Lagrangian

Consider

```math
\max_{x_1,x_2} u(x_1,x_2)
```

s.t.

```math
h(x_1,x_2)\geq b,
\quad
x_1\geq 0,
\quad
x_2\geq 0
```


The Lagrangian is

```math
\mathcal{L}
=
u(x_1,x_2)
+
\lambda[h(x_1,x_2)-b]
+
\mu_1x_1
+
\mu_2x_2
```
with
```math
\lambda\geq 0,
\quad
\mu_1\geq 0,
\quad
\mu_2\geq 0
```

--


```math
\left\{
\begin{aligned}
\frac{\partial \mathcal{L}}{\partial x_1} &=\frac{\partial \mathcal{L}}{\partial x_2} &= 0 \\
\lambda[h(x_1,x_2)-b] &=\mu_1x_1 &=\mu_2x_2 &= 0\\
\end{aligned}
\right.
```

--

This method is complete but can be lengthy when there are many choice variables.



#### Case 2: Kuhn-Tucker Formulation
In this formulation, the non-negativity multipliers are not included in the Lagrangian.
```math
\mathcal{L}
=
u(x_1,x_2)
-
\lambda[h(x_1,x_2)-b]
```
The usual Lagrangian (with the non-negativity multipliers) can be written as
```math
\widetilde{\mathcal{L}}
=
\mathcal{L}
+
\mu_1x_1
+
\mu_2x_2
```
From the FOCs of the usual Lagrangian $\widetilde{\mathcal{L}}$,
```math
\left\{
\begin{aligned}
\frac{\partial \widetilde{\mathcal{L}}}{\partial x_1}(x^*)=0
&\Rightarrow
\frac{\partial \mathcal{L}}{\partial x_1}(x^*)=-\mu_1
\\
\frac{\partial \widetilde{\mathcal{L}}}{\partial x_2}(x^*)=0
&\Rightarrow
\frac{\partial \mathcal{L}}{\partial x_2}(x^*)=-\mu_2
\\
\frac{\partial \mathcal{L}}{\partial \lambda}(x^*)
&=
b-h(x_1^*,x_2^*)\geq 0
\\
\lambda^*
&\geq 0
\end{aligned}
\right.
```
Since
```math
\mu_1\geq0,
\quad
\mu_2\geq0
```
we have
```math
\frac{\partial \mathcal{L}}{\partial x_1}(x^*)\leq0,
\quad
\frac{\partial \mathcal{L}}{\partial x_2}(x^*)\leq0
```
Thus, the KKT conditions can be written as:
```math
\left\{
\begin{aligned}
\frac{\partial \mathcal{L}}{\partial x_1}(x^*) &\leq 0,
&
x_1^*\frac{\partial \mathcal{L}}{\partial x_1}(x^*) &=0
\\
\frac{\partial \mathcal{L}}{\partial x_2}(x^*) &\leq 0,
&
x_2^*\frac{\partial \mathcal{L}}{\partial x_2}(x^*) &=0
\\
\frac{\partial \mathcal{L}}{\partial \lambda}(x^*) &\geq 0,
&
\lambda^*\frac{\partial \mathcal{L}}{\partial \lambda}(x^*) &=0
\end{aligned}
\right.
```
with
```math
x_1^*\geq0,
\quad
x_2^*\geq0,
\quad
\lambda^*\geq0
```

---

## 4. Interior and Corner Solutions (todo)

This section will summarize the difference between interior and corner solutions in constrained optimization.

Main points to add:

- Interior solution: all choice variables are strictly positive.
- Corner solution: at least one choice variable equals zero.
- In KKT conditions, corner solutions are handled by non-negativity constraints and complementary slackness.
- In economics, corner solutions often appear in consumer choice problems, especially with **perfect substitutes or binding constraints**.


---

## 5. Envelope Theorem

The **Envelope Theorem** provides a convenient method for comparative statics analysis. It allows us to examine how changes in exogenous parameters affect the optimized value of an objective function, without explicitly differentiating the optimal decision variables.

### 5.1 Static Analysis vs. Comparative Statics vs. Dynamic Analysis

- **Static analysis:** Studies equilibrium given a fixed set of exogenous parameters.
- **Comparative statics:** Examines how equilibrium changes when exogenous parameters change, without explicitly considering the adjustment process over time.
- **Dynamic analysis:** Studies intertemporal relationships among variables and the evolution of an economy over time.

The Envelope Theorem is particularly useful for analyzing the effect of parameter changes on **optimized value functions**.

&nbsp;

### 5.2 The Principle of the Envelope Theorem

Consider the optimization problem:

```math
\max_x f(x,a),
```

where $x$ is the choice variable and $a$ is an exogenous parameter.

Assume an interior optimum $x^*(a)$ satisfying the FOC:

```math
\frac{\partial f(x^*(a),a)}{\partial x}=0.
```

Define the optimized value function:

```math
M(a)=f(x^*(a),a).
```

By the chain rule,

```math
\frac{dM(a)}{da}
=
\underbrace{
\frac{\partial f}{\partial x}
\frac{dx^*(a)}{da}
}_{\text{Indirect effect}}
+
\underbrace{
\frac{\partial f}{\partial a}
}_{\text{Direct effect}}.
```

At the optimum,

```math
\frac{\partial f}{\partial x}=0.
```

Hence,

```math
\boxed{
\frac{dM(a)}{da}
=
\left.
\frac{\partial f(x,a)}{\partial a}
\right|_{x=x^*(a)}
}.
```

The indirect effect disappears due to the FOC.

The same principle applies to an interior minimization problem under appropriate regularity conditions.

**Constrained optimization**

For a constrained problem, the corresponding envelope result can be expressed using the Lagrangian:

```math
\boxed{
\frac{dV(a)}{da}
=
\left.
\frac{\partial\mathcal L}{\partial a}
\right|_{\text{optimum}}
}.
```

This assumes suitable differentiability and constraint qualifications.

&nbsp;

### 5.3 Applications in Consumer Theory

#### 5.3.1 Utility Maximization: Marshallian Demand and Roy's Identity

Consider the consumer's utility maximization problem:

```math
v(p,y)
=
\max_{x\geq0}u(x)
\quad
\text{s.t.}\quad p\cdot x\leq y.
```

- $v(p,y)$: **Indirect Utility Function**
- $x^M(p,y)$: **Marshallian (Uncompensated) Demand**

The optimal consumption bundle is

```math
x^M(p,y)
\in
\arg\max_{x\geq0}
\left\{u(x):p\cdot x\leq y\right\}.
```

Construct the Lagrangian:

```math
\mathcal L
=
u(x)+\lambda(y-p\cdot x).
```

By the Envelope Theorem,

```math
\boxed{
\frac{\partial v(p,y)}{\partial y}
=
\lambda^*
}
```

and

```math
\boxed{
\frac{\partial v(p,y)}{\partial p_i}
=
-\lambda^*x_i^M(p,y)
}.
```

Combining the two expressions:

```math
\boxed{
x_i^M(p,y)
=
-\frac{
\partial v(p,y)/\partial p_i
}{
\partial v(p,y)/\partial y
}
}.
```

This is **Roy's Identity**.

It recovers Marshallian demand from the derivatives of the indirect utility function, assuming $\partial v/\partial y>0$.

&nbsp;

#### 5.3.2 Expenditure Minimization: Hicksian Demand and Shephard's Lemma

Consider the expenditure minimization problem:

```math
e(p,\bar u)
=
\min_{x\geq0}p\cdot x
\quad
\text{s.t.}\quad u(x)\geq\bar u.
```

- $e(p,\bar u)$: **Expenditure Function**
- $x^H(p,\bar u)$: **Hicksian (Compensated) Demand**

The optimal consumption bundle is

```math
x^H(p,\bar u)
\in
\arg\min_{x\geq0}
\left\{p\cdot x:u(x)\geq\bar u\right\}.
```

Thus,

```math
e(p,\bar u)
=
p\cdot x^H(p,\bar u).
```

Construct the Lagrangian:

```math
\mathcal L
=
p\cdot x+\lambda[\bar u-u(x)].
```

By the Envelope Theorem,

```math
\boxed{
\frac{\partial e(p,\bar u)}{\partial p_i}
=
x_i^H(p,\bar u)
}.
```

This is **Shephard's Lemma**.

It recovers Hicksian demand from the expenditure function.

Similarly,

```math
\boxed{
\frac{\partial e(p,\bar u)}{\partial\bar u}
=
\lambda^*\geq0
}.
```

The multiplier measures the marginal expenditure required to increase the target utility level.

**Marshallian vs. Hicksian Demand**

- **Marshallian Demand** $x^M(p,y)$: Maximizes utility given prices and income.
- **Hicksian Demand** $x^H(p,\bar u)$: Minimizes expenditure given prices and a fixed utility level.

&nbsp;

### 5.4 Applications in Production Theory

#### 5.4.1 Profit Maximization: Hotelling's Lemma

Consider the profit maximization problem:

```math
\pi(p,w)
=
\max_{z\geq0}
\left\{
pf(z)-w\cdot z
\right\},
```

where $p$ is the output price, $w$ is the vector of input prices, and $z$ is the input vector.

By the Envelope Theorem,

```math
\boxed{
\frac{\partial\pi(p,w)}{\partial p}
=
q^*
}
```

where $q^*=f(z^*)$ is optimal output.

Similarly,

```math
\boxed{
\frac{\partial\pi(p,w)}{\partial w_i}
=
-z_i^*
}.
```

These are applications of **Hotelling's Lemma**:

- $\partial\pi/\partial p=q^*$: **Output Supply**
- $-\partial\pi/\partial w_i=z_i^*$: **Factor Demand**

&nbsp;

#### 5.4.2 Cost Minimization: Conditional Factor Demand

Consider

```math
C(w,q)
=
\min_{z\geq0}w\cdot z
\quad
\text{s.t.}\quad f(z)\geq q.
```

The cost function $C(w,q)$ represents the minimum cost of producing output $q$ at input prices $w$.

By the Envelope Theorem,

```math
\boxed{
\frac{\partial C(w,q)}{\partial w_i}
=
z_i^c(w,q)
}.
```

This gives **Conditional Factor Demand**.

Similarly,

```math
\boxed{
\frac{\partial C(w,q)}{\partial q}
=
MC(w,q)
}.
```

The derivative of the cost function with respect to output gives **Marginal Cost**.

&nbsp;

### 5.5 Connection to the Slutsky Equation

Marshallian and Hicksian demand are connected through the expenditure function:

```math
x_i^H(p,\bar u)
=
x_i^M(p,e(p,\bar u)).
```

Differentiate with respect to $p_j$, holding $\bar u$ constant:

```math
\frac{\partial x_i^H}{\partial p_j}
=
\frac{\partial x_i^M}{\partial p_j}
+
\frac{\partial x_i^M}{\partial y}
\frac{\partial e}{\partial p_j}.
```

By **Shephard's Lemma**,

```math
\frac{\partial e(p,\bar u)}{\partial p_j}
=
x_j^H(p,\bar u).
```

At $\bar u=v(p,y)$,

```math
x_j^H(p,\bar u)=x_j^M(p,y).
```

Substituting,

```math
\frac{\partial x_i^H}{\partial p_j}
=
\frac{\partial x_i^M}{\partial p_j}
+
x_j^M
\frac{\partial x_i^M}{\partial y}.
```

Rearranging gives the **Slutsky Equation**:

```math
\boxed{
\frac{\partial x_i^M}{\partial p_j}
=
\underbrace{
\frac{\partial x_i^H}{\partial p_j}
}_{\text{Substitution effect}}
-
\underbrace{
x_j^M
\frac{\partial x_i^M}{\partial y}
}_{\text{Income effect adjustment}}
}.
```

The equation decomposes the Marshallian price effect into a substitution effect and an income effect adjustment.

Although the Slutsky Equation is not itself an Envelope Theorem identity, its derivation uses **Shephard's Lemma** to connect the expenditure function with Hicksian demand.



---

## 6. Types of Optimization Problems (todo)

This section will briefly classify common optimization problems.

- Linear programming
- Nonlinear programming
- Mixed-integer programming
- Dynamic programming
- Optimization under uncertainty
- Optimization in machine learning
- ...
- Economic applications (game theory, DSGE[macroeconomics])

---
