# SOA FAM-L Study Notes
Author: Shanghao Zhong

Date: 2022-07-21

- [SOA FAM-L Study Notes](#soa-fam-l-study-notes)
  - [Reading Notes](#reading-notes)
  - [Syllabus](#syllabus)
    - [7. Insurance Coverages and Retirement Financial Security Programs](#7-insurance-coverages-and-retirement-financial-security-programs)
    - [8. Mortality Models](#8-mortality-models)
    - [9. Parametric and Non-Parametric Estimation](#9-parametric-and-non-parametric-estimation)
    - [10. Present Value Random Variables for Long-Term Insurance Coverages](#10-present-value-random-variables-for-long-term-insurance-coverages)
    - [11. Premium and Policy Value Calculation for Long-Term Insurance Coverages](#11-premium-and-policy-value-calculation-for-long-term-insurance-coverages)

## Reading Notes
Textbook: *Actuarial Mathematics for Life Contingent Risks, Third Edition (2020)*
> - Authors: David C. M. Dickson, Mary R. Hardy and Howard R. Water
> - Publisher: Cambridge University Press
> - ISBN: 978-1-108-47808-3

Required chapters:
| Chapter                        | Topic                    | Note                                                 | Status      | Related topics                                                                                                                                           |
| ------------------------------ | ------------------------ | ---------------------------------------------------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1                              | Intro to life insurance  | [md](reading_notes/01_intro.md)                      | Completed   | [7](#7-insurance-coverages-and-retirement-financial-security-programs)                                                                                   |
| 2                              | Survival model           | [md](reading_notes/02_survival_models.md)            | Completed   | [8](#8-mortality-models)                                                                                                                                 |
| 3 (except 3.11, 3.12)          | Life tables              | [md](reading_notes/03_life_tables_and_selection.md)  | Completed   | [8](#8-mortality-models)                                                                                                                                 |
| 4                              | Life insurance functions | [md](reading_notes/04_insurance_benefits.md)         | Completed   | [10](#10-present-value-random-variables-for-long-term-insurance-coverages)                                                                               |
| 5                              | Annuity functions        | [md](reading_notes/05_annuities.md)                  | Completed   | [10](#10-present-value-random-variables-for-long-term-insurance-coverages)                                                                               |
| 6                              | Premium calculation      | [md](reading_notes/06_premium_calculation.md)        | Completed   | [11. Premium and Policy Value Calculation for Long-Term Insurance Coverages](#11-premium-and-policy-value-calculation-for-long-term-insurance-coverages) |
| 7 (1-3, except 2.4, 2.5, 7, 8) | Policy values            | [md](reading_notes/07_policy_values.md)              | Completed   | [11. Premium and Policy Value Calculation for Long-Term Insurance Coverages](#11-premium-and-policy-value-calculation-for-long-term-insurance-coverages) |
| 18 (1-5)                       | Model estimation         | [md](reading_notes/18_estimating_survival_models.md) | Not started |                                                                                                                                                          |

## Syllabus

Topics 1-6 are for FAM-S and are not included in this note. The weights for the following FAM-L topics are scaled to sum to 100%.

### 7. Insurance Coverages and Retirement Financial Security Programs
Weight
: 5% - 15%

Learning objectives
: understand the key features of insurance coverages and retirement financial security programs.

Learning outcomes
:
  1. Define and apply the concept of insurable interest.
  2. Identify the long-term insurance coverages (life, health), annuities, and defined benefit and defined contribution pension plans.

### 8. Mortality Models
Weight
: 15% - 25%

Learning objectives
: understand key concepts concerning parametric and non-parametric mortality models for individual lives.

Learning outcomes
:
  1. Understand parametric survival models, life tables, and the relationships between them.
  2. Given a parametric survival model, calculate survival and mortality probabilities, the force of mortality function, and curtate and complete moments of the future lifetime random variable.
  3. Identify and apply standard actuarial notation for future lifetime distributions and moments, including select and ultimate functions.
  4. Given a life table, calculate survival and mortality probabilities, the force of mortality function, and curtate and complete moments of the future lifetime random variable, using appropriate fractional age assumptions where necessary.
  5. Understand and apply select life tables.
  6. Identify common features of population mortality curves.

### 9. Parametric and Non-Parametric Estimation
Weight
: 10% - 20%

Learning objectives
: understand and be able to estimate parameters for parametric and non- parametric survival models.

Learning outcomes
:
  1. Estimate the parameters for severity, frequency, and aggregate distributions using Maximum Likelihood Estimation for:
   
     - Complete, individual data
     - Complete, grouped data
     - Truncated or censored data
  
  2. Apply Kaplan Meier and Nelson Aalen methods to estimate empirical survival functions using censored and truncated lifetime data.
  3. Calculate approximate standard errors of the parameter/probability estimates.
  4. Construct linear and non-linear confidence intervals (as appropriate) for parameters/estimates.

### 10. Present Value Random Variables for Long-Term Insurance Coverages
Weight
: 20% - 30%

Learning objectives
: be able to perform calculations on the present value random variables associated with benefits and expenses for long term insurance coverages.

Learning outcomes
:
  1. Identify the present value random variables associated with life insurance, endowment, and annuity payments for single lives, based on annual, 1/m-thly and continuous payment frequency.
  2. Calculate probabilities, means, variances and covariances for the random variables in 10.1, using fractional age or claims acceleration approximations where appropriate.
  3. Understand the relationships between the insurance, endowment, and annuity present value random variables in 10.1, and between their expected values.
  4. Calculate the effect of changes in underlying assumptions (e.g., mortality and interest).
  5. Identify and apply standard actuarial notation for the expected values of the random variables in 10.1.

### 11. Premium and Policy Value Calculation for Long-Term Insurance Coverages
Weight
: 25% - 35%

Learning objectives
: be able to use and explain the premium and policy value calculation processes for long-term insurance coverages.

Learning outcomes
:
  1. Identify the future loss random variables associated with whole life, term life, and endowment insurance, and with term and whole life annuities, on single lives.
  2. Calculate premiums based on the equivalence principle, the portfolio percentile principle, and for a given expected present value of profit, for the policies in 11.1.
  3. Calculate and interpret gross premium, net premium and modified net premium policy values for the policies in 11.1.
  4. Calculate the effect of changes in underlying assumptions (e.g., mortality and interest).
  5. Apply the following methods for modelling extra risk: age rating; constant addition to the force of mortality, constant multiple of the rate of mortality.
