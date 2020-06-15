---
layout: post
title: "python3 quit unexpectantly"
subtitle: An Adventure through the Most Useless of Error Messages
image: /img/SpiderPlot2.png
---

This is a story of how sometimes something you think is going to be simple to do in a computer ends up being horribly complicated and frustrating... and (debatably) not worth the effort.

Several months ago I was working on a project that would recommend songs on spotify based on one song given by the user. This was not a solo project, and we had one week to do it in, and almost finished, but ultimately did not. So, last month I decided to dust it off and finish it. 

To get you to understand this, we need to have a brief discussion on Python and Flask. If you know how Flask works, do please skip this paragraph and the next, you'll probably be bored to tears. This is a massive oversimplificatin, but all programming you do on your own personal computer is essentially trapped there. So, if you want to put a piece of code that will do whatever it's trying to do for people other than a person using your physical computer, without having that person run your code on their own computer, you have to figure out how to put that program onto the Internet, so other people can use it. And you already know the name for these: Web applications. Or, more colloquially: Apps. These aren't always the phone and computer apps you're probably super comfortable with. If you've ever seen an interactive graph or chart on a website that has a bunch of dials and bars that you can click on and change, and then see how those changes affect the chart, it is highly likely something like that was an app as I'm using the term here. 

Now, all you need to know now before our story can begin is that, in Python, the library that most people use to create web applications is called Flask. Flask is a way of packaging your program such that it can be deployed where other people can see it and use it.

Alright. Let's now discuss how I managed to crash Python using Flask. 

Several months ago I was working on an app that would use Spotify song data to make song recommendations based on just one other song that, presumabely, the app user liked. Now, I was working with a group of people, and we only had a week to finish it, and we failed. We got close, but ultimately we didn't get a working app up and running. However, last month I returned to it to finish it on my own. Well, sort of. I don't do user interface programming or web design, what I do do is data analysis, and part of the original team were a few members were web designers. So, lacking them and their skills, I tried to make a simplified version of the original goal. Rather than selecting a song that the database had information on (something that would require drop-down menus of some kind or something like that), I decided it would be enough, for me personally, if it would just take a randomly chosen song, and make recommendations based on that. Everytime you refresh the web page, the app would choose a new random song and make new recommendations. Dead simple, very little practical use, but I knew that that was something I could do, and so I decided to try and do it.

And here is the result (it will likely take a bit of time to load initially, but once it loads the first time, refreshing the app to see a new song will be much quicker):  https://curtcalledburt-song-suggestor.herokuapp.com/.

It's nothing that looks too flashy. The song the app randomly chose is in the one in green, and the three songs the machine has found closest to it are projected on top of that song.

Now, if you're thinking to yourself at this moment, "Wait, that's all it does?" Yeah, that's what I thought too at the start of this descent into madness. I decided to finish this app in particular because I thought it would be simple to finish, BUT, as is usual in the world of programming, the programmer I once was in the past screwed the current programmer I am now over, big time. 

Now that you've now seen the finished product, what state would you think I found this app in one month ago? More or less what you see here actually. The problem wasn't in anything that the program was doing, it was in getting that program to behave within a Flask app. Running each function we had written, individually, one after the other in a Jupyter notebook or just in the Terminal worked just fine. But, the moment we tried telling an app to run those funcitons, in that same order, bugs abounded. 

Something was going wrong in Flask, and that's quite an annoyance becuase, if there is only one critique I have of Flask it is this: I've yet to encounter any error message even remotely helpful in solving any error. I've lost track of the number of times I google a Flask error message only to see a bunch of onine message boards with swarms of people saying, "So, when Flask says "x, y, z" is the problem, it means "a, b, c" is actually occurring. Now, the data science team did eventually sort all of these issues with Flask and by the end did have a working app, but due to some major coordination issues within the team, we ran out of time, and couldn't make the jump from having a working app to putting it online on a web app hosting site like Heroku for people to click on and see and interact with.

And so the project lay fallow until I gave it a look some months later. When I returned, I expected to find it much in the same state we all left it in. Functional, would run on my local machine, but will fail to upload to web app hosting service. That didn't happen. Instead, it somehow managed to work even worse than before. Without changing any of the code for MONTHS somehow, SOMEHOW, it had managed to break down even further. 

Now, now, when I ran the (once working!) Flask app on my computer, the computer would think for a bit, until it shut down the app, and my operating system would spit out, this: 
![](/img/Python_has_Quit.png)

Without even having done anything for months I'd somehow managed to crash Python. I didn't even know that was a thing a person could do. I've seen a lot of unhelpful error messages, and I'm sure I'll see many more, but I don't think this one will ever be topped. 

And it wasn't just that the message that didn't help. Going through the error log in Terminal was useless. It was all meaningless nonsense that I didn't understand, nor did googling any of it help. The final kicker, and what sets it apart from every other error I've had was this: In every message I've ever seen, there is an expectation that the error message will at least give you a starting point of where to look for the bug. Sometimes where the error message says the problem is ocurring isn't the line of code you need to fix, that's fine, that's to be expected sometimes. But a message that says, "Error at line XXX" is great to give you a place to start looking.

