# Problem set 4 (Vigenere)

## Parlez-vous francais?

* [Watch this video](http://cs50.tv/2012/fall/shorts/vigenere_cipher/vigenere_cipher-720p.mp4).

* Vigenere's cipher improves upon Caesar's by encrypting messages using a sequence of keys (or, put another way, a keyword). In other words, if _p_ is some plaintext and _k_ is a keyword (i.e., an alphbetical string, whereby `A` and `a` represent `0`, while `Z` and `z` represent 25), then each letter, _ci_, in the ciphertext, _c_, is computed as:

		ci = (pi + kj) % 26

  Note this cipher’s use of _kj_ as opposed to just _k_. And recall that, if _k_ is shorter than _p_, then the letters in _k_ must be reused cyclically as many times as it takes to encrypt _p_.

* Your challenge this week is to write, in `vigenere.c`, a program that encrypts messages using Vigenere's cipher. This program must accept a single command-line argument: a keyword, _k_, composed entirely of alphabetical characters. If your program is executed without any command-line arguments, with more than one command-line argument, or with one command-line argument that contains any non-alphabetical character, your program should complain and exit immediately, with `main` returning `1` (thereby signifying an error that our own tests can detect). Otherwise, your program must proceed to prompt the user for a string of plaintext, p, which it must then encrypt according to Vigenere's cipher with _k_, ultimately printing the result and exiting, with `main` returning `0`.

* As for the characters in _k_, you must treat `A` and `a` as `0`, `B` and `b` as `1`, ..., and `Z` and `z` as 25. In addition, your program must only apply Vigenere's cipher to a character in p if that character is a letter. All other characters (numbers, symbols, spaces, punctuation marks, etc.) must be outputted unchanged. Moreover, if your code is about to apply the jth character of _k_ to the ith character of p, but the latter proves to be a non-alphabetical character, you must wait to apply that jth character of k to the next alphabetical character in p; you must not yet advance to the next character in k. Finally, your program must preserve the case of each letter in _p_.

* Not sure where to begin? As luck would have it, this program’s pretty similar to `caesar.c`! Only this time, you need to decide which character in _k_ to use as you iterate from character to character in p.

* Need more help? [Watch this video.](http://www.youtube.com/watch?v=Uma2HZMPm2M)

* So that we can automate some tests of your code, your program must behave per the below.

		jharvard@appliance (~/Dropbox/pset4): ./vigenere bacon
		Meet me at the park at eleven am
		Negh zf av huf pcfx bt gzrwep oz

* How to test your program, besides predicting what it should output, given some input? You can use `check50` for that, but we’ve also written a program called `devigenere` that also takes one and only one command-line argument (a keyword) but whose job is to take ciphertext as input and produce plaintext as output.

  To use our program, execute

		~cs50/pset2/devigenere k
  
  at your prompt, where k is some keyword. Presumably you’ll want to paste your program’s output as input to our program; be sure, of course, to use the same key. Note that you do not need to implement `devigenere` yourself, only `vigenere`.

* A staff implementation and a `check50` command are available for this program. The commands are as follows:

		~cs50/pset2/vigenere
		check50 2013.pset2.vigenere vigenere.c

## Final steps

* When you are done with `vigenere.c`, submit it by going over to the **Submit** tab. Be sure to compile and test one last time before you submit.

* All done!
