Let's ensure that the Appliance is up to date by running **update50** from a Terminal before starting.

# Objectives

* Become better acquainted with functions and libraries.

* Dabble in cryptography.


# Getting Ready

First, curl up with these shorts on loops, functions, Caesar’s cipher, and command-line arguments:

<iframe width="711" height="400" src="https://www.youtube.com/embed/HHmiHx7GGLE" frameborder="0" allowfullscreen></iframe>

Be sure you’re reasonably comfortable answering the below when it comes time to submit this problem set’s form!

* How does a while loop differ from a do-while loop? When is the latter particularly useful?

* What does **undeclared identifier** usually indicate if outputted by **make** (or, really, **clang**)?

* Why is Caesar’s cipher not very secure?

* What’s a function?

* Why bother writing functions when you can just copy and paste code as needed?

Next, take a self-paced tour through Week 2’s examples, the source code for which can be found at [http://cdn.cs50.net/2014/fall/lectures/2/m/src2m/](http://cdn.cs50.net/2014/fall/lectures/2/m/src2m/) and [http://cdn.cs50.net/2014/fall/lectures/2/w/src2w/](http://cdn.cs50.net/2014/fall/lectures/2/w/src2w/), fast-forwarding through any programs with which you’re already comfortable:

<iframe width="711" height="400" src="https://www.youtube.com/embed/9zoRoz8Pq4E?list=PLhQjrBD2T380bVx_CQ2EXtlqZh0frwOsn" frameborder="0" allowfullscreen></iframe>

Finally, take a closer look at command-line arguments by way of these additional examples from Week 3, the source code for which can be found at [http://cdn.cs50.net/2014/fall/lectures/3/m/src3m/](http://cdn.cs50.net/2014/fall/lectures/3/m/src3m/):

<iframe width="711" height="400" src="https://www.youtube.com/embed/1VbHJz2L6dM" frameborder="0" allowfullscreen></iframe>

# Getting Started

Alright, here we go again!

Open a terminal window if not open already (as via *Menu* > *Accessories* > *gedit* or via *Menu* > *Accessories* > *Terminal*). Then execute

	update50

to make sure your appliance is up-to-date. In general, if you run into errors like "No such file or directory" with the staff’s solutions, best to re-run **update50**, just to make sure you have the latest updates.

Next, execute

	mkdir ~/Dropbox/pset2

to move yourself into (i.e., open) that directory. Your prompt should now resemble the below.

	jharvard@appliance (~/Dropbox/pset2):

If not, retrace your steps and see if you can determine where you went wrong. You can actually execute

	history

at the prompt to see your last several commands in chronological order if you’d like to do some sleuthing. You can also scroll through the same one line at a time by hitting your keyboard’s up and down arrows; hit Enter to re-execute any command that you’d like.


# Initializing

Alright, let’s get more comfortable with `string`.

Write, in a file called `initials.c`, a program that prompts a user for their name (using `GetString` to obtain their name as a `string`) and then outputs their initials in uppercase with no spaces or periods, followed by a newline (`\n`) and nothing more. You may assume that the user’s input will contain only letters (uppercase and/or lowercase) plus single spaces between words. Folks like `Joseph Gordon-Levitt`, `Conan O’Brien`, and `David J. Malan` won’t be using your program.

So that we can automate some tests of your code, your program must behave per the examples below. Assumed that the underlined text is what some user has typed.

	jharvard@appliance (~/Dropbox/pset2): ./initials
	Zamyla Chan
	ZC
	jharvard@appliance (~/Dropbox/pset2): ./initials
	robert thomas bowden
	RTB

If you’d like to check the correctness of your program with **check50**, you may execute the below.

	check50 2014.fall.pset2.initials initials.c

And if you’d like to play with the staff’s own implementation of `initials` in the appliance, you may execute the below.

~cs50/pset2/initials


# Hail, Caesar!

Recall from David DiCiurcio’s short that Caesar’s cipher encrypts (i.e., scrambles in a reversible way) messages by "rotating" each letter by k positions, wrapping around from `Z` to `A` as needed (cf. [http://en.wikipedia.org/wiki/Caesar_cipher](http://en.wikipedia.org/wiki/Caesar_cipher)). In other words, if *p* is some plaintext (i.e., an unencrypted message), p<sub>i</sub> is the i<sup>th</sup> character in p, and k is a secret key (i.e., a non-negative integer), then each letter, c<sub>i</sub>, in the ciphertext, c, is computed as:

* c<sub>i</sub> = (p<sub>i</sub> + k) % 26

This formula perhaps makes the cipher seem more complicated than it is, but it’s really just a nice way of expressing the algorithm precisely and concisely. And computer scientists love precision and, er, concision.

For example, suppose that the secret key, k, is 13 and that the plaintext, p, is "Be sure to drink your Ovaltine!" Let’s encrypt that p with that k in order to get the ciphertext, c, by rotating each of the letters in p by 13 places, whereby:

	Be sure to drink your Ovaltine!

becomes:

	Or fher gb qevax lbhe Binygvar!

We’ve deliberately printed the above in a monospaced font so that all of the letters line up nicely. Notice how `O` (the first letter in the ciphertext) is 13 letters away from `B` (the first letter in the plaintext). Similarly is `r` (the second letter in the ciphertext) 13 letters away from `e` (the second letter in the plaintext). Meanwhile, `f` (the third letter in the ciphertext) is 13 letters away from `s` (the third letter in the plaintext), though we had to wrap around from `z` to `a` to get there. And so on. Not the most secure cipher, to be sure, but fun to implement!

Incidentally, a Caesar cipher with a key of 13 is generally called ROT13 (cf. [http://en.wikipedia.org/wiki/ROT13](http://en.wikipedia.org/wiki/ROT13)). In the real world, though, it’s probably best to use ROT26, [which is believed to be twice as secure](http://www.urbandictionary.com/define.php?term=ROT26).

Anyhow, your next goal is to write, in `caesar.c`, a program that encrypts messages using Caesar’s cipher. Your program must accept a single command-line argument: a non-negative integer. Let’s call it *k* for the sake of discussion. If your program is executed without any command-line arguments or with more than one command-line argument, your program should yell at the user and return a value of `1` (which tends to signify an error) immediately as via the statement below:

	return 1;

Otherwise, your program must proceed to prompt the user for a string of plaintext and then output that text with each alphabetical character "rotated" by *k* positions; non-alphabetical characters should be outputted unchanged. After outputting this ciphertext, your program should exit, with `main` returning `0`, as via the statement below:

	return 0;

If you don’t explicitly return an `int` from within `main`, `0` is actually returned for you automatically. (Indeed, per its "return type," `main` does need to return an `int`. But more on that another time.) Now that you’re returning `1` explicitly to signify errors, it’s best to return `0` (by convention) explicitly to signify success. Whereas `0` generally represents success, any non-`0` `int` generally represents an error. That way, you can represent (gasp) upwards of four billion errors (since an `int` is generally 32 bits)!

Anyhow, even though there exist only 26 letters in the English alphabet, you may not assume that *k* will be less than or equal to 26; your program should work for all non-negative integral values of *k* less than 231 - 26. (In other words, you don’t need to worry if your program eventually breaks if the user chooses a value for *k* that’s too big or almost too big to fit in an `int`. Now, even if *k* is greater than 26, alphabetical characters in your program’s input should remain alphabetical characters in your program’s output. For instance, if *k* is 27, `A` should not become `[` even though `[` is 27 positions away from `A` in ASCII; `A` should become `B`, since 27 modulo 26 is 1, as a computer scientists might say. In other words, values like k = 1 and k = 27 are effectively equivalent.

Your program must preserve case: capitalized letters, though rotated, must remain capitalized letters; lowercase letters, though rotated, must remain lowercase letters.

Where to begin? Well, this program needs to accept a command-line argument, k, so this time you’ll want to declare `main` with:

	int main(int argc, string argv[])

Recall that `argv` is an "array" of strings. You can think of an array as row of gym lockers, inside each of which is some value (and maybe some socks). In this case, inside each such locker is a `string`. To open (i.e., "index into") the first locker, you use syntax like `argv[0]`, since arrays are "zero-indexed." To open the next locker, you use syntax like `argv[1]`. And so on. Of course, if there are `n` lockers, you’d better stop opening lockers once you get to `argv[n - 1]`, since `argv[n]` doesn’t exist! (That or it belongs to someone else, in which case you still shouldn’t open it.)

And so you can access *k* with code like

	string k = argv[1];

assuming it’s actually there! Recall that `argc` is an `int` that equals the number of strings that are in `argv`, so you’d best check the value of `argc` before opening a locker that might not exist! Ideally, `argc` will be `2`. Why? Well, recall that inside of `argv[0]`, by default, is a program’s own name. So `argc` will always be at least `1`. But for this program you want the user to provide a command-line argument, `k`, in which case `argc` should be `2`. Of course, if the user provides more than one command-line argument at the prompt, `argc` could be greater than `2`, in which case it’s time for some yelling.

Now, just because the user types an integer at the prompt, that doesn’t mean their input will be automatically stored in an `int`. Au contraire, it will be stored as a `string` that just so happens to look like an `int`! And so you’ll need to convert that string to an actual int. As luck would have it, a function, `atoi`, exists for exactly that purposes. Here’s how you might use it:

	int k = atoi(argv[1]);

Notice, this time, we’ve declared `k` as an actual `int` so that you can actually do some arithmetic with it. Ah, much better. Incidentally, you can assume that the user will only type integers at the prompt. You don’t have to worry about them typing, say, `foo`, just to be difficult (even though the staff’s solution does catch such); `atoi` will just return `0` in such cases.

Because `atoi` is declared in `stdlib.h`, you’ll want to `#include` that header file atop your own code. (Technically, your code will compile without it there, since we already `#include` it in `cs50.h`. But best not to trust another library to `#include` header files you know you need.)

Okay, so once you’ve got `k` stored as an `int`, you’ll need to ask the user for some plaintext. Odds are CS50’s own `GetString` can help you with that.

Once you have both `k` and some plaintext, it’s time to encrypt the latter with the former. Recall that you can iterate over the characters in a string, printing each one at a time, with code like the below:

	for (int i = 0, n = strlen(p); i < n; i++)
	{
	    printf("%c", p[i]);
	}

In other words, just as `argv` is an array of strings, so is a `string` an array of chars. And so you can use square brackets to access individual characters in strings just as you can individual strings in `argv`. Neat, eh? Of course, printing each of the characters in a string one at a time isn’t exactly cryptography. Well, maybe technically if *k* is 0. But the above should help you help Caesar implement his cipher! For Caesar!

Incidentally, you’ll need to `#include` yet another header file in order to use `strlen`.

And Zamyla has some tips for you as well:

<iframe width="711" height="400" src="https://www.youtube.com/embed/V6IDxl-3WAA" frameborder="0" allowfullscreen></iframe>

So that we can automate some tests of your code, your program must behave per the below. Assumed that the underlined text is what some user has typed.

	jharvard@appliance (~/Dropbox/pset2): ./caesar 13
	Be sure to drink your Ovaltine!
	Or fher gb qevax lbhe Binygvar!

Besides `atoi`, you might find some handy functions documented at [https://reference.cs50.net/](https://reference.cs50.net/) under *ctype.h* and *stdlib.h*. For instance, `isdigit` sounds interesting. And, with regard to wrapping around from `Z` to `A` (or `z` to `a`), don’t forget about `%`, C’s modulo operator. You might also want to check out [http://asciitable.com/](http://asciitable.com/), which reveals the ASCII codes for more than just alphabetical characters, just in case you find yourself printing some characters accidentally.

If you’d like to check the correctness of your program with **check50**, you may execute the below.

	check50 2014.fall.pset2.caesar caesar.c

And if you’d like to play with the staff’s own implementation of `caesar` in the appliance, you may execute the below.

	~cs50/pset2/caesar

BTW, `uggc://jjj.lbhghor.pbz/jngpu?i=bUt5FWLEUN0`.


# Final steps

* When you are done with `caesar.c`, submit it by going over to the [Submit](#submit) tab. Be sure to compile and test one last time before you submit. (Note that you do not have to submit `initials.c`.)

* All done!