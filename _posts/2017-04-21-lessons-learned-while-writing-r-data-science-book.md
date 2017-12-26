---
layout: post
title: Lessons learned while Writing R Data Science Book
date: 2017-04-21 01:08:02.000000000 -07:00
type: post
excerpt: The publisher told me that my R data science book manuscript is currently
  undergoing a second proofreading and it will be published around June after the
  final review. The process took me almost two years since July 2015 when I was first
  asked to write it. I would like to share a few tips that I learned during the writing
  process.
---
The publisher told me that my R data science book (in Korean! Not English, yet) manuscript is currently undergoing a second proofreading and it will be published around June after the final review. The process took me almost two years since 2015 when I was first asked to write it. I would like to share a few tips that I learned during the writing process.

## 1. Writing a book is hard
Understand that it is hard to write a book before accepting an offer to write one. I have written dozens of ~10-page [academic papers](https://scholar.google.com/citations?user=tVkKxokAAAAJ) and am familiar with the paper writing process. That was why I accepted the challenge to write a long form book relatively easily, thinking “How different would writing a book be from writing a few papers?” The two turned out to be very different!

Academic papers are aimed at professional audience (hence, paradoxically, easier to write!), short, and the draft is completed typically within a week or two. Writing an academic paper is like running a 1 km race (Of course, one or two weeks only include “writing”; research work itself takes a lot longer).

On the other hand, books are typically aimed at general audience, long, and takes at least a few months to write. Writing a book is like running a marathon. It requires better planning, more disciplined pacing, and lots of patience and perseverance. It was a particularly challenging and humbling experience for me, who tend to work better in many small projects in bursts.

## 2. Get feedback early on
Seek feedback on your writing early and often. Feedback is essential for good writing in general. (See [“the Sense of Style”](http://stevenpinker.com/publications/sense-style-thinking-persons-guide-writing-21st-century) for a great general introduction that touches on feedback and other guidances on good writing in general.) When writing a book, getting feedback has additional benefit of adding a few small milestones (make the whole process more incremental and agile). Also, feedbacks make book writing a lot more social and less lonely endeavor.

## 3. Collaborate with Google doc
Use online collaborative tools such as [Google Doc](http://drive.google.com) for drafting. Google Docs lets you easily share your drafts with reviewers and receive feedback and comments in real time. Very efficient.

## 4. Version control your codes
Version control computer codes for analysis and producing charts. [Reproducibility](https://cran.r-project.org/web/views/ReproducibleResearch.html) is one of the main themes of my upcoming book. Use GitHub to track R, python, or other source codes. You can provide the codes as an appendix to the book. (The source code for my book is tracked [here](https://github.com/Jaimyoung/ipds-kr).) Some books are even available as a github repo, like [Advanced R](https://github.com/hadley/adv-r) from Hadley Wickham!

## 5. Get the references right early on
Maintain the list of high-quality reference materials that are OK to use for publication. Many reference materials such as articles, diagrams, and photos could be found on the web. Record the URL, date and time of access of those materials. Check the copyright information to make sure the material is good to reproduce in a book. Materials on Wikipedia is typically OK to reference in most cases, but one should specify the source.

Here’s a challenging example: I was referencing “Aeron chair” in the book and sent a photo of one downloaded from Wikipedia to the publisher, but the picture quality was not good enough for publication. Publication in print needs resolution of 300 [dpi](https://en.wikipedia.org/wiki/Dots_per_inch) at the very least. I started searching the web for photos of an Aeron chair that are both high quality and copyright-free, but such photos turned out to be very difficult to find!  (If you have found such a picture, please let me know 🙂

<img class="alignnone size-full wp-image-203" src="https://upload.wikimedia.org/wikipedia/commons/e/ec/Aeron_chair_JN.jpg" alt="aeron_chair_jn" width="322" height="345" /><br />
Photo: Aeron Chair. (Source: <https://en.wikipedia.org/wiki/Aeron_chair>)

## 6. Get the image format right
Consult with the publisher to determine the size, resolution, and font size for charts.** In my case, the publisher was fine with [PNG file](https://stat.ethz.ch/R-manual/R-devel/library/grDevices/html/png.html), but it took some trial and error and going back and forth to arrive at the following personal standards (See the R code snippet at the bottom):
- Size is 5.5 in. X 4 in.,
- Resolution 600 dpi, and
- [Text Point Size](https://en.wikipedia.org/wiki/Point_(typography)) = 9 (if you use [ggsave](https://www.rdocumentation.org/packages/ggplot2/versions/2.2.1/topics/ggsave) function in R, you typically don’t need to worry about this at all)

## Wrapping up...
That’s it. I wish I knew these 2 years ago.

Writing a book for the first time in my life was a lot harder than I had thought, but it was also a great experience. I *learned a lot* (including above tips), there’s a *sense of achievement* (like finishing a marathon*), and it’s *rewarding* to think that my work when published in June would *benefit some readers* getting better in the trade of data science. If you have the experience and knowledge to share with the world, you should definitely consider it!

 

### Code Snippets:
a few R codes to export charts for publication quality. To use, specify the file names. Experiment different **width, height, dpi** options (in that order!) until you get satisfactory PNG file.

{% highlight r %}
# A few useful lines to export plots
# 1. base R graph
png("../../plots/.png", 5.5, 4, units='in', pointsize=9, res=600)
# Plot body
dev.off()
 
# 2. single ggplot
# Produce ggplot first. Then...
ggsave("../../plots/.png", width=5.5, height=4, units='in', dpi=600)
 
# 3. plot matrix from library(gridExtra)
# Produce p1, p2, p3, p4 individual ggplot object
g <- arrangeGrob(p1, p2, p3, p4, ncol=2)
ggsave("../../plots/.png", g, width=5.5, height=4, units='in', dpi=600)
{% endhighlight %}
 

* Well, I have never run marathon.

** This is English version of [this article](/2017/04/15/r-데이터-과학-서적을-집필하면서-배운-몇가지), originally in Korean.

