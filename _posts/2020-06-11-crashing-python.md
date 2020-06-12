---
layout: post
title: "Python has Crashed": An Adventure through the Most Useless of Error Messages
image: ### picture of "python has crashed" error message, or maybe of the spider plot
---

This is a story of how sometimes something you think is going to be simple to do in a computer ends up being horribly complicated and frustrating... and (debatably) not worth the effort.

Several months ago I was working on a project that would recommend songs on spotify based on one song given by the user. This was not a solo project, and we had one week to do it in, and almost finished, but ultimately did not. So, last month I decided to dust it off and finish it. 

To get you to understand this, we need to have a brief discussion on Python and Flask. If you know how Flask works, do please skip this paragraph and the next, you'll probably be bored to tears. This is a massive oversimplificatin, but all programming you do on your own personal computer is essentially trapped there. So, if you want to put a piece of code that will do whatever it's trying to do for people other than a person using your physical computer, without having that person run your code on their own computer, you have to figure out how to put that program onto the Internet, so other people can use it. And you already know the name for these: Web applications. Or, more colloquially: Apps. These aren't always the phone and computer apps you're probably super comfortable with. If you've ever seen an interactive graph or chart on a website that has a bunch of dials and bars that you can click on and change, and then see how those changes affect the chart, it is highly likely something like that was an app as I'm using the term here. 

Now, all you need to know now before our story can begin is that, in Python, the library that most people use to create web applications is called Flask. Flask is a way of packaging your program such that it can be deployed where other people can see it and use it.

Alright. Let's now discuss how I managed to crash Python using Flask. 

Several months ago I was working on an app that would use Spotify song data to make song recommendations based on just one other song that, presumabely, the app user liked. Now, I was working with a group of people, and we only had a week to finish it, and we failed. We got close, but ultimately we didn't get a working app up and running. However, last month I returned to it to finish it on my own. Well, sort of. I don't do user interface programming or web design, what I do do is data analysis, and part of the original team were a few members were web designers. So, lacking them and their skills, I tried to make a simplified version of the original goal. Rather than selecting a song that the database had information on (something that would require drop-down menus of some kind or something like that), I decided it would be enough, for me personally, if it would just take a randomly chosen song, and make recommendations based on that. Everytime you refresh the web page, the app would choose a new random song and make new recommendations. Dead simple, very little practical use, but I knew that that was something I could do, and so I decided to try and do it.

And here is the result (it will likely take a bit of time to load initially, but once it loads the first time, refreshing the app to see a new song will be much quicker):  https://curtcalledburt-song-suggestor.herokuapp.com/.

It's nothing that looks too flashy. The song the app randomly chose is in the one in green, and the three songs the machine has found closest to it are projected on top of that song.

Now, if you're thinking to yourself at this moment, "Wait, that's all it does?" Yeah, that's what I thought to at the start of this descent into madness. I decided to finish this app in particular because I thought it would be simple to finish, BUT, as is usual in the world of programming, to programmer I was in the past screwed the current me over, big time. 

Now that you've now seen the finished product, what state did I find this app in one month ago? More or less what you see here actually. The problem wasn't in anything that the program was doing, it was in getting that program to behave within a Flask app. Running each function we had written, individually, one after the other in a Jupyter notebook or just in the Terminal worked just fine. But, the moment we tried telling an app to run those funcitons, in that same order, bugs abounded. 

Something was going wrong in Flask, and that's quite an annoyance becuase, if there is only one critique I have of Flask so far it is this: I've yet to encounter any error message even remotely helpful in solving any error. I've lost track of the number of times I google a Flask error message only to see a bunch of onine message boards with swarms of people saying, "So, when Flask says "x, y, z" is the problem, it means "a, b, c" is actually occurring. Now, the data science team did eventually sort all of these issues with Flask and by the end did have a working app, but due to some major coordination issues within the team, we ran out of time, and couldn't make the jump from having a working app to putting it online on a web app hosting site like Heroku for people to click on and see and interact with.

And so the project lay fallow until I gave it a look some months later. When I returned, I expected to find it much in the same state we all left it in. Functional, would run on my local machine, but will fail to upload to web app hosting service. That didn't happen. Instead, it somehow managed to work even worse than before. Without changing any of the code for MONTHS somehow, SOMEHOW, it had managed to break down even further. 

Now, now, when I ran the (once working!) Flask app on my computer, the computer would think for a bit, until it shut down the app, and my operating system would spit out, this: ### picture of python has crashed

Without even having done anything for months I'd somehow managed to crash Python. And let me tell you, I've seen a lot of unhelpful error messages in my relatively short time coding, I don't think this one will ever be topped. Going through the error log in Terminal was useless. It was all meaningless nonsense that I didn't understand, nor did googling any of it help. All I had to go on was "Python has crashed".
