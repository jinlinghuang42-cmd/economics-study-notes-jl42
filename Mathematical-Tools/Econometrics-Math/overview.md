# Mathematical Foundations of Econometrics

> An overview note. This folder collects the mathematical tools econometrics rests on. This file frames *what kind of math this is*, *how it differs from the calculus in the other folder*, and organizes the tools by the three jobs of econometrics (**identification, estimation, inference**), since each rests on a different branch of math. Individual topics will get their own files later.

## 1. Theory vs. Empirics

Economic theory and empirical work draw on different mathematics, because they do different jobs. The contrast below is between the two toolkits most central to each side. It is not a claim that these are the only kinds of math economics uses.

The `Calculus` folder covers the math that **theory** leans on most: optimization, including gradients, Lagrange multipliers, and convexity. The setting is one where a consumer maximizes utility under a budget constraint, a firm maximizes profit, or a planner maximizes welfare. The core action is *solving a model*. Given a model, one computes the optimal choice, so the direction is model → behavior. A typical move there is a first-order condition:

```math
\max_{x} \; u(x) \quad\Longrightarrow\quad \nabla u(x^*) = 0.
```

This folder covers the math that **empirical work (econometrics)** leans on. Probability and statistics are at its core, though the field also borrows from optimization, set theory, and analysis (as the later sections show). The setting is one where data come with random noise and we want to recover the true parameter behind them. The core action is *inferring from data*. Given noisy, incomplete data, the truth is backed out, so the direction is data → parameter. A typical move here is replacing an unknown population average by a sample average.

In one line: **theory's math finds the optimum in a deterministic world; empirical math finds the truth in a random world.** The two are not permanently separate. They meet in **structural estimation**, where the optimization math first solves the model, and then the probability and statistics math estimates its parameters from data.

What is a **structural model**? It is a fully specified model of how an agent makes a decision, derived from an explicit optimization problem (for example, a consumer choosing whether to buy insurance by trading off its cost against the protection it provides). Several pieces fit together:

- **Deep (structural) parameters.** Quantities such as risk aversion, the discount rate, or technology. They characterize preferences or constraints and are assumed to be stable across environments.
- **Structural estimation.** The procedure of recovering these deep parameters from data. This is precisely where both sets of math are required together: the optimization math (calculus) solves the agent's problem to obtain a behavior rule, such as an Euler equation or a choice probability, and the probability/statistics math estimates the deep parameters of that rule from noisy data, typically by GMM or MLE.
- **The payoff.** Because the deep parameters are policy-invariant, the estimated model can predict behavior in environments not observed in the data, that is, a *counterfactual*, which reduced-form methods cannot do.
- **The cost.** The results are only as valid as the assumed model.

## 2. Basic blocks

**Expectation.** The expectation of a random variable is its probability-weighted average, the "center" it fluctuates around:

```math
\mathbb{E}[X] = \sum_x x\, p(x) \quad\text{(discrete)}, \qquad \mathbb{E}[X] = \int x\, f(x)\, dx \quad\text{(continuous)}.
```

**Variance.** How far $X$ spreads around that center, the second moment:

```math
\mathrm{Var}(X) = \mathbb{E}[(X - \mathbb{E}[X])^2].
```

(A note on the word **moment**: in statistics a "moment" is a summary of a distribution, where the first moment is the mean and the second relates to the variance. It has nothing to do with a *matrix*; the two words happen to share the character 矩 in Chinese but are entirely unrelated.)

Mean and variance are the basic summaries that estimators try to match between sample and population.

**Conditional expectation.** The average of $Y$ *given* a value of $X$, written $\mathbb{E}[Y \mid X]$. This is the mathematical heart of regression: a regression is essentially an estimate of how this conditional average moves with $X$. Roughly,

```math
Y = \mathbb{E}[Y \mid X] + \varepsilon, \qquad \mathbb{E}[\varepsilon \mid X] = 0.
```

## 3. Identification

Identification asks a question that comes *before* any data work: even in the best case, where the sample is so large that random sampling error has vanished, can the parameter be pinned down from what the data reveal? Identification is therefore not about statistical precision. It is about whether the data, even perfect data, contain enough information to single out one answer.

A concrete example makes this clear. Suppose the data show that cities with more police have more crime, and we want the causal effect of police on crime. The correlation alone cannot deliver it, because at least two opposite stories produce the very same data: police could increase crime, or high-crime cities could hire more police (reverse causation). No sample, however large, can separate these two stories on its own. When different parameter values imply the *same* observable distribution like this, they are called **observationally equivalent**, and the **identified set** $\Theta_I$ collects every parameter value observationally equivalent to the true one $\theta_0$:

```math
\Theta_I = \{ \theta \in \Theta : \theta \text{ is observationally equivalent to } \theta_0\}.
```

