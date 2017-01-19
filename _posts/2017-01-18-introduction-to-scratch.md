Today was our first introduction to programming in [Scratch][4]. But, before we dug in, I shared two things I thought were important with the class

## The course website now has help for physical health

I added two new pages to [cmse201.com](http://cmse201.com). The first was information about how to get help if you're physically sick.

![image of the cmse201.com website's Physical Health page, where students can see the contact info, address, and map to the student health center][1]

## I spoke to the class about mental health

I then showed the class the page on mental health. 

![image of the course webpage on mental health, with contact info and a map to counseling services](http://d.pr/i/C2MJ+)

Roughly, what I remember saying was:

> We care about you. So our first priority is to make sure your bodies *and* your minds are taken care of. To that end, we put the information for mental health front and center on the course website. 
>
> My mom was diagnosed with bipolar disorder when she was about 26. If any of you happen to know Carrie Fisher---Princess Leia from _Star Wars_---my mom's bipolar disorder is very very similar to Carrie's. When I grew up, my mom would periodically have acute manic episodes, and she would need to be hospitalized. That became a part of my life.
>
> When I was in graduate school in my late 20s, I was diagnosed with severe clinical depression and generalized anxiety disorder. I learned I wasn't alone. A large number of graduate students are diagnosed with mental disorders during graduate school, and that's no accident. In part it's a reflection of the structural problems inherent in graduate school. 
>
> If I had, say, a broken leg, it would be visible to you. You might look at the boot around my foot and think "oh, my dad had one of those after his skiing accident." But mental disorders don't make themselves visible like that, even though  they can be very painful and, at their worst, limiting.
>
> I go to therapy and take medications to help me manage my disorders. But, getting diagnosed also formed a lens of looking at life. It helped me understand things that happened to me when I was younger. And, it's helped me understand that the feelings I have that "I'm a piece of garbage not worth anything" aren't my fault. Those are depression.
>
> If it weren't for therapy and medication, I would not be here right now. And, I apologize for getting that serious, but it's true. If I hadn't had access to these resources, I wouldn't be here.
>
> That's why I want all of you to know that we care about you, and there's help. You may not need it now. It's possible you may never have a need to look at this webpage. But as students, every single one of you is entitled to counseling help.
>
> I'm also being honest about this because I'm trying to reduce the stigma around it. You don't need to feel like you have a problem to seek counseling. I think plenty of people benefit from therapy, regardless of their mental state. It can be extremely helpful to have someone who isn't your friend, who isn't related to you, who can see you and your life in ways you may not see it. Someone who can help.
>
> If you're having an emergency, you can always dial 911. If it's during business hours, counseling has walk-in hours for crisis handling. 
>
> Like I said, many of you may never look at this webpage again, or feel that you need to. But you might know someone who does need help. And sometimes things can get bad, and people who need help aren't able to do the thing they need to do to get it. So if someone you know needs it, you know who to call and where to go. And you know where to bring them if they can't go alone.
>
> All the services offered are completely confidential and private. So, again, please know that we care about you. You can always come talk to me at office hours, or by appointment. My office is a safe space. And if you want to talk to someone else, the number is right here. 
>
> I know not many courses would spend this much time talking about this. Probably not many courses would put the info on the course homepage, at the same level as the syllabus. But I think this is so important, so that's why I did it. Thanks for listening.

## Hidden figures in the history of computing

There was no easy way to transition from that topic to the next on my agenda, but I tried. Before we got into programming in earnest, I wanted to talk briefly about several women who were instrumental in what we were about to do.

I think I started by discussing [Grace Murray Hopper][2], who was an ultimate badass as far as I'm concerned. 

![image of Rear Admiral Grace Murray Hopper][3]

I hope I didn't inadvertently smudge parts of history, but I stressed to the students that:

- Hopper worked on one of the first electronic computers EVER
- She was so instrumental that after her mandatory retirement, the US Navy created a position *for her* so she could keep working.
- It was Hopper who pushed against the then-unpopular idea that we should write in human-readable code; we shouldn't be programming in machine code. So, it's thanks to her that we have compilers. And, it's thanks to her that what we're about to do uses English, and we're not still manipulating switches and dials on registers.

I also told the class that I strongly recommend they see the film _Hidden Figures_, which tells the story of three black women who were instrumental to getting us to space in the US Space Race. I stressed that they suffered a kind of double-discrimination, being both black and female at a time when neither were viewed as equal. I told them how brilliant those women were, and how all three of them were real, living, breathing people. 

Then, we got on with the remainder of the class.

## Introduction to programming with Scratch

### Motivating deliberate practice

As an exercise, I ask everyone in the class to raise their hands. "When I say something that applies to you, I want you to put your hand down, OK?"

Then, I move through the following list, again saying "put your hand down if this applies to you".

Lower your hand if you:

- Are or were in Marching Band? about 3 hands went down, and I said "yes! you are my people!"
- Play(ed) a sport (including motor sports, sailing, surfing)? I think all but two hands were up, meaning more than 90% of the class fit in those top two categories
- Play games competitively (chess, magic the gathering)? Still 1 hand up.
- Have been a musician (vocal, instrumental, electronic)? This is where the last hand went down
- Have learned to drive
- Have learned a new language

I said 

> OK. I'm asking this because all of you have some experiential basis for doing things like drills, where you do the same thing over and over again. Maybe it's an end zone drill in ultimate frisbee, and maybe it's musical scales. But the point is that you've all experienced having to focus on one thing over and over, even if it seems slightly removed from the main activity. Most music isn't scales, and yet musicians practice scales every day. Why? Because they give us practice in moving between notes, so that when we actually play that becomes almost automatic.
>
> Same thing with an End Zone drill. Most of an Ultimate Frisbee game doesn't happen at the End Zone. But you practice it so that when you *are* near the End Zone, it's almost automatic and you move fluidly into it.
>
> As we learn programming, you may find we're asking you to do the same small things over and over again. And, when we ask you to do that, it's just like those other drills. It's so that when we come face to face with more complex problems, you'll be able to do certain things almost automatically.

Sidenote: I think in some cases people would put their hands down, then a later statement also applied to them and they weren't sure what to do. Some folks re-raised their hands, which was how I figured it out. "Oh, is it that you're also a musician? OK, got it."

Extra Sidenote: this is a great experiential grounding for conditional statements (Boolean OR) as well as cumulative distribution functions (how many items did I have to go through before all hands were down?). We pick up more and more of the class with each category, but the biggest jump was "played a sport"


### Before kicking the tires on Scratch

I introduced the concept of a "development environment", which I told the students we would "come back to later".

I modeled for them dragging out a few blocks and telling the program to run. (What I always find not obvious in scratch is that to get just about anything to happen, you have to add event triggers. So, I showed them how to set up the "green flag" event trigger to be able to start a program.)

Then I gave them my "kick the tires" speech. In a nutshell, I'm trying to do with Scratch what we did in Maryland's Science Methods courses (often called "physics 115" for short) for teachers. In my physics 115 sections on "electricity", we'd have everyone start with a single bulb, a single battery, and one small length of wire. My instructions were:

> Take about 5-10 minutes to start messing around with these. Try some ways to get the bulb to light. In your notebooks, record what your setup was to get the bulb to light. But, also record setups where you _thought_ the bulb should light, but it didn't. 

That one activity usually provides enough starting material for the entire semester. And, to be clear, I'm definitely not the inventor of it. About the only thing I think I added was emphasizing that they pay attention to configurations that they think ought to work, but don't. 

As a quick example, this is something that won't work: running a single wire from one terminal of the battery to the bottom contact of the lightbulb

```
[battery]-------wire-----[bulb)
```

To bring it back to programming, there are tons of small parts of Scratch and plenty of things that just aren't obvious:

- what the hell does [block X] do?
- how do I delete a block?
- how do I make something happen over and over again?
- I put the pen down, but I don't see anything. WTF?

My choice of language is deliberate: "kick the tires" and "what the hell does X do?" are my way of trying to motivate a particular kind of skepticism. I don't just want them to be inquisitive, I want them to get in there and start smacking (virtual) parts, taking nothing for granted. If it's not clear what something does, that very well may be the designer's fault. Treat it as such until you get an answer.

### In which we turn them loose on Scratch for 20 minutes

We told them to start working individually, and what followed was the general murmur of activity punctuated by:

- questions they started asking each other and answering
- meows (at which point I said "aaaaand someone's found the sounds")
- musical tones

While they worked, I told them I would be working too. So, I hooked my computer to the projector and live-coded on the screen while they were coding on their respective computers.

A few minutes in I scribbled some things on the board and got their attention. I had drawn (I think) a circle, a stair-step line, a diagonal line, a triangle, and a square. When I had their attention I mentioned that if they were looking for something to focus on, they could try creating these shapes in their own environments.

### Bringing the class back together after kicking the tires

I tried to start with questions they had. Several had looked up at my livecoding during the exploration session, so I started talking about my code.

That allowed me to bring up ideas like: How can you change a `pen color` by 10. That kind of doesn't make sense. It does makes sense to say `set pen color to RED`. It doesn't seem obvious that you could do `RED + 10`. So that's kind of weird.

We got into a really juicy discussion when I asked if anyone had made progress on drawing a circle. One student, D, said he had kind of gotten it, but there was this straight bit in his circles. His code was essentially:

```
pen down
move 10
turn 15 degrees
```

So, I modified my code, and my cat was drawing rough circles. Then D asked "wait, how'd you do that?"

"How'd I do what?"

"Get it to keep going?"

That's when I realized my code had a `repeat` block in it, which *also* made me realize D's code did not. So, to make a circle D was pressing the green flag repeatedly until his sprite got back to its starting point.

The discussion opened out into:

- What if we define circle as "move 1, turn 1 degree"
- How can we copy and paste scratch code?
- What does defining your own block do?
    - Why would you do it?
- Why define your block when you can just copy and paste the code?
    - I talked about my dissertation work and how this is still an open problem? How do people get convinced abstraction is worthwhile?



[1]: http://d.pr/i/H4TS+
[2]: https://en.wikipedia.org/wiki/Grace_Hopper
[3]: https://upload.wikimedia.org/wikipedia/commons/a/ad/Commodore_Grace_M._Hopper%2C_USN_%28covered%29.jpg
[4]: http://scratch.mit.edu