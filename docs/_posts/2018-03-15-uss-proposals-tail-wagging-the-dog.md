---
slug: uss-proposals-tail-wagging-the-dog
title: 'USS proposals: Tail wagging the dog?'
categories:
- R
- Reproducible research
- UK parochial
- USS
---

**Update** on 16 March: There's now a follow-up post to this one, which gives more detail on how (mathematically) to achieve a fairer sharing-out of _whatever_ level of USS member pain might ultimately be deemed necessary.  See [Simple maths of a fairer USS deal](/2018/03/16/simple-maths-of-a-fairer-uss-deal/) (but ideally only _after_ reading the necessary background, below!).




* * *



In response to my previous post, "[Latest USS proposal: Who would lose most?](/2018/03/13/latest-uss-proposal-who-would-lose-most/)", someone asked me about doing the same calculation for the USS JNC-supported proposals from January.  For a summary of those January proposals and my comments about their fairness, please see my earlier post "[USS pension scheme and fairness](/2018/02/26/uss-pension-scheme-and-fairness/)".

Anyway, the calculation is quite simple, and it led to the following graph.  The black curve is as in my previous post, and the red one is from the same calculation done for the January USS proposal.

![lost-comparison](/assets/media/2018/03/lost-comparison.png)The red curve shows just over 5% effective loss of salary for those below the current £55.55k USS threshold, and then a fairly sharp decline to less than 2% lost at the salaries of the very highest-paid professors, managers and administrators.  Under the January proposals, higher-paid staff would contribute proportionately less to the "rescue package" for USS --- less, even, than under the March proposals.  (And if the salary axis were to be extended indefinitely, the **red curve would actually cross the zero-line**: that's because in the January proposals the defined-contribution rate from employers would actually have _increased_ from (max) 13% to 13.25%.)

In terms of unequal sharing of the "pain", then, the January proposal was even worse than the March one.

At the bottom here I'll give the _R_ code and a few words of explanation for the calculation of the red curve above.

But the main topic of this post arises from **a remarkable feature of the above graph!** At the current USS threshold salary of £55.55k, the amount lost is **the same --- it's 5.08% under both proposals**.  Which led me to wonder: is that a _coincidence_, or was it actually a (pretty weird!) _constraint_ used in the recent UUK-UCU negotiations?  And then to wonder: might the best solution (i.e., for the same cost) be to do _something that gives a better graph than **either** of the two proposals seen so far_?


## Tail wagging the dog?


The fact that the loss under the March proposal tops out at 5.08%, exactly (to 2 decimals, anyway) the same as in the January proposal, seems unlikely to be a coincidence?

If it's _not_ a coincidence, then a plausible route to the March proposal, at the UUK-UCU negotiating table, could have been along the lines of:


> How can we re-work the January proposal to
>   * retain defined benefit, up to some (presumably reduced) threshold and with some (presumably reduced) accrual rate,
>
> while at the same time
>
>   * nobody loses more than the maximum 5.08% that's in the January proposal
>
>   * the employer contribution rate to the DC pots of high earners is not reduced below the current standard (i.e., without the "match") level of 12%
>
> ?


Those constraints, coupled with total cost to employers, would lead naturally to a family of solutions indexed by just _two adjustable constants_, namely



	
  * the threshold salary up to which DB pension applies (previously £55.55k)

	
  * the DB accrual rate (previously 1/75)


--- and it seems plausible that the suggested (12 March 2018) new threshold of £42k and accrual rate of 1/85 were simply selected as the preferred candidate (among many such potential solutions) to offer to UUK and UCU members.


### But the curve ought to be flat, or even increasing!


The two constraints listed as second and third bullets in the above essentially **fix the position of the part of the black curve that applies to salaries over £55.55k**.  That's what I mean by "tail wagging the dog".  Those constraints inevitably result in a solution that implies substantial losses for those with low or moderate incomes.

Once this is recognised, it becomes natural to ask: what **should** the shape of that "percentage loss" curve be?

The answer is surely a matter of opinion.

Those wishing to preserve substantial pension contributions at high salary levels, at the expense of those at lower salary levels, would want a curve that decreases to the right --- as seen in the above curves for the January and March proposals.

For myself, I would argue the opposite: **The "percent lost" curve should either be roughly constant, or might reasonably even _increase_ as salary increases**.  (The obvious parallel being progressive rates of income tax: those who can afford to pay more, pay more.)

I had made a specific suggestion along these lines, in this earlier post:



	
  * [Future USS: Robin Hood can help?](/2018/03/01/future-uss-robin-hood-can-help/)


The details of any solution that satisfies the "**percent loss roughly constant, or even increasing**" requirement clearly would need to depend on data that's not so widely available (mainly, the distribution of all salaries for USS members).

But first the **principle** of fairness needs to be recognised.  And once that is accepted, the constraints underlying future UUK-UCU negotiations would need to change radically --- i.e., definitely away from those last two bullets in the above display.


## Calculation of the red curve


In the previous post I gave R code for the black curve.  Here is the corresponding calculation behind the red curve:

    
    sacrifice.Jan <- function(salary) { # salary in thousands
        old_threshold <- 55.55
        s <- salary
    
    ## sacrifice arising from income up to old_threshold
        s2 <- min(s, old_threshold)
        r2 <- s2 * (19/75 + 1/100 - (13.25 + 8)/100)
    
    ## sacrifice (max) arising from income over the old threshold
    ## -- note that this is negative
        r3 <- (s > old_threshold) * (s - old_threshold) * 
                    (13 - 13.25)/100
    
        return(r2 + r3)
    }
    
    ## A vector of salary values up to £150k
    salaries <- (1:1500) / 10
    
    ## Compute percent of salary that would be lost, 
    ## at each salary level
    sacrifices <- 100 * sapply(salaries, sacrifice.Jan) / salaries


In essence:

* salary under £55.55k would lose the defined benefit (that's the 19/75 part) and the 1% "match", and in its place would get 21.25% as defined contribution.  The sum of these parts is the computed loss _r2_.
* salary over £55.55k would _gain_ the difference between potential 13% employer contribution and the proposed new rate of 13.25% (that's the negative value _r3_ in the code).





* * *



© David Firth, March 2018

**To cite this entry:**
Firth, D (2018). USS proposals: Tail wagging the dog? Weblog entry at URL [https://DavidFirth.github.io/blog/2018/03/15/uss-proposals-tail-wagging-the-dog/](/2018/03/15/uss-proposals-tail-wagging-the-dog/)


