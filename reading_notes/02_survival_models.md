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
    \boxed{S_x(t+u) = S_x(t) S_{x+t}(u)}.
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
  \begin{aligned}
    \mu_x &= \lim_{dx \to 0^+} \frac{\Pr[T_x \leq dx]}{dx} \\
    &= \lim_{dx \to 0^+} \frac{1 - S_x(dx)}{dx}.
  \end{aligned}
$$

Since $\displaystyle{S_x(dx) = \frac{S_x(x + dx)}{S_0(x)}}$, we have

$$
  \begin{aligned}
    \mu_x &= \frac{1}{S_0(x)} \lim_{dx \to 0^+} \frac{S_0(x) - S_0(x + dx)}{dx} \\
    &= - \frac{1}{S_0(x)}S_0'(x)
  \end{aligned}
$$

Since $f_x = F_x' = -S_x'$, we then have

$$
  \boxed{\mu_x = \frac{f_0(x)}{S_0(x)}}.
$$

Similarly, for a live aged $x$, the force of mortality at age $x+t$ is

$$
  \boxed{\mu_{x + t} = \frac{f_x(t)}{S_x(t)}}.
$$

Since $F_x(t) = \int_0^t f_x(s) dx$, we can write

$$
  \boxed{F_x(t) = \int_0^t S_x(s) \mu_{x + s} ds}.
$$

This is important because this can be interpret as the following: the probability of dying in $t$ is the integral (i.e. "infinitesimal sum") of the probability of surviving to $s$ $\times$ the probability of dying in interval $(s, s+ds)$ for $s \in (0, t)$.

**Converting $\mu_x$ back to $S_x$**

Notice that for differentiable function $h$ where $h(x) > 0$ for all $x$, we have $\displaystyle{\frac{d}{dx} \log h(x)} = \frac{1}{h(x)} \frac{d}{dx} h(x)$. Hence,

$$
  \boxed{\mu_x = -\frac{d}{dx} \log S_0(x)}.
$$

If we integrate both size over $(0, t)$,

$$
  \int_0^t \mu_x dx = -\Bigl[\log S_0(x)\Bigr]^t_0 = - \log S_0(t).
$$

Hence,

$$
  \boxed{S_0(t) = \exp \left(-\int_0^t \mu_x dx\right)},
$$

and 

$$
  \boxed{S_x(t) = \frac{S_0(x+t)}{S_0(x)} = \exp \left(-\int_x^{x+t} \mu_r dr\right) = \exp \left(-\int_0^t \mu_{x+s} ds\right)}.
$$

This is important because if we know $\mu_y$ for all $y \geq 0$, then we can calculate all survival probabilities $S_x(t)$, for any $x$ and $t$. 
In other words, the force of mortality can fully describes the lifetime distribution, just like the survival function does.

### Mortality laws

Mortality laws are some assumptions made on the the force of mortality.

The **Gompertz's law** assumes that

$$
  \mu_x = Bc^x,
$$

where $B > 0$ and $c > 1$. It assumes that the force of mortality increases exponentially with age.

The **Makeham's law**, which is a generalization of Gompertz's law, assumes that 

$$
  \mu_x = A + Bc^x,
$$

where $A,B > 0$ and $c > 1$. The added constant $A$ was designed to reflect the risk of accidental death, and it has more impact when $x$ is small. 

A simple way to remember which is which is that the letter 'a' appears in both Makeham's name and his mortality law.

While the Gompertz's law and the Makeham's law are the most useful ones, there are other mortality laws.
- **De Moivre's law**
  - one of the earliest mortality laws
  - $\mu_x = 1 / (\omega - x)$ and $S_0(x) = 1 - x / \omega$ for $x in [0, \omega)$
  - since it assumes $T_x$ has a uniform distribution on $(0, \omega)$, it is a very unrealistic model for human population.
- **Generalized De Moivre's law**
  - $\mu_x = \alpha / (\omega - x)$ for $x in [0, \omega)$
  - it assumes the $T_x$ has a [beta distribution](https://en.wikipedia.org/wiki/Beta_distribution), which is also not very realistic.
- **Constant force of mortality**
  - assume the force of mortality is a constant and $T_x$ has an exponential distribution
  - also very unrealistic for human context
- While these mortality laws are not realistic for human mortality, it can be useful in other contexts, such as modelling the failure time of machine components.


## Actuarial notation

Actuarial science has developed its own notation, the **International Actuarial Notation**:

$$
  \begin{aligned}
    _tp_x &= S_x(t) \\
    _tq_x &= 1 - S_x(t) = F_x(t) \\
    _u|_tq_x &= \Pr[u < T_x \leq u + t] = S_x(u) - S_x(u+t)
  \end{aligned}
$$

$p$ represents the probability of surviving while $q$ is the probability of dying. If $t = 1$, it can be omitted, e.g., $_1q_x = q_x$.

In actuarial terminology, 
- $q_x$ is called the **mortality rate** at age $x$,
- $_u|_tq_x$ is called a **deferred mortality probability**.

We can then rewrite all the important definitions and relations using the actuarial notation.
## Mean and standard deviation of $T_x$

Let $\mathring{e}_x$ denote the expected future lifetime of $(x)$, $\mathrm{E}[T_x]$. We call this the **complete expectation of life**. By the definition of expected value, we have (note that the second equation can be derived using integration by part[^bypart])

$$
  \mathring{e}_x = \int_0^\infty tf_x(t) dt = \int_0^\infty S_x(t) dt = \int_0^\infty {}_tp_x dt.
$$

[^bypart]:
    $\displaystyle{\int_0^\infty tf_x(t) dt = \int_0^\infty t \cdot \left[-\frac{dS_x(t)}{dt}\right]dt}$. Let $u = t$ and $dv = dS_x(t)$. Then $v = S_x(t)$. We have $\displaystyle - \int_0^\infty t \cdot \left[-\frac{dS_x(t)}{dt}\right] dt = -\left(\Bigl[tS_x(t)\Bigr]_0^\infty - \int_0^\infty S_x(t)dt\right) = \int_0^\infty S_x(t)dt$.

Similarly, for $\mathrm{E}[T^2_x]$, we have

$$
  \begin{aligned}
    \mathrm{E}[T^2_x] &= \int_0^\infty t^2f_x(t)dt \\
    &=2\int_0^\infty tS_x(t)dt = 2\int_0^\infty  t\cdot {}_tp_xdt.
  \end{aligned}
$$

Hence, the variance of $T_x$ can be calculated as

$$
  \mathrm{Var}[T_x] = \mathrm{E}[T^2_x] - (\mathring{e}_x)^2 = 2\int_0^\infty  t\cdot {}_tp_xdt - \left[\int_0^\infty {}_tp_x dt\right]^2.
$$


## Curtate future lifetime
### $K_x$ and $e_x$

### Comparing $\mathring{e}$ and $e_x$
 