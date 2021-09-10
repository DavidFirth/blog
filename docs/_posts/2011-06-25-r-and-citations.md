---
slug: r-and-citations
title: R and citations
categories:
- Citations
- R
---

We’re hosting the international [_useR!_](http://www.R-project.org/useR-2011) conference at Warwick this summer, and I thought it might be interesting to try to get some data on how the use of [_R_](http://www.R-project.org) is growing. I decided to look at scholarly citations to _R_, mainly because I know where to find the relevant information.

I have access to the [ISI Web of Knowledge](http://wok.mimas.ac.uk), as well as to [Google Scholar](http://scholar.google.com). The data below comes from the _ISI Web of Knowledge_ database, which counts (mainly?) citations found in academic journals.

**Background: How _R_ is cited**
Since version 0.90.0 of _R_, which was released in November 1999, the distributed software has included a FAQ document containing (among many other things) information on how to _cite R._ Initially (in 1999) the instruction given in the FAQ was to cite



	
  * [Ihaka, R and Gentleman, R (1996). R: A Language for Data Analysis and Graphics, _Journal of Computational and Graphical Statistics_ **5**, 299-314](http://www.jstor.org/stable/1390807)


When _R_ version 1.8.1 was released in November 2003 the advice on citing _R_ changed: people using _R_ in published work were asked to cite



	
  * [R Development Core Team (2003). _R: A Language and Environment for Statistical Computing_. R Foundation for Statistical Computing, Vienna, Austria.](http://www.R-project.org)


The “2003” part of the citation advice has changed with each passing year; for example when _R_ 1.9.1 was released (in June 2004) it was updated to “2004”.

**ISI Web of Knowledge: Getting the data**
Finding the citation counts by searching the ISI database _directly_ does not work, because:



	
  1. the ISI database does not index _Journal of Computational and Graphical Statistics_ as far back as 1996; and

	
  2. the “R Core Development Team” citations are (rightly) not counted as citations to journal articles, so they also are not directly indexed.


So here is what I did: I looked up published papers in the ISI index which I knew would cite _R_ correctly. [This was easy; for example my friend [Achim Zeileis](http://eeecon.uibk.ac.at/~zeileis/) has published many papers of this kind, so a lot of the results were delivered through a search for his name as an author.] For each such paper, the citation of interest would appear in its references. I then asked the _Web of Knowledge_ search engine for all _other_ papers which cited the same source, with the resulting counts tabulated by year of publication.

It seems that the ISI database aims to associate a unique identifier with each cited item, including items that are not themselves indexed as journal articles in the database. This is what made the approach described above possible.

There’s a hitch, though! It seems that, for some cited items, more than one identifier gets used. Thus it is hard to be sure that the counts below include _all_ of the citations to _R_: indeed, as I mention further below, I am pretty sure that my search will have missed some citations to _R_, where the identifier assigned by ISI was not their “normal” one. (This probably seems a bit cryptic, but should become clearer from the table below.)

**Citation counts**
As extracted from the _ISI Web of Knowledge_ on 25 June 2011:
<table cellpadding="3" cellspacing="0" style="font-size:75%;" border="1" > 
<tbody >
<tr style="font-weight:bold;" >

<td align="LEFT" height="16" >ISI identifier
</td>

<td align="RIGHT" >1998
</td>

<td align="RIGHT" >1999
</td>

<td align="RIGHT" >2000
</td>

<td align="RIGHT" >2001
</td>

<td align="RIGHT" >2002
</td>

<td align="RIGHT" >2003
</td>

<td align="RIGHT" >2004
</td>

<td align="RIGHT" >2005
</td>

<td align="RIGHT" >2006
</td>

<td align="RIGHT" >2007
</td>

<td align="RIGHT" >2008
</td>

<td align="RIGHT" >2009
</td>

<td align="RIGHT" >2010
</td>

<td align="RIGHT" >Total
</td>
</tr>
<tr >

<td align="LEFT" height="16" >IHAKA R
J COMPUTATIONAL GRAP 5 : 299 1996
</td>

<td align="RIGHT" >5
</td>

<td align="RIGHT" >15
</td>

<td align="RIGHT" >18
</td>

<td align="RIGHT" >43
</td>

<td align="RIGHT" >131
</td>

<td align="RIGHT" >290
</td>

<td align="RIGHT" >472
</td>

<td align="RIGHT" >528
</td>

<td align="RIGHT" >435
</td>

<td align="RIGHT" >419
</td>

<td align="RIGHT" >449
</td>

<td align="RIGHT" >378
</td>

<td align="RIGHT" >396
</td>

<td align="RIGHT" >**3579**
</td>
</tr>
<tr >

<td align="LEFT" height="16" >*R DEV COR TEAM
R LANG ENV STAT COMP : 2003
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="RIGHT" >39
</td>

<td align="RIGHT" >123
</td>

<td align="RIGHT" >91
</td>

<td align="RIGHT" >57
</td>

<td align="RIGHT" >39
</td>

<td align="RIGHT" >25
</td>

<td align="RIGHT" >14
</td>

<td align="RIGHT" >**388**
</td>
</tr>
<tr >

<td align="LEFT" height="16" >*R DEV COR TEAM
R LANG ENV STAT COMP : 2004
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="RIGHT" >16
</td>

<td align="RIGHT" >235
</td>

<td align="RIGHT" >421
</td>

<td align="RIGHT" >327
</td>

<td align="RIGHT" >289
</td>

<td align="RIGHT" >187
</td>

<td align="RIGHT" >126
</td>

<td align="RIGHT" >**1601**
</td>
</tr>
<tr >

<td align="LEFT" height="16" >*R DEV COR TEAM
R LANG ENV STAT COMP : 2005
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="RIGHT" >42
</td>

<td align="RIGHT" >397
</td>

<td align="RIGHT" >531
</td>

<td align="RIGHT" >511
</td>

<td align="RIGHT" >445
</td>

<td align="RIGHT" >366
</td>

<td align="RIGHT" >**2292**
</td>
</tr>
<tr >

<td align="LEFT" height="16" >*R DEV COR TEAM
LANG ENV STAT COMP : 2005
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="RIGHT" >5
</td>

<td align="RIGHT" >39
</td>

<td align="RIGHT" >75
</td>

<td align="RIGHT" >41
</td>

<td align="RIGHT" >25
</td>

<td align="RIGHT" >10
</td>

<td align="RIGHT" >**195**
</td>
</tr>
<tr >

<td align="LEFT" height="16" >*R DEV COR TEAM
R LANG ENV STAT COMP : 2006
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="RIGHT" >55
</td>

<td align="RIGHT" >438
</td>

<td align="RIGHT" >849
</td>

<td align="RIGHT" >656
</td>

<td align="RIGHT" >461
</td>

<td align="RIGHT" >**2459**
</td>
</tr>
<tr >

<td align="LEFT" height="16" >*R DEV COR TEAM
R LANG ENV STAT COMP : 2007
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="RIGHT" >92
</td>

<td align="RIGHT" >714
</td>

<td align="RIGHT" >962
</td>

<td align="RIGHT" >733
</td>

<td align="RIGHT" >**2501**
</td>
</tr>
<tr >

<td align="LEFT" height="16" >*R DEV COR TEAM
R LANG ENV STAT COMP : 2008
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="RIGHT" >208
</td>

<td align="RIGHT" >1402
</td>

<td align="RIGHT" >1906
</td>

<td align="RIGHT" >**3516**
</td>
</tr>
<tr >

<td align="LEFT" height="16" >*R DEV COR TEAM
LANG ENV STAT COMP : 2008
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="RIGHT" >7
</td>

<td align="RIGHT" >21
</td>

<td align="RIGHT" >44
</td>

<td align="RIGHT" >**72**
</td>
</tr>
<tr >

<td align="LEFT" height="16" >*R DEV COR TEAM
R LANG ENV STAT COMP : 2009
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="RIGHT" >172
</td>

<td align="RIGHT" >1363
</td>

<td align="RIGHT" >**1535**
</td>
</tr>
<tr >

<td align="LEFT" height="16" >*R DEV COR TEAM
R LANG ENV STAT COMP : 2010
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="RIGHT" >205
</td>

<td align="RIGHT" >**205**
</td>
</tr>
<tr >

<td align="LEFT" height="16" >*R DEV COR TEAM
R LANG ENV STAT COMP :
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="LEFT" >
</td>

<td align="RIGHT" >1
</td>

<td align="RIGHT" >12
</td>

<td align="RIGHT" >14
</td>

<td align="RIGHT" >25
</td>

<td align="RIGHT" >36
</td>

<td align="RIGHT" >81
</td>

<td align="RIGHT" >93
</td>

<td align="RIGHT" >**262**
</td>
</tr>
<tr style="font-weight:bold;" >

<td align="LEFT" height="16" >Total
</td>

<td align="RIGHT" >5
</td>

<td align="RIGHT" >15
</td>

<td align="RIGHT" >18
</td>

<td align="RIGHT" >43
</td>

<td align="RIGHT" >131
</td>

<td align="RIGHT" >290
</td>

<td align="RIGHT" >528
</td>

<td align="RIGHT" >945
</td>

<td align="RIGHT" >1452
</td>

<td align="RIGHT" >1964
</td>

<td align="RIGHT" >3143
</td>

<td align="RIGHT" >4354
</td>

<td align="RIGHT" >5717
</td>

<td align="RIGHT" >18605
</td>
</tr>
</tbody>
</table>
For the “R Development Core Team (year)” citations, the peak appears about 2 years after the year concerned. This presumably reflects journal review and backlog times.

There are almost certainly some ISI identifiers missing from the above table (and, as a result, almost certainly some citations not yet counted by me). For example, the number of citations found above to _R Development Core Team (2009)_ is lower than might be expected given the general rate of growth that is evident in the table: there is probably at least one _other_ identifier by which such citations are labelled in the ISI database (I just haven’t found it/them yet!). If anyone reading this can help with finding the “missing” identifiers and associated citation counts, I would be grateful.

The graph below shows the citations found within each year since 1998.

© David Firth, June 2011

**To cite this entry:**
Firth, D (2011). R and citations. Weblog entry at URL [https://DavidFirth.github.io/blog/2011/06/25/r-and-citations/](/2011/06/25/r-and-citations/).

[![bb](/assets/media/2011/06/citations1.png?maxWidth=300)](/assets/media/2011/06/citations1.png?maxWidth=800&maxHeight=600)

The graph shows the citations found within each year since 1998.

[Click on the graph to view it at a larger size.]

Citations to _Ihaka and Gentleman (1996)_ and to _R Core Development Team_ (any year) are distinguished in the graph, and the total count of the two kinds of citation is also shown.
