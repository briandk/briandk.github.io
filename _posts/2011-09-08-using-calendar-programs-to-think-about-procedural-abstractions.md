---
id: 38
title: Using Calendar Programs to Think About Procedural Abstractions
date: 2011-09-08T18:25:13+00:00
author: Brian Danielak
layout: post
guid: http://BrianDK.com/?p=38
permalink: /2011/09/using-calendar-programs-to-think-about-procedural-abstractions/
gr_overridden:
  - 0
categories:
  - Uncategorized
---
## Abstract

This post explores _procedural abstraction_, a fundamental concept of computer science and software design. First, I give a rough (and overly formal) definition of what I think procedural abstraction is. Then, I talk about a concrete issue from class: how can we think about procedural abstraction for a program that prints a 12-month calendar? I share my own representation for how _I_ wrapped my head around what to abstract in a calendar program. Finally, I close with remarks about why procedural abstraction&#8212;both what it is and how it&#8217;s taught&#8212;might matter for my research.

## Intro

Today&#8217;s class covered a whirlwind review of topics from Intermediate Programming. The early parts of class focused on some basics of the C language: input and output, primitive data types, procedural control (if/else, while, for loops), to name a few.

But, when we got to talking about procedural abstraction. Procedural abstraction seems to be one of those things that everyone talks about but it&#8217;s hard to find a definition of. So, here&#8217;s mine:

> **procedural abstraction:** A name given to the process of observing, characterizing, unifying, and deploying an otherwise distributed (and re-used) set of instructions 

Pretty diffuse and hard to think-through, right?

Below, I&#8217;ll go into great depth and describe how to think about procedural abstraction for the specific example of a program that prints 12-month calendars.

## Procedural Abstraction with calendar programs

The instructor demonstrated a piece of C code ([`year.c`][1]) designed to print out a 12-month calendar. When you compile and run `year.c`, you get this:

    Enter a day of the week (0-6):
    

You&#8217;re not told:

  1. That the input range 0-6 is supposed to be integers
  2. That each distinct integer represents a weekday
  3. That the weekdays are mapped consecutively to the integers, with Sunday being 0

But, for this discussion those oversights aren&#8217;t important. What _is_ important is that the program generates a 12-month calendar assuming that the first of the year falls on the day you specify as input.

So, for example, the printed output of a single month (January) might look like this if you input 3:

    Su Mo Tu We Th Fr Sa
              1  2  3  4
     5  6  7  8  9 10 11
    12 13 14 15 16 17 18
    19 20 21 22 23 24 25
    26 27 28 29 30
    

And multiple months would look like this:

    Su Mo Tu We Th Fr Sa
                     1  2
      3  4  5  6  7  8  9
     10 11 12 13 14 15 16
     17 18 19 20 21 22 23
     24 25 26 27 28 29 30
    
    
     Su Mo Tu We Th Fr Sa
      1  2  3  4  5  6  7
      8  9 10 11 12 13 14
     15 16 17 18 19 20 21
     22 23 24 25 26 27 28
     29 30 31
    
     Su Mo Tu We Th Fr Sa
               1  2  3  4
      5  6  7  8  9 10 11
     12 13 14 15 16 17 18
     19 20 21 22 23 24 25
     26 27 28 29 30
    

Note that the months aren&#8217;t labeled (we&#8217;ll come back to that later).

If you were a student being given that task for the first time, how might you decompose it? There are several sets of considerations that might occur to you:

### Visual Considerations

  1. How should the overall display be formatted?
  2. How can I wrap the days 1-31 around the calendar?
  3. Should the months appear side-by-side? In sequence?

### User Considerations

  1. Are we going to standardize on the Gregorian Calendar?
  2. Should the names of the weekdays be in English?
  3. What about leap years?

But then there are the sets of concerns that are at the heart of the program&#8217;s logic. Beyond how it looks and what it affords, how should the thing _work_?

The answer to how it should work depends on how you see the problem. It also depends on whether you see certain aspects of the problem space you can exploit. Since different months have different numbers of days (30 vs. 31), you might decide to write a code section for each month.

Below is the code section for January. It assumes `weekDay` is the number of which day of the week (0-6) starts the month of January. Also, the percent sign (`%`) indicates modulo division; that&#8217;s actually a pretty clever way of solving the display problem &#8220;how do we wrap dates around when the week ends?&#8221;

