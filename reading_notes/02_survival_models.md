# Chapter 2: Survival Models

- [Chapter 2: Survival Models](#chapter-2-survival-models)
  - [The future lifetime random variable](#the-future-lifetime-random-variable)
  - [The force of mortality](#the-force-of-mortality)
    - [Derive survival function from force of mortality](#derive-survival-function-from-force-of-mortality)
    - [Mortality laws](#mortality-laws)
  - [Actuarial notation](#actuarial-notation)
  - [Complete expectation of life](#complete-expectation-of-life)
    - [Term expectation of life](#term-expectation-of-life)
  - [Curtate future lifetime](#curtate-future-lifetime)
    - [Expected curtate lifetime](#expected-curtate-lifetime)
      - [Recursive formula for expected curtate lifetime](#recursive-formula-for-expected-curtate-lifetime)
    - [Comparing $\mathring{e}$ and $e_x$](#comparing-mathringe-and-e_x)
  - [Generalized Gompertz-Makeham formula](#generalized-gompertz-makeham-formula)

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
To understand the **force of mortality**, $\mu_x$, aka the **hazard rate** or **failure rate**, we can interpret it as the probability of dying infinitesimally soon (normalized by unit time).

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

### Derive survival function from force of mortality

Notice that for differentiable function $h$ where $h(x) > 0$ for all $x$, we have $\displaystyle{\frac{d}{dx} \log h(x)} = \frac{1}{h(x)} \frac{d}{dx} h(x)$. Hence, we can derive $\mu_x$ from $S_0(x)$:

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

The **Gompertz' law** assumes that

$$
  \mu_x = Bc^x,
$$

where $B > 0$ and $c > 1$. It assumes that the force of mortality increases exponentially with age.

The **Makeham's law**, which is a generalization of Gompertz' law, assumes that 

$$
  \mu_x = A + Bc^x,
$$

where $A,B > 0$ and $c > 1$. The added constant $A$ was designed to reflect the risk of accidental death, and it has more impact when $x$ is small. 

A simple way to remember which is which is that the letter 'a' appears in both Makeham's name and his mortality law.

While the Gompertz' law and the Makeham's law are the most useful ones, there are other mortality laws.
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

## Complete expectation of life

Let $\mathring{e}_x$ denote the expected future lifetime of $(x)$, $\mathrm{E}[T_x]$. We call this the **complete expectation of life**:

$$
  \boxed{\mathring{e}_x = \int_0^\infty tf_x(t) dt = \int_0^\infty {}_tp_x dt}.
$$

<details><summary>Click here for derivation</summary>

Using the fact that $f_x(t) = -S'_x(t)$, we have

$$
  \begin{aligned}
    \mathring{e}_x 
    &= \int_0^\infty tf_x(t) dt \\
    &= \int_0^\infty t \cdot \left[-\frac{dS_x(t)}{dt}\right]dt
  \end{aligned}
$$

Let $u = t$ and $dv = dS_x(t)$. Then $v = S_x(t)$. We have

$$
  \begin{aligned}
    \mathring{e}_x 
    &= - \int_0^\infty t \cdot \left[\frac{dS_x(t)}{dt}\right] dt \\
    &= -\left(\Bigl[tS_x(t)\Bigr]_0^\infty - \int_0^\infty S_x(t)dt\right) \\
    &= \int_0^\infty S_x(t)dt
  \end{aligned}
$$

---
</details>

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

Note that not all models can have a analytic formulae for $\mathring{e}_x$. For example, if we model mortality using Gompertz' law, there is no explicit formula for $\mathring{e}_x$. However, with modern technology (i.e. desmos calculator), we can plot and tabulate the complete expectation of life at different age (see more in this [desmos plot](https://www.desmos.com/calculator/5mvvr9pa1b)).

**Theorem** (Exercise 2.11a in AMLCR3e) $\mathring{e} _x \leq \mathring{e} _{x+1}+1$. Intuitively, lives aged $x$ may not live for a year, so $\mathring{e} _x + x \leq \mathring{e} _{x+1} + x + 1$. We can also prove this from the definition.

<details><summary>Click here for proof</summary>

$$
  \begin{aligned}
    \mathring{e} _x - \mathring{e} _{x+1} &= \int_0^\infty S_x(t) dt - \int_0^\infty S _{x+1}(t) dt \\
    &= \int_0^\infty S_x(t) dt - \int_0^\infty \frac{S _{x}(t+1)}{S_x(1)} dt \\
    &= \int_0^\infty S_x(t) dt - \int_1^\infty \frac{S _{x}(t)}{S_x(1)} dt \\
    &\leq \int_0^\infty S_x(t) dt - \int_1^\infty S _{x}(t) dt \\
    &= \int_0^1 S_x(t) dt \\
    &\leq \int_0^1 1 dt = 1.
  \end{aligned}
$$

---
</details>

We can also take this further to show $\mathring{e} _x \leq \mathring{e} _{x+t}+t$.

### Term expectation of life

Sometimes it is useful to cap the lifetime rv to model term insurance. The expected value of of $\min(T_x, n)$ is called the **term expectation of life**, denoted $\mathring{e}_{x:\overline{n|}}$, and can be calculated as 

$$
  \mathring{e}_{x:\overline{n|}} = \int_0^n {}_tp_x dt.
$$

## Curtate future lifetime

The **curtate future lifetime** rv for a life aged $x$, denoted as $K_x$, is defined as the integer part of future lifetime

$$
  K_x = \lfloor T_x \rfloor,
$$

where $\lfloor \cdot \rfloor$ is the floor function. This is the complete years lived in the future by $(x)$. This is important in actuarial contexts because future payments are made periodically, usually annually.

By definition,

$$
  \begin{aligned}
    \Pr[K _x = k] &= \Pr[k \leq T _x < k+1] \\  
    &= {} _k|q _x \\
    &= {} _kp _x - {} _{k+1}p_x \\
    &= {} _kp _x - {} _kp _x\cdot p _{x+k} \\
    &= {} _kp _x\cdot q _{x+k}.
  \end{aligned} 
$$

### Expected curtate lifetime

The expected curtate lifetime, denoted $e_x$, can be calculated as 

$$
  \boxed{e _x = \sum _{k=1}^\infty {} _kp _x},
$$

and note that the summation starts from $k=1$ instead of $0$. This can be interpreted as summing the probability of living $k$ years for $k \geq 1$.

<details><summary>Click here for derivation</summary>

$$
  \begin{aligned}
    \mathrm{E}[K _x] &= \sum_{k=0}^\infty k\cdot ({} _kp _x - {} _{k+1}p _x) \\
    &= ({} _1p _x - {} _2p _x) + 2({} _2p _x - {} _3p _x) + 3({} _3p _x - {} _4p _x) + \cdots \\
    &= \sum _{k=1}^\infty {} _kp _x
  \end{aligned}
$$

---
</details>

The second moment of $K_x$ is

$$
  \mathrm{E}[K _x^2] = \sum _{k=1}^\infty (2k-1)\cdot {} _kp _x = 2\sum _{k=1}^\infty (k \cdot {} _kp _x) - e _x,
$$

and note again the summation starts from $k=1$ and its derivation is similar to that of $e_x$.

For term expected curate lifetime, i.e., the expected value of $\min(K_x, n)$, it can be calculated as

$$
  e _{x:\overline{n|}} = \sum _{k=1}^n {} _k p _x.
$$

#### Recursive formula for expected curtate lifetime

We can use $e_x$ and $p_x$ to calculate $e_{x+1}$: 

$$
  \boxed{e _{x+1} = \frac{e _x}{p _x} - 1}.
$$

<details><summary>Click here for derivation</summary>

$$
  \begin{aligned}
    e _{x+1} &= \sum _{k=1}^{\infty} {} _k p _{x+1} \\
    &= \sum _{k=1}^{\infty} \frac{{} _{k + 1} p _{x}}{{} _1 p _x} \\
    &= \frac{1}{p _x}\cdot \left(\sum _{k=1}^{\infty} {} _{k} p _{x} - {} _1 p _x \right)\\
    &= \frac{1}{p _x}(e _x - {} _1 p _x) = \frac{e _x}{p _x} - 1.
  \end{aligned}
$$

---
</details>

### Comparing $\mathring{e}$ and $e_x$

The curtate expected lifetime can be considered as an approximation of the complete expected lifetime. The former, instead of calculating area under the survival function, sums the area of the rectangles under it.  Hence, 

$$
  e _x < \mathring{e} _x.
$$

If we assume the lifetime variable within a year is uniformly distributed (which is a fair assumption because the chance of dying in December isn't much larger than dying in January), then

$$
  \mathring{e} _x \approx e _x + \frac{1}{2}.
$$

Because the mortality difference between the end of year and the beginning of year is larger for older lives than for younger lives, this approximation is less accurate at very old ages.

## Generalized Gompertz-Makeham formula

The Geompertz-Makeham approach has been generalize further to give the $\mathrm{GM}(r,s)$ (Gompertz-Makeham) formula,

$$
  \mu _x = h^1 _r(x) + e^{h^2 _s(x)},
$$

where $h_r^1$ and $h_s^2$ are polynomials in $x$ of degree $r$ and $s$, respectively.
