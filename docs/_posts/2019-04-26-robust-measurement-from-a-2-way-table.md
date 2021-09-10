---
slug: robust-measurement-from-a-2-way-table
title: Robust measurement from a 2-way table
categories:
- R
- universities
---

I work in a university. My department runs degree courses that allow students a lot of flexibility in their choice of course "modules". (A typical student takes 8-10 modules per year, and is assessed separately on each module).

After the exams are finished each year, we promise our students to look carefully at the exam marks for each module --- to ensure that students taking a "hard" module are not penalized for doing that, and that students taking an "easy" module are not unduly advantaged.

The challenge in this is to separate module difficulty from student ability: we need to be able to tell the difference between (for example) a hard module and a module that was chosen by weaker-than-average students.  This necessitates analysis of the exam marks for _all modules together_, rather than separately.

The data to be analysed are each student's score (expressed as a percentage) in each module they took.  It is convenient to arrange those scores in a 2-way table, whose rows are indexed by student IDs, and whose columns correspond to all the different possible modules that were taken.  The task is then to analyse the (typically incomplete) 2-way table, to determine a numerical "module effect" for each module (a relatively high number for each module that was found relatively "easy", and lower numbers for modules that were relatively "hard".

A standard method for doing this robustly (i.e., in such a way that the analysis is not influenced too strongly by the performance of a small number of students) is the clever _[median polish](https://en.wikipedia.org/wiki/Median_polish)_ method due to J W Tukey. My university department has been using median polish now for several years, to identify any strong "module effects" that ought to be taken into account when assessing each student's overall performance in their degree course.

Median polish works mostly OK, it seems: it gives answers that broadly make sense.  But there are some well known problems, including that _it matters which way round_ the table is presented (i.e., "rows are students", _versus_ "rows are modules") --- the answer will depend on that.  So median polish is actually not just one method, but two.

When my university department asked me recently to implement its annual median-polish exercise in _R_, I could not resist thinking a bit about whether there might be something even better than median polish, for this specific purpose of identifying the column effects (module effects) robustly.  This led me to look at some simple "toy" examples, to help understand the principles.  I'll just show one such example here, to illustrate how it's possible to do better than median polish in this particular context.



## Example: 5 modules, 3 students

My made-up "toy" data:

     > x
            module
     student  A  B  C  D  E
           i NA NA NA 45 60
           j NA NA NA 55 60
           k 10 20 30 NA 50

There were five modules (labelled _A,B,C,D,E_).  Students _i, j_ and _k_ each took a selection of those modules.  It's a small dataset, but that is deliberate: we can see easily what's going on in a table this small.  Module _E_ was easier than the others, for example; and student _k_ looks to be the weakest student (since _k_ was outperformed by the other two students in module _E_, the only one that they _all_ took).

I will call the above table _perfect_, as far as the measurement of module effects is concerned. If we assign module effects (−20, −10, 0, 10, 20) to the five modules _A,B,C,D,E_ respectively, then for _every_ pair of modules the observed within-student differences are centered upon the relevant difference in those module effects. For example, look at modules _D_ and _E_: student _i_ scores 15 points more in _E_, while _j_ scores 5 points more in _E_, and the median of those two differences is 10 --- the same as the difference between the proposed "perfect" module effects for _D_ and _E_.

When we perform _median polish_ on this table, we get different answers depending on whether we apply the method to the table directly, or to its transpose:

     > medpolish(x, na.rm = TRUE, maxiter = 20)
     ...
     Median Polish Results (Dataset: "x")
     
     Overall: 38.75
     
     Row Effects:
         i     j     k 
      0.00  5.00 -8.75 
     
     Column Effects:
          A      B      C      D      E 
     -20.00 -10.00   0.00   8.75  20.00 
     
     Residuals:
            module
     student  A  B  C    D     E
           i NA NA NA -2.5  1.25
           j NA NA NA  2.5 -3.75
           k  0  0  0   NA  0.00
     
     > medpolish(t(x), na.rm = TRUE, maxiter = 20)
     ...
     Median Polish Results (Dataset: "t(x)") 
     
     Overall: 36.25
     
     Row Effects:
          A      B      C      D      E 
     -20.00 -10.00   0.00  11.25  20.00 
     
     Column Effects:
          i      j      k 
      0.625  5.625 -6.250 
     
     Residuals:
           student
     module      i      j  k
          A     NA     NA  0
          B     NA     NA  0
          C     NA     NA  0
          D -3.125  1.875 NA
          E  3.125 -1.875  0

Neither of those answers is the same as the "perfect" module-effect measurement that was mentioned above.  The module effect for _D_ as computed by median polish is either 8.75 or 11.25, depending on the orientation of the input table --- but not the "perfect 10".



## A better method: Median difference analysis



I decided to implement, in place of median polish, a simple non-iterative method that targets directly the notion of "perfect" measurement that is mentioned above.

The method is in two stages.

**Stage 1** computes within-student differences and takes the median of those, for each possible module pair.  For our toy example:

     > md <- meddiff(x)
        A   B   C  D   E
     A NA -10 -20 NA -40
     B  1  NA -10 NA -30
     C  1   1  NA NA -20
     D  0   0   0 NA -10
     E  1   1   1  2  NA

The result here has all of the available median-difference values above the diagonal.  Below the diagonal is the count of how many differences were used in computing each one of those medians.  So, for example, the median difference between modules  _D_ and _E_ is −10; and that was computed from 2 students' exam scores.

**Stage 2** then fits a linear model to the median-difference values, using weighted least squares.  The linear model finds the vector of module effects that most closely approximates the available median differences (i.e., best approximates the numbers above the diagonal).  The weights are simply the counts from the lower triangle of the above matrix.

In this "perfect" example, we achieve the desired perfect answer (which here is presented with _E_ as the "reference" module):

     > fit(md)$coefficients
       A   B   C   D   E 
     -40 -30 -20 -10   0

My plan now is to make these simple _R_ functions robust enough to use for our students' _actual_ exam marks, and to add also _inference_ on the module-effect values (via a suitably designed _bootstrap_ calculation).

For now, here are my prototype functions in case anyone else wants to play with them:


    
    meddiff <- function(xmat) {
        ## rows are students, columns are modules
        S <- nrow(xmat)
        M <- ncol(xmat)
        result <- matrix(NA, M, M)
        rownames(result) <- colnames(result) <- colnames(xmat)
        for (m in 1:(M-1)) {
            for (mm in (m+1):M) {
                diffs <- xmat[, m] - xmat[, mm]
                ## upper triangle
                result[m, mm] <- median(diffs, na.rm = TRUE)
                ## lower triangle
                result[mm, m] <- sum(!is.na(diffs))
            }
        }
        return(result)
    }
    
    fit <- function(m) {
        ## matrix m needs to be fully connected above the diagonal
        upper <- upper.tri(m)
        diffs <- m[upper]
        weights <- t(m)[upper]
        rows <- factor(row(m)[upper])
        cols <- factor(col(m)[upper])
        X <- cbind(model.matrix(~ rows - 1), 0) - 
               cbind(0, model.matrix(~ cols - 1))
        colnames(X) <- colnames(m)
        rownames(X) <- paste0(colnames(m)[rows], "-", colnames(m)[cols])
        result <- lm.wfit(X, diffs, weights)
        result$coefficients[is.na(result$coefficients)] <- 0
        class(result) <- c("meddiff_fit", "list")
        return(result)
    }
    





* * *



© David Firth, April 2019

**To cite this entry:**
Firth, D (2019). Robust measurement from a 2-way table. Weblog entry at URL [https://DavidFirth.github.io/blog/2019/04/26/robust-measurement-from-a-2-way-table/](/2019/04/26/robust-measurement-from-a-2-way-table/)
