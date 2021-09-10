---
slug: simple-maths-of-a-fairer-uss-deal
title: Simple maths of a fairer USS deal
categories:
- R
- Reproducible research
- UK parochial
- USS
---

* * *



In [yesterday's post](/2018/03/15/uss-proposals-tail-wagging-the-dog/) I showed a graph, followed by some comments to suggest that future USS proposals with a flatter (or even increasing) "percent lost" curve would be fairer (and, as I argued earlier in my [Robin Hood post](/2018/03/01/future-uss-robin-hood-can-help/), more affordable at the same time).

It's now clear to me that my suggestion seemed a bit cryptic to many (maybe most!) who read it yesterday.  So here I will try to show more specifically how to achieve a _flat_ curve.  (This is not because I think flat is optimal.  It's mainly because it's easy to explain.  As already mentioned, it might not be a bad idea if the curve was actually to _increase_ a bit as salary levels increase; that would allow those with higher salaries to feel happy that they are doing their bit towards the sustainable future of USS.)


## Flattening the curve


The graph below is the same as yesterday's but with a flat (blue, dashed) line drawn at the level of 4% lost across all salary levels.

![lost-with-4pc-line](/assets/media/2018/03/lost-with-4pc-line.png)

I drew the line at 4% here just as an example, to illustrate the calculation.  The _actual_ level needed --- i.e, the "affordable" level for universities ---  would need to be determined by negotiation; but the maths is essentially the same, whatever the level (within reason).

Let's suppose we want to adjust the USS contribution and benefits parameters to achieve just such a flat "percent lost" curve, at the 4% level.  How is that done?

I will assume here the same _adjustable parameters_ that UUK and UCU appear to have in mind, namely:


  * **employee contribution rate** _E_ (as percentage of salary --- currently 8; was 8.7 in the 12 March proposal; was 8 in the January proposal)
  * **threshold salary** _T_, over which defined benefit (DB) pension entitlement ceases (which is currently £55.55k; was £42k in the 12 March proposal; and was £0 in the January proposal)
  * **accrual rate** _A_, in the DB pension.  Expressed here in percentage points (currently 100/75; was 100/85 in the 12 March proposal; and not relevant to the January proposal).
  * **employer contribution rate (%) to the defined contribution (DC) part** of USS pension.  Let's allow different rates $$C_1$$ and $$C_2$$ for, respectively, salaries between _T_ and £55.55k, and salaries over £55.55k. (Currently $$C_1$$ is irrelevant, and $$C_2$$ is 13 (max); these were both set at 12 in the 12th March proposal; and were both 13.25 in the January proposal.)


I will assume also, as all the recent proposals do, that the 1% USS match possibility is lost to all members.

Then, to get to 4% lost across the board, we need simply to solve the following linear equations.  (To see where these came from, please see [this earlier post](/2018/03/13/latest-uss-proposal-who-would-lose-most/).)

For **salary up to _T_**:


$$ (E - 8) + 19(100/75 - A) + 1] = 4. $$


For **salary between _T_ and £55.55k**:


$$  -8 + 19(100/75) - C_1 + 1 = 4. $$


For **salary over £55.55k**:


$$ 13 - C_2 = 4. $$


Solving those last two equations is simple, and results in


$$ C_1 = 14.33, \qquad C_2 = 9. $$


The first equation above clearly allows more freedom: it's just one equation, with two unknowns, so there are many solutions available.  Three _example_ solutions, still based the illustrative 4% loss level across all salary levels, are:


$$ E=8, \qquad A = 1.175 = 100/85.1 $$




$$ E = 8.7, \qquad A = 1.21 = 100/82.6 $$




$$ E = 11, \qquad A = 100/75. $$


At the end here I'll give code in _R_ to do the above calculation quite generally, i.e., for any desired percentage loss level.  First let me just make a few remarks relating to all this.


## Remarks




### **Choice of threshold**


Note that the value of _T_ does not enter into the above calculation.  Clearly there will be (negotiable) interplay between _T_ and the required percentage loss, though, for a given level of affordability.


### Choice of $$C_2$$


Much depends on the value of $$C_2$$.

The calculation above gives the value of $$C_2$$ needed for a _flat_ "percent lost" curve, at any given level for the percent lost (which was 4% in the example above).

