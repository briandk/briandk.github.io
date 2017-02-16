---
title: Blockpy Homework Grading Rubric
author: Brian A. Danielak
date: 2017-01-26
layout: post
categories: cmse201 spring2017
---

# Reasoning about radioactive decay modeling in code

On Monday, we had played a simple coin based game with the intent of simulating a pattern. I didn't discuss it explicitly, but the pattern was radioactive decay. In essence, every student starts with a coin tails up. For each round, any player whose coin shows tails flips that coin. At the end of each round, we tally. If a player's coin is heads up, that counts as a one for that player. Tales counts as a zero. The first time a coin shows heads, it can no longer be flipped. 

We played some variations of the game. For example, what happens if we give each player to coins? And in a two coin situation, how should we have that player report? One possibility is that if either coin shows heads, you are at heads and can no longer toss. Another possibility is that if one coin shows heads up, that coin is out, but if you still have a tails up coin, you can play with that remaining coin. This second method the students dubbed "the extra life method", because if you lost one coin, but the other coin was still tails, it was like an extra life that kept you in the game 

## Whiteboard photos

![whiteboard1](/assets/2017-02-15-reasoning-about-agent-based-decay-programs/asset.jpg)
![whiteboard2](/assets/2017-02-15-reasoning-about-agent-based-decay-programs/asset-2.jpg)
![whiteboard3](/assets/2017-02-15-reasoning-about-agent-based-decay-programs/asset-3.jpg)

![whiteboard4](/assets/2017-02-15-reasoning-about-agent-based-decay-programs/asset-4.jpg)
![whiteboard5](/assets/2017-02-15-reasoning-about-agent-based-decay-programs/asset-5.jpg)
![whiteboard6](/assets/2017-02-15-reasoning-about-agent-based-decay-programs/asset-6.jpg)

## Critically reading code

I gave students this code:

```python 
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import seaborn as sns

time_steps = np.linspace(
    start = 1,
    stop = 10,
    num = 10
)

particles = pd.Series(
    np.zeros(10000)
)

decay_data = pd.DataFrame({
    'time_step': [0],
    "percent_decayed": [0],
    "percent_remaining": [100]
})

def try_to_decay (particle):
    decay_probability = 0.5
    does_particle_decay = np.random.random() > decay_probability
    
    if (particle == 0 and does_particle_decay):
        particle = 1
        
    return particle

def evolve_system (particles):
    return particles.map(try_to_decay)

for time_step in time_steps:
    particles = evolve_system(particles)
    percent_decayed = particles.mean() * 100
    new_data = pd.DataFrame(
        {
            'time_step': [time_step],
            'percent_decayed': percent_decayed,
            'percent_remaining': (100 - percent_decayed)
        },
        index = [0]
    )
    
    decay_data = decay_data.append(new_data)

plt.plot(
    decay_data.time_step,
    decay_data.percent_decayed,
    decay_data.time_step,
    decay_data.percent_remaining
)

plt.show()
```

### Questions that came up

#### What do the first four lines do?

This was a great question. What does `import` do, really? We tried typing `numpy` in a fresh, restarted kernel console. It name errors. We tried importing numpy; it works. I discussed with them the cookbook metaphor: that you're working in the kitchen and you ask someone to grab a book of recipes off the shelf. In this case, the book is called numpy. 

Then we talked about `as`, as in 

```Python
import numpy as np
import pandas as pd
```

The as statements, I explained, provide nicknames or shorthand to refer to that imported package. I then showed them that if I `import numpy as np`, I could type `np.`and use tab completion to start getting a list of recipes contained within that module. 

Student a asked whether it was a hard rule that we had to import numpy as *np*. I explained we could use whatever shorthand we wanted, but that it was common that you would see `as np` in examples. I then spoke openly about how that presented a dilemma for me. To me, writing out import, followed by the module name, means that you're always using the full module name when you're referring to it in your code. I happen to think that this makes it clear when you're first learning the names of modules. 

My  dilemma was that once student started looking up examples of code, they would run into these abbreviations. If I brought up abbreviations first, it adds complexity to what we're trying to learn. But, if I never talk about them, then it's confusing to see them in example code and documentation. 

During this discussion, a serendipitous thing happened. I typed:

```Python
import numpy as np
numpy.zeros(10000)
```

The code threw an error: `name 'numpy' is not defined`. It was my mistake. I had used an abbreviation for the library when I imported it. But, in that subsequent command, I wasn't using the nickname under which I had imported the module. So, Python knew about `np`, but there was no `numpy` in scope. 

Student N suggested that  maybe adding a comma and another nickname would work. So, in essence:

```python 
import numpy as np, numpy
numpy.zeros(10000)
```

I had never even tried this before, so it was an opportunity for me to make a prediction as well as have the class make a prediction. I said that one possibility was to get the same name error as before. But, another possibility was that it would actually work. So we tried it.

And it worked. 

#### why are there decimal points after the zeros?

When you run this code:

```Python
import numpy as np
numpy.zeros(10000)
```

The result is:

```
array([ 0.,  0.,  0., ...,  0.,  0.,  0.])
```

But why are there dots after each zero? Why isn't the output this?:

```
array([ 0,  0,  0, ...,  0,  0,  0])
```

That question let us to a discussion about thinking about how computers represent numbers internally. We talked about allocating a certain number of switches to try and represent a number. With four switches we can easily represent the numbers one through four. Also, we could probably squeeze a zero in there.

So, why not add a switch for every additional number we want to represent? `5` would be `11111`, which would take five switches to represent. That was my challenge to the students: wouldn't it be just a simple to keep adding a switch for each plus-one number we want to represent?

They countered that binary was more efficient. I challenge them to come up with an argument to persuade me. What does efficiency mean and how can you prove it?

That discussion led us to the notion of making the off position significant. Which also let us down a quick tangent about place value systems, that Arabic numerals use a base 10 place value system, but that computers could use a base 2 system. 