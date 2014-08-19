Lecture notes by Andrew Sellergren. [Watch the video.](http://cs50.tv/2013/fall/lectures/4/w/)

## Announcements and Demos

Fifth Monday is on 10/7! This is the deadline for changing your grading
status in the course. Switching to SAT/UNS or Pass/Fail requires a signature,
so please do approach David, Rob, or Lauren if you need.

## Pointers

### `noswap.c`

Pointers are one of the more complex topics we cover, so don’t feel bad if
your mind feels stretched in the next few weeks. That’s a good thing!

Recall last time we ended with a function that didn’t live up to its name:

	#include <stdio.h>

	void swap(int a, int b);

	int main(void)
	{
	    int x = 1;
	    int y = 2;

	    printf("x is %i\n", x);
	    printf("y is %i\n", y);
	    printf("Swapping...\n");
	    swap(x, y);
	    printf("Swapped!\n");
	    printf("x is %i\n", x);
	    printf("y is %i\n", y);
	}

	void swap(int a, int b)
	{
	    int tmp = a;
	    a = b;
	    b = tmp;
	}

Though we expected to see `x` and `y` have the values 2 and 1, respectively,
we actually saw that they still had their original values 1 and 2.

To see why this doesn’t work, let’s bring a volunteer onstage. We’ll ask her
to pour orange juice and milk into two separate glasses representing two
different `int`. If we ask her to swap the orange juice and milk, she wisely
chooses to use another glass. This glass represents some temporary storage
which we call tmp in the swap function above. Interestingly, if we implement
the same code directly in main, the swapping actually works:

	#include <stdio.h>

	int main(void)
	{
	    int x = 1;
	    int y = 2;

	    printf("x is %i\n", x);
	    printf("y is %i\n", y);
	    printf("Swapping...\n");

	    int tmp = x;
	    x = y;
	    y = tmp;

	    printf("Swapped!\n");
	    printf("x is %i\n", x);
	    printf("y is %i\n", y);
	}

So why does this logic work in `main` but not in `swap`? `a` and `b` are
actually copies of `x` and `y`, so when we swap `a` and `b`, `x` and `y` are
unchanged.

One way to fix this would be to make `x` and `y` global variables, declaring
them outside of main. In `fifteen.c`, it made sense to make certain variables
global because they were to be used by the whole program. However, in a small
program like `noswap.c`, using global variables is sloppy design.

### `swap.c`

How can we change the definition of swap to work as intended? Turns out we
just need to add asterisks:

	void swap(int* a, int* b)
	{
	    int tmp = *a;
	    *a = *b;
	    *b = tmp;
	}

What is an `int*`? It’s the memory address of an `int`. More properly
speaking, it is a pointer to an `int`. If your computer has 2 gigabytes of
RAM, then there are 2 billion bytes, each of which has a memory address.
Let’s say the `int` that a points to is stored at the 123rd byte of RAM. The
value of a then, is 123. To get at the actual integer value that’s stored at
byte 123, we write `*a`. `*a = *b` says "store at location `a` whatever is at
location `b`."

Now that we’ve changed `swap`, we need to change how we call `swap`. Instead
of passing `x` and `y`, we want to pass the address of `x` and the address of
`y`:

	swap(&x, &y)

`&` is the "address-of" operator and `*` is the dereference operator.

Let’s assume our integers 1 and 2 are stored next to each other in memory and
1 is stored at byte 123. That means 2 is stored 4 bytes away (since an `int`
requires 4 bytes), so we’ll assume that it’s stored at byte 127. The values
of a and b, then, are 123 and 127. We can simulate passing those to swap by
writing them on pieces of paper and putting them in a black box.

We ask a volunteer to come onstage and retrieve the pieces of paper from the
black box. Next he needs to allocate a little bit of memory for variable tmp.
In tmp, he stores the value of the `int` whose address is in `a`. This is 1.

Next, at address 123, he erases the number 1 and writes in the number 2. This
corresponds to the `*a = *b` line, which says "store at location `a` whatever
is at location `b`."

Finally, at address 127, he erases the number 2 and writes in the number 2,
which was stored in `tmp`. `tmp` is a local variable, but goes away when swap
returns.

### `compare-0.c`

For the first few weeks, we have worked with `string` as a data type.
However, this is a type that we defined for you in the CS50 Library. A
`string` is really a `char*`. It’s the address of a char. In fact, it’s the
address of the first char in the string.

Consider the following program which claims to compare two strings:

	#include <cs50.h>
	#include <stdio.h>

	int main(void)
	{
	    // get line of text
	    printf("Say something: ");
	    string s = GetString();

	    // get another line of text
	    printf("Say something: ");
	    string t = GetString();

	    // try (and fail) to compare strings
	    if (s == t)
	    {
	        printf("You typed the same thing!\n");
	    }
	    else
	    {
	        printf("You typed different things!\n");
	    }
	}

Here, we simply ask the user for two strings and store them in `s` and `t`. Then
we ask if `s == t`. Seems reasonable, no? We’ve used the `==` operator for all
the other data types we’ve seen thus far.

But if we compile and run this program, typing "hello" twice, we always get
"You typed different things!"

Recall that a string is just an array of characters, so "hello" looks like
this in memory:

	h   e   l   l   o   \0

Although we’re able to access the first character "h" using bracket notation,
under the hood it’s really located at one of 2 billion or so memory
addresses. Let’s call it address 123 again. Then "e" is at address 124, "l"
is at address 125, and so on. A char only takes 1 byte, so this time the
memory addresses are only 1 apart.

If `GetString` is getting us this string, then what does it actually return?
The number 123! Before it does so, it allocates the memory necessary to store
"hello" and inserts those characters along with the null terminator.

But if we only know the memory address of the first character, how do we know
how long the string is? Recall that strings end with the special \0
character, so we can just iterate until we find it.

`compare-0.c` is buggy because it’s comparing the memory addresses of the two
strings, not the strings themselves. Maybe `s` is stored at memory address
123 and t is stored at memory address 200. Since 123 does not equal 200, our
program says they’re different strings.

### `copy-0.c`

Let’s take a look at a program that tries, but fails to copy a string:

	#include <cs50.h>
	#include <ctype.h>
	#include <stdio.h>
	#include <string.h>

	int main(void)
	{
	    // get line of text
	    printf("Say something: ");
	    string s = GetString();
	    if (s == NULL)
	    {
	        return 1;
	    }

	    // try (and fail) to copy string
	    string t = s;

	    // change "copy"
	    printf("Capitalizing copy...\n");
	    if (strlen(t) > 0)
	    {
	        t[0] = toupper(t[0]);
	    }

	    // print original and "copy"
	    printf("Original: %s\n", s);
	    printf("Copy:     %s\n", t);
	}

We check that `s` isn’t NULL in case the user has given us more characters
than we have memory for. NULL is actually the memory address 0. By
convention, no user data can ever be stored at byte 0, so if a program tries
to access this memory address, it will crash.

Now that we have the user-provided string in `s`, we assign the value of `s`
to `t`. But if `s` is just a memory address, say 123, then t is now the same
memory address. Both `s` and `t` are pointing to the same chunks of memory.

To prove that this program is buggy, we’ll try to capitalize `t`, but not
`s`. The output, though, shows that both `s` and `t` are capitalized.

To emphasize that their role is to point to other variables, pointers are
often represented as arrows.

### `compare-1.c`

Finally, a program that truly compares two strings:

	#include <cs50.h>
	#include <stdio.h>
	#include <string.h>

	int main(void)
	{
	    // get line of text
	    printf("Say something: ");
	    char* s = GetString();

	    // get another line of text
	    printf("Say something: ");
	    char* t = GetString();

	    // try to compare strings
	    if (s != NULL && t != NULL)
	    {
	        if (strcmp(s, t) == 0)
	        {
	            printf("You typed the same thing!\n");
	        }
	        else
	        {
	            printf("You typed different things!\n");
	        }
	    }
	}

Now that we know a string is really just a `char*`, we need to be careful
it’s not `NULL`.

`strcmp` is short for "string compare." It’s a function that comes in
`string.h`, which, according to the man page, returns 0 if two strings are
identical, a negative number if the first string argument comes before the
second string alphabetically, or a positive number if the first string
argument comes after the second string alphabetically.

### `copy-1.c`

Copying a string is a little more complicated than just using the assignment
operator:

	#include <cs50.h>
	#include <ctype.h>
	#include <stdio.h>
	#include <string.h>

	int main(void)
	{
	    // get line of text
	    printf("Say something: ");
	    char* s = GetString();
	    if (s == NULL)
	    {
	        return 1;
	    }

	    // allocate enough space for copy
	    char* t = malloc((strlen(s) + 1) * sizeof(char));
	    if (t == NULL)
	    {
	        return 1;
	    }

	    // copy string, including '\0' at end
	    int n = strlen(s);
	    for (int i = 0; i <= n; i++)
	    {
	        t[i] = s[i];
	    }

	    // change copy
	    printf("Capitalizing copy...\n");
	    if (strlen(t) > 0)
	    {
	        t[0] = toupper(t[0]);
	    }

	    // print original and copy
	    printf("Original: %s\n", s);
	    printf("Copy:     %s\n", t);

	    // success
	    return 0;
	}

In line 17, we’re declaring a pointer `t` and initializing it with the return
value of a function named malloc. malloc takes a single argument, the number
of bytes of memory requested, and returns the address in memory of the first
of those bytes or `NULL` if the memory couldn’t be allocated.

In this case, we’re allocating enough memory for all the characters in `s`
plus 1 extra for the null terminator. We multiply this number of characters
by `sizeof(char)`, which gives the size in bytes of a char on this particular
operating system. Normally it will be 1, but we’re handling other cases
correctly, too.

Once we have enough memory, we iterate through all of the characters in `s`
and assign them one at a time to `t`.

## Teaser

Let’s analyze some seemingly innocuous lines of code:

	int main(void)
	{
	    int* x;
	    int* y;

	    x = malloc(sizeof(int));

	    *x = 42;

	    *y = 13;

	    y = x;

	    *y = 13;
	}

First, we declare two pointers `x` and `y`. We allocate enough memory to
store an `int` and assign its address to `x`. We store the value 42 in this
memory. Then we store in the memory address `y` the value 13. But wait, we
didn’t allocate memory for a second `int`, so what does `y` point to? Who
knows! That’s the problem. Line 10 is pretty painful for Binky.
