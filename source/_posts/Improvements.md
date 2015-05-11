title: "Improvements"
date: 2015-05-11 20:35:09
tags:
---

This week, we have found a script opening a communication socket on Nao. With this one, we can send commands, having a particular syntax, to Nao, witch will analyse and execute the action. It uses the TCP protocol, on port 8080, and so can be easily used by a PHP script. 

Moreover, the usage is very simple : Choregraphe, which has to be install on the web server machine, executes the script once. There, it constantly listen to the port 8080, and treat every message it recieved.

We tried to implement a way for the Nao to remember the riddles it has already asked but without an actual Nao on which to try, we don't know if it work. For that we have written a small box that combine the "if box" and the "get data" box. We'll try on a robot next week !