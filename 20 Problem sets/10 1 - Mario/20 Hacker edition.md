*Please consult your teaching fellow before attempting any hacker edition!*

# About hacker's editions

* Hacker's editions offer more difficult challenges than normal editions, and offers less guidance than the normal editions do. While we would advise most anyone to choose the normal editions, if you're up for a challenge, definitely try out the hacker's edition! If you get stuck in a hacker's edition, odds are you'll find some useful tips in the normal edition's walkthroughs!

* You're free to switch between normal and hacker editions each week. Note that you're **not allowed** to submit a mix between normal and hacker edition problem sets. Either submit a full normal edition or a full hacker edition, and not an amalgam of both.


# Itsa Mario

For this hackers edition implement the normal edition, only with a twist:

* Instead of just one pyramid, print two pyramids as per the specification and image below. 


# Complete specification

Toward the beginning of World 1-1 in Nintendo’s Super Mario Brothers, Mario must hop over two "half-pyramids" of blocks as he heads toward a flag pole. Below is a screenshot.

  ![Mario!](pset13.png)

Write, in a file called `mario.c` in your `~/Dropbox/hacker1` directory, a program that recreates these half-pyramids using hashes (`#`) for blocks. However, to make things more interesting, first prompt the user for the half-pyramids' heights, a non-negative integer no greater than `23`. (The height of the half-pyramids pictured above happens to be `4`, the width of each half-pyramid `4`, with an a gap of size `2` separating them.) Then, generate (with the help of `printf` and one or more loops) the desired half-pyramids. Take care to left-align the bottom-left corner of the left-hand half-pyramid, as in the sample output below, wherein boldfaced text represents some user’s input.

	jharvard@appliance (~/Dropbox/hacker1): ./mario
	Height: 4
	   #  #
	  ##  ##
	 ###  ###
	####  ####

No need to generate the bricks, cloud, numbers, or text in the sky or Mario himself. Just the half-pyramids! And be sure that main returns `0`.

We leave it to you to determine how to compile and run this particular program!

If you’d like to check the correctness of your program with check50, you may execute the below.

	check50 2014.fall.hacker1.mario mario.c

And if you’d like to play with the staff’s own implementation of mario in the appliance, you may execute the below.

	~cs50/hacker1/mario



# Final steps

* When you are done with `mario.c`, submit it by going over to the [Submit](#submit) tab. Be sure to compile and test one last time before you submit. (Note that you do not have to submit `hello.c`.)

* All done!