The parameter is **point identified** if this set is a single value, $\mathrm{card}(\Theta_I) = 1$ (the standard case usually assumed), and **partially identified** if it is larger than a point but smaller than everything, $1 < \mathrm{card}(\Theta_I) < \mathrm{card}(\Theta)$, so the data narrow the parameter to a region but not to one value. An **identifying assumption** is what rules out the rival stories and shrinks $\Theta_I$. This is exactly what the standard designs do: randomizing which cities get more police (**RCT**) rules out reverse causation by construction; an instrument that shifts police for reasons unrelated to crime (**IV**) isolates the effect through its exclusion restriction; comparing before-and-after across treated and untreated cities (**DID**) relies on parallel trends. Each is an assumption strong enough to collapse $\Theta_I$ to a single point.

**Partial identification** takes the opposite stance: rather than impose a strong assumption that might be wrong, it keeps only weak, credible assumptions and accepts that the answer is a *set*, an honest range the effect must lie in. Such models often deliver **moment inequalities** (rather than equalities) that carve the set out:

```math
\Theta_I = \{ \theta \in \Theta : \mathbb{E}[m(W, \theta)] \geq 0\},
```

and to say how close an estimated set is to the true one, the ordinary $|\hat\theta - \theta|$ no longer works, so a distance *between sets* is needed, the **Hausdorff distance**:

```math
d_H(A, B) = \max \{ \sup_{a \in A}\inf_{b \in B} d(a,b),\ \sup_{b \in B}\inf_{a \in A} d(a,b) \}.
```

So the two roads trade off the same thing in opposite directions: point identification (RCT, IV, DID) bets on a strong assumption to get one precise number, while partial identification gives up precision for a range that is far more likely to be correct.

This is the most "pure-math" corner: set theory, convex analysis, and (at the frontier) random set theory.

