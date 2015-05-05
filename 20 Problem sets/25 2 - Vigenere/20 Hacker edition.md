*Please consult your teaching fellow before attempting any hacker edition!*

Let's ensure that the Appliance is up to date by running `update50` from a Terminal before starting.


# Passwords Et Cetera

On most, if not all, systems running Linux or UNIX is a file called `/etc/passwd`. By design, this file is meant to contain usernames and passwords, along with other account-related details (e.g., paths to users' home directories and shells). Also by (poor) design, this file is typically world-readable. Thankfully, the passwords therein aren’t stored "in the clear" but are instead encrypted using a "one-way hash function." When a user logs into these systems by typing a username and password, the latter is encrypted with the very same hash function, and the result is compared against the username’s entry in `/etc/passwd`. If the two ciphertexts match, the user is allowed in. If you’ve ever forgotten some password, you may have been told that "I can’t look up your password, but I can change it for you." It could be that person doesn’t know how. But, odds are they just can’t if a one-way hash function’s involved.

Even though passwords in `/etc/passwd` are encrypted, the crypto involved is not terribly strong. Quite often are adversaries, upon obtaining files like this one, able to guess (and check) users' passwords or crack them using brute force (i.e., trying all possible passwords). Only in recent years have (most) system administrators stopped storing passwords in `/etc/passwd`, instead using `/etc/shadow`, which is (supposed to be) readable only by root. (Take a look at `/etc/passwd` in the appliance, for instance; wherever you see `x` a password once was.) Below, though, are some `username:ciphertext` [pairs](passwd) from an outdated (fake) system.

	belindazeng:50q/EEJnOmtxc
	caesar:50zPJlUFIYY0o
	jharvard:50yoN9fp966dU
	malan:50q.zrL5e0Sak
	rob:HAYRs6vZAb4wo
	zamyla:50NwUtF.OmQNY

Crack these passwords, each of which has been encrypted with C’s DES-based (not MD5-based) crypt function. Specifically, write, in `crack.c`, a program that accepts a single command-line argument: an encrypted password. (In case you test your code with other ciphertexts, know that command-line arguments with certain characters (e.g., `?`) must be enclosed in single or double quotes; those quotation marks will not end up in `argv` itself.) If your program is executed without any command-line arguments or with more than one command-line argument, your program should complain and exit immediately, with `main` returning any non-zero `int` (thereby signifying an error that our own tests can detect). Otherwise, your program must proceed to crack the given password, ideally as quickly as possible, ultimately printing to standard output the password in the clear followed by `\n`, nothing more, nothing less, with `main` returning `0`. The underlying design of this program is entirely up to you, but you must explain each and every one of your design decisions, including any implications for performance and accuracy, with profuse comments throughout your source code. Your program must be designed in such a way that it could crack all of the passwords above, even if said cracking might take quite a while. That is to say, it’s okay if your code might take several minutes or days or longer to run. What we demand of you is correctness, not necessarily optimal performance. Your program should certainly work on inputs other than these as well; hard-coding into your program the solutions to the above is not acceptable.

Your program must behave per the below; underlined is some sample input.

	jharvard@appliance (~/Dropbox/hacker2): ./crack 50yoN9fp966dU
	crimson

Assume that users' passwords, as plaintext, are composed of [printable ASCII characters](http://en.wikipedia.org/wiki/ASCII#ASCII_printable_characters) and are no longer than eight characters long. As for their ciphertexts, you’d best pull up the "man page" (i.e., manual) for `crypt` by executing

	man crypt

in a terminal window so that you know how the function works. In particular, make sure you understand its use of a "salt." (According to the man page, a salt "is used to perturb the algorithm in one of 4096 different ways," but why might that be useful?) As implied by that man page, you’ll likely want to put

	#define _XOPEN_SOURCE
	#include <unistd.h>

at the top of your file. Moreover, you’ll want to link with **-lcrypt**, as by compiling not with **make** but with:

	clang -o crack crack.c -lcrypt

You might also want to read up on C’s support for file I/O, as there’s quite a number of English words in `/usr/share/dict/words` in the appliance that might (or might not) save your program some time.

By design, `/etc/passwd` entrusts the security of passwords to an assumption: that adversaries lack the computational resources with which to crack those passwords. Once upon a time, that may have been true. Perhaps some still do. But when it comes to security, assumptions are dangerous. May that this problem set make that claim all the more real.

We should note that this problem set is no invitation to seek out other passwords to crack. Do not conflate these Hacker Editions with "black hat" editions. We hope, though, that by understanding better the design of today’s systems, you might one day build better systems yourself. Besides acquainting you further with C, this problem set urges you to start questioning designs, as vulnerabilities (if not regrets) often result from poor ones.

If you’d like to play with the staff’s own implementation of `crack`, well, sorry! :-) Where’d be the fun in that?


# Final steps

* When you are done with `crack.c`, submit it by going over to the [Submit](#submit) tab. Be sure to compile and test one last time before you submit.

* All done!