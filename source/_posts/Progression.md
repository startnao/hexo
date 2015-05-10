title: "Where we are"
date: 2015-04-14 08:16:50
tags:
---

*******************

{% asset_img IMG_20150413_175741.jpg %}

###Group 1
Firstly, we’ve move forward on creating customized boxes using Nao’s implemented functions which are described in the thechnical documentation. For example we’ve made a box that allow the Nao robots to record a sound and play it.

Furthermore we’ve find out that we can use something called “La transformation de Fourier” and implement it as a function so the Nao can isolate specific sound frequency in a record. That’s probably how we can detect whistles but research is still on going. The part of making the Nao detect someone yelling is considered as done. Indeed a box call “soundpeak” allow us to do that. Still the Nao won’t make the difference between a normal sound coming from a close source and a loud sound coming from a distance source but this not really a problem for what we are doing.

###Group 2 :

Nao need to perform some actions/movement when we are doing some large movements in front of the camera. If he cannot recognize these movements, he does a movement with his arms like protecting himself(he puts his arms in front of his face).. Which consist of not doing the good movement. And After downloading opencv, We have successfully managed to use the motion detector.

{% asset_img core2.PNG %}  <br />



###Group 3 :

Nao starts asking if the person wants to play. In case of a negative answer, he sits down, makes his head going down, turns his eyes to red and stays like that. When the player replies positively, he asks a riddle.
A random question is taken in a list of 10, and NAO detects if the given answer is the correct one. He continues and takes another question, different from the old one.

{% asset_img core1.PNG %} <br />  

{% asset_img core3.PNG %} <br />  



###Group 4:
In our team, we are trying to make Nao recognize red and blue balls. For this, we use the open source library OpenCV for the Nao.
We managed to analyze pictures with OpenCV and locate blue and red.
Today, we did not manage to use well OpenCV with the Nao.  