To achieve an _increasing_ "percent lost" curve, we could simply reduce the value of $$C_2$$ further than the answer given by the above calculation.  Alternatively, as suggested in my earlier Robin Hood post, USS could apply a lower value of $$C_2$$ only for salaries above some _higher_ threshold --- i.e., in much the same spirit as progressive taxation of income.

Just as with income tax, it would be important not to set $$C_2$$ _too_ small, otherwise the highest-paid members would quite likely want to leave USS.  There is clearly a delicate balance to be struck, at the top end of the salary spectrum.

But it is clear that if the higher-paid were to sacrifice at least as much as everyone else, in proportion to their salary, then that would allow the overall level of "percent lost" to be appreciably reduced, which would benefit the vast majority of USS members.


### Determination of the overall "percent lost"


Everything written here constitutes a _methodology _to help with finding a good solution.  As mentioned at the top here, the _actual_ solution --- and in particular, the _actual_ level of USS member pain (if any) deemed to be necessary to keep USS afloat --- will be a matter for negotiation.  The maths here can help inform that negotiation, though.


## Code for solving the above equations





* * *




    
    ## Function to compute the USS parameters needed for a
    ## flat "percent lost" curve
    ##
    ## Function arguments are:
    ## loss: in percentage points, the constant loss desired
    ## E: employee contribution, in percentage points
    ## A: the DB accrual rate
    ##
    ## Exactly one of E and A must be specified (ie, not NULL).
    ##
    ## Example calls:
    ## flatcurve(4.0, A = 100/75)
    ## flatcurve(2.0, E = 10.5)
    ## flatcurve(1.0, A = 100/75)  # status quo, just 1% "match" lost
    
    flatcurve <- function(loss, E = NULL, A = NULL){
    
        if (is.null(E) && is.null(A)) {
            stop("E and A can't both be NULL")}
        if (!is.null(E) && !is.null(A)) {
            stop("one of {E, A} must be NULL")}
    
        c1 <- 19 * (100/75) - (7 + loss)
        c2 <- 13 - loss
    
        if (is.null(E)) {
            E <- 7 + loss - (19 * (100/75 - A))
        }
    
        if (is.null(A)) {
            A <- (E - 7 - loss + (19 * 100/75)) / 19
        }
    
    return(list(loss_percent = loss,
                employee_contribution_percent = E,
                accrual_reciprocal = 100/A,
                DC_employer_rate_below_55.55k = c1,
                DC_employer_rate_above_55.55k = c2))
    }





* * *



The above function will run in base _R_.

Here are three examples of its use (copied from an interactive session in _R_):



* * *




    
    ###  Specify 4% loss level, 
    ###  still using the current USS DB accrual rate
    
    > flatcurve(4.0, A = 100/75)
    $loss_percent
    [1] 4
    
    $employee_contribution_percent
    [1] 11
    
    $accrual_reciprocal
    [1] 75
    
    $DC_employer_rate_below_55.55k
    [1] 14.33333
    
    $DC_employer_rate_above_55.55k
    [1] 9
    
    #------------------------------------------------------------
    ###  This time for a smaller (2%) loss, 
    ###  with specified employee contribution
    
    > flatcurve(2.0, E = 10.5)
    $loss_percent
    [1] 2
    
    $employee_contribution_percent
    [1] 10.5
    
    $accrual_reciprocal
    [1] 70.80745
    
    $DC_employer_rate_below_55.55k
    [1] 16.33333
    
    $DC_employer_rate_above_55.55k
    [1] 11
    
    #------------------------------------------------------------
    ### Finally, my personal favourite:
    ### --- status quo with just the "match" lost
    
    > flatcurve(1, A = 100/75)
    $loss_percent
    [1] 1
    
    $employee_contribution_percent
    [1] 8
    
    $accrual_reciprocal
    [1] 75
    
    $DC_employer_rate_below_55.55k
    [1] 17.33333
    
    $DC_employer_rate_above_55.55k
    [1] 12





* * *



© David Firth, March 2018

**To cite this entry:**
Firth, D (2018). Simple maths of a fairer USS deal. Weblog entry at URL [https://DavidFirth.github.io/blog/2018/03/16/simple-maths-of-a-fairer-uss-deal/](/2018/03/16/simple-maths-of-a-fairer-uss-deal/)
