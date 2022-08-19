# Chapter 4: Insurance Benefits

- [Chapter 4: Insurance Benefits](#chapter-4-insurance-benefits)
  - [Introduction](#introduction)
  - [Assumptions](#assumptions)
  - [Valuation of insurance benefits](#valuation-of-insurance-benefits)
    - [Notation](#notation)
    - [Whole life insurance](#whole-life-insurance)
      - [The continuous case](#the-continuous-case)
      - [The annual case](#the-annual-case)
      - [The monthly case](#the-monthly-case)
      - [Recursions](#recursions)
    - [Term insurance](#term-insurance)
      - [The continuous case](#the-continuous-case-1)
      - [The annual case](#the-annual-case-1)
      - [The monthly case](#the-monthly-case-1)
    - [Pure endowment](#pure-endowment)
    - [Endowment insurance](#endowment-insurance)
    - [Deferred insurance](#deferred-insurance)
  - [Relating the continuous case, the annual case, and the monthly case](#relating-the-continuous-case-the-annual-case-and-the-monthly-case)
    - [Using the UDD assumption](#using-the-udd-assumption)
    - [Using the claims acceleration approach](#using-the-claims-acceleration-approach)
  - [Variable insurance benefits](#variable-insurance-benefits)


## Introduction
Here, we develop formulas for the valuation of traditional insurance benefits (e.g. whole life, term, and endowment insurance). It will be based on the complete lifetime rv $T_x$, the curtate future lifetime rv $K_x$, and a new rv $K^{(m)}_x$, the curtate future lifetime rv where each period is $1/ m$ year.

When valuing insurance benefits, we also need to combine survival models with time value of money to derive the distribution of the present value of an uncertain, life contingent future benefit. In this chapter, we will generally assume the interest rate is constant and fixed.

It is also easier if we work in continuous time (interest and annuity payment are paying continuously, death payment is paid at the exact time of death, etc.). In practice, insurers work in discrete time and discrete life tables are used.

## Assumptions

We use the term **basis** to denote a set of assumptions used in life insurance or pension calculations. Many example in the textbook uses the **standard ultimate survival model**:

$$
  \mu_x = A + Bc^x
$$

where $A = 0.00022$, $B = 2.7 \times 10^{-6}$, and $c = 1.124$.

A refresher on interest theory functions:

- $i$: effective annual rate of interest.
- $v = 1 / (1+i)$ and $d = 1 - v = i\cdot v$. $d$ is also called the effective rate of discount.
- $\delta = \ln(1+i) \iff e^\delta = 1 + i$. $\delta$ is the force of interest (aka the continuously compounded rate of interest). In financial mathematics contexts, and in particular if the rate of interest is assumed risk free, the common notation for the force of interest is $r$.
- $i^{(p)}$ is the nominal rate of interest compounded $p$ times per year: $1 + i = (1 + i^{(p)} / p)^p \iff i^{(p)} = p\cdot (\sqrt[p]{1+i}-1)$.
- $d^{(p)}$ is the nominal rate of discount compounded $p$ times per year: $(1 - d^{(p)}/p)^p = v \iff d^{(p)} = p(1 - \sqrt[p]{v})$.


## Valuation of insurance benefits

### Notation

- $A$: actuarial value of life insurance with benefit of 1 at the time of death
- $\bar{A}$: a bar indicates a continuous case
- $A^{\mathbf{(m)}}$: $\mathbf{(m)}$ indicates the $1/m$-thly case
- $A$ without a bar or $\mathbf{(m)}$ is the annual case
- $A_\mathbf{x}$: $\mathbf{x}$ is the current age of the insured
- ${} ^\mathbf{k} A$: $\mathbf{k}$ is the multiplier on the force of interest
- $A ^\mathbf{1} _{x:\overline{\mathbf{n}|}}$: term insurance of $\mathbf{n}$ years, the $\mathbf{1}$ on top of $x$ indicates the life $(x)$ must die before the term of $\mathbf{n}$ years expires in order for the benefit to be payable. 
- $A_{x:\overset{\mathbf{1}}{\overline{\mathbf{n}|}}}$: pure endowment insurance of $\mathbf{n}$ years, the $\mathbf{1}$ on top of $\overline{\mathbf{n}|}$ indicates the term of $\mathbf{n}$ years must expire before life $(x)$ dies in order for the benefit to be payable.
- ${}_n E_x$: same as $A_{x:\overset{1}{\overline{n|}}}$, but easier to typeset.
- $\bar{A} _{x:\overline{n|}}$: if there is not $1$ on top, it indicates the benefit will pay when $(x)$ dies or the term of $n$ years expires, i.e., a combination of term and pure endowment.
- ${} _\mathbf{u} | A$: the $\mathbf{u}$ indicates the death benefit coverage only starts after the deferred periods of $u$ years.

### Whole life insurance

We first consider the value of a benefit of 1 payable following the death of a life currently aged $x$.

#### The continuous case

For our life $(x)$ with lifetime distribution $T_x$, the present value of a benefit of 1 payable immediately on death is a rv $Z$:

$$
  Z = v^{T_x} = e^{-\delta\cdot T_x}.
$$

We usually concern the **Expected Present Value** (EPV), commonly referred to as the **Actuarial Value** (AV) or the **Actuarial Present Value** (APV). 

For the continuous case, we denote the AV of benefit of 1 payable at death is $\bar{A}_x$. Since $T_x$ has pdf $f_x(t) = {} _t p _{x} \cdot \mu _{x+t}$, we have

$$
  \bar{A} _x = \mathrm{E}[e^{-\delta\cdot T_x}] = \int_0^\infty e^{-\delta \cdot t}\cdot {} _t p _{x} \cdot \mu _{x+t}dt.
$$

There is a nice way to understand the formula if we interpret $\mu _{x+t}dt$ as the probability of dying during in infinitesimal duration $(t,t+dt)$ after current age $x$. Then, the formula is integrating (like summing)

$$
  (\text{PV of 1 paid at } t) \times (\text{Probability of surviving to } t) \times (\text{Probability of dying in } (t, t+dt))
$$

for $t \in (0, \infty)$.

To calculate the second moment of $Z$ (and then the variance),

$$
  \mathrm{E}[Z_x^2] = \mathrm{E}[e^{-2\delta\cdot T_x}] = \int_0^\infty e^{-2\delta \cdot t}\cdot {} _t p _{x} \cdot \mu _{x+t}dt = {} ^2 \bar{A}_x.
$$

Here, the left superscript indicates that the calculation is at force of interest $2\delta$ or at rate of interest $j$, where $1 + j = (1+i)^2$.

Then, the variance of $Z$ is

$$
  \mathrm{Var}[Z_x] = {} ^2 \bar{A}_x - (\bar A _x)^2.
$$

When the death benefit is $S$ instead of 1, the EPV is $\mathrm{E}[SZ_x] = S\cdot \mathrm{E}[Z_x] = S\cdot \bar A_x$ and the variance is $\mathrm{Var}[SZ] = S^2 \cdot \mathrm{Var}[Z] = S^2 \cdot ({} ^2 \bar{A}_x - (\bar A _x)^2)$.

We can also calculate the **cdf** of $Z_x$:

$$
  \begin{aligned}
    \Pr[Z_x \leq z] &= \Pr[e^{-\delta\cdot T_x} \leq z] \\
    &=\Pr[T_x > -\ln (z) /\delta] \\
    &=S_x(-\ln (z) /\delta) = {} _{-\ln (z) /\delta} p _x.
  \end{aligned}
$$

We can also see that low values of $Z_x$ are associated with high values of $T_x$. This makes sense because the benefit is more expensive to the insurer if it is paid early, as there has been little opportunity to earn interest.

#### The annual case

In an annual case, the benefit is payable at the end of the year of death, therefore, we should use the curtate future lifetime rv $K_x$ and the death benefit is paid at $K_x + 1$.

Let $Z$ be the present value of the benefit 1 paid at the end of the year of death, then

$$
  Z = v ^{K_x+1}.
$$

We denote the EPV of $Z$ as $A_x = \mathrm{E}[Z]$, and since the probability of dying in year $k$ is $\Pr[K_x = k] = {} _k | q_x$, we have

$$
  A_x = \mathrm{E}[v^{K_x+1}] = \sum _{k=0}^\infty v^{k+1} \cdot {} _k| q_x .
$$

And the second moment is 

$$
  {} ^2 A_x = \mathrm{E}[v^{2(K_x+1)}] = \sum _{k=0}^\infty v^{2(k+1)} \cdot {} _k| q_x .
$$

#### The monthly case

Here, let's say there are $m$ "months" (periods) in a year, if $m = 12$ each period is a month and if $m=4$ each period is a quarter.

We now defined a $1/m$-thly curtate future lifetime rv, $K^{(m)} _x$, where $m \in \mathbb{Z}_{>1}$, to be the future lifetime of $(x)$ in years rounded to the lower $1 /m$-th of a year. It can also be defined as $K ^{(m)}_x = \frac{1}{m} \lfloor m \cdot T_x \rfloor$.

The probability function of $K^{(m)}_x$ can be derived as 

$$
  \Pr[K ^{(m)} _x = k] = \Pr[k \leq T _x \leq k + \frac{1}{m}] = {} _k | _{\frac{1}{m}} q _x = {} _k p _x - {} _{k + \frac{1}{m}} p _x.
$$

The present value rv $Z$ will then be

$$
  Z = v^{K ^{(m)} _x + \frac{1}{m}}.
$$

The EPV of $Z$ is denoted as $A ^{(m)} _x$ and can be calculated as

$$
  A^{(m)} _x = \sum _{k=0}^\infty v^{\frac{k+1}{m}} \cdot {} _{\frac{k}{m}} | _{\frac{1}{m}} q_x.
$$

Here, each summand is the present value of the expected payment for the $k$-th period. If $m = 1$, this formula is the same as the annual case.

The second moment and thus the variance can be derived similarly.

#### Recursions

While it is unusual to only pay death benefit at the end of the year of death, $A_x$ is still useful because it can be calculated using life table and can then be adjusted to a more appropriate frequency using the relationships and assumptions we develop later in this chapter.

$A_x$ can also be calculated using **backward recursion**, which is particularly efficient in a spreadsheet setting.

- Since we assume there is a maximum age $\omega$, i.e., any life attaining age $\omega - 1$ will die in a year. The AV at $\omega-1$ will just be the benefit 1 discounted by 1 year.
  
  $$
    A _{\omega - 1} = v.
  $$

- For $x < \omega - 1$, we have

  $$
    \boxed{A_x = v\cdot(q_x + p_x \cdot A _{x+1})}.
  $$

  This can be interpreted as the follow: for any life attaining age $x$, if they die at the end of the year (with probability $q_x$), the benefit is 1; if they survive this year (with probability $p_x$), $A_{x+1}$ is the EPV of future benefits. The EPV at the end of year $x$, including the possible death benefit, is $q_x + p_x \cdot A _{x+1}$. If we discount it by a year, that will be the EPV at the benefit of year $x$.

The recursive formula for $A ^{(m)} _x$ can be derived similarly:

$$
  A^{(m)}_x = v^{\frac{1}{m}} \cdot \left({} _{\frac{1}{m}} q _x + {} _{\frac{1}{m}} p _x \cdot A^{(m)} _{x + \frac{1}{m}}\right).
$$

### Term insurance

#### The continuous case

Under term insurance, the death benefit is payable only if the policy holder dies within a fixed term of, say, $n$ years. Hence the present value of benefit 1 rv $Z$ is 

$$
  Z = 
  \begin{cases}
    v^{T_x} & T_x \leq n, \\
    0 & T_x > n.
  \end{cases}
$$

The EPV of $Z$ is denoted as $\bar{A} ^{1} _{x:|\overline{n|}}$, where the $1$ above $x$ indicates that the life $(x)$ must die before the term of $n$ years expires in order for the benefit to be payable. It can be calculated as

$$
  \bar{A} ^{1} _{x:|\overline{n|}} = \int _0 ^n e^{-\delta t}\cdot {}_t p _x \cdot \mu_{x+t} dt.
$$

The second moment of $Z$ can be derived similarly and it is equal to 

$$
  {}^2 \bar{A} ^{1} _{x:|\overline{n|}} = \int _0 ^n e^{-2\delta t}\cdot {}_t p _x \cdot \mu_{x+t} dt.
$$

#### The annual case

The AV is denoted $A ^{1} _{x:|\overline{n|}}$ and can be calculated as 

$$
  \bar{A} ^{1} _{x:|\overline{n|}} = \sum _{k=0}^{n-1} v^{k+1} \cdot {} _k | q _x.
$$

The second moment of the present value rv is


$$
  {}^2 \bar{A} ^{1} _{x:|\overline{n|}} = \sum _{k=0}^{n-1} v^{2(k+1)} \cdot {} _k | q _x.
$$

#### The monthly case

In a $1/m$-thly case, it is denoted $A^{(m)} {} ^1 _{x:\overline{n|}}$:

$$
  A^{(m)} {} ^1 _{x:\overline{n|}} = \sum _{k=0}^{mn-1} v^{\frac{k+1}{m}} \cdot {} _{\frac{k}{m}} | _{\frac{1}{m}} q _x.
$$

The second moment can be calculated similarly.

### Pure endowment
 
Pure endowment benefits are conditional on the survival of the policyholder at a policy maturity date. It only pays if the policyholder is still alive at the end of the policy, and pays nothing otherwise. They are not sold as stand-alone but in conjunction with term insurance to create endowment insurance. However, the pure endowment valuation functions are very useful when we value other benefits.

With pure endowment benefit of 1, issued to a life aged $x$, with a term of $n$ years, the present value rv $Z$ is

$$
  Z =
  \begin{cases}
    0 & T_x < n, \\
    v^n & T_x \geq n.
  \end{cases}
$$

It is denoted $A_{x:\overset{1}{\overline{n|}}}$, where the $1$ over the term subscript indicates that the term must expire before the life does for the benefit to be
paid. Since this is particularly cumbersome, it is commonly denoted as ${} _n E _x$ and 

$$
  \boxed{{} _n E _x = v^n \cdot {} _n p_x}.
$$

For the second moment of $Z$,

$$
  \mathrm{E}[Z^2] = v^{2n} \cdot {} _n p _x = v^n \cdot {} _n E _x = {} ^2_n E _x.
$$

### Endowment insurance

Endowment insurance is a combination of a term insurance and a pure endowment. Hence, the present value rv $Z$ for a endowment insurance of term $n$ can be described as 

$$
  Z = 
  \begin{cases}
    v^{T_x} & T_x < n \\
    v^n & T_x \geq n
  \end{cases}
  = v^{\min(T_x, n)} = e ^{-\delta\cdot\min(T_x, n)}.
$$

While it is rarely sold these day, the valuation function is quite useful.

The EPV of $Z$, i.e., the AV of endowment insurance is denoted $\bar{A} _{x:\overline{n|}}$ and it's equal to AV of a term insurance and a pure endowment:

$$
   \bar{A} _{x:\overline{n|}} = \bar{A} _{x:\overline{n|}} + {} _n E _x.
$$

The second moment is 
$$
  {}^2 \bar{A} _{x:\overline{n|}} = {}^2 \bar{A} _{x:\overline{n|}} + {} ^2 _n E _x.
$$

For the annual case and the $1/m$-thly cases, the expected values and the second moments are also the sum of those for the term insurance and pure endowment of the same frequency.

### Deferred insurance

Deferred insurance only pays death benefit if the policyholder dies after the deferred period (after the policy starts). Specifically, a deferred insurance issued to life $(x)$ with deferred period of $u$ years and coverage term of $n$ years only pay death benefit if $(x)$ dies between ages $x + u$ and $x + u + n$. Hence, the present value rv for the continuous case is

$$
  Z =
  \begin{cases}
    v^{T_x} & T_x \in [u, u+n), \\
    0 & T_x \notin [u, u+n).
  \end{cases}
$$

The AV is denoted as ${} _u | \bar{A} ^1_{x:\overline{n|}}$. It can be calculated as 

$$
  {} _u | \bar{A} ^1_{x:\overline{n|}} = \int _u^{u+n} e^{-\delta t} \cdot {} _t p _x \cdot u _{x+t} dt.
$$

With some substitution, 

$$
  {} _u | \bar{A} ^1_{x:\overline{n|}} = e^{-\delta u} \cdot {} _u p_x \cdot \bar{A} ^1 _{x+u:\overline{n|}} = {} _u E _x \cdot \bar{A} ^1 _{x+u:\overline{n|}}.
$$

This equation makes sense because the deferred insurance is the same as a term life issued on age $x+u$ but contingent on surviving to age $u$.

Alternatively, 

$$
  {} _u | \bar{A} ^1_{x:\overline{n|}} = \bar{A} ^1_{x:\overline{u+n|}} - \bar{A} ^1_{x:\overline{n|}}.
$$

This also makes sense because the deferred insurance has the same payout as those of a term life of $u+n$ years minus a term life of $u$ years.

On the other hands, the AV of deferred insurance can be served as a building block for other valuation functions. For example, for a term life

$$
  \bar{A} ^1 _{x:\overline{n|}} = \sum _{r=0}^{n-1} {} _r | \bar{A} ^1 _{x:\overline{1|}},
$$

and for a whole life policy,

$$
  \bar{A} _{x} = \sum _{r=0}^{\infty} {} _r | \bar{A} ^1 _{x:\overline{1|}}.
$$

We also have similar relationships for the annual case and the $1/m$-thly case using deferred insurance of the corresponding frequencies, i.e., ${} _u | A ^1 _{x:\overline{n|}}$ and ${} _u | A^{(m)} {}^1 _{x:\overline{n|}}$.

## Relating the continuous case, the annual case, and the monthly case

In practice, $A$, the annual case, can be derived using integer-age life tables, but it is unrealistic that death benefits are only paid at the end of the year of death. We can use some approximation to derive $\bar{A}$ and $A^{(m)}$.

### Using the UDD assumption

The difference between $\bar{A}_x$ and $A_x$ depends on the lifetime distribution between ages $y$ and $y + 1$ for all $y \geq x$.

Under UDD, 

$$
  \boxed{\bar{A} _x \approx \frac{i}{\delta} \cdot A _x}.
$$

<details><summary>Click here for derivation</summary>

$$
  \begin{aligned}
    \bar{A} _x &= \int _0 ^\infty e ^{-\delta t} \cdot {} _t p _x \cdot \mu _{x+t} dt \\
    &= \sum _{k=0}^\infty \int _k ^{k+1} e ^{-\delta t} \cdot {} _t p _x \cdot \mu _{x+t} dt \\
    &= \sum _{k=0}^\infty e^{-\delta\cdot (k+1)} \cdot {} _k p _x \cdot \int _0 ^{1} e ^{-\delta \cdot (1-s)} \cdot \underbrace{{} _s p _{x+k} \cdot \mu _{x+k+s}} _{f _{x+k}(s)} ds \\
    &\approx \sum _{k=0}^\infty e^{-\delta\cdot (k+1)} \cdot {} _k p _x \cdot q_{x+k} \cdot \int _0 ^{1} e ^{-\delta \cdot (1-s)}ds 
    & (\text{using UDD, } f _{x+k}(s) = q_{x+k})\\
    &= A_x \cdot \frac{e^{-\delta} - 1}{\delta}.
  \end{aligned}
$$

Because $e ^{\delta} = 1 + i$, $\bar{A} _x = \frac{i}{\delta} \cdot A_x$.

---
</details>

Directionally, since $\forall i > 0, i / \delta > 1$, $\bar{A} _x > A _x$. This makes sense because paying soon would result in a higher present value. Such approximation applies to term insurance and deferred insurance. And for the $1/m$-thly case,

$$
  \boxed{A ^{(m)} _x = \frac{i}{i^{(m)}} \cdot A _x}.
$$

Note that such approximation only works for death benefits but **not pure endowment** (since the present value for pure endowment is the same for all cases). For endowment insurance, since it is a combination of term insurance and pure endowment, it is

$$
  \bar{A} _{x:\overline{n|}} = \frac{i}{\delta} \cdot A ^1 _{x:\overline{n|}} + {} _n E _x
$$

under UDD.

### Using the claims acceleration approach

With the claims acceleration approach, we approximate $A^{(m)}$ and $\bar A$ by considering how much earlier are the death benefit payments paying compared to the annual case.

For the annual case, the death benefit is paid at time $K_x + 1$, while for the $1/m$-thly case, it can be paid on $K_x + \frac{1}{m}, K_x + \frac{2}{m}, \ldots, K_x + \frac{m}{m}$. We assume the deaths occur evenly, then the benefit, on average, is paid at time $K_x + \frac{m+1}{2m}$ for all $x$. Because the payment is $\frac{m-1}{2m}$ earlier than that of the annual case,

$$
  \boxed{A^{(m)}_x \approx A_x \cdot (1+i)^\frac{m-1}{2m}}.
$$

For the continuous case, the benefit is paid half a year earlier.

$$
  \boxed{A^{(m)}_x \approx A_x \cdot (1+i)^\frac{1}{2}}.
$$

Again, these approximations apply only to death benefits and **not pure endowment**. For any insurance with pure endowment (i.e. endowment insurance), we only need to approximate the death benefit portion:

$$
  \bar A _{x:\overline{n|}} \approx (1+i)^{\frac{1}{2}}\cdot A^1 _{x:\overline{n|}} + {} _n E _x.
$$

## Variable insurance benefits

In the case where the life-contingent benefits can change over time, e.g., different death benefit for different age of death, we will need a more flexible way to describe the policy's present value.

We first need an **indicator rv**, $I$, of an life contingent event $E$. If $E$ is true, $I$ is 1; else, $I$ is 0.

This can be used to describe traditional insurance. For example, a deferred term insurance with deferred period $k$ and term $1$ can be described in an event $E$: a life aged $x$ dies in the interval of $[k, k+1)$. Then, the expected value if such policy is $\mathrm{E}[I(E)]$.

Another example is increasing death benefit, where an amount $k$ is paid when the policyholder dies in year $k$. Denoted $\bar{I} \bar{A}$ (the $I$ indicates it is increasing and the bar indicates it is increasing continuously), the AV can be calculated as

$$
  (\bar{I} \bar{A})_x = \int_0^\infty t\cdot e^{-\delta t} \cdot {} _t p _x \cdot \mu _{x+t} dt.
$$

The annual case whose death benefit is $k+1$ can be calculated similarly:

$$
  (IA)_x = \sum_{k=0}^{\infty} (k+1)\cdot v^k \cdot {} _k|q _x.
$$
