---
slug: part-2-further-comments-on-ofs-grade-inflation-report
title: Part 2, further comments on OfS grade-inflation report
categories:
- R
- Reproducible research
- UK parochial
- universities
---

* * *



**Update**, 2019-01-07: I am pleased to say that the online media article that I complained about in Sec 1 below has now been amended by its author(s), to correct the false attributions.  I am grateful to Chris Parr for helping to sort this out.

**Update**, 2021-09-09: Just to note that the "Part 3" never got written! As well as having too much else to do in 2019, I lost all confidence that any further work by me on this topic would actually influence anything.


* * *



In [my post a few days ago](/2019/01/02/office-for-students-report-on-grade-inflation/) (which I'll now call "Part 1") I looked at aspects of the statistical methods used in a report by the UK government's _Office for Students_, about "grade inflation" in English universities.  This second post continues on the same topic.

In this _Part 2_ I will do two things:

1. Set the record straight, in relation to some incorrect reporting of [Part 1](/2019/01/02/office-for-students-report-on-grade-inflation/) in the specialist media.
2. Suggest a new statistical method that (in my opinion) is better than the one used in the OfS report.


The more substantial stuff will be the second bullet there (and of course I wish I didn't need to do the first bullet at all).   In this post (at section 2 below) I will just _outline_ a better method, by using the same artificial example that I gave in [Part 1](/2019/01/02/office-for-students-report-on-grade-inflation/): hopefully that will be enough to give the general idea, to both specialist and non-specialist readers.  Later I will follow up (in my intended _Part 3_) with a more detailed description of the suggested better method; that _Part 3_ post will be suitable mainly for readers with more specialist background in Statistics.


## 1. For the record


I am aware of two places where the analysis I gave in [Part 1](/2019/01/02/office-for-students-report-on-grade-inflation/) has been reported:


* At [https://www.researchprofessional.com/0/rr/he/agencies/ofs/2019/OfS-grade-inflation-analysis-not-fit-for-purpose--says-expert.html](https://www.researchprofessional.com/0/rr/he/agencies/ofs/2019/OfS-grade-inflation-analysis-not-fit-for-purpose--says-expert.html), an article entitled "OfS grade inflation analysis not fit for purpose, says expert"
* At [https://www.researchresearch.com/news/article/?articleId=1379083](https://www.researchresearch.com/news/article/?articleId=1379083), which seems to be a straight copy of the same article (I have not checked in detail).


The first link there is to a paywalled site, I think. The second one appears to be in the public domain. I do not recommend following either of those links, though! If anyone reading this wants to know about what I wrote in _Part 1_, then my advice is just to read [Part 1](/2019/01/02/office-for-students-report-on-grade-inflation/) directly.

Here I want to mention three specific ways in which **that article misrepresents what I wrote in [Part 1](/2019/01/02/office-for-students-report-on-grade-inflation/)**. Points 2 and 3 here are the more important ones, I think (but #1 is also slightly troubling, to me):


1. The article refers to my blog post as **"a review commissioned by HE"**. The reality is that a journalist called Chris Parr had emailed me just before Christmas. In the email Chris introduced himself as "I'm a journalist at Research Fortnight", and the request he made in the email (in relation to the newly published OfS report) was "Would you or someone you know be interested in taking a look?". I had heard of _Research Fortnight_. And I was indeed interested in taking a look at the methods used in the OfS report. But until the above-mentioned article came to my attention, I had never even heard of a publication named _HE_. Possibly I am mistaken in this, but to my mind the phrase "a review commissioned by HE" indicates some kind of formal arrangement between _HE_ and me, with specified deliverables and perhaps even payment for the work. There was in fact no such "commission" for the work that I did. I merely spent some time during the Christmas break thinking about the methods used in the OfS report, and then I wrote a blog post (and told Chris Parr that I had done that). And let me repeat: I had never even heard of _HE_ (nor of the article's apparent author, which was not Chris Parr). No payment was offered or demanded. I mention all this here only in case anyone who has read that article got a wrong impression from it.
2. The article contains this false statement: **"The data is too complex for a reliable statistical method to be used, he said"**. The "he" there refers to me, David Firth. I said no such thing, neither in my blog post nor in any email correspondence with Chris Parr. Indeed, it is not something I ever _would_ say: the phrase "data...too complex for a reliable statistical method" is a nonsense.
3. The article contains this false statement: **"He calls the OfS analysis an example of Simpson's paradox"**. Again, the "he" in that statement refers to me. But I did not call the OfS analysis an example of Simpson's paradox, either in my blog post or anywhere else.  (And nor could I have, since I do not have access to the OfS dataset.) What I actually wrote in my blog post was that my own _artificial, specially-constructed example_ was an instance of Simpson's paradox --- which is not even close to the same thing!


The article mentioned above seems to have had an agenda that was very different from giving a faithful and informative account of my comments on the OfS report. I suppose that's journalistic license (although I would naively have expected better from a specialist publication to which my own university appears to subscribe). The false attribution of misleading statements is not something I can accept, though, and that is why I have written specifically about that here.

To be completely clear:

* **The article mentioned above is misleading. I do not recommend it to anyone.**
* **All of my posts in this blog are my own work, not commissioned by anyone.** In particular, none of what I'll continue to write below (and also in _Part 3_ of this extended blog post, when I get to that), about the OfS report, was requested by any journalist.



## 2. Towards a better (statistical) measurement model


I have to admit that in [Part 1](/2019/01/02/office-for-students-report-on-grade-inflation/) I ran out of steam at one point, specifically where --- in response to my own question about what would be a better way than the method used in the OfS report --- I wrote "_I do not have an answer_". I could have and should have done better than that.

Below I will outline a fairly simple approach that overcomes the specific pitfall I identified in _Part 1_, i.e., the fact that measurement at too high a level of aggregation can give misleading answers. I will demonstrate my suggested new approach through the same, contrived example that I used in _Part 1_. This should be enough to convey the basic idea, I hope. [Full generality for the analysis of real data will demand a more detailed and more technical treatment of a hierarchical statistical model; I'll do that later, when I come to write _Part 3_.]

On reflection, I think a lot of the criticism seen by the OfS report since its publication relates to the use of the word "explain" in that report. And indeed, that was a factor also in my own (mentioned above) "_I do not have an answer_" comment. It seems obvious --- to me, anyway --- that any serious attempt to _explain_ apparent increases in the awarding of First Class degrees would need to take account of a lot more than just the attributes of students when they enter university. With the data used in the OfS report I think the best that one can hope to do is to _measure_ those apparent increases (or decreases), in such a way that the measurement is a "fair" one that appropriately takes account of incoming student attributes and their fluctuation over time. If we take that attitude --- i.e, that **the aim is _only_ to measure things well**, not to explain them --- then I do think it is possible to devise a better statistical analysis, for that purpose, than the one that was used in the OfS report.

(I fully recognise that this actually _was_ the attitude taken in the OfS work! It is just unfortunate that the OfS report's use of the word "explain", which I think was intended there mainly as a technical word with its meaning defined by a statistical regression model, inevitably leads readers of the report to think more broadly about substantive _explanations_ for any apparent changes in degree-class distributions.)


### 2.1 Those "toy" data again, and a better statistical model


Recall the setup of the simple example from Part 1: **_Two academic years, two types of university, two types of student._** The data are as follows:

    
    2010-11
      University A           University B
        Firsts  Other          Firsts  Other
      h   1000      0        h    500    500 
      i      0   1000        i    500    500
    2016-17
      University A          University B
        Firsts  Other          Firsts  Other 
      h   1800    200       h       0      0
      i      0      0       i     500   1500
    


Our measurement (of change) should reflect the fact that, _for each type of student within each university_, where information is available, _the percentage awarded Firsts actually decreased_ (in this example).

    
    Change in percent awarded firsts:
      University A, student type h:  100% --> 90%
      University A, student type i:   no data
      University B, student type h:   no data
      University B, student type i:   50% --> 25%


This provides the key to specification of a suitable (statistical) measurement model:



	
  * measure the changes at the lowest level of aggregation possible;

	
  * then, if aggregate conclusions are wanted, combine the separate measurements in some sensible way.


In our simple example, "lowest level of aggregation possible" means that we should measure the change separately for each type of student within each university.  (In the _real_ OfS data, there's a lower level of aggregation that will be more appropriate, since different _degree courses_ within a university ought to be distinguished too --- they have different student intakes, different teaching, different exam boards, etc.)

In Statistics this kind of analysis is often called a _stratified_ analysis.  The quantity of interest (which here is the change in % awarded Firsts) is measured separately in several pre-specified _strata_, and those measurements are then combined if needed (either through a formal statistical model, or less formally by simple or weighted averaging).

In our simple example above, there are 4 strata (corresponding to 2 types of student within each of 2 universities).  In our specific dataset there is information about the change in just 2 of those strata, and we can summarize that information as follows:



	
  * in University A, student type _i_ saw their percentage of Firsts reduced by 10%;

	
  * in University B, student type _h_ saw their percentage of Firsts reduced by 50%.


That's all the information in the data, about changes in the rate at which Firsts are awarded.  (It was a deliberately small dataset!)

If a combined, "sector-wide" measure of change is wanted, then the separate, stratum-specific measures need to be combined somehow.  To some extent this is arbitrary, and the choice of a combination method ought to depend on the _purpose_ of such a sector-wide measure and (especially) on the _interpretation desired_ for it.  I might find time to write more about this later in _Part 3_.

For now, let me just recall what was the "sector-wide" measurement that resulted from analysis (shown in [Part 1](/2019/01/02/office-for-students-report-on-grade-inflation/)) of the above dataset using the OfS report's method.  The result obtained by that method was a sector-wide _increase_ of 7.5% in the rate at which Firsts are awarded --- which is plainly misleading in the face of data that shows substantial _decreases_ in both universities.  Whilst I do not much like the OfS Report's "compare with 2010" approach, it does have the benefit of transparency and in my "toy" example it is easy to apply to the stratified analysis:

    
    2016-17          Expected Firsts       Actual
                     based on 2010-11
      University A         2000             1800
      University B         1000              500
      ------------------------------------------
      Total                3000             2300


--- from which we could report a sector-wide decrease of 700/3000 = 23.3% in the awarding of Firsts, once student attributes are taken properly into account.  (This could be viewed as just a suitably weighted average of the 10% and 50% decreases seen in University A and University B respectively.)

As before, I have [made the full _R_ code available](https://gist.github.com/DavidFirth/d2a2a82684396a928f42823cb688f58d) (as an update to my earlier _R Markdown_ document).  For those who don't use _R_, I attach here also a PDF copy of that: [grade-inflation-example.pdf](/assets/media/2019/01/grade-inflation-example.pdf)


### 2.2  Generalising the better model: More strata, more time-points


The essential idea of a better measurement model is presented above in the context of a small "toy" example, but the real data are of course much bigger and more complex.

The key to generalising the model will simply be to recognise that it can be expressed in the form of a logistic regression model (that's the same _kind_ of model that was used in the OfS report; but the "better" logistic regression model structure is different, in that it needs to include a term that defines the strata within which measurement takes place).

This will be developed further in _Part 3_, which will be more technical in flavour than Parts 1 and 2 of this blog-post thread have been.  Just by way of a taster, let me show here the mathematical form of the logistic-regression representation of the "toy" data analysis shown above.  With notation



	
  * _u_ for providers (universities); _u_ is either _A_ or _B_ in the toy example

	
  * _t_ for type of student; _t_ is either _h_ or _i_ in the toy example

	
  * _y_ for years; _y_ is either 2010-11 or 2016-17 in the toy example

	
  * $$\pi_{uty}$$ for the probability of a First in year _y_, for students of type _t_ in university _u_


the logistic regression model corresponding to the analysis above is

$$\log\left(\pi_{uty}\over 1-\pi_{uty}\right) = \alpha_{ut} + \beta_{uy}$$.

This is readily generalized to situations involving more strata (more universities _u_ and student types _t_, and also degree-courses _within_ universities).  There were just 4 stratum parameters $$\alpha_{Ah},\alpha_{Ai}, \alpha_{Bh}, \alpha_{Bi}$$ in the above example, but more strata are easily accommodated.

The model is readily generalized also, in a similar way, to more than 2 years of data.

For comparison, the corresponding logistic regression model as used _in the OfS report_ looks like this:

$$\log\left(\pi_{uty}\over 1-\pi_{uty}\right) = \alpha_{t} + \beta_{uy}$$.

So it is superficially very similar.  But the all-important term $$\alpha_{ut}$$ that determines the necessary strata _within_ universities is missing from the OfS model.

I will aim to flesh this out a bit in a new _Part 3_ post within the next few days, if time permits.  For now I suppose the model I'm suggesting here needs a name (i.e., a name that identifies it more clearly than just "my better model"!)  Naming things is not my strong point, unfortunately!  But, for now at least, I will term the analysis introduced above "stratified by available student attributes" --- or "SASA model" for short.

(The key word there is "stratified".)



* * *



© David Firth, January 2019

**To cite this entry:**
Firth, D (2019). Part 2, further comments on OfS grade-inflation report. Weblog entry at URL 
[https://DavidFirth.github.io/blog/2019/01/07/part-2-further-comments-on-ofs-grade-inflation-report/](/2019/01/07/part-2-further-comments-on-ofs-grade-inflation-report/)