<pre><code class="c">/* Print January */
printf(" Su Mo Tu We Th Fr San")

/* prints spaces before the first date is printed */
for (i = 0; i &lt; weekDay; i++) {
  printf("   ");
}

/* prints the dates */
for (i = 1; i &lt;= 31; i++) {
  printf("%3d", i);
  if (!((i+weekDay) % DAYS_IN_WEEK))
    printf("n");
}
printf("n");
</code></pre>

If you write one section for each month&#8212;and you do it by hand&#8212;then the section for February would look similar. Except the tough part is, February starts the day after January ends. So, how do you handle which day to print first in February?

The answer isn&#8217;t necessarily obvious, though here&#8217;s one way to think about it. January starts on whatever day the user passes in (`0-6`). February starts 31 days after that. So, the _weekday_ February starts on is whatever day of the week is `[user input] + 31`.

So, one way to figure out February&#8217;s starting day is to add 31 days to January&#8217;s starting day, then wind those days into 7 day week-segments and see what&#8217;s left over. Sounds like a job for modulo arithmetic (`%` in C).

<pre><code class="c">/* Print February */
int februaryStart = (weekDay + 31) % 7;

printf("n"); // To make space for the next month
printf(" Su Mo Tu We Th Fr San");

/* prints spaces before the first date is printed */
for (i = 0; i &lt; februaryStart; i++) {
  printf("   ");
}


/* prints the dates */
for (i = 1; i &lt;= 28; i++) {
  printf("%3d", i);
  if (!((i + februaryStart) % DAYS_IN_WEEK))
    printf("n");
}
printf("n");
</code></pre>

This code works. It prints each month and it adjusts the number of days it prints depending on the month. Mission accomplished, right?

## Here&#8217;s the part where we presume students see the computational and design inefficiencies that experts would see in this code

This code is wasteful. Can you see why?

Actually, if I hadn&#8217;t said it was wasteful would you have even thought it was? Do you think students would have thought it was?

* * *

Here&#8217;s where it&#8217;s wasteful:

  1. This line will end up being repeated _exactly as it&#8217;s written_ 12 times, one for each month: 
        printf(" Su Mo Tu We Th Fr Sa\n")
        
    
    Take a second. Remember what the output months look like
  
    when they&#8217;re printed, given the pattern, and convince
  
    yourself that every month has the same seven weekdays in it:
    
         /* Print January */ 
         printf(" Su Mo Tu We Th Fr Sa\n")
        
         ...
        
         /* Print February */ 
         printf(" Su Mo Tu We Th Fr Sa\n")
        
         ...
        
         /* Print March */ 
         printf(" Su Mo Tu We Th Fr Sa\n")
        

  2. For every month, we&#8217;re going to want to print each day in the month. But that means we&#8217;re essentially repeating this statement: 
        ```c
        for (i = 0; i <= 28; i++)
        ```
        
    
    and only fiddling with the upper limit of `i` (since all months start at 1, but some end at 28, 29, 30, or 31) . So, the pattern means a top-level view of repetition in our code looks like this:
    
        for (i = 0; i <= 31; i++) // January
        for (i = 0; i <= 28; i++) // February
        for (i = 0; i <= 31; i++) // March
        for (i = 0; i <= 30; i++) // April
        

  3. For every month, we&#8217;re going to want to wrap weeks around the display, so that each 7-day-week of the month is on a new line of the output. Notice how similar the wrapping code for January looks to the wrapping code for February 
        //January
        printf("%3d", i);
        if (!((i+weekDay) % DAYS_IN_WEEK))
          printf("\n");
        
        //February
          printf("%3d", i);
          if (!((i + februaryStart) % DAYS_IN_WEEK))
            printf("\n");
        

## How can we really start to appreciate the wastefulness?

I created the slideshow below to offer a fuller sense of where and why this code is wasteful.

<a title="View ProceduarlAbstraction on Scribd" href="http://www.scribd.com/doc/64282895/ProceduarlAbstraction" style="margin: 12px auto 6px auto; font-family: Helvetica,Arial,Sans-serif; font-style: normal; font-variant: normal; font-weight: normal; font-size: 14px; line-height: normal; font-size-adjust: none; font-stretch: normal; -x-system-font: none; display: block; text-decoration: underline;">ProceduarlAbstraction</a>





