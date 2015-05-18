title: "Improvements"
date: 2015-05-11 20:35:09
tags:
---


[4] This week, we have found a script opening a communication socket on Nao. With this one, we can send commands, having a particular syntax, to Nao, witch will analyse and execute the action. It uses the TCP protocol, on port 8080, and so can be easily used by a PHP script. 

Moreover, the usage is very simple : Choregraphe, which has to be install on the web server machine, executes the script once. There, it constantly listen to the port 8080, and treat every message it recieved.

We tried to implement a way for the Nao to remember the riddles it has already asked but without an actual Nao on which to try, we don't know if it work. For that we have written a small box that combine the "if box" and the "get data" box. We'll try on a robot next week !

Today we started by trying to see more clearly through the functions proposed at this link : [http://www.lucubratory.eu/independent-socket-server-on-nao/](http://www.lucubratory.eu/independent-socket-server-on-nao/). We are trying to see where does the error came from and how to correct it if we can. So we changed the “port” argument in the function into a chosen number (8080), we could get send packets from computer to the Nao with no loss. This means that the Nao and the computer are actually connected, but we can’t get any authentication from the Nao. 
Thanks to this [http://dhrc.snu.ac.kr/nao-robot-programming-guide-creating-a-tcpip-module-using-motion-capture-part-1/](http://dhrc.snu.ac.kr/nao-robot-programming-guide-creating-a-tcpip-module-using-motion-capture-part-1/), we succeeded in creating a communication socket on Nao in order to communicate with him though a web server machine.
Here is a picture of the Choregraphe’s boxes setting:

{% asset_img screenshot.png %}   <br />

The socket is created and the Nao will listen on port 8080 for any incoming request. We will show the code of the box later. Basically now we can communicate with Nao from the computer, we can send him some sentences to say. So the connection is done but we still have some issues:

* For now we still need to manually run Choregraphe in order to run the server on the Nao, but we will try to write a PHP script that would automatically run it.
* We are still learning the syntax of the request to send to Nao, we could make him speak but for now we couldn’t make him move.
* Also we’ve set the Nao’s right foot button as an interrupter to cut the connection.
