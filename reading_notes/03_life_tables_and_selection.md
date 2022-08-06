# Chapter 3: Life Tables and Selections

Exclude 3.11 and 3.12

## Life tables

To create a life table, we need 

- $x_0$: initial age
- $\omega$: maximum or limiting age
- $l _{x_0}$: radix of the table, an arbitrary positive number indicating the population at the initial age, and
- ${} _t p_x$, the survival function.

Then, the life table is constructed using a function $l_x$ and 

$$
  l_{x_0+t} = l_{x_0} \cdot {} _t p _{x_0}
$$

for $t \in [0, \omega - x_0]$. And for $x_0 \leq x \leq x + t \leq \omega$, 

$$
  \boxed{l _{x+t} = l _x \cdot {} _t p _x}.
$$

If we let $L_{x,t}$ be a rv of the number of survivors to age $x + t$, it will follow a binomial distribution with parameters $l_x$ and ${} _t p _x$. 
$\mathrm{E}[L_{x,t}] = l_x \cdot {} _t p _x = l_{x + t}$, so $l_{x + t}$ can be interpret as the **expected number of survivors** at age $x + t$ given there are $l_x$ independent lives aged $x$.

Thus, to calculate the survival probability, we can use ${} _t p _x = l _{x+t} / l_x$.

In principle, a life table may be defined for all $x \in [x_0, \omega]$, but in practice, it is very common for a life table to be presented at integer ages only.

In some cases, a life table also shows the **expected number of deaths**,

$$
  \boxed{d_x = l_x - l_{x+1} = l_x \cdot q_x}.
$$

## Fractional age assumptions

Since a life table is usually tabulated at integer ages only, when we are calculating survival probabilities at non-integer ages, we need an additional assumption, which is called **fractional age assumption**.

### Uniform distribution of deaths

The uniform distribution of deaths (UDD) assumption is the most common one. It can be formulated in tow equivalent ways:

1. For $s \in [0, 1)$, we assume ${} _s q _x = s \cdot q_x$.
2. For a life $(x)$ where $x \in \mathbb{Z}_{>0}$, let $T_x$ is the future lifetime rv and $K_x$ is the curtate future lifetime rv. We define $R_x$ is the factional part of the future lifetime of $(x)$ lived in a year of death, hence $T_x = K_x + R_x$. We assume $R_x \sim \mathrm{Uniform}(0,1)$, independent of $K_x$.

While the textbook has the proof on why these 2 assumptions are equivalent, the first formulation is more useful for working with life tables. Immediately from the assumption, we have

$$
  l_{x+s} = l_x  - s\cdot d_x
$$

for $s \in [0, 1)$.

And for **survival function** at fractional ages, we have

$$
  \boxed{{} _{t+s} p _x = (1 - s)\cdot \frac{l _{x+t}}{l _x} + s\cdot \frac{l _{x+t+1}}{l _x} = (1-s) \cdot {} _t p _x + s \cdot {} _{t+1} p _x}.
$$

Under this assumption, the **pdf** of $T_x$ at fractional age is

$$
  f_x(s) = \frac{d({} _s q _x)}{ds} = \frac{d(s \cdot q _x)}{ds} = q_x,
$$

which is a constant for all $s \in [0, 1)$ at a given $x$. Since $f_x(s) = {} _s p_x \cdot \mu_{x+s}$, we have

$$
  q_x = {} _s p_x \cdot \mu_{x+s}.
$$

Because ${} _s p_x$ is a decreasing function and $q_x$ is a constant, the force of mortality is an increasing function for all $s \in [0,1)$, confirming it is an appropriate assumption. One drawback, albeit not serious, is that the force of mortality has discontinuities at integer ages.

### Constant force of mortality

A second fractional age assumption is that the force of mortality is constant between integer ages. Hence, for $x \in \mathbb{Z}_{>0}$, $\mu_{x+s}$ does not depend on $s, \forall s \in [0,1)$. We can denote $\mu_{x+s} = \mu_x^*$.

To calculate $\mu_x^*$, we use

$$
  \begin{aligned}
    p_x &= \exp\left(-\int_0^1 \mu_{x+s} ds\right) \\
    &= \exp\left(-\int_0^1 \mu_x^* ds\right) \\
    &= e^{-\mu_x^*},
  \end{aligned}
$$

hence 

$$
  \boxed{\mu_x^* = - \ln p_x}.
$$

To calculate any fractional **survival probability**,

$$
  {}_r p _x = \exp\left(-\int_0^r \mu_x^* ds\right) = e^{-r\cdot \mu_x^*} \implies \boxed{{} _r p_x = (p_x)^r}.
$$

for $r \in [0,1)$. Similarly, for $r,t >0$ and $r + t < 1$, 

$$
  \boxed{{} _r p _{x+t} = (p_x)^r}.
$$

## National life tables

A national life table captures mortality experience of the whole population of a country. It is regularly produced and usually has separate life tables for males and females, and possibly for other groups of individuals, e.g., race or socioeconomic groups.

In actual life tables,

- The value of $q_0$ is relatively high. It termed **perinatal mortality** and are high due to low survival rates for babies with serious congenital disabilities. The value of $q_x$ may not reach this level again until about age 55.
- rate of mortality is much lower after the first year, less than 10% of its level in the first year, and declines until around age 10.
- mortality rates for young adults males have a steeper incline than those for young females. This phenomenon is called **the accident hump** and can be observed from historical to current populations as well as across different countries. 
- Female mortality rates are less than male rates, sometimes very significantly.
- Gompertz' law can fit mortality rates quite well for later ages, but it cannot model the perinatal mortality nor the accident hump.

## Survival models for life insurance policyholders

## Life insurance underwriting

## Select and ultimate survival models

## Notation and formulas for select survival models

## Select life tables

## Some comments on heterogeneity in mortality

## Mortality improvement

Not in the exam. Please refer to section 3.11 and 3.12.
