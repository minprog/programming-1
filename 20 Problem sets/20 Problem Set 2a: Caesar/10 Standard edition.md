# Problem set 3 (Caesar)

## Getting started

* Watch these videos: [loops](http://cs50.tv/2012/fall/shorts/loops/loops-720p.mp4), [scope](http://cs50.tv/2012/fall/shorts/scope/scope-720p.mp4), [Caesar's cipher](http://cs50.tv/2012/fall/shorts/caesar_cipher/caesar_cipher-720p.mp4), [command-line arguments](http://cs50.tv/2012/fall/shorts/command_line_arguments/command_line_arguments-720p.mp4).

## Initials

* Open up your terminal, head to your desktop, and create a new `pset3` folder with a file named `initials.c` in it. If you forgot how, here are the commands:

		cd Desktop
		mkdir pset3
		cd pset3
		touch initials.c

* Then open the newly created file using `gedit`:

		gedit initials.c

* Go to [this playlist](http://www.youtube.com/playlist?list=PLhQjrBD2T383LBd7z_5k32rbPdO99LNB9) and watch `string-0`, `string-1`, and `string-2`. Then watch `capitalize-0`, `capitalize-1`, and `capitalize-2`. Feel free to watch any other walkthroughs of interest.

* Next, write, in a file called `initials.c`, a program that prompts a user for their name (using `GetString` to obtain their name as a string) and then outputs their initials in uppercase with no spaces or periods, followed by a newline (`\n`) and nothing more. You may assume that the user's input will contain only letters (uppercase and/or lowercase) plus single spaces between words. Folks like `Joseph Gorden-Levitt`, `Conan O'Brien`, and `R.J. Aquino` won't be using your program.

* So that we can automate some tests of your code, your program must behave per the examples below. Assumed that the underlined text is what some user has typed.

		jharvard@appliance (~/Dropbox/pset3): ./initials
		Milo Banana
		MB

		jharvard@appliance (~/Dropbox/pset3): ./initials
		robert thomas bowden
		RTB

* If you’d like to check the correctness of your program with `check50`, you may execute the below.

		check50 2013.pset2.initials initials.c

* And if you’d like to play with the staff’s own implementation of initials in the appliance, you may execute the below.

		~cs50/pset2/initials

* You do not need to submit `initials.c` for grading.

## Hail, Caesar!

* Recall from David DiCiurcio’s short that Caesar’s cipher encrypts (i.e., scrambles in a reversible way) messages by "rotating" each letter by _k_ positions, wrapping around from `Z` to `A` as needed (cf. [Wikipedia](http://en.wikipedia.org/wiki/Caesar_cipher)).

* For example, suppose that the secret key, k, is 13 and that the plaintext, p, is "Be sure to drink your Ovaltine!" Let’s encrypt that p with that k in order to get the ciphertext, c, by rotating each of the letters in p by 13 places, whereby

		Be sure to drink your Ovaltine!

  becomes

		Or fher gb qevax lbhe Binygvar!

* We’ve deliberately printed the above in a monospaced font so that all of the letters line up nicely. Notice how `O` (the first letter in the ciphertext) is 13 letters away from `B` (the first letter in the plaintext). Similarly is `r` (the second letter in the ciphertext) 13 letters away from `e` (the second letter in he plaintext). Meanwhile, `f` (the third letter in the ciphertext) is 13 letters away from `s` (the third letter in the plaintext), though we had to wrap around from `z` to `a` to get there. And so on. Not the most secure cipher, to be sure, but fun to implement!

* Incidentally, a Caesar cipher with a key of 13 is generally called ROT13 (cf. [Wikipedia](http://en.wikipedia.org/wiki/ROT13)). In the real world, though, it’s probably best to use ROT26, which is believed to be [twice as secure](http://www.urbandictionary.com/define.php?term=ROT26).

* Anyhow, your next goal is to write, in `caesar.c`, a program that encrypts messages using Caesar’s cipher. Your program must accept a single command-line argument: a non-negative integer. Let’s call it k for the sake of discussion. If your program is executed without any command-line arguments or with more than one command-line argument, your program should yell at the user and return a value of `1` (which tends to signify an error) immediately as via the statement below:

		return 1;

* Otherwise, your program must proceed to prompt the user for a string of plaintext and then output that text with each alphabetical character "rotated" by k positions; non-alphabetical characters should be outputted unchanged. After outputting this ciphertext, your program should exit, with main returning `0`.

* Although there exist only 26 letters in the English alphabet, you may not assume that k will be less than or equal to 26; your program should work for all non-negative integral. However, you don't need to worry about the case in which the user provides an integer that is too large or almost too large to fit inside an `int`. Now, even if k is greater than 26, alphabetical characters in your program’s input should remain alphabetical characters in your program’s output. For instance, if k is 27, `A` should not become `[` even though `[` is 27 positions away from `A`in ASCII; `A` should become `B`, since 27 modulo 26 is 1, as a computer scientists might say. In other words, values like _k = 1_ and _k = 27_ are effectively equivalent.

* Your program must preserve case: capitalized letters in the input string should remain capitalized in the encoded string. The same applies to lowercase strings.

* Where to begin? Well, this program needs to accept a command-line argument, k, so this time you’ll want to declare main with:

		int main(int argc, string argv[])

* Recall that argv is an "array" of string's. You can think of an array as row of gym lockers, inside each of which is some value (and maybe some socks). In this case, inside each such locker is a string. To open (i.e., "index into") the first locker, you use syntax like `argv[0]`, since arrays are "zero-indexed." To open the next locker, you use syntax like `argv[1]`. And so on. Of course, if there are `n` lockers, you’d better stop opening lockers once you get to `argv[n - 1]`, since `argv[n]` doesn’t exist! (That or it belongs to someone else, in which case you still shouldn’t open it.)

  And so you can access k with code like

		string k = argv[1];

  assuming it’s actually there! Recall that `argc` is an `int` that equals the number of strings that are in `argv`, so you’d best check the value of `argc` before opening a locker that might not exist! Ideally, `argc` will be `2`. Why? Well, recall that inside of `argv[0]`, by default, is a program’s own name. So `argc` will always be at least `1`. But for this program you want the user to provide a command-line argument, k, in which case `argc` should be `2`. Of course, if the user provides more than one command-line argument at the prompt, `argc` could be greater than `2`, in which case it’s time for some yelling.

* Now, just because the user types an integer at the prompt, that doesn’t mean their input will be automatically stored in an `int`. Au contraire, it will be stored as a string that just so happens to look like an int! And so you’ll need to convert that string to an actual `int`. As luck would have it, a function, `atoi`, exists for exactly that purposes. Here’s how you might use it:

		int k = atoi(argv[1]);

* Notice, this time, we’ve declared k as an actual `int` so that you can actually do some arithmetic with it. Ah, much better. Incidentally, you can assume that the user will only type integers at the prompt. You don’t have to worry about them typing, say, foo, just to be difficult (even though the staff’s solution does catch such); `atoi` will just return `0` in such cases.

* Because `atoi` is declared in `stdlib.h`, you’ll want to `#include` that header file atop your own code. (Technically, your code will compile without it there, since we already `#include` it in `cs50.h`. But best not to trust another library to `#include` header files you know you need.)

* Okay, so once you’ve got k stored as an `int`, you’ll need to ask the user for some plaintext. Odds are CS50’s own `GetString` can help you with that.

* Once you have both k and some plaintext, it’s time to encrypt the latter with the former. Recall that you can iterate over the characters in a string, printing each one at a time, with code like the below:

		for (int i = 0, n = strlen(p); i < n; i++)
		{
		    printf("%c", p[i]);
		}

  In other words, just as `argv` is an array of strings, so is a string an array of `char`s. And so you can use square brackets to access individual characters in `string`s just as you can individual `string`s in `argv`.  Neat, eh? Of course, printing each of the characters in a string one at a time isn’t exactly cryptography. Well, maybe technically if k is `0`. But the above should help you help Caesar implement his cipher! For Caesar!

  Incidentally, you’ll need to `#include` yet another header file in order to use `strlen`.

* For some help with this program, you can  [watch this video](http://www.youtube.com/watch?v=V6IDxl-3WAA).

* So that we can automate some tests of your code, your program must behave per the below. Assumed that the underlined text is what some user has typed.

		jharvard@appliance (~/Dropbox/pset3): ./caesar 13
		Be sure to drink your Ovaltine!
		Or fher gb qevax lbhe Binygvar!

* Besides `atoi`, you might find several other functions of use. For instance, the function `isdigit` sounds interesting for handling user input with regards to the key. Also, don't forget about `%`, C's modulo operator. You'll surely need it! Finally, [this website](http://asciitable.com/) has a useful diagram of the ASCII table.

* A staff implementation and a `check50` command are available for this program. The commands are as follows:

		~cs50/pset2/caesar
		check50 2013.pset2.caesar caesar.c

## Final steps

* When you are done with `caesar.c`, submit it by going over to the **Submit** tab. Be sure to compile and test one last time before you submit. (Note that you do not have to submit `initials.c`.)

* All done!