## Seeing wastefulness as a way in to procedural abstraction

If you look at how the code is wasteful, what you see is

  1. Identical procedures get repeated
  2. The procedures are repeated on very similar objects (months) for very similar reasons (we need to print each month)
  3. There are elements of commonality in how the procedures differ

In fact, if you look at slide 5 above, the only bits of unique code<sup id="fnref-38-comments"><a href="#fn-38-comments" rel="footnote">1</a></sup> that _matter_ are `weekDay` and `februaryStart`. When you look at it that way, it might become obvious that all months of a calendar have 7-day-weeks, and they only really differ in

  1. How many days are in the month
  2. What day of the week starts the month (`weekDay` and `februaryStart` are both different names for this same general idea)

To a sharp programmer, then, all the groundwork is there for a procedural abstraction. But now, ask yourself: **is it obvious what the abstraction should look like?** How do we begin to understand wastefulness? And, how does noticing a pattern of waste in code bring us to a point where the form of a new abstraction is clear?

        // Determine the day offset that starts the month
        // Print enough blank spaces to offset the start 
        //     of the month from Sunday
        // Print a number for each day of the month
        // Wrap a display line when you finish a week
    

## From wastefulness to abstraction

Hopefully, I&#8217;ve convinced you by now that&#8212;in the case of the calendar&#8212;_seeing the wastefulness_ can be tightly coupled to _developing a procedural abstraction_. For myself, I needed to generate my own kind of representation (seen in the slideshow above) to explore common patterns in wastefulness.

I don&#8217;t know how other programmers operate, but I find that I can&#8217;t move to a level of procedural abstraction without first crafting a clear connection between repetition of code and patterns in procedure. In my slideshow I did that visually&#8212;lots of other people might have other ways.

## Why this matters for my study

The (at times) extremely fast pace of Intermediate Programming can mean the instructor doesn&#8217;t have time to explore the subtleties of sample code. My field notes indicate the instructor discussed the abstraction mechanism in `year.c` for about 10 minutes. In his full defense, 10 minutes can be an extensive and thorough use of lecture time. Furthermore, I imagine the topic will come up many times throughout the semester. So, I&#8217;m not just noticing the amount of time given the topic; I&#8217;m also noticing the tone and structure of the discussion in that time.

The instructor started the procedural abstraction discussion by opening `year.c` and showing students the already-abstracted `print_month()` procedure:

<pre><code class="c">void print_month(int weekDay, int monthDay)
{
  int i;

  /* print header line */
  printf(" Su Mo Tu We Th Fr San");

  /* prints spaces before the first date is printed */
  for (i = 0; i &lt; weekDay; i++) {
    printf("   ");
  }

  /* prints the dates */
  for (i = 1; i &lt;= monthDay; i++) {
    printf("%3d", i);
    if (!((i+weekDay) % DAYS_IN_WEEK))
      printf("n");
  }
  printf("n");
}
</code></pre>

The rest of the discussion was about why this was an obviously better alternative to writing separate procedures for each month. So, the concern here is something Wil would call &#8220;giving students solutions to problems they don&#8217;t have yet,&#8221; or, &#8220;handing solutions to students who may not yet realize why the problem even matters.&#8221;

If I were a cognitive-constructivist, I&#8217;m not quite sure I&#8217;d know what to make of the instructor&#8217;s approach. Part of me believes that helping students construct knowledge of procedural abstraction should entail an authentic appreciation of what problems might call for it. But, it seemed to me that my creation of the slideshow graphics above was my way of constructing a sense of procedural abstraction for this problem. Furthermore, it gave me a visual metaphor to think with&#8212;a pathway to move from an observing wasteful code to identifying common elements, and ultimately wrapping my mind around what pattern was getting repeated.

I think then, that one open question for me is: how do students think about and see procedural abstractions in their own work of trying to solve problems.

<li id="fn-38-comments">
  excluding comments, which look <code>//like this</code> or <code>/* like this */</code>&#160;<a href="#fnref-38-comments" rev="footnote">&#8617;</a> </fn></footnotes>