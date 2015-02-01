Lecture notes by Andrew Sellergren. [Watch the video.](http://cs50.tv/2013/fall/lectures/2/w/)

## Announcements and Demos

## Functions

### `function-0.c`

Thus far, we've used functions like `printf`, which prints to the screen, and
`GetString`, which gets a string from the user, but what if we want to write
our own function? Let's revisit this program that prompts a user for his name
and try to factor out some of the logic:

	#include <cs50.h>
	#include <stdio.h>

	void PrintName(string name)
	{
	    printf("hello, %s\n", name);
	}

	int main(void)
	{
	    printf("Your name: ");
	    string s = GetString();
	    PrintName(s);
	}

Although this function is actually only one line of code, it's much nicer to
write just the function name than to copy and paste that one line when we
want to reuse it.

Above the definition of `main`, we declared our function `PrintName` to have
a return type of `void` (because it doesn't return anything but has a side
effect) and a single argument `name` of type `string`.

Notice that although we call the user's name `s` in `main`, we refer to it as
`name` in `PrintName` because that was what we chose to call the argument.

What if we had chosen to write the definition of `PrintName` after `main`?
The compiler would have complained of "implicit declaration of function
PrintName" because it reads top to bottom and we called `PrintName` before we
defined it. Better than defining it above `main`, however, is declaring it
above `main` and then defining it below. This keeps `main` at the top of the
file:

	#include <cs50.h>
	#include <stdio.h>

	void PrintName(string name);

	int main(void)
	{
	    printf("Your name: ");
	    string s = GetString();
	    PrintName(s);
	}

	void PrintName(string name)
	{
	    printf("hello, %s\n", name);
	}

This declaration of function `PrintName` is called a _prototype_.

### `function-1.c`

Let's rewrite our program that asks for a positive integer using a function:

	#include <cs50.h>
	#include <stdio.h>

	int main(void)
	{
	    int n = GetPositiveInt();
	    printf("Thanks for the positive int!\n", n);
	}

At this stage, we're going to get an "implicit declaration" compiler error
again because we haven't defined `GetPositiveInt`. We need to put the
prototype at the top like so:

	#include <cs50.h>
	#include <stdio.h>

	int GetPositiveInt(void);

	int main(void)
	{
	    int n = GetPositiveInt();
	    printf("Thanks for the %i!\n", n);
	}

As its name suggests, `GetPositiveInt` returns an `int`. Because it doesn't
take any arguments, we've explicitly declared it as taking `void`, meaning
nothing. Now for the definition of `GetPositiveInt`:

	#include <cs50.h>
	#include <stdio.h>

	int GetPositiveInt(void);

	int main(void)
	{
	    int n = GetPositiveInt();
	    printf("Thanks for the %i!\n", n);
	}

	int GetPositiveInt(void)
	{
	    int n;
	    do
	    {
	        printf("Give me a positive integer: ");
	        n = GetInt();
	    }
	    while (n <= 0);
	}

When we compile this program, though, we get an error: "control reaches end
of non-void function." What this means is that `GetPositiveInt` isn't returning
anything even though we've specified that it should return an `int`. To fix
this, we add a return statement:

	#include <cs50.h>
	#include <stdio.h>

	int GetPositiveInt(void);

	int main(void)
	{
	    int n = GetPositiveInt();
	    printf("Thanks for the %i!\n", n);
	}

	int GetPositiveInt(void)
	{
	    int n;
	    do
	    {
	        printf("Give me a positive integer: ");
	        n = GetInt();
	    }
	    while (n <= 0);
	    return n;
	}

Question: main has a return type of `int` too, so why aren't we returning
anything from it? Technically, in the version of C we're using, 0 is returned
by default at the end of `main`. 0 means nothing went wrong, whereas each
non-zero return value could represent a different error code.

## Strings

Last time, we saw that we can think of strings as collections of contiguous
boxes, each containing a single character requiring a single byte of memory.
To access the individual characters/bytes of a string, we index into the
string using the square bracket notation.

Realize that there are two types of memory in your computer: disk, where you
store your music and photos, etc., and RAM, or random access memory, which
store information that needs to be accessed quickly while a program is
running. The memory that stores a string like "hello" for your program is RAM.

### `string-1.c`

Consider again the program that takes a string from the user and prints it one character per line:

	#include <cs50.h>
	#include <stdio.h>
	#include <string.h>

	int main(void)
	{
	    string s = GetString();

	    if (s != NULL)
	    {
	        for (int i = 0; i < strlen(s); i++)
	        {
	            printf("%c\n", s[i]);
	        }
	    }
	}

What's the deal with the `s != NULL`? It turns out that the `GetString` will
not always succeed in getting a string from the user. If it fails, perhaps
because the user typed a string that was too long to hold in memory,
`GetString` will return a special *sentinel value* named `NULL`. Without this
check, other things we try to do with `s` might cause the program to crash.

`s[i]`, where `i` is 0, 1, 2, is an individual character in the string, so we
ask `printf` to substitute it into `%c`.

### `string-2.c`

There's at least one inefficiency in this `string-1.c` as it's currently
written. `strlen(s)` will only ever return one value, yet we're calling it on
every iteration of the loop. To optimize our program, we should call `strlen`
once and store the value in a variable like so:

	#include <cs50.h>
	#include <stdio.h>
	#include <string.h>

	int main(void)
	{
	    string s = GetString();

	    if (s != NULL)
	    {
	        for (int i = 0, n = strlen(s); i < n; i++)
	        {
	            printf("%c\n", s[i]);
	        }
	    }
	}

Although computers are very fast these days and this optimization may not be
immediately noticeable, it's important to look for opportunities to improve
design. These little optimizations can add up over time. One of the problem
sets we've done in years past was writing a spellchecker in C with the goal
of making it as fast as possible. An optimization like this might save a few
milliseconds of runtime!

### `capitalize-0.c`

In `capitalize-0.c`, we claim to capitalize all the letters in a string:

	#include <cs50.h>
	#include <stdio.h>
	#include <string.h>

	int main(void)
	{
	    string s = GetString();

	    for (int i = 0, n = strlen(s); i < n; i++)
	    {
	        if (s[i] >= 'a' && s[i] <= 'z')
	        {
	            printf("%c", s[i] - ('a' - 'A'));
	        }
	        else
	        {
	            printf("%c", s[i]);
	        }
	    }
	    printf("\n");
	}

The first condition within the loop is checking if the character is
lowercase. If it is, then we subtract from it the value of `a - A`. Under the
hood, characters are actually just numbers, which is why we can compare them
with `>=` and subtract them from each other. The value of `a - A` is the
offset between the lowercase and uppercase characters on the ASCII chart. By
subtracting this offset from `s[i]`, we're effectively capitalizing the
letter.

### `capitalize-1.c`

Thus far, we've worked with a few libraries of code that gave us convenient
functions. Let's add one more to that list:

* stdio.h
* cs50.h
* string.h
* ctype.h

Rather than write our own condition to check if a character is lowercase and
our own logic to capitalize a character, let's use functions someone else
already implemented:

	#include <cs50.h>
	#include <ctype.h>
	#include <stdio.h>
	#include <string.h>

	int main(void)
	{
	    string s = GetString();

	    for (int i = 0, n = strlen(s); i < n; i++)
	    {
	        if (islower(s[i]))
	        {
	            printf("%c", toupper(s[i]));
	        }
	        else
	        {
	            printf("%c", s[i]);
	        }
	    }
	    printf("\n");
	}

### `capitalize-2.c`

We don't strictly need the curly braces around if-else blocks so long as they
are only a single line. However, there's an even better way to shorten this
program:

	#include <cs50.h>
	#include <ctype.h>
	#include <stdio.h>
	#include <string.h>

	int main(void)
	{
	    string s = GetString();

	    for (int i = 0, n = strlen(s); i < n; i++)
	    {
	        printf("%c", toupper(s[i]));
	    }
	    printf("\n");
	}

Turns out that `toupper` handles both lowercase and uppercase characters
properly, so we don't even need the `islower` check. We know this because we
checked the man page, or manual page, for `toupper` by typing `man toupper`
at the command line. This page tells us that the return value is the
converted letter or the original letter if conversion was not possible.
Perfect!

### The Null Terminator

If strings are stored as characters back to back in memory, how do we know
where one ends and another begins? When inserting a string into memory, the
computer actually adds a special character called NUL after the last
character of the string. NUL is represented as `\0`.

## Arrays

### ages.c

Strings are actually a special case of a data type called an array. Arrays
allow us to store related variables together in one place. For example,
consider a program that stores and prints out the ages of everyone in the
room:

	#include <cs50.h>
	#include <stdio.h>

	int main(void)
	{
	    // determine number of people
	    int n;
	    do
	    {
	        printf("Number of people in room: ");
	        n = GetInt();
	    }
	    while (n < 1);

	    // declare array in which to store everyone's age
	    int ages[n];

	    // get everyone's age
	    for (int i = 0; i < n; i++)
	    {
	        printf("Age of person #%i: ", i + 1);
	        ages[i] = GetInt();
	    }

	    // report everyone's age a year hence
	    printf("Time passes...\n");
	    for (int i = 0; i < n; i++)
	    {
	        printf("A year from now, person #%i will be %i years old.\n", i + 1, ages[i] + 1);
	    }
	}

The first lines should be familiar to you by now: we're prompting the user
for a positive number. In line 16, we use that number as the number of places
in our array called `ages`. `ages` is a bucket with room for `n` integers.
Using an array is a better alternative than declaring an `int` for every
single person in the room, especially since we don't even know how many there
are until the user tells us!

The rest of the program is pretty straightforward. We iterate through `ages`
the same way we iterated through strings, accessing each element using square
bracket notation.

### Cryptography

Can you guess what this encrypted string actually says?

> Or fher gb qevax lbhe Binygvar

It says "Be sure to drink your Ovaltine." Each character of the string is
changed to another character using an encryption technique known as ROT-13.
Each letter is simply rotated by 13 around the alphabet. This isn't very
sophisticated, of course, as there are only 25 different numbers to rotate
by, so it can easily be cracked by brute force.

On certain systems, your password might be stored as an encrypted string like so:

Your password was encrypted using secret-key cryptography. That means it was
translated from plaintext to so-called *ciphertext* using a secret. Only with
that secret can the ciphertext be decrypted back to plaintext. In the Hacker
Edition of the upcoming problem set, you'll be asked to decrypt some
passwords without knowing the secret! In the Standard Edition, we'll
introduce you to some ciphers, one called Caesar and one called Vigenère.

[Be sure to drink your Ovaltine!](http://www.youtube.com/watch?v=zdA__2tKoIU)


