## Chapter 2

2. Scientists are searching for a vaccine for a disease. You are given:
   1. 100,000 lives age $x$ are exposed to the disease
   2. Future lifetimes are independent, except that the vaccine, if available, will be given to all at the end of year 1
   3. The probability that the vaccine will be available is $0.2$
   4. For each life during year 1, $q _x = 0.02$
   5. For each life during year 2, $q _{x +1} = 0.01$ if the vaccine has been given, and $q _{x+1} = 0.02$ if it has not been given
   
   Calculate the standard deviation of the number of survivors at the end of year 2.

   - [ ] 100
   - [ ] 200
   - [ ] 300
   - [ ] 400
   - [ ] 500

<details><summary>Solution</summary>
Answer: 400.

This question requires the law of total variance

$$
  \mathrm{Var}[Y] = \mathrm{E}[\mathrm{Var}[X|Y]] + \mathrm{Var}[\mathrm{E}[X|Y]]
$$

Here, the vaccine availability rv is $Y \sim \mathrm{Bernoulli}(0.2)$, and the number of survivors rv is $X \sim \mathrm{Binomial}(100000, p)$, where $p = 0.98 \cdot 0.99$ if $Y = 1$ and $p = 0.98 ^2$ if $Y = 0$.

Hence,

| $Y$ | $p_y$ | $p_x$             | $\mathrm{E}[X\|Y] = 100000 \cdot p _x$ | $\mathrm{Var}[X\|Y] = 100000 \cdot p _x \cdot (1 - p _x)$ |
| --- | ----- | ----------------- | -------------------------------------- | --------------------------------------------------------- |
| $0$ | $0.8$ | $0.98 ^2$         | $96040$                                | $3803.184$                                                |
| $1$ | $0.2$ | $0.98 \cdot 0.99$ | $97020$                                | $2891.196$                                                |

And

$$
  \begin{aligned}
    \mathrm{E}[\mathrm{Var}[X|Y]] &= 0.8 \cdot 3803.184 + 0.2 \cdot 2891.196 = 3620.7864\\
    \mathrm{Var}[\mathrm{E}[X|Y]] &= 0.8 \cdot 96040^2 + 0.2 \cdot 97020 - (0.8 \cdot 96040 + 0.2 \cdot 97020) = 153664 \\
    \implies \mathrm{Var}[Y] &= 157284.7864 \\
    \sigma _Y &= 396.59
  \end{aligned}
$$
</details>

Remark: Law of total variance.

## Chapter 3

2. You are given
   1. The following extract from a mortality table with a one-year select period:
      | $x$ | $l _{[x]}$ | $d _{[x]}$ | $l _{x+1}$ | $x + 1$ |
      | :-: | :--------: | :--------: | :--------: | :-----: |
      | 65  |    1000    |     40     |     -      |   66    |
      | 66  |    955     |     45     |     -      |   67    |
   2. Deaths are uniformly distributed over each year of age.
   
   $\mathring e _{[65]} = 15.0$

   Calculate $\mathring e _{[66]}$.

   - [ ] 14.1
   - [ ] 14.3
   - [ ] 14.5
   - [ ] 14.7
   - [ ] 14.9



<details><summary>Solution</summary>
Answer: 13.7

Remember that under UUD, the complete expectation of life is calculated as

$$
  \mathring e _{[x]} = \sum _{k = 1} ^\infty \int _0 ^1 {}_k p _{[x]} dt = \sum _{k = 1} ^\infty {} _{k-1} p _{[x]} \cdot \int _0 ^1  p _{[x] + k - 1} dt = \sum _{k = 0} ^\infty {} _{k} p _{[x]} \cdot \left(1 - \frac{1}{2} \cdot  q _{[x] + k}\right).
$$

Hence,
$$
  \begin{aligned}
    \mathring e _{[65]} &= \left(1 - \frac{1}{2} \cdot  q _{[65]}\right) + p _{[65]} \cdot \left(1 - \frac{1}{2} \cdot  q _{66}\right) + {} _2 p _{[65]} \cdot \mathring e _{67} \\
    \implies {} _2 p _{[65]} \cdot \mathring e _{[67]} &= 15 - \left(1 -\frac{1}{2} \cdot \frac{40}{1000} \right) - \frac{960}{1000} \cdot \left(1 - \frac{1}{2} \cdot \frac{960 - 910}{960}\right)
    = 14.37912 \\
    \implies \mathring e _{[67]} &= \frac{13.085}{p _{[65]} \cdot p _{66}} = 13.37912 \\
    \mathring e _{[66]} &= \left(1 - \frac{1}{2} \cdot  q _{[66]}\right) + p _{[66]} \cdot \mathring e _{67} \\
    &= \left( 1- \frac{1}{2}\cdot \frac{45}{955} \right) + \frac{910}{955} \cdot 14.37912 = 14.678
    
  \end{aligned}
$$
</details>

Remark: complete expectation of life under UUD, select life table.

## Chapter 6

