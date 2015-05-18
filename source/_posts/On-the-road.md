title: "On the road"
date: 2015-05-10 23:15:26
tags:
---



[1] During the last project session we finally decided after a lot debates to give up on trin to implement a whistle detector in the Nao as it really feels difficult and we are scared to remain stuck on this until the end and get no results. 

Instead we are going to build the web interface for Nao, the concept is to great an interface from which we could perform simple action with the Nao, like getting up, sitting, tai-chi … So we first started to search for information on how to implement a server with the Nao, we found some tutorials that unfortunatelly required some administrator access to the Nao that we don’t have, but we’re seeing with the CCRI if we could get it or not.

We tried to communicate with Nao by using TCP protocol. Actually, we managed to connect to his port, but there, no action was possible. So we tried to start a web server on the port 8080, using the same library that it uses in order to create the admin interface (port 80). However, we hadn't the permissions in order to perform this action.