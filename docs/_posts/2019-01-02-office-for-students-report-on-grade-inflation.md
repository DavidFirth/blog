---
slug: office-for-students-report-on-grade-inflation
title: Office for Students report on "grade inflation"
categories:
- R
- Reproducible research
- UK parochial
- universities
---

* * *

Chris Parr, a journalist for [_Research Professional_](https://www.researchprofessional.com), asked me to look at a recent report, [Analysis of degree classifications over time: Changes in graduate attainment](https://www.officeforstudents.org.uk/publications/analysis-of-degree-classifications-over-time-changes-in-graduate-attainment/).  The report was published by the UK government's _Office for Students_ (OfS) on 19 December 2018, along with a headline-grabbing [press release](https://www.officeforstudents.org.uk/news-blog-and-events/press-and-media/universities-must-get-to-grips-with-spiralling-grade-inflation/):

> ![ofs-screenshot](../assets/media/2019/01/ofs-screenshot-e1546435828658.png?w=600)

The report uses a statistical method --- the widely used method of _logistic regression_ --- to devise a yardstick by which each English university (and indeed the English university sector as a whole) is to be measured, in terms of their tendency to award the top degree classes (_First Class_ and _Upper Second Class_ honours degrees).  The OfS report looks specifically at the extent to which apparent "grade inflation" in recent years can be explained by changes in student-attribute data available to OfS (which include grades in pre-university qualifications, and also some other characteristics such as gender and ethnicity).

I write here as an experienced academic, who has worked at the University of Warwick (in England) for the last 15 years.  At the end, below, I will briefly express some _opinions_ based upon that general experience (and it should be noted that _everything_ I write here is my own --- definitely not an official view from the University of Warwick!)

My specific expertise, though, is in _statistical methods_, and this post will focus mainly on that aspect of the OfS report.  (For a more wide-ranging critique, see for example https://wonkhe.com/blogs/policy-watch-ofs-report-on-grade-inflation/)

Parts of what I say below will get a bit technical, but I will aim to write first in a non-technical way about the big issue here, which is just how _difficult_ it is to devise a meaningful measurement of "grade inflation" from available data.  My impression is that, unfortunately, the OfS report has either not recognised the difficulty or has chosen to neglect it.  In my view the methods used in the report are not actually fit for their intended purpose.


## 1.  Analysis of an idealized dataset


In much the same way as when I give a lecture, I will aim here to expose the key issue through a relatively simple, concocted example.  The _real_ data from all universities over several years are of course quite complex; but the essence can be captured in a much smaller set of idealized data, the advantage of which is that it allows a crucial difficulty to be seen quite directly.


### An imagined setup: Two academic years, two types of university, two types of student


Suppose (purely for simplicity) that there are just two identifiable types of university (or, if you prefer, just two distinct universities) --- let's call them _A_ and _B_.

Suppose also (purely for simplicity) that all of the measurable characteristics of students can be encapsulated in a single binary indicator: every student is known to be either of type _h_ or of type _i_, say.  (Maybe _h_ for _hardworking_ and _i_ for _idle_?)

Now let's imagine the data from two academic years --- say the years 2010-11 and 2016-17 as in the OfS report --- on the numbers of _First Class_ and _Other_ graduates.

The **2010-11 data** looks like this, say:

    
      University A           University B
        Firsts  Other          Firsts  Other
      h   1000      0        h    500    500 
      i      0   1000        i    500    500


The two universities have identical intakes in 2010-11 (equal numbers of type _h_ and type _i_ students).  Students of type _h_ do a lot better at University _A_ than do students of type _i_; whereas University _B_ awards a _First_ equally often to the two types of student.

Now let's suppose that, in the years that follow 2010-11,



	
  * students (who all know which type they are) learn to target the "right" university for themselves

	
  * both universities _A_ and _B_ tighten their final degree criteria, so as to make it harder (for both student types _h_ and _i_) to achieve a _First._


As a result of those behavioural changes, the **2016-17 data** might look like this:

    
      University A          University B
        Firsts  Other          Firsts Other 
      h   1800    200       h       0     0
      i      0      0       i     500  1500


Now we can **combine the data from the two universities**, so as to look at how degree classes across the whole university sector have changed over time:

    
      Combined data from both universities:
        2010-11                  2016-17
              Firsts  Other            Firsts  Other
            h   1500    500          h   1800    200
            i    500   1500          i    500   1500
              -------------            -------------
        Total   2000   2000      Total   2300   1700
            %     50     50              57.5   42.5




### The conclusion (not!)


The last table shown above would be interpreted, according to the methodology of the OfS report, as showing **an unexplained increase of 7.5 percentage points in the awarding of first-class degrees**.

(It is 7.5 percentage points because that's the difference between _50% Firsts_ in 2010-11 and _57.5% Firsts_ in 2016-17.  And it is _unexplained_ --- in the OfS report's terminology --- because the composition of the student body was unchanged, with 50% of each type _h_ and _i_ in both years.)

**But such a conclusion would be completely misleading.** In this constructed example, both universities actually made it _harder_ for every type of student to get a First in 2016-17 than in 2010-11.


### The real conclusion


The constructed example used above should be enough to demonstrate that **the method developed in the OfS report does not necessarily measure what it intends to**.

The constructed example was deliberately made both simple and quite extreme, in order to make the point as clearly as possible.  The real data are of course more complex, and patterns such as shifts in the behaviour of students and/or institutions will usually be less severe (and will _always_ be less obvious) than they were in my constructed example.  The point of the constructed example is merely to demonstrate that any conclusions drawn from this kind of combined analysis of all universities will be unreliable, and such conclusions will often be incorrect (sometimes severely so).


### That false conclusion is just an instance of [_Simpson's Paradox_](https://en.wikipedia.org/wiki/Simpson%27s_paradox), right?


Yes.

The phenomenon of analysing aggregate data to obtain (usually incorrect) conclusions about disaggregated behaviour is often (in Statistics) called _ecological inference_ or the _ecological fallacy_.  In extreme cases, even the _direction_ of effects can be apparently reversed (as in the example above) --- and in such cases the word "paradox" does seem merited.


### Logistic regression


The simple example above was (deliberately) easy enough to understand without any fancy statistical methods.  For more complex settings, especially when there are several "explanatory" variables to take into account, the method of logistic regression is a natural tool to choose (as indeed the authors of the OfS report did).

It might be thought that a relatively sophisticated tool such as logistic regression can solve the problem that was highlighted above.  But that is not the case.  The method of logistic regression, with its results aggregated as described in the OfS report, merely yields the same (incorrect) conclusions in the artificial example above.

For anyone reading this who wants to see the details: [here is the full code in R, with some bits of commentary](https://gist.github.com/DavidFirth/d2a2a82684396a928f42823cb688f58d).


## 2.  So, what is a better way?


The above has shown how the application of a statistical method can result in potentially very misleading results.

Unfortunately, it is hard for me (and perhaps just as hard for anyone else?) to come up with a purely statistical remedy --- i.e., a better statistical method.

The problem of measuring "grade inflation" is an intrinsically difficult one to solve.  Subject-specific _Boards of Examiners_ --- which is where the degree classification decisions are actually made within universities --- work very hard (in my experience) to be fair to all students, including those students who have graduated with the same degree title in previous years or decades.  This last point demands attention to the maintenance of standards through time.  Undoubtedly, though, there are other pressures in play --- pressures that might still result in "grade inflation" through a gradual lowering of standards, despite the efforts of exam boards to maintain those standards.  (Such pressures could include the publication of _%Firsts _and similar summaries, in league tables of university courses for example.)   And even if standards are successfully held constant, there could still be _apparent_ grade-inflation wherever actual achievement of graduates is improving over time, due to such things as increased emphasis on high-quality teaching in universities, or improvements in the range of options and the information made available to students (who can then make better choices for their degree courses).

I should admit that I do not have an answer!


## 3.  A few (more technical) notes


a.  For the artificial example above, I focused on the difficulty caused by aggregating university-level data to draw a conclusion about the whole sector.  But the problem does not go away if instead we want to draw conclusions about individual universities, because each university comprises several subject-specific exam boards (which is where the degree classification decisions are actually made).  Any statistical model that aims to measure successfully an aspect of behaviour (such as grade inflation) would need to consider data at the right level of disaggregation --- which in this instance would be the separate Boards of Examiners within each university.

b.  Many (perhaps all?) of the reported _standard errors_ attached to estimates in the OfS report seem, to my eye, unrealistically small.  It is unclear how they were calculated, though, so I cannot judge this reliably.  (A more general point related to this: It would be good if the OfS report's authors could publish their complete code for the analysis, so that others can check it and understand fully what was done.)

c.  In tables D2 and D3 of the OfS report, the model's parameterization is not made clear enough to understand it fully.  Specifically, how should the _Year_ estimates be interpreted --- do they, for example, relate to one specific university?  (Again, giving access to the analysis code would help with understanding this in full detail.)

d.  In equations E2 and E3 of the OfS report, it seems that some _independence_ assumptions (or, at least, uncorrelatedness)  have been made.  I missed the justification for those; and it is unclear to me whether all of them are indeed justifiable.

e.  The calculation of thresholds for "significance flags" as used in the OfS report is opaque.  It is unclear to me how to interpret such statistical significance, in the present context.


## 4.  Opinion


This topic seems to me to be a really important one for universities to be constantly aware of, both qualitatively and quantitatively.

Unfortunately I am unconvinced that the analysis presented in this OfS report contributes any reliable insights.  This is worrying (to me, and probably to many others in academia) because the _Office for Students _is an important government body for the university sector.

It is especially troubling that the OfS appears to base aspects of its regulation of universities upon such a flawed approach to measurement.  As someone who has served in many boards of examiners, at various different universities in the UK and abroad (including as an external examiner when called upon), I cannot help feeling that a lot of careful work by such exam boards is in danger of simply being dismissed as "unexplained", on the basis of some well-intentioned but inadequate statistical analysis.  The written reports of exam boards, and especially of the external examiners who moderate standards across the sector, would surely be a much better guide than that?



* * *

**Update, 7 January:** There's now also [**Part 2**](../2019/01/07/part-2-further-comments-on-ofs-grade-inflation-report/) of this blog post, for those who are keen to know more!

* * *

© David Firth, January 2019

**To cite this entry:**
Firth, D (2019). Office for Students report on "grade inflation". Weblog entry at URL [https://DavidFirth.github.io/blog/2019/01/02/office-for-students-report-on-grade-inflation](/2019/01/02/office-for-students-report-on-grade-inflation)
