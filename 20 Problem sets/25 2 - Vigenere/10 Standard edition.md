Let's ensure that the Appliance is up to date by running **update50** from a Terminal before starting.

# Objectives

* Become better acquainted with functions and libraries.

* Dabble in cryptography.


# Parlez-vous français?

<iframe width="711" height="400" src="https://www.youtube.com/embed/9zASwVoshiM" frameborder="0" allowfullscreen></iframe>

Well that last cipher was hardly secure. Fortunately, per Nate’s short on Vigenère’s cipher, there’s a more sophisticated algorithm out there. Suffice it to say it’s French, per [http://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher](http://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher). Though do not be mislead by the article’s discussion of a tabula recta. Each ci can be computed with relatively simple arithmetic! You do not need a two-dimensional array.

Vigenère’s cipher improves upon Caesar’s by encrypting messages using a sequence of keys (or, put another way, a keyword). In other words, if *p* is some plaintext and *k* is a keyword (i.e., an alphbetical string, whereby `A` and `a` represent 0, while `Z` and `z` represent 25), then each letter, *c<sub>i</sub>*, in the ciphertext, *c*, is computed as:

* c<sub>i</sub> = (p<sub>i</sub> + k<sub>j</sub>) % 26

Note this cipher’s use of *k<sub>j</sub>* as opposed to just *k*. And recall that, if *k* is shorter than *p*, then the letters in *k* must be reused cyclically as many times as it takes to encrypt *p*.

Your challenge this week is to write, in `vigenere.c`, a program that encrypts messages using Vigenère’s cipher. This program must accept a single command-line argument: a keyword, *k*, composed entirely of alphabetical characters. If your program is executed without any command-line arguments, with more than one command-line argument, or with one command-line argument that contains any non-alphabetical character, your program should complain and exit immediately, with main returning `1` (thereby signifying an error that our own tests can detect). Otherwise, your program must proceed to prompt the user for a string of plaintext, *p*, which it must then encrypt according to Vigenère’s cipher with *k*, ultimately printing the result and exiting, with `main` returning `0`.

As for the characters in *k*, you must treat `A` and `a` as 0, `B` and `b` as 1, … , and `Z` and `z` as 25. In addition, your program must only apply Vigenère’s cipher to a character in *p* if that character is a letter. All other characters (numbers, symbols, spaces, punctuation marks, etc.) must be outputted unchanged. Moreover, if your code is about to apply the *j<sup>th</sup>* character of *k* to the *i<sup>th</sup>* character of *p*, but the latter proves to be a non-alphabetical character, you must wait to apply that *j<sup>th</sup>* character of *k* to the next alphabetical character in *p*; you must not yet advance to the next character in *k*. Finally, your program must preserve the case of each letter in *p*.

Not sure where to begin? As luck would have it, this program’s pretty similar to `caesar`! Only this time, you need to decide which character in *k* to use as you iterate from character to character in *p*.

And here’s Zamyla again with some tips:

<iframe width="711" height="400" src="https://www.youtube.com/embed/Uma2HZMPm2M" frameborder="0" allowfullscreen></iframe>

So that we can automate some tests of your code, your program must behave per the below; highlighted in bold are some sample inputs.

	jharvard@appliance (~/Dropbox/pset2): ./vigenere bacon
	Meet me at the park at eleven am
	Negh zf av huf pcfx bt gzrwep oz

How to test your program, besides predicting what it should output, given some input? Well, recall that we’re nice people. And so we’ve written a program called `devigenere` that also takes one and only one command-line argument (a keyword) but whose job is to take ciphertext as input and produce plaintext as output.

To use our program, execute

	~cs50/pset2/devigenere k

at your prompt, where **k** is some keyword. Presumably you’ll want to paste your program’s output as input to our program; be sure, of course, to use the same key. Note that you do not need to implement `devigenere` yourself, only `vigenere`.

If you’d like to check the correctness of your program with **check50**, you may execute the below.

	check50 2014.fall.pset2.vigenere vigenere.c

And if you’d like to play with the staff’s own implementation of `vigenere` in the appliance, you may execute the below.

	~cs50/pset2/vigenere


# Final steps

* When you are done with `vigenere.c`, submit it by going over to the [Submit](#submit) tab. Be sure to compile and test one last time before you submit.

* All done!