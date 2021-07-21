# Redis-Codeigniter-NO-AB-Testing
Redis in Codeigniter working example of better than AB testing. 

Originally from: https://web.archive.org/web/20130818090404/https://glynrob.com/database/redis-in-codeigniter/

Redis in Codeigniter

So I was reading this excellent post about how A/B testing is not the best method for deciding success of clicks so I decided to build Steve Hanov’s method.
http://stevehanov.ca/blog/index.php?id=132


In short, it is a different way to see if a ‘BUY NOW’ button has more success in different colours.
Read his post if you wish to understand the Math more of the reasons why.


http://redis.io/
Redis is an open source, advanced key-value store.
It is super fast so suits the needs of this test if it was to be implemented into a live system.


So first you will need to get Redis working on your local machine for testing purposes.
I use Windows so I used http://code.google.com/p/servicestack/wiki/RedisWindowsDownload


Once you have downloaded the files, run redis-server.exe which is the server which will hold this data.

You can play with the command terminal redis-cli.exe if you want to try queries by hand.


So once you have Redis working on your local machine you can now try to use it with PHP.


This is a great library already created by Joelcox on GitHub https://github.com/joelcox/codeigniter-redis
So download this library and place it into your new codeigniter build.
You can run the test script he provides if you want to check that the connections to your Redis server is working correctly.


As always, a working example of my code is available in my GitHub repository:
https://github.com/glynrob/Redis-Codeigniter-NO-AB-Testing


So download this code and add to your codeigniter build and you should be all ready to go and see the page provide different buttons on each click depending with which button has the most success.


Quick explination of the Contoller:


Still using the Model method we make all our calls to the Model that makes the connection to the Redis Server.
The Index function makes a random number and 10% of the time it will pick a colour from random, the other 90% it will show the most successful colour.
Also once it is selected which colour to choose, it will record that it has shown that colour to keep track of how many times each colour is shown.
If the user clicks skip, it makes no amends to the database and loads the index page again.
If the user clicks on the button then that is a success so it increments that colours click by +1.



The Model


This is a list of functions that we use to call our Redis Server and provide back the results.

getFields just gets all 6 key-values and returns the results.

increaseShow will increment the value of the shown key provided by +1.

increaseClick will increment the value of the clicked key by +1.

I added a reset option so you can test again and again easily.



So thats it.
A small easy example of how to use Redis and implementing a cleaver method to try and get the most success from your ‘BUY NOW’ buttons.