**A little set-theory background (to-learn list; I haven't studied this yet).** The notation above leans on a few basic ideas from set theory that I want to learn properly:

- A **set** is just a collection of objects; here, $\Theta$ is the set of all possible parameter values, and $\Theta_I \subseteq \Theta$ is the subset consistent with the data.
- A **map (function)** sends each model to the observable distribution it implies. The reverse question, which models could have produced a given observed distribution (the **pre-image**), is exactly what identification is about: is that set of models a single one, or many?
- **Cardinality** $\mathrm{card}(\cdot)$ counts the elements of a set: $\mathrm{card}(\Theta_I) = 1$ means one point (point identified), more than one means a set (partially identified).
- **Convexity**: a set is convex if the segment between any two of its points stays inside it. Intervals and regions cut out by linear inequalities are convex, which is why moment inequalities produce well-behaved identified sets.

Identification is what justifies the key assumption behind each causal design, and the whole of partial identification:

- **RCT.** Randomization makes treatment independent of potential outcomes, so a simple comparison of groups identifies the causal effect.
- **IV.** Identification needs relevance (the instrument moves the treatment) and the exclusion restriction (the instrument affects the outcome only through the treatment).
- **DID.** Identification rests on the parallel-trends assumption: treated and control groups would have moved together absent the treatment.
- **RDD.** Identification rests on continuity at the cutoff, so units just above and just below are comparable.
- **Partial identification / bounds.** When these point-identifying assumptions are too strong, the parameter is identified only to a set (e.g. moment-inequality models, or games with multiple equilibria).

## 4. Estimation

An estimator is defined as the solution to an optimization: OLS minimizes the squared residuals, MLE maximizes a likelihood, GMM minimizes a weighted quadratic in the moments. So a first-order condition appears, and this is exactly where the calculus from the other folder re-enters:

```math
\hat\theta = \arg\min_{\theta} Q_n(\theta) \quad\Longrightarrow\quad \frac{\partial Q_n(\hat\theta)}{\partial \theta} = 0.
```

That the estimate actually lands on the truth as the sample grows, a property called **consistency** ($\hat\theta \xrightarrow{p} \theta_0$), rests on the **Law of Large Numbers (LLN)**, which says the sample average converges to the population mean:

```math
\bar{X}_n = \frac{1}{n}\sum_{i=1}^{n} X_i \;\xrightarrow{p}\; \mathbb{E}[X].
```

This is the formal reason "sample mean ≈ population mean" is allowed at all.

Every method that produces a point estimate is, underneath, an optimization solved this way:

- **OLS (Ordinary Least Squares).** Minimizes the sum of squared residuals.
- **MLE (Maximum Likelihood Estimation).** Assumes a full probability distribution for the data, then picks the parameter that makes the observed data the most likely under it. Because it assumes the whole distribution, it is efficient when that assumption is correct but biased if it is wrong. It is the standard tool when the outcome is not a plain continuous number, such as a yes/no choice, which is what **Logit** and **Probit** estimate: both model the *probability* of a 0/1 outcome (a firm enters a market or not, a person buys insurance or not), pressing the prediction into the 0-to-1 range. They differ only in the assumed distribution behind that probability (Logit uses the logistic, Probit the normal) and usually give very similar results.
- **GMM (Generalized Method of Moments).** Assumes only a few *moment conditions* (population averages the model says should equal zero, often coming from economic theory), then picks the parameter that makes the matching sample averages as close to zero as possible. Because it assumes less than a full distribution, it is more robust but typically a little less efficient than a correctly specified MLE. It is the general framework that contains OLS and IV as special cases.
- **2SLS (Two-Stage Least Squares).** The IV estimator, computed as two successive least-squares regressions.

MLE can in fact be written as a special case of GMM, so GMM is the wider framework and MLE is its most efficient special case.

## 5. Inference

Once an estimate is in hand, its random wobble around the truth is described by a distributional limit. The **Central Limit Theorem (CLT)** says that, scaled by $\sqrt{n}$, this wobble is approximately normal, *whatever* the original distribution of the data:

```math
\sqrt{n}\,(\hat\theta - \theta_0) \;\xrightarrow{d}\; \mathcal{N}(0,\ V).
```

That predictable normal limit is what produces standard errors, confidence intervals, and tests. Pushing inference to whole functions (nonparametrics, ML-based causal inference) needs **empirical process theory**, the deep end.

Everything that quantifies how reliable an estimate is:

- **Standard errors (robust / clustered).** Measure the sampling variability of an estimate, allowing for heteroskedasticity or within-group correlation.
- **Hypothesis tests ($t$, Wald).** Judge whether a coefficient differs from a hypothesized value, using the estimate's asymptotic distribution.
- **Bootstrap and resampling.** Approximate the sampling distribution by recomputing the estimate on resampled data, useful when a formula is unavailable.
- **Confidence intervals.** A range that covers the true value with a stated probability, including the set-valued confidence regions used under partial identification.

## 6. How the three layers connect

The three layers are not just parallel categories; they run in order, and each depends on the one before it.

1. **Identification** *Why can this coefficient be read as causal rather than mere correlation?* Before using data, the question is whether the parameter could be recovered even with infinite data. If it cannot be identified, no amount of estimation or inference will fix that.
2. **Estimation** *What is the coefficient?* Once the parameter is identified, a finite sample is used to actually compute it.
3. **Inference** *Has the uncertainty of this coefficient been computed correctly, and is its significance credible?* Given the estimate, the task is to quantify how much of its value is real signal versus sampling noise.

This ordering is also why the math differs by layer: identification is a logical question about infinite data (sets and logic), while estimation and inference are genuinely statistical (optimization and convergence for estimation, distributions and the CLT for inference). 

## Todo: What will go in this folder (later, each its own file)

Rough ideas: probability and distribution basics, moments and the method of moments, the large-sample results (LLN, CLT), conditional expectation and projection.

## The Broader Math of Econometrics

This section maps out the wider range of mathematics econometrics draws on. It is not a list of things I already know, but a guide to what exists, so I can fill it in over time. The foundations are what everyday applied work relies on; the extensions are deeper tools that appear mainly in econometric theory or in specialized topics. The extensions are things I haven't learned yet, so this doubles as a loose to-do list, though not everything here is something I will necessarily need to study.

**Foundations**

- **Linear algebra.** Vectors and matrices. *Used to:* write and compute OLS, IV/2SLS, and panel estimators (the regression formulas are matrix expressions).
- **Calculus and optimization.** Derivatives, gradients, first-order conditions. *Used to:* define estimators as the solution to a minimization or maximization (OLS, MLE, GMM).
- **Probability.** Random variables, distributions, expectation. *Used to:* model the error term and describe noisy data in every regression.
- **Statistics and asymptotic theory.** LLN, CLT, consistency, asymptotic normality. *Used to:* justify why estimators work and produce standard errors and tests.

**Extensions**

- **Numerical methods.** Optimization algorithms, simulation, integration. *Used to:* compute estimators with no closed form, such as many MLE models and simulation-based structural estimation (SMM, simulated MLE).
- **Set theory and logic.** Maps, pre-images, uniqueness. *Used to:* state and analyze identification, including identified sets in partial identification.
- **Convex analysis.** Convex sets and inequalities. *Used to:* moment-inequality models in partial identification, and convergence arguments in optimization.
- **Measure theory.** The rigorous foundation of probability (sample spaces, sigma-fields, expectation as an integral). *Used to:* prove the LLN and CLT rigorously, and define conditional expectation precisely (the object regression estimates).
- **Real analysis and metric spaces.** Convergence, continuity, and distances between objects, such as the Hausdorff distance between sets. *Used to:* establish consistency and asymptotic normality of estimators on a rigorous footing, and measure how close an estimated set is to the true set in partial identification.
- **Functional analysis.** Spaces of functions and operators (including Hilbert spaces and projection). *Used to:* nonparametric and series/sieve estimation (estimating a whole function rather than a few coefficients), and the projection view of regression and IV.
- **Empirical process theory.** The behavior of an entire estimated function uniformly across its range. *Used to:* inference in nonparametrics, kernel and series estimation, and modern machine-learning-based causal inference such as double/debiased machine learning.
- **Random set theory.** The math of sets that are themselves random. *Used to:* estimation and inference in partial identification, where the identified set must itself be estimated from data (moment-inequality models, set estimation).


## Reference

A partial list; more to be added as I read.

- Bruce E. Hansen, Probability and Statistics for Economists, Princeton University Press.
- Bruce E. Hansen, Econometrics, Princeton University Press.
