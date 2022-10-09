# Chapter 5: Annuities

- [Chapter 5: Annuities](#chapter-5-annuities)
  - [Introduction](#introduction)
  - [Review of annuities-certain](#review-of-annuities-certain)
  - [Annual life annuities](#annual-life-annuities)
    - [Whole life annuity-due](#whole-life-annuity-due)
    - [Term annuity-due](#term-annuity-due)
    - [Immediate life annuities](#immediate-life-annuities)
  - [Annuities payable continuously](#annuities-payable-continuously)
  - [Annuities payable monthly](#annuities-payable-monthly)
  - [Deferred annuities](#deferred-annuities)
  - [Guaranteed annuities](#guaranteed-annuities)
    - [Arithmetically increasing annuities](#arithmetically-increasing-annuities)
  - [Increasing annuities](#increasing-annuities)
    - [Geometrically increasing annuities](#geometrically-increasing-annuities)
  - [Evaluating annuity function](#evaluating-annuity-function)
    - [Recursion](#recursion)
    - [Applying the UDD assumption](#applying-the-udd-assumption)
    - [Woolhouse's formula](#woolhouses-formula)
  - [Functions for select lives](#functions-for-select-lives)

## Introduction

A **life annuity** is a series of payments which are contingent on a specified individual’s survival to each potential payment date. The non-life-contingent annuity is referred to as **annuities-certain**. Depended on when is the payment:

- **Annuity-due**: payment made at the start of the time interval,
- **Immediate annuity**: payment made at the end of a time interval.

## Review of annuities-certain

Annuity-due:

$$
  \ddot{a} _{\overline{n|}} = 1 + v + v^2 + \cdots + v^{n-1} = \frac{1- v^n}{1 - v} = \frac{1- v^n}{d}
$$

Annuity-immediate:

$$
  a _{\overline{n|}} = v + v^2 +v^3 + \cdots + v_n = \frac{1 - v^n}{1 - v} \cdot v = \frac{1- v^n}{i}.
$$

Annuity-certain with continuous payment:

$$
  \bar{a} _{\overline{n|}} = \int_0^n v^t dt = \frac{1-v^n}{\delta}.
$$

For annuity-due and annuity-immediate that pay every $1/m$-thly:

$$
  \ddot{a} ^{(m)} _{\overline{n|}} = \frac{1 - v^n}{d^{(m)}}
$$

and 

$$
  a ^{(m)} _{\overline{n|}} = \frac{1 - v^n}{i^{(m)}},
$$

respectively.

## Annual life annuities

The annual life annuity is paid once each year, conditional on the survival of a life (the annuitant) to the payment date. If the annuity is to be paid throughout the annuitant’s life, it is called a **whole life annuity**. If there is to be a specified maximum term, it is called a **term annuity** or **temporary annuity**.

Annual annuities are quite rare because of their low payment frequency. But this is important as it can be built with an integer age life table.

### Whole life annuity-due

In a whole life annuity-due, the first payment occurs immediately, and the subsequent annual payments depend on whether the life survived at the time of payment.

To calculate the EPV, if the life $(x)$ has curtate future lifetime $K_x$, there will be $K_x + 1$ payments (including the initial one). The present value of an annuity-due of $K_x  + 1$ payments is

$$
  Y = \ddot{a} _{\overline{K _x + 1|}} = \frac{1 - v^{K _x + 1}}{d}.
$$

Note that $Y$ is in of itself the rv of the present value. The EPV of the whole life annuity-due is then

$$
  \ddot{a}_x = \mathrm{E}[Y] = \mathrm{E}\left[\frac{1 - v^{K _x + 1}}{d}\right] = \frac{1 - \mathrm{E}[v^{K _x + 1}]}{d}.
$$

Since $\mathrm{E}[v^{K _x + 1}] = A _x$, we have

$$
  \boxed{\ddot{a} _ x = \frac{1 - A _x}{d}}.
$$

Alternatively, we can calculate it using a series:

$$
  \ddot{a}_x = 1 + v \cdot p_x + v^2\cdot {} _2 p _x + \cdots = \sum^\infty _{t = 0} v^t \cdot {} _t p _x.
$$

This is also summing the EPV of pure endowments of terms 0, 1, 2, ...

And if we know the deferred mortality probability function, we can directly calculate the EPV:

$$
  \ddot{a}_x = \mathrm{E}\left[\ddot{a} _{\overline{K _x +1|}}\right] = \sum^\infty _{k=0} \ddot{a} _{\overline{k+1|}} \cdot {} _k | q _x.
$$

Here, the whole-life annuity has a probability of ${} _k | q_x$ to be an annuity-due certain of $k+1$ payments. Note that this is less often used in practice than the previous 2 formulations.

The variance of the present value rv is 

$$
  \mathrm{Var}[Y] = \mathrm{Var}\left[\frac{1 - v^{K _x + 1}}{d}\right] = \frac{1}{d^2} \mathrm{Var}[v^{K _x + 1}] = \frac{{}^2 A _x - A^2 _x}{d^2}.
$$

Or we can directly calculate it given the deferred mortality probability function.

### Term annuity-due

For a term annuity-due, the present value rv is

$$
  Y = \ddot{a} _{\overline{\min(K _x + 1, n)|}}.
$$

The EPV is

$$
  \ddot{a} _{x : \overline{n|}} = \mathrm{E}[Y] = \frac{1 - \mathrm{E}[v^{\min(K _x + 1, n)}]}{d}.
$$

Since $\mathrm{E}[v^{\min(K _x + 1, n)}]$ is the same as $A _{x:\overline{n|}}$, it can be calculated as 

$$
  \ddot{a} _{x : \overline{n|}} = \frac{1 - A _{x:\overline{n|}}}{d}.
$$

**Important: The term annuity function is related to the endowment function, not term life!!!**

Alternatively, it can be calculated as the sum of expected present value of each payment:

$$
  \ddot{a} _{x : \overline{n|}} = 1 + v\cdot p _x + v^2 \cdot {} _2 p _x + \cdots + v^{n-1} \cdot {} _{n-1} p_x = \sum _{t=0} ^{n-1} v^t \cdot {} _t p _x.
$$

Or it can be calculated using deferred mortality probability:

$$
  \ddot{a} _{x : \overline{n|}} = \sum _{k=0} ^{n-1} \ddot{a} _{\overline{k+1|}} \cdot {} _k | q _x + {} _n p _x \cdot \ddot{a} _{\overline{n|}}.
$$

Note that both dying in year $n - 1$ (with probability ${} _{n-1} |q _x$) and surviving for year $n$ (with probability ${} _n p _x$) will both resulting in an $n$-payment annuity.

### Immediate life annuities

For **whole life immediate annuities**, there won't be an initial payment at time 0. Hence, there is only $K_x$ payments. Let $Y^*$ be the present value rv of an immediate life annuities and $Y$ be that of a life annuity-due; then $Y^* = Y - 1$. The EPV is then

$$
  a_x = \ddot{a} _x + 1.
$$

For **term life immediate annuities**, there won't be payment at $t = 0$ but there will be payment at $t = n$ should the policyholder survive at $t = n$. Hence,

$$
  a _{x:\overline{n|}} = \ddot{a} _{x:\overline{n|}} - 1 + v^n \cdot {} _n p _x.
$$

## Annuities payable continuously

For a **continuous whole life annuity**, the present value rv can be expressed using the complete lifetime rv $T_x$ as

$$
  Y = \bar{a} _{\overline{T_x|}} = \frac{1 - v^{T _x}}{\delta}.
$$

The EPV is

$$
  \bar{a} _x = \frac{1 - \bar{A} _x}{\delta}.
$$

The variance of $Y$ is

$$
  \mathrm{Var}[Y] = \frac{{} ^2 \bar{A} _x - \bar{A}^2 _x}{\delta^2}.
$$

We can integrate over the expected present value,

$$
  \bar{a} _x = \int ^\infty _0 e^{-\delta t} \cdot {} _t p _x dt,
$$

or over all possible infinitesimal periods of death:

$$
  \bar{a} _x = \int ^\infty _0 \bar{a} _{\overline{t}} \cdot {} _t p _x \cdot \mu _{x+t} dt.
$$

For a **continuous term life annuity**,

$$
  \bar{a} _{x : \overline{n|}} = \frac{1 - \bar{A} _{x:\overline{n|}}}{\delta} = \int ^\infty _0 e^{-\delta t}\cdot {} _t p _x dt = \int ^\infty _0 \bar{a} _{\overline{t|}}\cdot {} _t p _x \cdot \mu _{x + t} dt + \bar{a} _{\overline{n|}} \cdot {} _n p _x.
$$

## Annuities payable monthly

For **whole life annuity-due** that pay $m$ times a year, each time of amount $1/m$, it can be calculated as

$$
  \ddot{a} ^{(m)} _x = \frac{1 - A ^{(m)} _x}{d ^{(m)}} = \sum ^\infty _{r=0} \frac{1}{m} \cdot v ^{\frac{r}{m}} \cdot {} _{\frac{r}{m}} p _x.
$$

For **whole life $\mathbf{1/m}$-thly immediate annuity**, since it is only missing the initial payment of $1/m$ at time 0, 

$$
  a ^{(m)} _x = \ddot{a} ^{(m)} _x - \frac{1}{m}.
$$

For **term life $\mathbf{1/m}$-thly annuity-due**, 

$$
  \ddot{a} ^{(m)} _{x:\overline{n |}} = \frac{1 - A ^{(m)} _{x:\overline{n|}}}{d ^{(m)}} = \sum _{r=0} ^{mn-1} \frac{1}{m} \cdot v ^{\frac{r}{m}}\cdot {} _{\frac{r}{m}} p _x.
$$

For **term life $\mathbf{1/m}$-thly annuity-immediate**, 

$$
  a ^{(m)} _{x:\overline{n|}} = \ddot{a} ^{(m)} _{x:\overline{n|}} - \frac{1}{m} + \frac{1}{m} \cdot v ^n \cdot {} _n p _x.
$$

Comparing life annuities of different payment time, we have

$$
  a_x < a ^{(m)} _x < \bar{a} _x < \ddot{a} ^{(m)} _x < \ddot{a} _x.
$$

Such ordering makes sense because

- time value of money: paying sooner will result in higher present value
- high survival probability: paying sooner will have a higher chance of surviving, hence receiving the payment

Because of these 2 reasons, the formulas for annuities of different payment periods have different denominators (due to time value of money) and different numerators (due to different mortality).

## Deferred annuities

A deferred annuity is an annuity under which the first payment occurs at some specified future time. An annuity-due deferred $u$ years will make the first payment on time $u$ (should the policyholder survives) instead of time $0$. It is denoted as ${} _u | \ddot{a}_x$. The actuarial value is 

$$
  \boxed{{} _u | \ddot{a} _x = \ddot{a} _x - \ddot{a} _{x:\overline{u|}}}.
$$

Alternatively, 

$$
  \begin{aligned}
    {} _u | \ddot{a} _x &= v^u \cdot {} _u p _x \cdot (1 + v \cdot p _{x+u} + v^2 \cdot {} _2 p _{x+u} + \cdots) \\
    &= v^u \cdot {} _u p _x \cdot \ddot{a} _{x+u} \\
    &= {} _u E _x \cdot \ddot{a} _{x+u}
  \end{aligned}
$$

**Life table trick**

When ${} _t E _x$, the pure endowment function, is given in a life table, it can be used a a discount function that takes mortality into consideration (as we can see from the 3rd equation above).

Hence, for example,

$$
  {} _u | a _{x:\overline{n|}} = {} _u E _x \cdot a _{x+u:\overline{n|}}.
$$

Also, note that difference between a whole-life annuity and a deferred whole-life annuity of $u$ years is a $u$-term annuity, i.e. $\ddot{a} _{x:\overline{u|}} = \ddot{a} _x - {} _u | \ddot{a} _x$. When a life table provided the annuity-due function $\ddot{a}_x$, we can calculate the term annuity-due as 

$$
  \ddot{a} _{x:\overline{n|}} = \ddot{a}_x - {} _n E _x \cdot \ddot{a} _{x+n}.
$$

## Guaranteed annuities

### Arithmetically increasing annuities

For an annuity-due with a guaranteed for $n$ years, the plan will make $n$ payments even if the policyholder dies before year $n$. The present value rv is

$$
  Y =
  \begin{cases}
    \ddot{a} _{\overline{n |}} & K _x \leq n - 1, \\
    \ddot{a} _{\overline{K _x + 1}} & K _x \geq n
  \end{cases}
  = \ddot{a} _{\overline{n|}} +
  \underbrace{
    \begin{cases}
      0 & K _x \leq n - 1, \\
      \ddot{a} _{\overline{K _x + 1|}} - \ddot{a} _{\overline{n |}} & K_x \geq n.
    \end{cases}
  } _{\text{annuity-due deferred $n$ years}}
$$

To find the EPV, denoted $\ddot{a} _{\overline{x:\overline{n |}}}$, it is equal to an annuity certain plus an deferred annuity

$$
  \ddot{a} _{\overline{x:\overline{n |}}} = \ddot{a} _{\overline{n |}} + \underbrace{{} _n E _x\cdot \ddot{a} _{x+n}} _{{} _n | \ddot{a} _x}.
$$

For annuity of other payment frequency, the right hand side of the formula should replace the annuity functions with the corresponding payment frequency.

## Increasing annuities

Consider an increasing annuity-due where the amount of the annuity is $t+1$ at time $0, 1, 2, \ldots$ provided that $(x)$ is alive at time $t$. Such annuity-due is denoted as $(I\ddot{a}) _x$. It can be calculated using a series:

$$
  \boxed{(I\ddot{a}) _x = \sum _{t=0} ^\infty (t+1) \cdot v^t \cdot {} _t p _x}.
$$

For increasing annuity-due of term $n$, it is denoted as $(I\ddot{a}) _{x:\overline{n|}}$ and it has the same formula as above except the upper bound of the summation is $n - 1$.

For a continuously increasing annuity that pay continuously, 

$$
  (\bar{I} \bar{a}) _{x:\overline{n|}} = \int _0 ^n t\cdot e^{-\delta t} \cdot {} _t p _x dt.
$$

### Geometrically increasing annuities

An annuity that increases geometrically makes senses to offset the effect of inflation. For example, consider an whole life annuity-due with annuity payments $(1 + j) ^t$ at time $t = 0, 1,2, \ldots$ Its EPV is 

$$
  \begin{aligned}
    &\sum _{t=0} ^\infty (1+j) ^t \cdot v ^t \cdot {} _t p _x  \\
    = &\sum _{t=0} ^\infty (v') ^t \cdot {} _t p _x  
    &\text{where } v' = \frac{1 + j}{1 + i}\\
    = &\ddot{a} _{x:i'} 
    &\text{this is annuity-due evaluated with interest rate } i', \text{ where } i' = \frac{1 + i}{1 + j} - 1.
  \end{aligned}
$$

## Evaluating annuity function

This section discusses how to evaluate the EPV of different annuities with integer-value life tables.

### Recursion

In a spreadsheet, given values for ${} _t p _x$, we may calculate $\ddot{a} _x$ using a backward recursion:

- assuming the limiting age is $\omega$, 
  
  $$
    \ddot{a} _{\omega - 1} = 1;
  $$

- for age $x < \omega - 1$,

  $$
    \boxed{\ddot{a} _x = 1 + \underbrace{v \cdot p _x}_{{} _1 E _x} \cdot \ddot{a} _{x+1}}.
  $$

For $1/m$-thly annuity-due,

$$
  \ddot{a} ^{(m)} _{x} = 
  \begin{cases}
    \frac{1}{m} & x= \omega - \frac{1}{m}, \\
    \frac{1}{m} + v^\frac{1}{m} \cdot {} _\frac{1}{m} p _x \cdot \ddot{a} ^{(m)} _{x + \frac{1}{m}}
    & x = \omega - \frac{2}{m}, \omega - \frac{3}{m}, \omega - \frac{4}{m}, \ldots, 0.
  \end{cases}
$$

The recursive formulas can be interpreted as the follow: the EPV of the annuity-due purchased now is the initial payment plus the discounted (by interest and mortality) EPV of the annuity-due purchased next period.

### Applying the UDD assumption

Here we are trying to use the annual annuity-due functions to approximate annuity-due of other payment frequency.

From [Chapter 4](04_insurance_benefits.md#using-the-udd-assumption), we know, under UDD assumption,

$$
  A ^{(m)} _x = \frac{i}{i ^{(m)}} \cdot A_x
$$

and 

$$
  \bar{A} _x = \frac{i}{\delta} \cdot A _x.
$$

Then, to approximate $\ddot{a} ^{(m)} _x$,

$$
  \begin{aligned}
    \ddot{a} ^{(m)} _x &= \frac{1 - A ^{(m)} _x}{d ^{(m)}} \\
    &= \frac{1 - \frac{i}{i ^{(m)}} \cdot A ^{(m)} _x}{d ^{(m)}} & \because \text{using UUD}\\
    &= \frac{i ^{(m)} - i \cdot A ^{(m)} _x}{i ^{(m)} \cdot d ^{(m)}} \\
    &= \frac{i ^{(m)} - i \cdot A ^{(m)} _x}{i ^{(m)} \cdot d ^{(m)}} \\
    &= \frac{i ^{(m)} - i \cdot (1 - d\cdot \ddot{a} _x)}{i ^{(m)} \cdot d ^{(m)}} & \because \ddot{a} _x = \frac{1 - A _x}{d}\\
    &= \frac{i\cdot d}{i^{(m)} \cdot d^{(m)}} \cdot \ddot{a}_x - \frac{i - i^{(m)}}{i^{(m)} \cdot d^{(m)}} \\
    &= \alpha(m)\cdot \ddot a _x - \beta (m) & \text{$\alpha(m)$ and $\beta (m)$ are in the formula sheet}
  \end{aligned} 
$$

For the continuous case, since $\lim _{m \to \infty} i ^{(m)} = \lim _{m \to \infty} d ^{(m)} = \delta$,

$$
  \bar{a} _x = \frac{i\cdot d}{\delta ^2} \cdot \ddot{a} _x - \frac{i - \delta}{\delta ^2}.
$$

For term annuities,

$$
  \begin{aligned}
    \ddot{a} ^{(m)} _{x:\overline{n|}} &= \ddot{a} ^{(m)} _x - {} _n E _x \cdot \ddot{a} ^{(m)} _{x+n} \\
    &= \frac{i\cdot d}{i^{(m)} \cdot d^{(m)}} \cdot \ddot{a} _{x:\overline{n|}} - \frac{i - i^{(m)}}{i^{(m)} \cdot d^{(d)}} \cdot (1 - {} _n E _x) \\
    &= \alpha(m) \cdot \ddot{a} _{x:\overline{n|}} - \beta(m) \cdot (1 - {} _n E _x).
  \end{aligned}
$$

It can be shown that $\frac{i\cdot d}{i^{(m)} \cdot d^{(m)}} \approx 1$ and $\frac{i - i^{(m)}}{i^{(m)} \cdot d^{(d)}} \approx \frac{m-1}{2m}$, leading to the approximation

$$
  \begin{aligned}
  \ddot{a} ^{(m)} &\approx \ddot{a} ^{(m)} - \frac{m-1}{2m}\\
  \ddot{a} ^{(m)} _{x:\overline{n|}} &\approx \ddot{a} _{x:\overline{n|}} - \frac{m-1}{2m} \cdot (1 - {} _n E _x)  
  \end{aligned}
$$

which is the same as the two-term Woolhouse formula in the following section.

### Woolhouse's formula

Woolhouse's formula is based on the Euler-Maclaurin formula for numerical integration. It works for function $g$ that is differentiable a certain number of times. If $\lim _{t \to \infty} g(t) = 0$, then for $h > 0$,

$$
  \int _0 ^\infty g(t) dt = h\cdot \sum _{k=0} ^\infty g(kh) - \frac{h}{2}\cdot g(0) + \frac{h^2}{12}\cdot g'(0) - \frac{h^4}{720}\cdot g'''(0) + \cdots
$$

where the omitted terms are not needed for our purposes.

If we let $g(t) = {} _t p _x \cdot e ^{-\delta t}$, $\int _0 ^\infty g(t) dt = \bar a _x$.

We can get that

- $g(0) =1$
- $g'(0) = -(\delta + \mu _x)$

If we let $h = 1$, we have

$$
  \bar{a} _x  \approx \sum _{k=0} ^\infty {} _k p _x \cdot e ^{-\delta k} - \frac{1}{2} - \frac{1}{12}(\delta + \mu _x) = \ddot{a} _x - \frac{1}{2} - \frac{1}{12}(\delta + \mu _x),
$$

which gives us the **three-term Woolhouse formula** for $\bar a _x$.

If we let $h = m$, where $m \in \mathbb Z _{>0}$, we have

$$
  \bar{a} _x \approx \frac{1}{m} \sum _{k=0} ^\infty {} _{\frac{k}{m}} p _x \cdot e ^{-\delta \cdot \frac{k}{m}} - \frac{1}{2m} - \frac{1}{12m^2}\cdot(\delta + \mu _x) = \ddot{a} ^{(m)} _x - \frac{1}{2m} - \frac{1}{12m^2}\cdot(\delta + \mu _x).
$$

If we set this equal to the RHS of $\bar a _x$'s approximation, we have

$$
  \ddot{a} ^{(m)} _x \approx \ddot{a} _x -\frac{m-1}{2m} - \frac{m^2 - 1}{12m^2}(\delta + \mu _x),
$$

which is the **three-term Woolhouse formula** for $\ddot a ^{(m)} _x$.

The three-term Woolhouse formula is extremely accurate, more so than the UDD approach. If we omit the third term (done often if great accuracy is less important), we have the **two-term Woolhouse formula**, which is less accurate, in general, than the UDD approximation.

For term annuities, we have

$$
  \ddot{a} ^{(m)} _{x:\overline{n|}} = \ddot{a}  _{x:\overline{n|}} - \frac{m-1}{2m} \cdot (1 - {} _n E _x) - \frac{m^2 - 1}{12m^2} \cdot (\delta + \mu_x) \cdot (1 -{} _n E _x).
$$

**Tips on using formulas sheet**: The formula sheet only provide three-term Woolhouse formula for whole life annuity. Hence, it may be easier to let $\ddot{a} ^{(m)} _{x:\overline{n|}} = \ddot a ^{(m)} _{x} - {} _ n E _x \cdot \ddot a ^{(m)} _{x+n}$ and approximate those 2 whole life annuity function separately.

With three-term Woolhouse formula, we can even get better approximation for life insurance by applying $A ^{(m)} _x = 1 - d^{(m)} \cdot \ddot{a} ^{(m)} _x$ and replacing $\ddot{a} ^{(m)} _x$ with Woolhouse formula. This can be more accurate than the UUD approach. 

We can also have a more accurate relationship between the complete expectation of life and the curtate lifetime expectation: $\mathring e _x \approx e _x + \frac{1}{2} - \frac{1}{12} \cdot \mu _x$.

For life tables that doesn't provide $\mu _x$ (a common practice), we can approximate $\mu_x$ first and then apply Woolhouse formula. To do that, note that 

$$
  \begin{aligned}
    & \frac{l _{x+1}}{l _{x - 1}} = {} _2 p _{x - 1} = \exp \left(- \int _{x-1} ^ {x+1} \mu _s ds\right) \approx e ^{-2\mu_x} \\
    \implies & \mu_x \approx -\frac{1}{2} \cdot \ln \frac{l _{x+1}}{l _{x-1}}.
  \end{aligned}
$$

## Functions for select lives

The relationship between annuity and life insurance also apply to select lives. For example,

$$
  \ddot{a} _{[x]} = \frac{1 - A _{[x]}}{d}.
$$

Similar formulas apply for term annuity and annuity with different payment frequency.

Woolhouse formula also apply similarly, as long as all annuity functions and force of mortality functions are from the same select age. For example,

$$
  \ddot{a} ^{(m)} _{[x] + k} \approx \ddot{a} _{[x] + k} - \frac{m-1}{2m} - \frac{m^2 - 1}{12 m^2} \cdot (\delta + \mu _{[x] + k}).
$$