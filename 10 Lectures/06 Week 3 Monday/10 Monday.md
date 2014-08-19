Lecture notes by Andrew Sellergren. [Watch the video.](http://cs50.tv/2013/fall/lectures/3/m/)

## Announcements and Demos

* Please welcome special guest lecturer Rob Bowden!
* No CS50 Lunch this Friday!

## From Last Time

We’ve seen how a string is a sequence of characters. More properly speaking,
it is an array of characters with a null terminator (`\0`) at the end.

We can also have arrays of other types, not just characters. In the `ages.c`
program, we used an array of `int` to store the age of everyone in the room:

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

In line 16, we use bracket notation to declare an array of `int` of size `n`. To
access the element `i` of that array, we write `ages[i]`. Arrays are
zero-indexed, so the first element is stored in `ages[0]`. There’s no element
in `ages[n]` even though the array has size `n`!

## Command-line Arguments

Thus far, we’ve started our programs with the line `int main(void)`. `void` means
that we’re not passing any arguments to the `main` function. However, it’s
possible to pass arguments to the `main` function using the following syntax:

	int main(int argc, string argv[])

Here, we pass two arguments, `argc` and `argv`. `argc` is an `int` and `argv`
is an array of string. argc actually indicates how many arguments we’ve
passed to a program.

Earlier, when we typed `./ages` at the command line, there was 1 command-line
argument: the name of the program itself. If we had typed `./ages hello world`,
there would have been 3 command-line arguments. In these cases, `argc` would
have taken the values 1 and 3, respectively. There is always at least 1
command-line argument.

Whereas `argc` contains the number of command-line arguments, `argv` contains
the command-line arguments themselves.

### `argv-0.c`

Listen to David describe a short program that uses command-line arguments:

	#include <cs50.h>
	#include <stdio.h>

	int main(int argc, string argv[])
	{
	    printf("%s\n", argv[1]);
	}

We could modify this program to print out the second command-line argument as
an integer:

	#include <cs50.h>
	#include <stdio.h>

	int main(int argc, string argv[])
	{
	    int x = atoi(argv[1]);
	    printf("%d\n", x);
	}

This works well as long as we actually send two command-line arguments. What
happens when we don’t? The program crashes with a segmentation fault. This is
because we tried to access an element beyond the bounds of the array. We
should add a check to protect against this:

	#include <cs50.h>
	#include <stdio.h>

	int main(int argc, string argv[])
	{
	    if (argc < 2)
	    {
	        printf("Not enough command line arguments\n");
	    }
	    int x = atoi(argv[1]);
	    printf("%d\n", x);
	}

### `argv-1.c`

Let’s try printing out all of the command-line arguments:

	#include <cs50.h>
	#include <stdio.h>

	int main(int argc, string argv[])
	{
	    // print arguments
	    for (int i = 0; i < argc; i++)
	    {
	        printf("%s\n", argv[i]);
	    }
	}

### `argv-2.c`

Now, to go even deeper[^1], let's print each character of each command-line
argument on its own line:

	#include <cs50.h>
	#include <stdio.h>
	#include <string.h>

	int main(int argc, string argv[])
	{
	    // print arguments
	    for (int i = 0; i < argc; i++)
	    {
	        for (int j = 0, n = strlen(argv[i]); j < n; j++)
	        {
	            printf("%c\n", argv[i][j]);
	        }
	    }
	}

`argv[i][j]` represents character `j` in command-line argument `i`.

How would we go about writing strlen if it weren't provided to us in the
library `string.h`? Recall that all strings end with the special `\0`
character. If we iterate through each character of the string until we find
`\0`, we'll know the length of the string:

	int my_strlen(string s)
	{
	    int length = 0
	    while(s[length] != '\0')
	    {
	        length++;
	    }
	    return length;
	}

We could even move this logic into our second loop and avoid a function call altogether:

	#include <cs50.h>
	#include <stdio.h>
	#include <string.h>

	int main(int argc, string argv[])
	{
	    // print arguments
	    for (int i = 0; i < argc; i++)
	    {
	        for (int j = 0; argv[i][j] != '\0'; j++)
	        {
	            printf("%c\n", argv[i][j]);
	        }
	    }
	}

Each time we reach a `\0` within `argv`, our array of array of characters, we
terminate the inner for loop and execute the outer for loop again (provided
that we still have command-line arguments left, i.e. `i < argc`).

## Debugging

### `debug.c`

The best way to learn to debug is to work with buggy code like the following:

	#include <stdio.h>
	#include <cs50.h>

	void foo(int i)
	{
	    printf("%i\n", i);
	}

	int main(void)
	{
	    printf("Enter an integer: ");
	    int i = GetInt();

	    while (i > 10)
	    {
	        i--;
	    }

	    while (i != 0)
	    {
	        i = i - 3;
	    }

	    foo(i);
	}

Let’s assume that the user provides an integer greater than 10 (a bad
assumption). The first while loop will then decrement `i` by 1 until it equals
10, at which point the loop condition `i > 10` will no longer be true and the
loop will exit. The second while loop will decrement `i` by 3 until it equals
0. But if it starts at 10, `i` will go to 7, then 4, then -1, then -4, and so
on to negative infinity. That’s not what we intended!

One useful debugging technique is to add some `printf` statements:

	#include <stdio.h>
	#include <cs50.h>

	void foo(int i)
	{
	    printf("%i\n", i);
	}

	int main(void)
	{
	    printf("Enter an integer: ");
	    int i = GetInt();

	    printf("Outside first while loop");
	    while (i > 10)
	    {
	        printf("First while loop: %i\n", i);
	        i--;
	    }

	    printf("Outside second while loop");
	    while (i != 0)
	    {
	        printf("Second while loop: %i\n", i);
	        i = i - 3;
	    }

	    foo(i);
	}

When we compile and run `debug.c` now, we can clearly see that the second
while loop is infinite.

As your programs get longer and more complicated, you’ll find more
sophisticated debugging techniques more useful.

### GDB

GDB, or GNU Debugger, is a program that allows your to step through your code
line by line while it’s executing. Whenever you have run make on your code
thus far, the compiler `clang` has executed with a command-line argument
`-ggdb3`. This instructs `clang` to compile your code so that you can debug it
within GDB if you so choose.

After you’ve compiled `debug.c`, you can open it in GDB by executing `gdb debug`.
Note that the name of the program you want to walk through, in this case
`debug`, is provided as a command-line argument to `gdb`.

Once you’ve started GDB, you’ll find yourself at a prompt. Type `run` to begin
the execution of your program. This alone isn’t very useful, as the program
will finish executing just as it would outside of GDB.

Before typing `run`, you can type `break main` to insert a breakpoint at the
beginning of the `main` function. A breakpoint is a place at which execution of
the program is paused. Once you’ve reached a breakpoint, you can type `next`
repeatedly to step through your code line by line. Hitting Enter will redo
the last command you typed.

* Whenever we want to view the value of `i`, we can type `print i`.

* `list` will display the code before and after your current position.

* After stepping forward through many more executions of the second loop,
  printing `i` will give a negative number.

Let’s move the infinite loop inside the `foo` function for more practice with
GDB:

	#include <stdio.h>
	#include <cs50.h>
	
	void foo(int i)
	{
	    while (i != 0)
	    {
	        i = i - 3;
	    }
	    printf("%i\n", i);
	}
	
	int main(void)
	{
	    printf("Enter an integer: ");
	    int i = GetInt();
	
	    while (i > 10)
	    {
	        i--;
	    }
	
	    foo(i);
	}

After starting GDB by executing `gdb debug`, we’ll again set a breakpoint at
the beginning of `main` by typing break` main`. If we `next` over the `foo`
function call, the program will finish executing. Note that although the
second while loop appears infinite, it will eventually terminate for reasons
we’ll wave our hands at for now.

If we want to examine what foo is doing, we need to type `step` instead of
`next`. `step` is identical to `next` if the `next` line of code is not a
function call.

We can also set a breakpoint at the `foo` function by typing `break foo`. Now
when we type `run`, we’ll first stop at `main`. If we type `continue`,
execution will resume until we hit the next breakpoint at foo.

## Security

In Problem Set 2, you’ll be working with encrypting and decrypting passwords.
Of course, the strength of the encryption doesn’t matter all that much if you
choose a weak password.

Consider the code that implements the login prompt on your laptop. If it’s
working properly, it will check that what the user types matches your
password before letting the user in. However, if it’s working maliciously, it
might check that what the user types matches some master password that lets
anyone in. We can hope that this backdoor might be caught by at least one of
the many people who have reviewed it.

But what if the malicious code is in the compiler? Then the compiler might
actually insert the backdoor into the login prompt even though the code for
the login prompt seems safe and has been reviewed. We can hope again that
this would be caught by one of the people who reviewed the code for the
compiler.

But what if the malicious code is in the compiler that is used to compile the
compiler? Well, then, the backdoor might get inserted without anyone knowing.

If you think this scenario is unlikely, consider the speech that Ken Thompson
gave, Reflections on Trusting Trust, when he accepted the Turing Award (more
or less the Nobel Prize of computer science). In it, he describes this exact
technique for compromising a compiler so that it would introduce a backdoor
into a login program. The login program he refers to, however, is not some
toy program, but rather the login program for all of UNIX. Since delivering
this speech, Thompson has confirmed that this exploit was actually
implemented and released to at least one company, BBN Technologies[^2].

[^1]: Even deeper.

[^2]: Now he works at Google! Ask me how you can too.
