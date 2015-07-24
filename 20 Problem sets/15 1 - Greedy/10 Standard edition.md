# Problem Set 1: Greedy

Questions?  Head to Slack or join classmates at office hours!

Let's ensure that the Appliance is up to date by running **update50** from a Terminal before starting.

# Objectives

* Get comfortable with Linux.

* Start thinking more carefully.

* Solve some problems in C.


# Time for Change

Speaking of money, "counting out change is a blast (even though it boosts mathematical skills) with this spring-loaded changer that you wear on your belt to dispense quarters, dimes, nickels, and pennies into your hand." Or so says the website on which we found this here accessory (for ages 5 and up).

  ![Picture of an awesome gadget](pset12.png)

Of course, the novelty of this thing quickly wears off, especially when someone pays for a newspaper with a big bill. Fortunately, computer science has given cashiers everywhere ways to minimize numbers of coins due: greedy algorithms.

According to the National Institute of Standards and Technology (NIST), a greedy algorithm is one "that always takes the best immediate, or local, solution while finding an answer. Greedy algorithms find the overall, or globally, optimal solution for some optimization problems, but may find less-than-optimal solutions for some instances of other problems."

What’s all that mean? Well, suppose that a cashier owes a customer some change and on that cashier’s belt are levers that dispense quarters, dimes, nickels, and pennies. Solving this "problem" requires one or more presses of one or more levers. Think of a "greedy" cashier as one who wants to take, with each press, the biggest bite out of this problem as possible. For instance, if some customer is owed 41¢, the biggest first (i.e., best immediate, or local) bite that can be taken is 25¢. (That bite is "best" inasmuch as it gets us closer to 0¢ faster than any other coin would.) Note that a bite of this size would whittle what was a 41¢ problem down to a 16¢ problem, since 41 - 25 = 16. That is, the remainder is a similar but smaller problem. Needless to say, another 25¢ bite would be too big (assuming the cashier prefers not to lose money), and so our greedy cashier would move on to a bite of size 10¢, leaving him or her with a 6¢ problem. At that point, greed calls for one 5¢ bite followed by one 1¢ bite, at which point the problem is solved. The customer receives one quarter, one dime, one nickel, and one penny: four coins in total.

It turns out that this greedy approach (i.e., algorithm) is not only locally optimal but also globally so for America’s currency (and also the European Union’s). That is, so long as a cashier has enough of each coin, this largest-to-smallest approach will yield the fewest coins possible.

How few? Well, you tell us. Write, in a file called `greedy.c` in your `~/Dropbox/pset1` directory, a program that first asks the user how much change is owed and then spits out the minimum number of coins with which said change can be made. Use `GetFloat` from the CS50 Library to get the user’s input and `printf` from the Standard I/O library to output your answer. Assume that the only coins available are quarters (25¢), dimes (10¢), nickels (5¢), and pennies (1¢).

We ask that you use `GetFloat` so that you can handle dollars and cents, albeit sans dollar sign. In other words, if some customer is owed $9.75 (as in the case where a newspaper costs 25¢ but the customer pays with a $10 bill), assume that your program’s input will be `9.75` and not `$9.75` or `975`. However, if some customer is owed $9 exactly, assume that your program’s input will be `9.00` or just `9` but, again, not `$9` or `900`. Of course, by nature of floating-point values, your program will likely work with inputs like `9.0` and `9.000` as well; you need not worry about checking whether the user’s input is "formatted" like money should be. And you need not try to check whether a user’s input is too large to fit in a `float`. But you should check that the user’s input makes cents! Er, sense. Using `GetFloat` alone will ensure that the user’s input is indeed a floating-point (or integral) value but not that it is non-negative. If the user fails to provide a non-negative value, your program should re-prompt the user for a valid amount again and again until the user complies.

Incidentally, do beware the inherent imprecision of floating-point values. For instance, `0.01` cannot be represented exactly as a float. Try printing its value to, say, `50` decimal places, with code like the below:

	float f = 0.01;
	printf("%.50f\n", f);

Before doing any math, then, you’ll probably want to convert the user’s input entirely to cents (i.e., from a `float` to an `int`) to avoid tiny errors that might otherwise add up! Of course, don’t just cast the user’s input from a `float` to an `int`! After all, how many cents does one dollar equal? And be careful to [round](https://cs50.harvard.edu/resources/cppreference.com/stdmath/round.html) and not truncate your pennies!

Not sure where to begin? Not to worry, start with a walkthrough:

<iframe width="711" height="400" src="http://www.youtube.com/embed/9dZzyl7dCuw" frameborder="0" allowfullscreen></iframe>

Incidentally, so that we can automate some tests of your code, we ask that your program’s last line of output be only the minimum number of coins possible: an integer followed by `\n`. Consider the below representative of how your own program should behave, wherein underlined text is some user’s input.

	jharvard@appliance (~/Dropbox/pset1): ./greedy
	O hai! How much change is owed?
	0.41
	4

By nature of floating-point values, that user could also have inputted just `.41`. (Were they to input `41`, though, they’d get many more coins!)

Of course, more difficult users might experience something more like the below.

	jharvard@appliance (~/Dropbox/pset1): ./greedy
	O hai! How much change is owed?
	-0.41
	How much change is owed?
	-0.41
	How much change is owed?
	foo
	Retry: 0.41
	4

Per these requirements (and the sample above), your code will likely have some sort of loop. If, while testing your program, you find yourself looping forever, know that you can kill your program (i.e., short-circuit its execution) by hitting ctrl-c (sometimes a lot).

We leave it to you to determine how to compile and run this particular program!

If you’d like to check the correctness of your program with **check50**, you may execute the below.

	check50 2014.fall.pset1.greedy greedy.c

And if you’d like to play with the staff’s own implementation of `greedy` in the appliance, you may execute the below.

	~cs50/pset1/greedy


# Final steps

* When you are done with `greedy.c`, submit it by going over to the [Submit](#submit) tab. Be sure to compile and test one last time before you submit.

* All done!