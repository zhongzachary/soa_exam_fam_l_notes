# Chapter 7: Policy values

- [Chapter 7: Policy values](#chapter-7-policy-values)
  - [The future loss rv and the policy value function](#the-future-loss-rv-and-the-policy-value-function)
  - [Policies with annual cash flows](#policies-with-annual-cash-flows)
    - [Variance of future loss rv](#variance-of-future-loss-rv)
    - [Recursive formulae for policy values](#recursive-formulae-for-policy-values)
  - [Policy values for policies with monthly cash flows](#policy-values-for-policies-with-monthly-cash-flows)
    - [Recursions with monthly cash flows](#recursions-with-monthly-cash-flows)
    - [Valuation between premium dates](#valuation-between-premium-dates)
  - [Negative policy values](#negative-policy-values)
  - [Deferred acquisition expenses and modified net premium reserves](#deferred-acquisition-expenses-and-modified-net-premium-reserves)
    - [Full preliminary term reserve](#full-preliminary-term-reserve)

## The future loss rv and the policy value function
Policy values are a fundamental tool in insurance risk management, as they are used to determine the economic or regulatory capital needed to remain solvent, and also to determine the profit or loss for the company over any time period.

We define the policy value as the **expected value of future net cash flows** for a policy in force, and distinguish **gross premium policy values**, which explicitly allow for expenses and for the full gross premium, from **net premium policy values**, where expenses are excluded from the outgoing cash flows, and only the net premium is counted as income.


In the last chapter, we discuss the loss rv at issue, $L_0$. Here, for a policy in force at time $t$, we extend the concept to the time $t$ **future loss rv**. There are also a net version and a gross version:

$$
  L ^n _t = \text{PV of future benefits at } t - \text{PV of future net premiums at } t,
$$

and 

$$
  L ^g _t = \text{PV of future benefits at } t + \text{PV of future expenses at } t - \text{PV of future gross premiums at } t.
$$

Generally speaking, the future premiums should be expected to be sufficient to pay for future benefits and expenses at time 0. However, for a policy that is still in force $t$ years after issue, the future premiums are not expected to cover all future benefits. The difference between future benefits and future premiums is called the **policy value**.

The insurer should already be building up assets from past premiums. In the early years of the policy, when the premium income is usually larger than benefit outgo, the insurers can prepare for a future when the premium income is no longer enough for benefit outgo. Therefore, another way to understand **policy value** is the future value  of the accumulated surplus.

When 

1. the premium was calculated using the equivalence principle,
2. $\mathrm{E}[L_t]$ is calculated using the premium basis, and
3. the experience followed precisely the assumptions in the premium basis,

the FV at $t$ of premiums received minus the benefits paid before time $t$ should be the same as the policy value at time $t$ (i.e. PV at $t$ of the benefits to be paid minus premiums to be received after time $t$).


We denote a policy value $t$ years after issue as ${} _t V$, we have the following equation:

$$
  \boxed{{} _t V + \mathrm{EPV}_t(\text{future premiums}) = \mathrm{EPV}_t(\text{future benefits} + \text{expenses})}.
$$

For an insurance company, it is important to calculate the sum of all policy values and the value of all investments. This process is called **valuation**. 

In the literature, the terms **reserve**, **prospective reserve** and **prospective policy value** are sometimes used in place of policy value.
We use **policy value** to mean the expected value of the future loss rv, and restrict **reserve** to mean the actual provision made in respect of future policy obligations.

The precise definitions of policy value are as follows.

**Gross premium policy value**: The gross premium policy value for a policy in force at duration $t \geq 0$ years after it was purchased is the expected value at that time of the gross future loss rv on a specified basis. The premiums used in the calculation are the actual premiums payable under the contract.

**Net premium policy value**: The net premium policy value for a policy in force at duration $t \geq 0$ years after it was purchased is the expected value at that time of the net future loss rv on a specified basis (which makes no allowance for expenses). The premiums used in the calculation are the net premiums calculated on the policy value basis using the equivalence principle, not the actual premiums payable.

Note that the assumptions used for valuation, called the **policy value basis**, may differ from the assumptions used to calculate premium (i.e. the premium basis). The policy value basis can also have a different expense assumption then the premium basis. Hence, the net premiums used in valuation can be different from the net premiums at issue.

## Policies with annual cash flows

In this section, we restrict ourselves to policies where the cash flows occur only at the start or end of a year since these policies have some simplifying features in relation to policy values.

Caveats:
- Premiums and/or expenses and/or benefits payable at precisely that time and we need to be careful about which cash flows are included in our future loss random variable. 
- Usually, premium and premium-related expenses due at that time as *future payments*, and benefit and related expenses as *past payments*. 
- For annuity, however, annuity payments and related expenses may be treated either as future or as past payments.
- For an insurance policy with finite term, $n$ years, the policy value at time $n$ is technically undefined as the policy is no longer in force. However, it is common to use ${} _n V$ to refer to the policy value immediately before the expiry of the policy (i.e. immediately before the last payment). In other words, ${} _n V = \lim _{t \to n^-} {} _t V$.

**Example** Consider a fully discrete $n$-year endowment insurance sold to a select life aged $x$ and assume there are no expenses. Let $P$ denote the net premium, and let $S$ denote the sum insured. The net policy values for $0 \leq t < n$ is

$$
  {} _t V = S\cdot A_{[x] + t:\overline{n - t|}} - P\cdot \ddot{a}_{[x] + t:\overline{n - t|}}.
$$

Let also see an example with expenses.

**Example** Consider a deferred annuity policy issued to a life aged $x$, with annual premiums during deferment, annuity payments of $M$ per year starting age $x + d$, and where any premiums paid are returned on death during the deferred period.

Expenses are 10% of the first premium and 5% of subsequent premiums, plus $25 with each annuity payment, and $100 on payment of death benefit.

The policy value will be losses and their expenses:
- death benefit during the deferred period. Note that this has increasing death benefit. At time $t$, the death benefit at time $t+1, t+2, t+3, \ldots, d$ (assuming the policyholder dies during the year) is $t+1, t+2, t+3, \ldots, d$. Hence, the EPV of death benefit at time $t$ is  $P\cdot (IA) _{[x] + t:\overline{d - t|}} ^ 1 + t\cdot P \cdot A _{[x] + t:\overline{d - t|}} ^ 1$;
- expense on death benefit: $100\cdot A _{[x] + t:\overline{d - t|}} ^ 1$;
- annuity benefit: $M \cdot {} _{d - t} E _{[x]+t} \cdot \ddot{a} _{[x]+ d}$
- expense on annuity benefit: $25 \cdot {} _{d - t} E _{[x]+t} \cdot \ddot{a} _{[x]+ d}$

The EPV of future premiums less associated expenses is $(1 - 5\%)\cdot P \cdot \ddot{a} _{[x] + t: \overline{d - t|}}$. If $t = 0$, there are additional expense on premium $5\% \cdot P$.

Hence, the policy value at time $t$ is 

$$
  \begin{aligned}
    {} _t V = &P\cdot (IA) _{[x] + t:\overline{d - t|}} ^ 1 + (t\cdot P + 100) \cdot A _{[x] + t:\overline{d - t|}} ^ 1 + (M + 25) \cdot {} _{d - t} E _{[x]+t} \cdot \ddot{a} _{[x]+ d} \\ 
    &- (1 - 5\%)\cdot P \cdot \ddot{a} _{[x] + t: \overline{d - t|}}
  \end{aligned}
$$

### Variance of future loss rv

For a whole life insurance policy of sum insured $S$ issued to $(x)$, let $L_t$ be the future loss rv at time $t$.

Then, the expected value is 

$$
  \mathrm{E}[L_t] = \mathrm{E}\left[S \cdot v ^{K _{x+t} + 1} - P\cdot \frac{1- v^{K _{x+t} + 1}}{d}\right] = S\cdot A _{x+t} - P\cdot \ddot {a} _{x+t},
$$

And the variance is

$$
  \begin{aligned}
    \mathrm{Var}[L_t] &= \mathrm{Var}\left[S \cdot v ^{K _{x+t} + 1} - P\cdot \frac{1- v^{K _{x+t} + 1}}{d}\right] \\
    &= \left(S+\frac{P}{d}\right)^2\cdot \mathrm{Var}[v ^{K _{x+t} + 1}] \\
    &= \left(S+\frac{P}{d}\right)^2\cdot \left({} ^ 2 A _{x+t} - A _{x+t} ^2\right) \\
  \end{aligned}
$$

If the premium is calculated using equivalent principle, we have

$$
  P = \frac{S \cdot A_{x}}{\ddot{a}_{x}} 
  = \frac{S \cdot (1 - d \cdot \ddot{a} _x)}{\ddot a _{x}} = S\cdot \left(\frac{1}{\ddot a _x} - d\right).
$$

Then,

$$
  \begin{aligned}
    \mathrm{Var}[L_t] &= \left(\frac{S\cdot d + S\cdot \left(\frac{1}{\ddot a _x} - d\right)}{d} \right)^2 \cdot \left({} ^ 2 A _ {x+t} - A _{x+t} ^2\right) \\
    &= \left( \frac{S}{d\cdot \ddot a _x} \right) ^2 \cdot \left({} ^ 2 A _ {x+t} - A _{x+t} ^2\right) \\
    &= \left( \frac{S}{1 - A_x} \right) ^2 \cdot \left({} ^ 2 A _ {x+t} - A _{x+t} ^2\right)
  \end{aligned}
$$

### Recursive formulae for policy values

**Example** Consider a fully discrete $n$-year endowment insurance sold to a select life aged $x$ and assume there are no expenses. Let $P$ denote the net premium, and let $S$ denote the sum insured. For $0 \leq t < n$, we have

$$
  ({} _t V + P)\cdot (1 + i) = S \cdot q_{[x] + t} + {} _{t+1} V \cdot p _{[x] + t}.
$$

This formulations make senses because the LHS is the current policy value plus premium, accumulating interest for 1 year, while the RHS is the expected death benefit payout (if the policyholder dies in 1 year) and the next year's expected policy value (if the policy hold survives 1 year).

Let also see an example with expenses.

**Example** Consider a deferred annuity policy issued to a life aged $x$, with annual premiums during deferment, annuity payments of $M$ per year starting age $x + d$, and where any premiums paid are returned on death during the deferred period.

Expenses are 10% of the first premium and 5% of subsequent premiums, plus $25 with each annuity payment, and $100 on payment of death benefit.

Then, we have the following recursive formula

$$
({} _t V + 95\% \cdot P) \cdot (1 +i) = ((t+1) \cdot P + 100) \cdot q _{[50] + t} + p _{[50] + t} \cdot {} _{t+1} V.
$$

Again, to make sense of this formula, the LHS is current policy value plus the premium less expenses (i.e. the premium that can be added to the fund), accumulating interest for 1 year. The RHS is the expected death benefit plus expenses (if the policyholder dies) and the next year's expected policy value (if the policyholder survives).

With these 2 examples, we can come up with something that applies more generally. Let
- $i_t$ denote the annual effective interest for year $t$.
- $P_t$ denote the premium payable at time $t$,
- $e_t$ denote the renewal expenses payable at time $t$,
- $S_{t}$ denote the sum insured payable at time $t$ if the policyholder dies during $t-1$ and $t$,
- $E_{t}$ denote the expenses of paying the sum insured at time $t$, and
- ${} _t V$ denote the gross premium policy value for a policy in force at time $t$.

Then, we have
$$
  \boxed{({} _t V + P _t - e _t) \cdot (1 + i _t) = q _{[x] + t} \cdot (S _{t+1} + E _{t+1}) + p _{[x]+t} \cdot {} _{t+1} V}.
$$

We also have a very important concept call **Sum at Risk** (SAR), or the **death strain at risk** or the **net amount at risk**. This is the different because the death benefit at $t$ and the policy value at $t$, i.e. $S_t - {} _ t V$. It measures how much the insurer need to make up to cover the death benefit at time $t$. It is useful in determining risk management strategy, including reinsurance.

There are also cases where the death benefit is related to the policy value and direct calculation of policy value using premiums and benefit is impossible. Then, we have to use recursive formula.

For example, consider a $n$-year endowment with a level premiums of $P$. A sum insured of $S$ is payable at the the end of the term if the life survives. On death before the end of the term, a sum insured is payable at the end of the year of death equal to the policy value. Assuming there is no expense, we then have to following backward recursion to calculate policy value:

- ${} _n V = S$
- $({} _{t} V + P) \cdot (1 + i) = q_{x+t} \cdot {} _{t} V + p _{x+t} \cdot {} _{t+1} V$. Hence, $\displaystyle {} _t V =  \frac{p _{x+t} \cdot {} _{t+1} V - P \cdot (1 + i)}{1 + i - q _{x+t}}$ for $0 \leq t < n$.

---

Skip 7.2.4 and 7.2.5

## Policy values for policies with monthly cash flows

The policy values for policies with $1/m$-thly cash flows  can be calculate similarly to the annual case but with actuarial value functions of the similar frequency.

### Recursions with monthly cash flows

Recursive formulas of the $1/m$-thly case is again similar to the annuity case. 

For example, For a policy with premiums of $P$ every $1/m$ years, premium expenses of $e_t$ at time $t$, and sum insured $S$ payable at the end of the $1/m$-th year of death, we have

$$
  ({} _ V + P - e _t) \cdot (1 + i) ^{1/m} = {} _{1/m}q _{[x]+t} \cdot S + {} _{1/m} p _{[x] +t} \cdot {} _{t+1/m}V.
$$

### Valuation between premium dates

The principle when valuing between premium dates is the same as when valuing on premium dates; the policy value is the EPV of future benefits plus expenses minus premiums. 

In general, say we are calculating ${} _t V$ where $t$ is not a benefit or premium payment date; let $h$ denote the time to the next benefit date, which is assumed to be at or before the next premium date. Assume that we known ${} _{t+h} V$. Then for an insurnace with death benefit $S$, we have

$$
  {} _t V \cdot (1 + i) ^h = {} _h q _{[x] + t} \cdot S + {} _h p _{[x] +t} \cdot {} _{t+h} V.
$$

Note that it would not be appropriate to apply simple interpolation of the policy values of premium dates right before and after the valuation. This is because the policy value will jump right after the premium payment and decreases until the next premium. 

A more reasonable approximation is to interpolation the policy value just after the previous premium and the policy value just before the next premium. Suppose the premium dates are $1/m$ years apart, and that $t$ is the premium date. For $0 < s < 1/m$, we can approximate policy value at $t + s$ by interpolating between ${} _t V + P_t - e_t$ and ${} _{t + 1/m} V$.

---

Skip continuous cash flow, policy alterations, and retrospective policy values (7.4 - 7.6)

---

## Negative policy values

It can happen that a policy value is negative. This is not uncommon in the first few months of a contract, after initial expenses have been incurred and before sufficient premium is collected.

However, it would be unusual for policy values to be negative after the early period of the contract. The only way for a negative policy value to arise is if the future benefits are worth less than the future premiums.

In practice, negative policy values would generally be set to zero when carrying out a valuation of the insurance company. This is because policyholders have the option to to lapse the contract, hence should not be booked as an asset (negative policy value).

Negative policy values arise when a contract is poorly designed, so that the value of benefits in early years exceeds the value of premiums. If the policyholder lapses then the policyholder will have benefitted from the higher benefits in the early years without waiting around to pay for the benefit in the later years.

## Deferred acquisition expenses and modified net premium reserves

The insurance regulators decide the principles of reserve calculation, such as whether to use a gross or net premium policy value, and how to determine the appropriate basis. While most jurisdictions use a gross premium policy value approach, as mentioned above, the net premium policy value is still used in the USA.

The use of the net premium approach can be computationally advantageous, and perhaps smoothing results. But when large initial expenses (acquisition expenses) incurred, it can be quite a severe standard.

To reduce the impact, the reserve is not calculated directly as the net premium policy value, but can be modified, to approximate a gross premium policy value approach, while maintaining the advantages of the net premium approach.

First we define the expense loading $P^e = P^g - P^n$, that is the gross premium minus the net premium, all calculated on the same basis.

Then

$$
  \begin{aligned}
    {} _t V ^g = & \text{ EPV future benefits } + \text{ EPV future expenses} \\ 
    &- (\text{EPV future net premiums } + \text{ EPV future expense loadings}) \\
    = & {}_t V ^n + \text{ EPV future expenses } - \text{ EPV future expense loadings } \\
    = & {} _t V ^n + {}_t V ^e,
  \end{aligned}
$$

where ${} _t V^e$ is the expense policy value.

In general, for $t > 0$, ${} _t V ^e < 0$, i.e. the gross premium is less than the net premium. If both the expenses and the premiums are level, ${} _t V ^g$ and ${} _t V ^n$ are the same as the extra expenses will be exactly offset by the extra premium. In practice, the acquisition expenses are always larger than the renewal and claim expenses, so $P^e$ will need to cover both renewal expenses and some of the initial expenses. Thus, EPV of future expenses will be less than EPV of future expense loadings, making ${} _t V ^e$ negative.

The negative expense reserve is referred to as the **deferred acquisition cost** (DAC). The use of net premium reserve can be viewed as being overly conservative, as it doesn't allow for DAC reimbursement like gross premium reserve. To maintain the computational advantage of net premium reserve, we can use **modified net premium reserves**, in which a lower initial premium is assumed to allow implicitly for the DAC.

### Full preliminary term reserve

To achieve modified net premium reserves, the most common method is the full preliminary term (FPT) reserve. It separates the policy into 2: the policy that covers only the 1st year, and the policy that covers all subsequent years.

For example, consider a whole life insurance with level annual premiums payable throughout the term. Then, 
- The first year FPT premium is ${} _1 P _{[x]} = S \cdot A ^1 _{[x]:\overline{1|}} = S \cdot v \cdot q _{[x]}$. This is also the first year cost of insurance.
- The subsequent FPT premium is 
  
  $$
    P _{[x] + 1} = \frac{S \cdot A _{[x] + 1}}{\ddot{a} _{[x] + 1}}
  $$

Because ${} _1 P _{[x]}$ is much lower than $P _{[x] + 1}$, that's how FPT implicitly accounts for higher acquisition cost.

Note that

- FPT reserves at time $t = 0$ and $t = 1$ are always equal to 0.
- FPT approach (and other modified net premium approaches) uses **net premium policy values**. The modified net premium approaches is only different than unmodified net premium approach in that the former doesn't assume level premiums.
- The FPT reserve is intended to very roughly approximate the gross premium policy value, especially in the first few years. All policy values will eventually converge.
- The FPT approach assume all first year's gross premium is spent on the cost of insurance and the acquisition expenses.
- There is a partial preliminary term method that would assume additional net premium than the cost of insurance. This will result in a slightly lower modified premium since the second year.
