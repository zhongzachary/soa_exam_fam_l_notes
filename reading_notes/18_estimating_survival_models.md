# Chapter 18: Estimating survival models

- [Chapter 18: Estimating survival models](#chapter-18-estimating-survival-models)
  - [Introduction](#introduction)
  - [Actuarial lifetime data](#actuarial-lifetime-data)
  - [Non-parametric survival function estimation](#non-parametric-survival-function-estimation)
    - [The empirical distribution for seriatim data](#the-empirical-distribution-for-seriatim-data)
    - [The empirical distribution for grouped data](#the-empirical-distribution-for-grouped-data)
    - [The Kaplan–Meier estimator](#the-kaplanmeier-estimator)
    - [The Nelson–Aalen estimator](#the-nelsonaalen-estimator)
  - [The alive–dead model](#the-alivedead-model)
  - [Confidence interval of estimate](#confidence-interval-of-estimate)
    - [CI of survival function estimate](#ci-of-survival-function-estimate)
    - [CI of cumulative hazard function estimate](#ci-of-cumulative-hazard-function-estimate)

## Introduction

In this chapter, we consider some ways to use data to calibrate survival models. The statistical basis for this chapter largely comes from **survival analysis**. 

For actuarial applications, the lifetime data come from information about policyholders or pension plan members. Historically, data are substantially grouped. But it is now more common to collect and analyze data policy by policy. This is the **seriatim approach**. For each data point, the data will include all important information like date of birth and the date of purchase. If the policy is no longer active, the data will include the date that the policy expired, and it is due to death or surrender, or reaching end of the policy.

## Actuarial lifetime data

Here we are using a maximum likelihood approach to fit the model. Let $f_0$ denote the density function of the lifetime rv $T_0$. Let $t_j$ denote the age at death of the $j$-th life. If all the lives in the sample are observed from birth to death, then the likelihood function is 

$$
  L = \prod _{j=1} ^n f_0(t_j) = \prod _{j=1} ^n {} _{t_j} p _0 \cdot \mu _{t_j}.
$$

However, it is very rare that we can observe all lives from birth to death. More commonly the data are collected over a relatively short time interval. They are **left truncated** and **right censored**.

**Left truncated** means the information is conditional because there are some data points that are unseen (if the lives die before the starting age of the observations). This means if the life enters observation at age $x$, and dies at age $x+t$, then the contribution to the likelihood is conditional on survival to age $x$; hence it's density function is 

$$
  f _x(t) = \frac{f _0(x+t)}{S _0 (x)} = \frac{{} _{x+t} p _0 \cdot \mu _{x+t}}{{} _x p _0} = {} _t p _x \cdot \mu _{x+t}.
$$

**Censored data** occur when we know a range for a variable, but not an exact figure. Typically, mortality data are right censored, i.e., we know the individual is still alive when the period of observation ends. There are 2 types of censoring:

- **Type 1 censoring**: most common in lifetime data. In this case, lives are observed for a fixed period (or until earlier death). The period may differ for different lives, but it is known when the life enters the study. (Think of it like term insurance.) 
  - **Random censoring**: the censoring times are random, like the cases of lapsing. If the random time to censoring is independent of the time to death, then there is no effective different than type 1 censoring. However, this is unlikely to be true for term insurance, as people who are more likely to die are least likely to lapse. However, we will assume independence of the time to death and the time to the censored exit from observation.
  - **Interval censoring**: the interval, instead of the exact time, is observed.
- **Type 2 censoring**: less common in lifetime and more common in quality control. Under Type 2 censoring, a population is observed until a pre-specified number of failures (deaths in our case) has been recorded. In this case, the censoring time is random and depended on the times of failure.

To model right censored data, we need 2 random variables: the time until exit from the study, and the mode of exit. For the $j$-th life entered the study at age $x_j$, the time until exit is denoted $t_j$ and the mode of exit is denoted $\delta_j$. $\delta _j$ is a death indicator variable, signaling if the exit is due to death or censorship:

$$
  \delta _j = 
  \begin{cases}
    1 & \text{if } (x_j) \text{ died at time } t_j, \\
    0 & \text{if } (x_j) \text{ was right censored at time } t_j.
  \end{cases}
$$

Then, model fitting will be performed on a joint distribution with likelihood function

$$
  f_x(t, \delta) = {} _t p _x \cdot (\mu _{x+t})^\delta.
$$

If the mode of exit is **not death** (i.e. end of term or lapsing), the likelihood function is just the survival function $S_x(t)$, i.e., ${} _t p _x$.

For interval censoring, the likelihood function is 

$$
  {} _k p _x - {} _{k+1} p _x
$$

if life $(x)$ dies between time $k$ and $k+1$.

## Non-parametric survival function estimation

### The empirical distribution for seriatim data

If we have a sample of $n$ distinct failure times $t_1, t_2, \ldots, t_n$ with no censoring or truncation (sorted from the smallest to the largest), the empirical distribution have $\hat f (t_j) = 1 / n$ for all $n$. That means the survival function is a step function with

$$
  \hat S (t) = 
  \begin{cases}
    1               & 0   \leq t < t_1 \\
    1 - \frac{1}{n} & t_1 \leq t < t_2 \\
    1 - \frac{2}{n} & t_2 \leq t < t_3 \\
    \ldots \\
    0               & t_n \leq t       \\
  \end{cases}
$$

In other words,

$$
  \hat S (t) = \frac{\text{Number of survivors at time } t}{n} = \frac{n _ t}{n}.
$$

Note that the true distribution $S(t)$ is unknown. The number of survivors at time $t$ from $n$ lives has a binomial distribution, $N_t \sim \mathrm{Binomial}(n, S(t))$ and thus $\hat S(t) \sim N_t / n$. It has variance

$$
  \mathrm{Var}[\hat S (t)] = \frac{\mathrm{Var}[N_t]}{n^2} = \frac{S(t) \cdot (1 - S(t))}{n}.
$$

Again, $S(t)$ is unknown but we can approximate it with $\hat S$:

$$
  \mathrm{Var}[\hat S (t)] \approx \hat S (t) ^2 \cdot \left(\frac{1}{n_t} - \frac{1}{n}\right).
$$

### The empirical distribution for grouped data

When the data are interval censored, we don't have exact information on the times of death. 

We can construct the empirical survival function at the end of each interval. For the value between the grouped intervals, we need to make some assumption about the distribution of deaths. For example, we can assume the deaths are uniformly distributed and thus we can use linear interpolation. This is called the **ogive empirical survival function**.

### The Kaplan–Meier estimator

Say we have a list of $k$ exit times in our observation. Let's label the deceased lives in the observation as $(1), (2), \ldots, (n)$, ordered ascendingly by the death time. Note that $n \leq k$ because not all samples exited due to death.

The **Kaplan-Meier estimate (aka the product limit estimate) considers the survival probability at time when deaths occurred**, i.e., $t_{(j)}$ for $j = 1, 2, \ldots, n$. Then, **it estimate the survival function by multiplying all survival probability**.

First, we define $p_{(j)}$. This is the probability that a life survived right before time $t_{(j)}$ but deceased right after $t_{(j)}$. It can be estimated by

$$
  \hat{p}_{(j)} = \frac{\text{number of lives surviving to time $t^+ _{(j)}$}}{\text{number of lives surviving to time $t^- _{(j)}$}}.
$$

Here, $t^+$ and $t^-$ indicate the time right after and right before time $t$, correspondingly.

Then, the survival function can be estimated by

$$
  \hat{S}(t) = \prod_{\forall j: t_{(j)} < t} \hat{p}_{(j)}.
$$

Let's do an example to demonstrate how it works. Say we have the following observations:

$$
  4^+, 5, 10, 10+, 14, 15^+, 16^+, 17, 19^+, 20.
$$

Here, the ${} ^+$ indicates the observation is right-censored (i.e. the exit time is not due to death). There are 5 times of deaths that the Kaplan-Meier estimate will concern about: $5, 10, 14, 17, 20$.

We can create a table like this

| $j$ | $t _{(j)}$ | $r _j$ | $d _j$ | $\hat{p} _{(j)}$ | $\hat{S} (t _{(j)})$ |
| --: | ---------: | -----: | -----: | ---------------: | ------------: |
|   0 |          0 |     10 |        |                  |             1 |
|   1 |          5 |      9 |      1 |              8/9 |           8/9 |
|   2 |         10 |      8 |      1 |              7/8 |           7/9 |
|   3 |         14 |      6 |      1 |              5/6 |         35/54 |
|   4 |         17 |      3 |      1 |              2/3 |        70/162 |
|   5 |         20 |      1 |      1 |              0/1 |             0 |

Here, 
- $r _j$, aka the **risk set**, is the number of lives survives right before time $t _{(j)}$. It doesn't count lives exit before time $t _{(j)}$ regardless of exit mode. 
- $d _j$ is the number of deaths at time $t _{(j)}$.
- $\hat p _{(j)}$ is calculated as $1 - \frac{d _j}{r _j}$.
- $\hat S (t _{(j)}) = \hat S (t _{(j-1)}) \cdot \hat p _{(j)}$.

And for $t$ such that $t \in [t _{(j)}, t _{(j+1)})$, $S(t) = S(t _{(j)})$.

To handle incoming (left-truncated) observations, a very small modification is needed by adding these incoming observations to the risk set $r _{(j)}$.

The Kaplan-Meier estimate also works very well with grouped data as the $d _{(j)}$'s need not to be 1s.

To estimate the variance of $\hat S (t)$, we can use Greenwood formula (available in the formula sheet):

$$
  \mathrm{Var}[\hat S (t)] \approx \hat{S} (t) ^2 \cdot \sum _{\forall j: t _{(j)} < t} \frac{d _j}{r _j \cdot (r _j - d _j)}.
$$

Notes on Kaplan-Meier calculations
- The $t$ in the model can be either age (for life table) or time (for other survival analysis like survival time of a disease).
- If the final value is censored, a maximum age can be set and use exponential extrapolation.
- For a very large dataset with short interval of, say $h$, $h \cdot \mu _{t _{(j)}}$ will be close to $1 - \hat p _{(j)}$.
- Kaplan-Meier survival function could be used as the basis of a life table, though it probably needs some smoothing first.
- Kaplan-Meier can also be used to assess if experience aligns with a given life table.

### The Nelson–Aalen estimator

The Nelson–Aalen estimator is a non-parametric estimator of the cumulative hazard function, $H(x)$, which can be used to construct a non-parametric estimator for the survival function. 

Note that the cumulative hazard function is 

$$
  H(x) = \int _0 ^x \mu _{y} dy,
$$

and thus $S _0 (x) = e ^{-H(x)}$.

To estimate $H(x)$, we use

$$
  \hat H(x) = \sum _{\forall j: t_{(j)} \leq x} \frac{d _j}{r _j},
$$

where the definition of each variable can be found in the previous section. As a refresher, $r _j$ is the number of lives survived right before the $j$-th death time, and $d _j$ is the number of deaths at the $j$-th death time.

The variance of $\hat H (x)$ is 

$$
  \mathrm{Var}[\hat H (x)] \approx \sum _{\forall j: t_{(j)} \leq x} \frac{d _j \cdot (r _j - d _j)}{r _j ^3}.
$$

But we are more concern about the survival function, $\hat S (x) = e ^{- \hat H (x)}$. Using the delta method again, we can derive the variance of the survival function estimate (also in the formula sheet):

$$
  \mathrm{Var}[\hat S (x)] \approx \hat S(x) ^2 \cdot \mathrm{Var}[\hat H (x)] = \hat S(x) ^2 \cdot \sum _{\forall j: t_{(j)} \leq x} \frac{d _j \cdot (r _j - d _j)}{r _j ^3}.
$$

## The alive–dead model

The previous methods use the mortality data to estimate the survival function or the cumulative hazard function. However, the **force of mortality** is the more basic building block and that's what the **alive-dead model** is trying to estimate.

In an alive-dead model, the data are partitioned into age-years, and the force of mortality for each age is calculated separately.

For example, say we have a life that entered the observation at age 40.2 and died at age 50.3. It will be partitioned into multiple data points:
- for $\mu _{40}$, the partitioned data point is $x = 40.2, t = 0.8, \delta = 0$. Here $t$ is called the **waiting time**, i.e., the time to reach the end of the observation window for $\mu _{40}$. $\delta$, the death indicator, is 0, which indicated the data point didn't die before the observation window for $\mu _{40}$.
- for $\mu _{k}$, where $k = 41, 42, \ldots, 50$, the partition data points are $x = k, t = 1, \delta = 0$.
- for $\mu _{50}$, the data point is $x = 50, t = 0.2, \delta = 1$.

Here, the exit mode of the life is death so the last data point has $\delta = 1$. In the case where the exit mode is not death, the last data point will have $\delta = 0$.

Then, given that there are $n$ data points to estimate $\mu _x$, the probability density function of $(t _j, \delta _j)$ for the $j$-th data point is

$$
  f _{x _j} (t _j , \delta _j) = {} _{t _j} p _{x _j} \cdot (\mu _{x _j + t _j}) ^ {\delta _j}.
$$

Note that $t _j$ and $\delta _j$ are not independent (since $t _j = 1$ will indicate $\delta _j = 0$). We also **assume constant force of mortality** within each age-year; hence, 

$$
  f _{x _j} (t _j , \delta _j) = e ^{- t _j \cdot \mu _x} \cdot \mu _x ^ {\delta _j},
$$

and the likelihood function for $\mu _x$ is $L(\mu _x) = \prod _{j = 1} ^n f _{x _j} (t _j , \delta _j)$. The **maximum likelihood estimate** of $\mu _x$ will then be 

$$
  \hat \mu _x = \frac{d _x}{w _x} = \frac{\text{total number of deaths of $n$ data points}}{\text{total waiting time of $n$ data points}}.
$$

Here, the total waiting time of $\mu _x$ is traditionally called the **central exposed to risk**, denoted $E ^c _x$. 

And the variance of the estimate is 

$$
  \mathrm{Var} [\hat \mu _x] = \frac{d _x}{w _x ^2}.
$$

With the force of mortality, we can estimate the mortality rate

$$
  \hat q _x  = 1 - e ^{- \hat \mu _x}.
$$

The variance of $\hat q _x$ can be estimated using the delta method:

$$
  \mathrm{Var}[\hat q _x] = e ^{- 2 \cdot \hat \mu _x} \cdot \mathrm{Var}[\hat \mu _x].
$$

One caveat is that since the estimator takes data points for ages between $x$ and $x+1$, it is more appropriate for $\mu _{x + 0.5}$, i.e. $\hat \mu _{x + 0.5} = \frac{d _x}{w _x}$. Under UDD, we can show that 

$$
  q_x = \frac{\mu _{x + 0.5}}{1 + 0.5 \cdot \mu _{x + 0.5}}.
$$

Hence,

$$
  \tilde q = \frac{d _x}{w _x + 0.5 \cdot d_x},
$$

which is called the **actuarial estimate** of $q _x$. There is very small difference between $\hat q _x$ and $\tilde q _x$ when $\mu _x$ is small. But the MLE $\hat q _x$ is more consistent, therefore generally preferred. One problem of $\tilde q _x$ is that the estimator assume constant force of mortality but than it used UDD later to create the actuarial estimate.

## Confidence interval of estimate

The formula sheet provides the variance of the survival function estimate $\hat S (t)$ for both the Kaplan-Meier estimator and the Nelson-Aalen estimator.

Note that in the variance formula of $\hat S(t)$ for Nelson-Aalen estimator, it also embedded the variance formula for $\hat H(t)$. Specifically, the formula sheet shows

$$
    \mathrm{Var}[\hat S (t)] \approx  \hat S(t) ^2 \cdot \underbrace{\sum _{\forall j: t_{(j)} \leq x} \frac{d _j \cdot (r _j - d _j)}{r _j ^3}}_{\mathrm{Var}[\hat H (t)]}.
$$

### CI of survival function estimate

Now, we can move on to the discussion of **confidence interval (CI) of the survival function estimates**. There are 2 types of CI:
- **linear CI**
  
  $$
    \mathrm{CI} = \hat S(t) \pm z\cdot \sqrt{Var[\hat S(t)]}.
  $$
  
  But the shortcoming is that since $\hat S(t) \in [0, 1]$, the CI may be out of range. Hence we use the log CI.

- **log CI**
  
  Since $\hat S(t) \in [0, 1]$, we can use function $g: [0, 1] \to (-\infty, \infty), g(t) = \ln (- \ln (t))$ to transform $\hat S (t)$. By delta method, 

  $$
    \mathrm{Var}[g(\hat S(t))] \approx \left(\frac{d g(\hat S (t))}{d\hat S (t)}\right)^2 \cdot \mathrm{Var}[\hat S (t)] = \left( \frac{1}{\hat S (t) \cdot \ln \hat S (t)}\right) ^2 \cdot \mathrm{Var}[\hat S (t)].
  $$

  If we denote $\sigma _g = \frac{\sqrt{\mathrm{Var}[\hat S (t)]}}{\hat S (t) \cdot |\ln \hat S (t)|}$, then the CI for  $g(\hat S(t))$ is 

  $$
    \mathrm{CI}[g(\hat S(t))] = g(\hat S(t)) \pm z \cdot \sigma _g.
  $$

  Let's denote the above CI as $(L_g, U_g)$. Note that $t \to 0, g(t) \to \infty$ and $t \to 1, g(t) \to -\infty$, the $L_g$ will be the upper bound of $\mathrm{CI}[\hat S(t)]$, and vice versa. And to transform back to $\mathrm{CI}[\hat S(t)]$, we use $g ^{-1}(t) = e ^{-e ^ t}$:

  $$
    \begin{aligned}
      \mathrm{CI}[\hat S(t)] &= \Big( g ^{-1}(U_g), g ^{-1} (L_g) \Big) \\
      &= \Big( g ^{-1}(g(\hat S(t)) + z \cdot \sigma _g), g ^{-1} (g(\hat S(t)) - z \cdot \sigma _g) \Big) \\
      &= \Big( (\hat S(t)) ^ {\exp(z\cdot \sigma _g)}, (\hat S(t)) ^ {\exp(-z\cdot \sigma _g)} \Big)
    \end{aligned}
  $$

  **Exam tips**: In the exam, it may provide the log-CI of $\hat S (t)$, denoted $(L', U')$. The above formula will help us to find out the followings
  - $\exp({z \cdot \sigma _g}) = \sqrt{\ln L' / \ln U'}$,
  - $\hat S (t) = \sqrt[\exp({z \cdot \sigma _g})]{L}$, and
  - $\mathrm{Var} [\hat S(t)]$ by using the definition of $\sigma_g$.

### CI of cumulative hazard function estimate

The same **log CI method can also be applicable to the Nelson-Aelen cumulative hazard function estimate**, $\hat H(t)$. Since $\hat H(t)$ has a range of $(0, \infty)$, we just need to use $g(t) = \ln x$. Then

$$
  \mathrm{Var}[g(\hat H(t))] \approx \left(\frac{d g(\hat H (t))}{d\hat H (t)}\right)^2 \cdot \mathrm{Var}[\hat H (t)] = \left( \frac{1}{\hat H (t)}\right) ^2 \cdot \mathrm{Var}[\hat H (t)].
$$

If we denote $\mathrm{CI}[g(\hat H(t))] = \big( \mathrm{Lower}_{g(\hat H(t))}, \mathrm{Upper} _{g(\hat H(t))} \big)$, the CI for $\hat H(t)$ is 

$$
  \mathrm{CI}[\hat H(t)] = \Big( \exp (\mathrm{Lower} _{g(\hat H(t))}), \exp (\mathrm{Upper}_{g(\hat H(t))}) \Big).
$$
