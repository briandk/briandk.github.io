---
id: 86
title: Creating a better data graphic for Advanced Placement exam data
date: 2014-01-31T02:04:31+00:00
author: Brian Danielak
layout: post
guid: http://BrianDK.com/?p=86
permalink: /2014/01/creating-a-better-data-graphic-for-advanced-placement-exam-data/
categories:
  - Uncategorized
---
### The background

[Danielle Kurtzleben at US News](http://www.usnews.com/news/blogs/data-mine/2014/01/14/ap-test-shows-wide-gender-gap-in-computer-science-physics):

> During the past week, tech and education writers have been talking about data showing that the gender gap in the tech world is evident even in high school.
> 
> They cite Barbara Ericson, director of computing outreach at Georgia Tech, who recently broke down the 2013 Advanced Placement exams and found that in three states (Mississippi, Montana, and Wyoming), zero girls took the AP computer science test. Even in the state where girls are best represented among computer science test-takers, Tennessee, girls only took 29 percent of the exams. 

US News then went ahead and made this graph, which [Mark Guzdial linked to](http://computinged.wordpress.com/2014/01/30/powerful-visualization-of-gender-skew-in-ap-cs-from-usa-today/) on his blog:

[![graph of gender disparity in Advanced Placement courses](https://raw.githubusercontent.com/briandk/ap-exam-data/a3629f3c5a334cc97792d21204f339e817e8946a/usatodaygraphic.jpeg)](https://raw.githubusercontent.com/briandk/ap-exam-data/a3629f3c5a334cc97792d21204f339e817e8946a/usatodaygraphic.jpeg)

From my best read, the graph is based off of the national numbers [available directly from the college board](http://research.collegeboard.org/programs/ap/data/participation/2013).

I think this graph has a number of great features:

  1. Since the TOTAL EXAMS bar at the top doesn&#8217;t break 1, we can see that there&#8217;s less than one female student taking an Advanced Placement (AP) exam for every one male student who takes one.
  2. The most egregious disparities where male test-takers outnumber females are in mathematics and science, because those bars are manifestly higher than the orange line which represents a 1:1 male:female ratio
  3. Of the math/science exams, computer science has the greatest gender disparity. More than four males took the test for every female who did.

But, I think this graph isn&#8217;t as good as it could be, and here&#8217;s why:

  1. There&#8217;s no useful ordering the list of exams; they&#8217;re alphabetical. This lack of ordering is a classic case of what Howard Wainer (and subsequently Andrew Gelman) call the [&#8220;Alabama First&#8221; error](http://andrewgelman.com/2008/05/08/unalphabetize/). When there&#8217;s a chance to order data in more meaningful ways, we should.
  2. This is a big one to me: a ratio cannot shrink below zero, but its growth is effectively unbounded. This graph has an x-axis which goes to zero. Empirically, it&#8217;s impossible for any test that a student actually took to have a zero ratio. But there&#8217;s an even bigger problem.
  3. The choice of a ratio scale means that there&#8217;s far less visual space to show classes where females vastly outnumber males. In French Language and Culture, for example, females outnumber males more than 2:1. That&#8217;s a greater disparity than the gender disparity in Calculus or Physics B. The gender disparity in Art History is also nearly 2:1, which makes it a far greater disparity than the 1.5:1 we see in Microeconomics. By setting a ratio scale that goes to zero, it&#8217;s much more difficult to spot the places where females may be greatly outnumbering males, which I would argue _is also a gender problem._

### Making a better graph

My mentor [William E. J. Doane](http://drdoane.com/) is fond of saying you shouldn&#8217;t criticize without offering a better solution. So, with my thanks to US News and Mark for getting me thinking about this, here&#8217;s [my refined graph](https://raw.githubusercontent.com/briandk/ap-exam-data/master/ap-exam-data.png), made with help from [Angela Zoss](http://angelazoss.com/) ([click to embiggen](https://raw.githubusercontent.com/briandk/ap-exam-data/master/ap-exam-data.png))

[![a reimagined plot of the ap exam data](https://raw.githubusercontent.com/briandk/ap-exam-data/master/ap-exam-data.png)](https://raw.githubusercontent.com/briandk/ap-exam-data/master/ap-exam-data.png)

Why do I think this graph is more helpful?

  1. _Instead of using a ratio scale, it uses a log-ratio scale_. That means equal distances from the center line correspond to equal degrees of gender disparity. Computer Science A is still an extreme disparity (more than 4:1 females to males), but now we clearly see the cluster of studio art courses, all of which have a greater than 2:1 female/male ratio. 
  2. _It maps point size to total number of test takers_. The disparity in computer science A is a problem, but one of the things that jumps out is that nearly three times as many students took English Language Composition, where the gender balance is decidedly skewed female rather than male. The same is true for English Literature Composition. And Psychology, which has roughly twice as many students taking it, also has more than 1.5 female test takers for every male test taker.
  3. _Instead of alphabetical ordering, it orders by the degree of gender disparity_. Computer Science and Studio Art are at the extremes. Science and math are toward the bottom. But what also stands out is the degree to which humanities-focused courses (art, romance languages) are imbalanced in favor of females, sometimes exceedingly so.

### Now it&#8217;s your turn

I&#8217;ve open-sourced all of this work under an [MIT license](http://choosealicense.com/).

  * [Fork the repo](https://github.com/briandk/ap-exam-data)
  * [Open an Issue](https://github.com/briandk/ap-exam-data/issues/new)
  * Make a better graph
  * Put [the scalable PDF version](https://github.com/briandk/ap-exam-data/raw/master/ap-exam-data.pdf) somewhere