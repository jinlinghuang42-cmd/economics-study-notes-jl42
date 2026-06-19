# Convexity

> Convexity is the structural property that makes optimization *tractable*: it decides
> whether a stationary point (FOC) is a max or a min, and it governs the **existence** and
> **uniqueness** of solutions.
>
> The note runs *set → function → application in optimization*.

---

## 1. Convex Set

A set $S$ is **convex** if, for any $x, y \in S$ and $\lambda \in [0,1]$, there is:

$$
\lambda x + (1-\lambda) y \in S
$$

| Convex Set | Non-convex Set |
|---|---|
| segment $\overline{xy}$ stays inside | some segment $\overline{xy}$ leaves the set |

> Sets come first: convex functions are defined over convex domains.

> todo: add pics

---

## 2. Concave & Convex Function

Let $\lambda \in [0,1]$.

| | **Concave** ($\cap$) | **Convex** ($\cup$) |
|---|---|---|
| Definition | $f(\lambda x+(1-\lambda)y) \ge \lambda f(x)+(1-\lambda)f(y)$ | $\le$ |
| Geometry | graph lies **above** the chord (secant) | graph lies **below** the chord |
| Second order ($C^2$) | Hessian $\nabla^2 f \preceq 0$ (NSD) | $\nabla^2 f \succeq 0$ (PSD) |
| Optimization role | **maximize** | **minimize** |

---

## 3. Extended of Concave & Convex

**Quasi-concave / quasi-convex** (weaker than concave/convex):

$$
\text{quasi-concave:} \quad f(\lambda x+(1-\lambda)y) \ge \min\lbrace f(x), f(y) \rbrace
$$

$$
\text{quasi-convex:} \quad f(\lambda x+(1-\lambda)y) \le \max\lbrace f(x), f(y) \rbrace
$$

Equivalently: the **upper contour sets** $\lbrace x : f(x) \ge c \rbrace$ are convex (quasi-concave), or the
**lower contour sets** are convex (quasi-convex).

**Strict** — replace $\ge$ / $\le$ with strict inequality for $x \neq y$, $\lambda \in (0,1)$;
rules out flat segments, so the optimum is unique.

**Strong** — curvature bounded away from zero by some $m > 0$ (i.e. $\nabla^2 f \preceq -mI$);
used for convergence-rate guarantees.

> **Why is utility usually only *quasi*-concave, not *strictly* concave?**
> Utility need not grow linearly — different input patterns (e.g. $x_1 : x_2 = 1 : 2$) can land
> on the **same indifference curve** (same utility level). Indifference curves convex toward the
> origin = convex upper contour sets = **quasi-concavity**, which is already enough for a
> well-behaved UMP solution.

---

## 4. Convexity in Optimization

| Convex programming | Concave programming |
|---|---|
| $\min f(x)$, $f$ convex | $\max f(x)$, $f$ concave (← UMP) |

**Convex optimization** = minimizing a convex function over a convex set, equivalently
maximizing a concave function over a convex set.

Why convex optimization is considered "easy" — its good properties:

1. every **local minimum is a global minimum**;
2. the **set of optimal solutions is convex**;
3. if **strictly convex**, there is **at most one** optimal point.

> **Complexity context (P / NP / NP-hard):**
> - **P** — can be solved quickly
> - **NP** — a given solution can be verified quickly
> - **NP-hard** — neither
>
> Convex optimization is generally in **P** ("easy").

---

> Framework adapted from the *Cornell University Computational Optimization Open Textbook*.
> (P.s.: "programming" was coined in WWII so the work could qualify for military funding —
> nothing to do with coding.)

**1. LP — Linear Programming**
- Tools: duality, interior-point methods, …
- LP is a **special case of convex optimization**: objective *and* constraints are linear; the
  optimum occurs at a **vertex or on the boundary** of the feasible region.

**2. NLP — Nonlinear Programming**
- **Unconstrained** → numerical methods: gradient descent · Newton's method (uses the Hessian) ·
  quasi-Newton (BFGS)
- **Constrained, equality** → Lagrange multipliers + Envelope theorem
- **Constrained, inequality** → KKT conditions
- **Convex optimization**, …

---

## 5. Application: Consumer Optimization

Budget set:

$$
B = \lbrace x \in \mathbb{R}^n_+ : p \cdot x \le y \rbrace
$$

Problem:

$$
\max_{x}\ u(x) \qquad \text{s.t.} \quad p \cdot x - y \le 0, \quad x \ge 0
$$

**Two layers of conditions:**

- **Necessary conditions (FOC).** Any optimum must satisfy the first-order conditions, but FOC
  alone cannot tell max from min from saddle — that classification needs the **convexity /
  concavity** of the objective.
- **Sufficient conditions (existence + uniqueness).**
  - ① $u(x)$ is continuous (real-valued)
  - ② $u(x)$ **quasi-concave** and $B$ a **convex set** → unique maximizer
  - ③ $B$ non-empty, closed, bounded $\Rightarrow$ **compact** (an open interval is non-compact)
    → a maximizer **exists** by the **Weierstrass (Extreme Value) theorem**

**Convexity ↔ Preferences:**

| Convex preferences | Concave preferences |
|---|---|
| $x' \succsim x^0,\ x' \neq x^0 \Rightarrow t x' + (1-t)x^0 \succ x^0,\ \forall t \in (0,1)$ (strict convexity) | → **extreme bundles** (very rare) |
| → more **balanced consumption bundles** preferred; corresponds to **quasi-concave utility** | |

---

## Appendix — Utility Functions (cross-reference)

>These are specific utility *functional forms*, not convexity per se; kept here only as a cross-reference.


| Utility | Form | Indifference curve | $\sigma$ | Convexity |
|---|---|---|---|---|
| Perfect substitutes | $a x_1 + b x_2$ | straight line | $\infty$ | linear → concave **and** convex; quasi-concave |
| Cobb–Douglas | $A x_1^a x_2^b$ | convex to origin | $1$ | strictly quasi-concave |
| Perfect complements (Leontief) | $\min\lbrace a x_1, b x_2 \rbrace$ | L-shaped (kinked) | $0$ | concave, not strict (kink) |
| CES | $(a x_1^\rho + b x_2^\rho)^{1/\rho},\ \rho \le 1,\ \rho \neq 0$ | convex to origin | $\frac{1}{1-\rho}$ | quasi-concave |


**CES nests the other three**:

- $\rho \to 1$: $\sigma \to \infty$ → **perfect substitutes**
- $\rho \to 0$: $\sigma = 1$ → **Cobb–Douglas**
- $\rho \to -\infty$: $\sigma \to 0$ → **perfect complements (Leontief)**

### With reference-dependent (Cobb–Douglas → Stone–Geary)

$$
u(x,y) = x^a y^b \quad \longrightarrow \quad u(x,y) = (x-c)^a (y-d)^b
$$

- "+" form, e.g. $(x+c)^a y^b$: baseline utility even with zero purchase
- "-" form, e.g. $(x-c)^a y^b$: minimum (subsistence) consumption threshold

### Quasi-linear utility function

$$
u(x_1, x_2) = v(x_1) + x_2, \quad v \quad is \text{ concave } (\ln x_1,\ \sqrt{x_1},\ \dots)
$$

$MU_{x_1} = v'(x_1)$ (independent), $MU_{x_2} = 1$ (constant) → demand for $x_1$ is
**independent of income**.
