# Chapter 2: Survival Models

## The future lifetime random variable
Let $(x)$ denotes a life aged $x$, where $x \geq 0$. We model the **future lifetime** of $(x)$ by a continuous random variable (rv) $T_x$. This means $x + T_x$ is the rv of age-at-death for $(x)$.

Let $F_x$ be the cumulative distribution function (cdf) of $T_x$, aka **lifetime distribution** from age $x$, i.e.

$$
    F_x(t) = \Pr[T_x \leq t],
$$

which represents the probability that $(x)$ does not survive beyond age $x + t$.

Similarly, the **survival function** is

$$
    S_x(t) = 1 - F_x(t) = \Pr[T_x > t],
$$

which represents the probability that $(x)$ survives for at least $t$ years.

Note that $T_x$ is a rv that already assume the life already reaches age $x$. In other word,

$$
    \begin{aligned}
        \Pr[T_x \leq t] &= \Pr[T_0 \leq x + t | T_0 > x] \\
        &= \frac{\Pr[x < T_0 \leq x + t]}{\Pr[T_0 > x]} \\
        F_x(t) &= \frac{F_0(x+t) - F_0(x)}{S_0(x)}.
    \end{aligned}
$$

Represent it with the survival function,

$$
    S_x(t) = \frac{S_0(x+t)}{S_0(x)} \iff S_0(x+t) = S_0(x) S_x(t).
$$

This is important because we can interpret the probability of survival from birth to age $x + t$ as the product of
1. the probability of survival from birth to $x$, and 
2. the probability, having survived to $x$, of further surviving to age $x+t$.

To generalize it a bit further, if we know the survival probabilities from $x \geq 0$, then we also know survival probabilities from any future age $x + t$, where $t \geq 0$:

$$
    S_x(t+u) = S_x(t) S_{x+t}(u).
$$

A survival function also needs to satisfy the following **conditions**:
1. $S_x(0) = 1$;
2. $\lim_{t \to \infty} S_x(t) = 0$ (i.e. all lives will die);
3. $S_x(t)$ must be a non-increasing function of $t$.

These are both necessary and sufficient for $S_x(t)$ to be a survival function. However, we have 3 more **assumptions**:
1. $S_x(t)$ is **differentiable** for all $t > 0$;
2. $\lim_{t \to \infty} t S_x(t) = 0$;
3. $\lim_{t \to \infty} t^2 S_x(t) = 0$.

Assumptions 2 and 3 ensure that the **mean and variance exist** for $T_x$.

## The force of mortality
To understand the force of mortality, $\mu_x$, we can interpret it as the probability of dying infinitesimally soon (normalized by unit time).

$$
    \mu_x = \lim_{dx \to 0^+} \frac{\Pr[T_x \leq dx]}{dx}.
$$
### Mortality laws

## Actuarial notation


$$
    \begin{aligned}
      _tp_x &= \Pr[T_x > t] = S_x(t) \\
      _tq_x &= \Pr[T_x \leq t] = 1 - S_x(t) = F_x(t) \\
      _u|_tq_x &= \Pr[u < T_x \leq u + t] = S_x(u) - S_x(u+t)
    \end{aligned}
$$

## Mean and standard deviation of $T_x$

## Curtate future lifetime
### $K_x$ and $e_x$

### Comparing $\mathring{e}$ and $e_x$
 