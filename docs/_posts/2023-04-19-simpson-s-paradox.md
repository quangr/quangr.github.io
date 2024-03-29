---
layout: post
title: simpson's paradox
date: 2023-04-19 17:50 +0800
---
Let's say you are a student of statistics who recently just finished your regression class, or maybe you are just learning some cool machine learning methods that must run on 1000 gpus. You are facing a task: finding the best treatment for kidney stones. "I can do that" you thought, since there are no complex high-dimensional data involved.



|Stone size  |Treatment A |Treatment B |
|:--         |:--        |:--        |
|Small stones|Group 1<br>'''93% (81/87)'''|Group 2<br>87% (234/270)|
|Large stones|Group 3<br>'''73% (192/263)'''|Group 4<br>69% (55/80)  |
|Both        |78% (273/350)|'''83% (289/350)'''|


"78<83, easy decision". But hold on a second, what if the doctor already told you that you needed to pick a treatment for the patient with small tones? In this case, 93>87, which means you need to pick Treatment A. "This is weird, maybe I need to check the math." This may be your first thought, after using `calc.exe`. you finally admit that there were no stupid calclations involved. So what happens? How do I even make a desicion?

So that's simpson's paradox, a trend that appears in subgroups reverses in the overall group. The first thing we need to admit is that even though $\frac{81}{87}>\frac{234}{270}$,$\frac{192}{263}>\frac{55}{80}$,$\frac{81+192}{87+270}$can smaller than $\frac{192+55}{263+80}$. This is the first counterintuition.

So I'm not that good at math. But how should I make a decision? A guy named Pearl says, we can use casual inference to solve this! Pearl explainde that the stone size can affect both the treatment success rate and the choice of using treatment. This is called a confounder.

Treatment B seems to perform better not because it performs better for any stone size, but because it is more frequently used in easier situation(smaller stone). If we randomly assign each treatment to each situation, the reversation will never happens. So if we know the effect of treatment is only affected by stone size and treatment type, we should pick A!



Wow, that's solid, but if you are pessimistic enough like me, you may wonder, what if we don't know the result for each stone size? Most importantly it is totally possible that the underlying result is 


|Stone size  |Treatment A |Treatment B |
|:--         |:--        |:--        |
|Small stones|Group 1<br>'''78% (136/175)'''|Group 2<br>83% (144/175)|
|Large stones|Group 3<br>'''78% (137/175)'''|Group 4<br>83% (145/175)  |
|Both        |78% (273/350)|'''83% (289/350)'''|


It's important to remember that statistical data can only tell us so much about the world around us. Without a clear understanding of the data generation process and the assumptions that underlie our statistical models, we can't draw meaningful conclusions from the data alone. Simply owning a powerful GPU or having access to a large dataset isn't enough - we need to design experiments that are specifically tailored to the question we're trying to answer in order to draw valid conclusions."


What if there is always some underlying confunder in an experiment that can always reverse our result, does that mean we will never be able to find the scientific truth? Well, We need to remember that what we know can change as we learn more. In other words, scientific knowledge is not set in stone and can be updated when new information becomes available.



https://en.wikipedia.org/wiki/Simpson%27s_paradox