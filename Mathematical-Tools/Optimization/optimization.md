# Optimization

This note summarizes basic optimization tools used in economics.

Main topics:

- Unconstrained optimization
- Constrained optimization
- Lagrangian Method and KKT conditions
- *Interior and corner solutions* (todo)
- *Envelope theorem* (todo)
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

## 5. Envelope Theorem (todo)

This section will summarize the envelope theorem and its use in comparative statics.

- The envelope theorem studies how the optimized value changes when an external parameter changes.
- The indirect effect through the optimal choice disappears because of the first-order condition.
- It is widely used in consumer theory, producer theory, and comparative statics.

Possible applications to add later:

- Indirect utility function
- Expenditure function
- Profit function
- Roy's identity
- Shephard's lemma
- Hotelling's lemma

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
