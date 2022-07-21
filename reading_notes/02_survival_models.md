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

## The force of mortality

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