7. For a special fully discrete 20-year endowment insurance on (40), you are given:
   1. The only death benefit is the return of annual net premiums accumulated with interest at 5% to the end of the year of death
   2. The endowment benefit is 100,000
   3. Mortality follows the Standard Ultimate Life Table
   4. $i = 0.05$
   
   Calculate the annual net premium.

   - [ ] 2680
   - [ ] 2780
   - [ ] 2880
   - [ ] 2980
   - [ ] 3080

<details><summary>Solution</summary>

Answer: 2880

There are 2 efficient ways to think about this question.

1. For those who dies within 20 years, their accumulated premiums are exactly the same as their death benefits, regardless what the annual net premium is. Hence, the premiums should be set based on the pure endowment of $100,000.
   
   $$
     P \cdot \ddot a_{\overline{20 |}} = 100000 \cdot v ^{20}
   $$
   
   Note that $\ddot a_{\overline{20 |}} = \frac{1 - v^{20}}{1 - v}$ and thus $P = 2880.25$.

2. Alternatively, note if we pay any death benefit at year $x +t$, its present value is the same as the annuity of $P$ of $t$ terms. However, there is no such present value if the policyholder survive 20 years. Hence, the EPV of death benefit, if paid, is $P \cdot (\ddot a _{40:\overline{20|}} - {} _ {20} p _{40}\cdot \ddot a _{\overline {20}|})$. If the policyholder survives 20 years, then EPV of benefit is just the pure endowment $100000 \cdot {} _{20} E _{40}$. We then can set up an equation
   
   $$
     P \cdot \ddot a_{40:\overline{20 |}} = 100000 \cdot v ^{20} + P \cdot (\ddot a _{40:\overline{20|}} - {} _ {20} p _{40}\cdot \ddot a _{\overline {20}|})
   $$

   which should give the same result as method 1.
</details>

## Chapter 7

6. For a fully discrete whole life insurance policy of 2000 on (45), you are given:
   
   1. The gross premium is calculated using the equivalence principle
   2. Expenses, payable at the beginning of the year, are:

      |               | % of Premium | Per 1000 | Per Policy |
      | ------------: | :----------: | :------: | :--------: |
      |    First year |     25%      |   1.5    |     30     |
      | Renewal years |      5%      |   0.5    |     10     |
    
   3. Mortality follows the Standard Ultimate Life Table
   4. i = 0.05

   Calculate the expense policy value at the end of policy year 10.

   - [ ] -2
   - [ ] -8
   - [ ] -12
   - [ ] -21
   - [ ] -25

<details><summary>Solution</summary>

Answer: -25

While here $V ^ e$ can be calculated using $V^g - V^n$ (gross policy value minus net policy value), to it can be calculated by using the EPV of future expenses minus the EPV of the expense premium, there is a much better shortcut.

Notice that the expense premium consists of 2 parts: the part covers the renewal expenses, and the part that amortizes the initial expenses. When calculating the expense policy value, the first part will cancel out with the renewal expenses perfectly and the only thing left is the EPV of the second part.

Under the context of this question, the first-year, non-renewal expense is $0.2G + 11$, which will be amortized to $(0.2G + 11)\div\ddot a_{45}$ and hence the expense policy value at the end of policy year 10 is $-(0.2G + 11)\div\ddot a_{45} \times \ddot a_{55}$.

We then only need to calculate the gross premium $G$:

$$
  G = \frac{2000 A _{45} + 11 \ddot a _{45} + 22}{0.95\ddot a_{45} - 0.2} = 31.16.
$$

Then, the answer is

$$
  -(0.2G + 22) \cdot \frac{\ddot a _{55}}{\ddot a _{45}} = -25.
$$

</details>

11. For a fully discrete whole life insurance of 10,000 on (45), you are given:
    
    1. $i = 0.05$
    2. ${} _ 0 L$ denotes the loss at issue random variable based on the net premium
    3. If $K_{45} =10$, then ${} _0 L = 4450$
    4. $\ddot a _{55} = 13.4205$

    Calculate ${} _{10} V$, the net premium policy value at the end of year 10 for this insurance.

    - [ ] 1010
    - [ ] 1460
    - [ ] 1820
    - [ ] 2140
    - [ ] 2300

<details><summary>Solution</summary>

Answer: 1460

One of the missing piece is the net premium, and that is also the tricky part (at least for me). To calculate that, we can use fact #3: 4450 is the present value of the death benefit paid in time 11 (**tricky!** it is not 10 because the curtate lifetime is 10 so that benefit paid at 11) and the present value of all 11 (**tricky! not 10**) premium payments. Hence,

$$
  \begin{aligned}
    4450 &= 10000 v^{11} - P\cdot \frac{1 - v ^{11}}{1 - v}  \\
    P &= 160.15
  \end{aligned}
$$

The answer is simple afterward

$$
  {} _{10} V = 10000 A _{55} - P \ddot a _{55} = 10000 (1- d\ddot a _{55}) - 160.15\ddot a _{55} = 1460
$$

</details>

