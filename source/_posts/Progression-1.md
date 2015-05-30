title: "Progression"
date: 2015-05-30 21:19:57
tags:
---

[Raphael,Adrien,Benjamin]
18/05/2015

We finally succeed to test our code on the Nao robot, unfortunattely some errors appeared. We asked Titouan to help us in order to reprogram an « if » box. We didn't find out what the real problem was.

19/05/2015

We found the solution to our problem, we reconfigured the « random int » box which returns a random number between 1 and 10. The robot will asked us 4 questions and then will stop. When we answer « NO » to the question « Would you like to play ? » , the robot will sit down and be quiet. If we wait 10s and say « Ok let's play » to it, it will answer « Cool ! », get up and start to ask the questions.


[Yani]

Today, we tried to find out how to send movements request to the Nao robot through the computer terminal. As last week we could send “say” request but didn’t succeed in sending “motion” request. We are not sure if we can send direct request for motion through terminal. We found online some code in which the developers seem to create more or less their own keywords and syntax that implements the Nao movements. We’ve spend a lot of time trying to understand the code and building on top it. 

Firstly we could succeed in sending Say requests using the code found online. Just before the end of the work session we understood a little bit more about how are implemented the boxes found online. But we are not completely sure that we use it correctly and we are trying many different manipulations with. Here is the Boxes we found online:

{% asset_img screenshot.png %}

The next step is to use the motions keywords.