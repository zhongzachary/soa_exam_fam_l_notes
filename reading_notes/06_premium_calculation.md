# Chapter 6: Premium calculation

- [Chapter 6: Premium calculation](#chapter-6-premium-calculation)
  - [Preliminaries](#preliminaries)
  - [The loss at issue random variable](#the-loss-at-issue-random-variable)
  - [The equivalence principle premium](#the-equivalence-principle-premium)
    - [Net premiums](#net-premiums)
    - [Gross premiums](#gross-premiums)
  - [Profit](#profit)
  - [The portfolio percentile premium principle](#the-portfolio-percentile-premium-principle)
  - [Extra risks](#extra-risks)
    - [Age rating](#age-rating)
    - [Constant addition to the force of mortality](#constant-addition-to-the-force-of-mortality)
    - [Constant multiple of mortality rates](#constant-multiple-of-mortality-rates)

## Preliminaries

By whether it includes expenses
- Net premium: doesn't expenses 
- Gross premium: includes expenses, aka office premium or expense-loaded premium

By number of payments
- Single premium: a single payment by the policyholder
- Regular series of payments: annually, monthly (more common), weekly, etc. Payments can be a level amount, but they don't have to be.

Payment time: 
- premiums are payable in advance. If the premium is due at the end of the payment period, the person would have had a year of coverage without paying for it.
- whole life premiums are common to cease at a certain age; term life premiums usually have the same term as the policy (but can be shorter).
- immediate annuities are always purchased by a single premium, while deferred annuity may be purchased using a single premium or regular premiums paid throughout the deferred period.

Assumptions:
- We use the **Standard Select Survival Model**, where the ultimate force of mortality is 
  - $\mu_x = A + Bc^x$, where $A = 2.2 \times 10 ^{-4}$, $B = 2.7 \times 10 ^{-6}$ and $c = 1.124$.
  - It has a select period of 2 years, and for $0 \leq s < 2$, $\mu _{[x] + s} = 0.9 ^{2-s} \cdot \mu _{x+s}$.

## The loss at issue random variable

The cash flows of life insurance contract consist of the benefit outgo (and the associated expenses) and the premium income, both of which are life contingent. We can model the present value at issue of the future loss with a rv. When expenses are excluded, such rv is called **present value of net future loss at issue**, or more commonly **net loss at issue**, denoted $L^n _0$. When we include expenses, it is the **gross loss at issue**, denoted $L^g _0$.

For example, for a whole life insurance to a select life aged $x$, with sum insured $S$ payable immediately on death. Premiums are payable annually in advance, ceasing at age $d$ or on earlier death. The net annual premium is $P$. Then, the net loss at issue is

$$
  L^n _0 = S\cdot v ^{T _{[x]}} - P\cdot \ddot{a} _{\overline{\min(K _{[x]} + 1, d - x)|}}.
$$

Given the survival model + assumptions on future interest + expenses, the insurers can determine a distribution for the loss at issue. To find the premium from the distribution, the insurer needs to use a **premium principle**.

## The equivalence principle premium

Under the **equivalence principle**, the premium is set such that the expected value of the loss at issue random variable is zero.

### Net premiums

The net premium for a contract is the equivalence principle premium using the net loss at issue random variable.

It is a premium where the expected net loss at issue is 0, i.e., $\mathrm{E}[L^N _0] = 0$. Hence, net premium can be defined as the premium that solves the equation of value:

$$
  \textbf{EPV of benefit outgo} = \textbf{EPV of premium income}.
$$

### Gross premiums

There are 3 main types of expenses: initial expenses, renewal expenses, and termination or claim expenses.

- Initial expenses: loosely referred to as acquisition expenses. They can be commission and underwriting expenses. 
  - Commission is often paid to an agent in the form of a high percentage of the first year's premiums plus a much lower percentage of subsequent premiums. 
  - Underwriting expenses may vary according to the amount of mortality risk involved. If the risk of adverse selection is high, the underwriting process is more stringent, hence high underwriting cost.
- Renewal expenses: aka maintenance expenses, normally incurred by the insurer each time a premium is payable, or when an annuity payment is made. 
  - They can include renewal commissions, payment processing costs, statement issuing cost, staff salaries, rent, etc.
  - Renewal expenses may be expressed as a percentage of premium, or as a fixed per policy amount (but may increase at a compound rate to reflect inflation).
- Termination expenses, aka claim expenses, occur when a policy expires, typically on the death of a policyholder or annuitant, or on the maturity date of a term insurance or endowment insurance.
  - Usually a small expense associated with the paperwork require to finalize and pay a claim.
  - It can be a fixed sum, or proportional to the benefit amount.

The  equivalence principle gross premium is when the expected gross loss at issue is 0, $\mathrm{E}[L^g _0] = 0$. In other words,

$$
  \textbf{EPV of gross premiums} = \textbf{EPV of benefits} + \textbf{EPV of expenses}.
$$

## Profit

The equivalence principle does not allow explicitly for a loading for profit, but it is necessary for the business to generate sufficient income for the shareholders to make an adequate rate of return.

Profit can be loaded implicitly through margins in valuation assumptions. For example, using a low interest than te actual return on asset (aka **interest spread**). We may also use margins in the mortality assumptions (**mortality spread**). Insurers may use a slightly higher overall mortality for term insurance, or a slightly lower one for annuity.

Insurers also need to sell a large amount of policies. While the probability of actual profit greater expected profit is decreasing and approaching 0.5 as the number of policies increases, the probability of very large aggregate losses, relative to total premiums, is much lower for larger number of polices. This is **diversification**.

## The portfolio percentile premium principle

With the portfolio percentile premium principle, we assume a large portfolio of policies whose policyholders' lifetime distributions are identical and independently distributed (i.i.d.). Then, we are trying to solve for a premium such that the probability of total loss being less than 0 is some fixed percentage (i.e. the percentage of making a profit in total).

Let $N$ denote the number of policies and let $L_{0,i}$ represent the loss at issue rv for the $i$-th policy. The portfolio total loss at issue is $L$ and 

$$
  \begin{aligned}
    \mathrm{E}[L] &= \sum _{i=1} ^N \mathrm{E}[L _{0,i}] \\
    &= N\cdot \mathrm{E}[L_{0,1}] & \because \text{i.i.d.} \\
    \mathrm{Var}[L] &= \sum _{i=1} ^N \mathrm{Var}[L _{0,i}] \\
    &= N\cdot \mathrm{Var}[L_{0,1}] & \because \text{i.i.d.} \\
  \end{aligned}
$$

Then, let $0 < \alpha < 1$ such that 

$$
  \Pr[L < 0] = \alpha.
$$

We want $\alpha$ to be large enough so that the probability of having a profit (aka loss is negative) is high.

Now, if $N$ is sufficiently large, the central limit theorem tells us the $L \sim \mathcal{N}(\mu = N\cdot \mathrm{E}[L], \sigma ^2 = N \cdot \mathrm{Var}[L])$. In that case,

$$
  \Pr[L < 0] = \Pr\left( \frac{L - \mathrm{E}[L]}{\sqrt{\mathrm{Var}[L]}} < \frac{0 - \mathrm{E}[L]}{\sqrt{\mathrm{Var}[L]}}\right) = \Phi\left(\frac{- \mathrm{E}[L]}{\sqrt{\mathrm{Var}[L]}}\right) = \alpha,
$$

where $\Phi$ is the cumulative distribution function of the standard normal distribution, $\mathcal{N}(0,1)$.

## Extra risks

This section discusses some of the common ways in which extra mortality risks is modelled in EPV calculations.

### Age rating

Extra risk is modeled by using mortality from an older life. For example, an impaired life aged 40 might be asked to pay the same premium paid by a non-impaired life aged 45. Then, we just apply the apply the equivalence principle in our calculation with the risk-adjusted rating age instead.

### Constant addition to the force of mortality

Individuals can also be deemed to be ineligible for standard rates if they regularly participate in hazardous pursuits. Since the extra risk is largely independent of age, we can add a constant $\phi$ to the force of mortality:

$$
  \mu^* _{[x] + s} = \mu _{[x] + s} + \phi.
$$

Then,

$$
  {} _t p^* _{[x]} = e ^{- \int _0 ^t (\mu _{[x] + s} + \phi) ds} = e ^{- \phi t} \cdot {} _t p _{[x]}
$$

The pure endowment function is

$$
  {} _t E ^* _x = v^t \cdot e ^{-\phi t} \cdot {} _t p _x = e ^{-(\delta + \phi)t} \cdot {} _t p _x.
$$

Hence, the pure endowment with a constant addition $\phi$ to $\mu_x$ is the same as the standard pure endowment evaluated with interest rate $j = e ^{\delta + \phi} - 1$, i.e. ${} _t E ^* _x = ({} _t E _{x})_j$. Then, for annuity-due function, 

$$
  \ddot{a} ^* _{[x]:\overline{n|}} = \sum _{t=0} ^{n-1} e ^{-(\delta + \phi)t} \cdot {} _t p _{[x]} = \ddot{a} _{[x]:\overline{n|}j}.
$$

Note that such adjustment-to-interest trick only apply to pure endowment (hence annuity) but not life insurance function. To derive the life insurance function, we use the relationship between annuity and life insurance:

$$
  A ^* _{[x]:\overline{n|}} = 1 - d\cdot \ddot{a} ^* _{[x]:\overline{n|}} = 1 - d\cdot \ddot{a} _{[x]:\overline{n|}j}.
$$

### Constant multiple of mortality rates

In this method, we assume the mortality rate for the substandard lives are a constant multiplier higher than the standard lives, i.e. $q ^* _{[x] + t} = m \cdot q _{[x] + t}$. To calculate the survival probability, a product of a sequence is needed:

$$
  {} _t p ^* _{[x]} = \prod _{r = 0} ^ {t - 1} (1 - m \cdot q _{[x] + r}),
$$

which can be done a spreadsheet for any annual interval. Another computational disadvantage of this approach is that we have to apply approximations in calculating EPVs if payments are at other than annual intervals.
