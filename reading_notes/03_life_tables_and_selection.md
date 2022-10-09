# Chapter 3: Life Tables and Selections

Exclude 3.11 and 3.12

- [Chapter 3: Life Tables and Selections](#chapter-3-life-tables-and-selections)
  - [Life tables](#life-tables)
  - [Fractional age assumptions](#fractional-age-assumptions)
    - [Uniform distribution of deaths](#uniform-distribution-of-deaths)
    - [Constant force of mortality](#constant-force-of-mortality)
  - [National life tables](#national-life-tables)
  - [Survival models and underwriting](#survival-models-and-underwriting)
  - [Select and ultimate survival models](#select-and-ultimate-survival-models)
  - [Notation and formulas for select survival models](#notation-and-formulas-for-select-survival-models)
  - [Select life tables](#select-life-tables)
  - [Using life tables in exams](#using-life-tables-in-exams)
    - [For fractional-age survival calculation](#for-fractional-age-survival-calculation)
    - [For select survival model](#for-select-survival-model)
  - [Heterogeneity in mortality](#heterogeneity-in-mortality)
  - [Mortality improvement](#mortality-improvement)

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
$\mathrm{E}[L _{x,t}] = l_x \cdot {} _t p _x = l _{x + t}$, so $l _{x + t}$ can be interpret as the **expected number of survivors** at age $x + t$ given there are $l_x$ independent lives aged $x$.

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
2. For a life $(x)$ where $x \in \mathbb{Z}_{>0}$, let $T_x$ is the future lifetime rv and $K_x$ is the curtate future lifetime rv. We define $R_x$ is the fractional part of the future lifetime of $(x)$ lived in a year of death, hence $T_x = K_x + R_x$. We assume $R_x \sim \mathrm{Uniform}(0,1)$, independent of $K_x$.

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

which is a constant for all $s \in [0, 1)$ at a given $x$. Since $f _x(s) = {} _s p _x \cdot \mu _{x+s}$, we have

$$
  q _x = {} _s p_x \cdot \mu _{x+s}.
$$

Because ${} _s p_x$ is a decreasing function and $q_x$ is a constant, the force of mortality is an increasing function for all $s \in [0,1)$, confirming it is an appropriate assumption. One drawback, albeit not serious, is that the force of mortality has discontinuities at integer ages.

Given a curtate lifetime distribution, if we create a complete lifetime distribution using UDD (hence $S(t)$ is not continuous), we can show that

$$
  \mathring{e}_x = e_x + \frac{1}{2}.
$$

### Constant force of mortality

A second fractional age assumption is that the force of mortality is constant between integer ages. Hence, for $x \in \mathbb{Z} _{>0}$, $\mu _{x+s}$ does not depend on $s, \forall s \in [0,1)$. We can denote $\mu _{x+s} = \mu _x ^*$.

To calculate $\mu _x ^*$, we use

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

We can see between 2 integers, the survival probability **memoryless**, meaning it only depends on the length of the duration, not the start of the duration. We can also show this that the lifetime distribution between 2 integers has **exponential distribution**.

Given a curtate lifetime distribution, if we create a complete lifetime distribution using constance force of mortality (hence $S(t)$ is not continuous), we can show that

$$
  \mathring{e}_x = \sum _{j = 0}^\infty \frac{{} _{j+1} p _x - {} _{j} p _x}{\ln p _{j+1}}.
$$

<details><summary>Click here for derivation</summary>

$$
  \begin{aligned}
    \mathring{e} _x &= \int_0^1 {} _s p _x ds + \int_0^1 {} _{1+s} p _x ds + \int_0^1 {} _{2+s} p _x ds \cdots \\
    &= \int_0^1 {} _s p _x ds + \int_0^1 p _x \cdot {} _s p _{x+1} ds + \int_0^1 {} _2 p _x \cdot {} _s p _{x+2} ds + \cdots \\
    &= \int_0^1 (p _x)^s ds + p _x \cdot \int_0^1 {} (p _{x+1})^s ds + {} _2 p _x \cdot \int_0^1 (p _{x+2})^s ds + \cdots \\
    &= \frac{p _x - 1}{\ln p _x} + p _x \cdot \frac{p _{x+1} - 1}{\ln p _{x+1}} + {} _2 p _x \cdot \frac{p _{x+2} - 1}{\ln p _{x+2}} + \cdots \\
    &= \frac{p _x - 1}{\ln p _x} + \frac{{} _2 p _x - p _x}{\ln p _{x+1}} + \frac{{} _3 p _x - {} _2 p _x}{\ln p _{x+3}} + \cdots \\
    &= \sum _{j = 0}^\infty \frac{{} _{j+1} p _x - {} _{j} p _x}{\ln p _{j+1}}.
  \end{aligned}
$$

</details>

## National life tables

A national life table captures mortality experience of the whole population of a country. It is regularly produced and usually has separate life tables for males and females, and possibly for other groups of individuals, e.g., race or socioeconomic groups.

In actual life tables,

- The value of $q_0$ is relatively high. It termed **perinatal mortality** and are high due to low survival rates for babies with serious congenital disabilities. The value of $q_x$ may not reach this level again until about age 55.
- rate of mortality is much lower after the first year, less than 10% of its level in the first year, and declines until around age 10.
- mortality rates for young adults males have a steeper incline than those for young females. This phenomenon is called **the accident hump** and can be observed from historical to current populations as well as across different countries. 
- Female mortality rates are less than male rates, sometimes very significantly.
- Gompertz' law can fit mortality rates quite well for later ages, but it cannot model the perinatal mortality nor the accident hump.

## Survival models and underwriting

The mortality experience can be different between

- people who purchase life insurance policies and the whole population as a whole,
- people who purchase different types of life insurance, and
- people who purchase life insurance at different age.

Therefore, there are different life tables for different products.

When comparing the **national life tables vs the product specific life tables**, the product specific life tables usually have lower mortality, which be explained by:

- The time of the experience. Usually newer experience will have lower mortality rates due to overall health improvement.
- Different demographic. People who buy the specific type of insurance can have different socio-economic classification. People who buy insurance are likely to be richer and thus have better mortality rates.
- Selection from underwriting. Policyholders must complete an underwriting process that makes sure they are healthy enough to be insured at the time of purchase.

However, when we compare the **life tables of the same product but of different purchase ages**, we can see that

- the more recently the policy was purchased, the lower the force of mortality, and
- after some years has passed, different purchase ages will have the same force of mortality.

This is the effect of the underwriting process. People who recently purchase life insurance have recently gone through a health check, while people who have bought life insurance a while ago may no longer be healthy. But after a couple years, the effect of passing the health checks wears off, and the mortality rate may be the same as those who bough life insurance before them.

## Select and ultimate survival models

Previously, the mortality rates only depend on the current age. These models are called **aggregate survival models**. Because of the underwriting effect from the last section, the mortality of a group of individuals is usually described by a **select and ultimate survival model**, shortened to **select survival model**, where

- Future survival probabilities for an individual in the group depend on the **individual’s current age** and on **the age at which the individual joined the group**.
- There is a positive number (generally an integer), $d$, such that if an individual joined the group more than $d$ years ago, future survival probabilities depend only on current age. The initial selection effect is assumed to have worn off after $d$ years.

In a select survival model,

- an individual who enters the group at age $x$ is said to be **selected** (or just **select**) at age $x$,
- the period $d$ is call the **select period**, and 
- the mortality after the select period is called the **ultimate** mortality.

Selection is not a feature of national life tables since an individual can only enter the population at age 0 (ignoring immigration). But for life insurance, select survival models are important because the effect on mortality can be considerable.

The select period will be different for different contexts. Some term life tables have 5 years as select period, while some whole life and endowment tables only have 2 years of select period. Generally, more rigorous underwriting process leads to a longer selection impact.

## Notation and formulas for select survival models

We use $[x]$ to indicate an individual is selected at age $x$. Specifically,

- ${} _t p _{[x] + s}$ is the survival probability for an individual whose is selected at $x$, currently $x+s$, and survives to $x + s + t$,
- similarly, ${} _t q _{[x] + s}$ is the probability of that individual dies before $x + s + t$, and
- $\mu _{[x] + s}$ is the fore of mortality at age $x + s$ for an individual who was select at age $x$.

If $t$ is the number of years after selection and $x$ is the current age, 

- when $t < d$, $\mu _{[x-t] + t}$, ${} _s p _{[x-t] + t}$, and ${} _u | _s q _{[x-t] + t}$ are in the **select** part of the survival model, and 
- when $t \geq d$, they are in the **ultimate** part of the survival model.

## Select life tables

A **select life table** can be construct in a similar way as aggregate life table, but it need to reflect both the duration since selection and age during the select period.

Let $x_0$ be the minimal selection age. Let $d$ be the select period. We set some arbitrary number for $l _{x_0 + d}$. For age $y$ that is in the ultimate period, 

$$
  l_y = {} _{y - x} p _{x} \cdot l_{x},
$$

for $y > x \geq x_0 + d$. Note that in the ultimate period, we don't need to know the selection age.

And for age in the select period with selection age $x \geq x_0$, we can work backwards from $l_{x+d}$ (note $x+d$ is in the ultimate period):

- if $l _{x+d}$ and ${} _{d-t}p _{[x] + t}$ are known, $l _{[x] + t}$ is derived directly from $l _{x+d}$ for $0 \leq t \leq d$:

$$
  {} _{d-t}p _{[x] + t} = \frac{l _{x+d}}{l _{[x] + t}} \implies l _{[x] + t} = \frac{l _{x+d}}{{} _{d-t}p _{[x] + t}},
$$

- if $l _{[x] + t + 1}$ and $p _{[x] + t}$ are known, $l _{[x] + t}$ is derived from $l _{[x] + t + 1}$ recursively, starting from $l _{[x] + d -1}$ to $l _{[x]}$:

$$
  p _{[x] + t} = \frac{l _{[x] + t + 1}}{l _{[x] + t}} \implies l _{[x] + t} = \frac{l _{[x] + t + 1}}{p _{[x] + t}}.
$$


## Using life tables in exams

### For fractional-age survival calculation
When $l_x$ is provided in a life table, $d_x$ can also be calculated, making it easier to perform calculation under UDD assumption. We can simply calculate

$$
  {} _{t+s} p _x = \frac{l _{x+t} + s \cdot d _{x+t} }{l _x},
$$

where $t \in \mathbb{Z}_{\geq 0}$, $0 \leq s < 1$, and $d _{x+t} = l _{x+t} - l _{x+t+1}$.

### For select survival model

Select life tables can provide different values, for examples

-  the population, $l _{[x]}, l _{[x]+1}, \ldots, l _{[x]+d-1}, l _{x+d}$.
-  the mortality, $q _{[x]}, q _{[x]+1}, \ldots, q _{[x]+d-1}, q _{x+d}$.
-  sometimes $x$ is the select age, hence the suffices are $[x], [x]+1, \ldots, [x]+d-1, x+d$.
-  sometimes $x$ is the attained age, hence the suffices are $[x], [x-1] + 1, \ldots, [x-(d-1)]+d-1, x$.

When $q$ is provided, ${} _t p _{[x] + s}$ can be calculated iteratively:

- ${} _1 p _{[x] + s} = 1 - q _{[x] + s}$, and
- ${} _{t} p _{[x] + s} = {} _{t-1} p _{[x] + s} \cdot (1 - q _{[x] + s + t - 1})$

**Calculator trick**: iteratively calculation can be done relatively easily by referring to `ans` and copying previous formula. In TI-30XS MultiView, you can use select previous formula and click `enter`, the formula will be copied.

## Heterogeneity in mortality

Male and female have very different mortality, in shape and level, so are smoker vs non-smoker. Hence, there are usually different life table for male/female and smoker/non-smoker.

In addition, insurers will generally use product-specific mortality tables. The difference generally follows some principles according to mortality studies:

- Wealthier lives experience lighter mortality overall than less wealthy lives.
- **Self-selection** has some impact on mortality. People who has some reason to anticipate heavier mortality is less likely to buy annuity and more likely to by term insurance and whole life insurance. This is often called **adverse selection** or **anti-selection**. While underwriting can identify some selective factors, there may be other information that cannot be gleaned from the underwriting process (at least not without excessive cost). 
- The more rigorous the underwriting, the lighter the resulting mortality experience.
- All of these factors may be confounded by tax or legislative systems that encourage or require certain types of contracts. If there are tax benefit from buying annuity, there may be less self-selection for that product.

## Mortality improvement

Not in the exam. Please refer to section 3.11 and 3.12.
