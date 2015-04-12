*Please consult your teaching fellow before attempting any hacker edition!*

# Crack

* Let's ensure that the Appliance is up to date by running `update50` from a Terminal before starting.

## Passwords

* On most, if not all, systems running Linux or UNIX is a file called `/etc/passwd`. By design, this file is meant to contain usernames and passwords, along with other account-related details (e.g., paths to users' home directories and shells). Also by (poor) design, this file is typically world-readable. Thankfully, the passwords therein aren't stored "in the clear" but are instead encrypted using a "one-way hash function." When a user logs into these systems by typing a username and password, the latter is encrypted with the very same hash function, and the result is compared against the username's entry in /etc/passwd. If the two ciphertexts match, the user is allowed in. If you've ever forgotten some password, you may have been told that "I can't look up your password, but I can change it for you." It could be that person doesn't know how. But, odds are they just can't if a one-way hash function's involved.

* Even though passwords in `/etc/passwd` are encrypted, the crypto involved is not terribly strong. Quite often are adversaries, upon obtaining files like this one, able to guess (and check) users' passwords or crack them using brute force (i.e., trying all possible passwords). Only in recent years have (most) system administrators stopped storing passwords in `/etc/passwd`, instead using `/etc/shadow`, which is (supposed to be) readable only by root. (Take a look at `/etc/passwd` in the appliance, for instance; wherever you see x a password once was.) Below, though, are some username:ciphertext pairs from an outdated (fake) system.

		caesar:50zPJlUFIYY0o
		hirschhorn:50q.zrL5e0Sak
		jharvard:50yoN9fp966dU
		malan:HA610l/.LeOak
		milo:HAL7ye0Ms7wZY
		zamyla:50NwUtF.OmQNY

* Many people often like to use real words as their passwords, as they are easy to remember. Adversaries often make use of this fact by first trying out a so-called dictionary attack; rather than brute-forcing all possibilities, they try out (common) words first. Only when this doesn't work out, they resort to the brute-force method previously mentioned.
  
* Write a program called `crack.c` that implements a dictionary lookup using the words from a raw text file containing words, which is located at `~cs50/pset6/dictionaries/large` inside your appliance. Read in all of the words in this file and try each one of them on the password.
  
* Then, expand your `crack.c` program with a brute-force attack in case the password cannot be cracked using your dictionary attack. (To be clear, your program must always first attempt the dictionary lookup, and only when that doesn't work out, it should resort to the brute-force method.)
  
* You will want to include these two lines atop your code:
  
		#define _XOPEN_SOURCE
		#include <unistd.h>

  Ensure that the `#define _XOPEN_SOURCE` is above the inclusion of `unistd.h`, or you'll run into trouble when compiling!

* In addition, you'll need to compile with the `-lcrypt` switch. Note that the standard `make` command in the Appliance does not include this switch for you!

* Your program must work per the below (e.g. it must only print the cracked password and nothing else). It should return `0` on success.

		jharvard@appliance (~/Dropbox/hacker4): ./crack 50yoN9fp966dU
		crimson

* Dictionary lookups perform quite fast, but brute-force cracking methods may take several days or, if the password is long enough, several years! That being said, it is OK if the program runs exceptionally long before it finds a solution, as long as the program's code is syntactically correct.

* There's no example solution or `check50` available for this program. (But you can use `style50`.)

## Final steps

* When you are done with `crack.c`, submit it by going over to the **Submit** tab. Be sure to compile and test one last time before you submit.

* All done!