This error didn't have that. 

You can look at the full thing: 
![](/img/Python_Has_Quit_Error.png)

Okay, so the most basic service of an error message is to tell you about where the problem is, so you don't have to comb EVERY LINE OF THE PROGRAM, and this error didn't provide it. Maybe it couldn't provide it, who knows? In hind sight that sort of makes sense. I mean, how is Python supposed to tell you on what line your code broke if it shuts down before it can do that?

So, I am 5 minutes into trying to resurrect a complicated app, with various functions, routes, and hundreds of lines of code, one or more of which was crashing Python, and the first problem I run into requires that I look at every line of code, individually, out of hundreds of line, that I wrote months ago, and ask myself, "Could this be the problem? And how?"

And the only help the computer gave me was "python3 has quit". I was not happy. Not one bit.

Take a moment to think about how you would find the bug in such a situation. How do you systematically check every line of code for a possible error, and make sure you don't miss it when you hit it? Because if you miss it, and it's likely a subtle bug, you may get to the end having missed it, and realize you have to look over every line, again. And maybe you'll miss it again.

So, if you're looking through a bug in a big program and you have no starting point to look, what do you do?

I hope you've come up with a better solution than mine, because the solution I offered in the previous paragraph with one addictional step: comment out every line of code after the one you are currently checking for bugs. If I just got rid of every line after the line I was currently looking at, and the error reappeared, then the error wasn't ocurring in lines before the one I was on, I'd already run the program with them uncommented and things were fine. And it couldn't be the lines after the current line, because as far as Python was concerned they didn't exist.

And I think this solution is... okay, as long as your program doesn't take ages to run, which, thankfully, this one did not. In cases where you are training models on massive amounts of data that can take hours to do, this method is obviously unfeasible. But in that case you'll likely be working with more people than just yourself and you can divide and conquer a bit more. But all by your lonesome? Not so much. Also, I was very frustrated with Python, so if there was anyway I could force my machine to do the bug checking that it was refusing to do in the first place, I was okay with it, even if it was barely better than brute force.

Okay, so, after commenting out every line of code after the first line of program, running the program, uncommenting the next line, and repeated for as long as necessary, where was the bug? It was in a function, unsurprisingly, most of the complex stuff that could go wrong was tucked away in functions, that plotted the results of the model. Which was surprising. It's quite a mundane thing to have A PYTHON CRASHING ERROR in. Especially when there is nothing complicated going on data-wise in it. It does some trigonometry to get the arcs of the spider plot the right size. It does a lot of fiddleing to get the ticks on the x and y axis in the right places (well, it's hard to describe what x and y mean in a polar grid, but... on second thought this is already too deep). In short! it does a lot of small, minute things to make a basic plot look pretty good. But all it's doing is plotting a graph. This is basic coding langauge stuff, so how in the hell is this CRASHING one of the most popular coding languages? And how is it that a GRAPH is failing so hard that Python couldn't even tell me that this was where the problem was occurring in the first place?

And this is the moment you are about to realize how hilariously fitting this all is. 

I worked on a few sections of the app with several people. Naturally there were parts of the app I didn't work on, but those were also the work of several people on the team. The whole app was a massive group effort. That is, all except one piece. Out of the several functions coded to make the app work, one function was the work of only one person in the group. 

You already know which function of course.
It was the spider plot function.

And you already know who coded it too.
It was me. 

Of course it was me!
How else could this story have possibly gone?

Let me tell you, learning that the me of several months ago had become the bane of the me of one month's ago existence was great fun. It was absolutely hilarious. Just PEACHY!

But really, could it have been more fitting? The guy who worked as hard as he could with a group to make something, only to fail in the end, returns to finish what he started only to realize that it was he, secretly, who it was that had sabotaged them all along, and then works to redeem himself and fix the failings of his past self!

You cannot write this level of stupidity!

Anyway, onto the actual bug. I still don't quite get what's going on, but it has to do with how matplotlib.pyplot (the library I was using to make the spider plot) interprets what you mean when you use "plt.whatever_you_want_to_plot" commands, and how it interprets actually making changes to a figure or subplot. I don't really know what that difference is. But I know this; using "plt.whatever_you_want_to_plot" commands inside a Flask app breaks something, somewhere, somehow. If you want Flask to create a figure in an app, actually create a matplotlib Figure, give it subplots, and then change and adjust those. 

For example, if you want to set the ticks on the y axis to be at certain points on your graph do NOT do this: 
![](/img/Change_Flask_Graph_Bad.png)

Instead, given a subplot (or axis) to a Figure object called "ax" make changes to the axis, or "ax," directly like so:
![](/img/Change_Flask_Graph_Good.png)

So, I just replaced the 5 or 6 places I had just used "plt.the_method_I_wanted" to their equivelent versions that act directly on a matplotlib figure, and that was it. The app worked after that. It was then I uploaded it to heroku where you can see it now.

I'm not sure what the moral of this story is yet, or indeed if it even has just one... or any at all really. But it might be to just be aware that, when coding, somehow, somewhere, somewhen, you will screw yourself over, and to learn to laugh at yourself when you do.
