# CS50 style guide

There's no one, right way to stylize code. But there are definitely a lot of
wrong (or, at least, bad ways). Even so, CS50 does ask that you adhere to the
green conventions below so that we can reliably analyze your code's style.
Similarly do companies typically adopt their own, company-wide conventions
for style.

## Comments

Comments make code more readable, not only for others (e.g., your TA) but
also for you, especially when hours, days, weeks, months, or years pass
between writing and reading your own code. Commenting too little is bad.
Commenting too much is bad. Where's the sweet spot? Commenting every few
lines of code (i.e., interesting blocks) is a decent rule of thumb. Try to
write comments that address one or both of these questions:

* What does this block do?
* Why did I implement this block in this way?

Within functions, use inline comments and keep them short (e.g., one line),
else it becomes difficult to distinguish comments from code, even with syntax
highlighting. No need to write in full sentences, but do leave one space
between the `//` and your comment's first character, as in:

	// compute student's average
	average = (int) (sum / QUIZZES + 0.5);

In other words, don't do this:

	//compute student's average
	average = (int) (sum / QUIZZES + 0.5);

Or this:

	// Compute student's average.
	average = (int) (sum / QUIZZES + 0.5);
  
Do not place comments on the same line as actual code, as in

	average = (int) (sum / QUIZZES + 0.5); // compute student's average

Atop your `.c` and `.h` files should be multi-line comments that summarize
what your program (or that particular file) does along with, perhaps, your
name and that of the file. Consider what I tend to do:

	/****************************************************************************
	 * hello.c
	 *
	 * Computer Science 50
	 * David J. Malan
	 *
	 * Says hello to the world.
	 *
	 * Demonstrates use of printf.
	 ***************************************************************************/

Atop each of your functions (except, perhaps, main) should be multi-line
comments that summarize what your function does along with, perhaps, its
signature. Consider what I tend to do:

	/**
	 * Sings about a number, b, of bottles.
	 */
	void chorus(int b)
	{
	    // use proper grammar
	    string s1 = (b == 1) ? "bottle" : "bottles";
	    string s2 = (b == 2) ? "bottle" : "bottles";
	
	    // sing verses
	    printf("%d %s of beer on the wall,\n", b, s1);
	    printf("%d %s of beer,\n", b, s1);
	    printf("Take one down, pass it around,\n");
	    printf("%d %s of beer on the wall.\n\n", b - 1, s2);
	}

## Conditions

If a branch involves just one statement, you don't need curly braces:

	if (x > 0)
	    printf("x is positive\n");
	else if (x < 0)
	    printf("x is negative\n");

But it's fine to include them, especially if you think you might add
additional statements later:

	if (x < 0)
	{
	    printf("x is negative\n");
	}
	else if (x < 0)
	{
	    printf("x is negative\n");
	}

Notice how the curly braces line up nicely, making perfectly clear what's
inside the branch.

Do not indent your curly braces:

	if (x < 0)
	    {
	    printf("x is negative\n");
	    }
	else
	    {
	    printf("x is negative\n");
	    }

Don't omit the space between if and the parenthesis that follows, lest it
resemble a function call (which it isn't):

	if(x < 0)
	{
	    printf("x is negative\n");
	}

## Functions

Declare functions as follows, with curly braces on lines of their own:

	int main(void)
	{
	
	}

But it's also fine if you want to put the curly brace on the same line as the
function declaration as in (but don't omit the space between the function and
curly brace):

	int main(void) {
	
	}

## Indentation

Indent your code four spaces at a time to make clear which blocks of code are
inside of others. If you use your keyboard's Tab key to do so, be sure that
your text editor's configured to convert tabs (`\t`) to four spaces, else
your code may not print or display properly on someone else's computer, since
`\t` renders differently in different editors. Here's some nicely indented
code:

	// print arguments
	printf("\n");
	for (int i = 0; i < argc; i++)
	{
	    for (int j = 0, n = strlen(argv[i]); j < n; j++)
	        printf("%c\n", argv[i][j]);
	    printf("\n");
	}

## Loops

Whenever you need temporary variables for iteration, use `i`, then `j`, then
`k`, unless more specific names would make your code more readable:

	for (int i = 0; i < LIMIT; i++)
	{
	    for (int j = 0; j < LIMIT; j++)
	    {
	        for (int k = 0; k < LIMIT; k++)
	        {
	            // do something
	        }
	    }
	}

If you need more than three variables for iteration, it might be time to
rethink your approach.

## main

Because CS50 uses C99, main should be declare in either of two ways, namely:

	int main(void)
	{
	
	}

or:

	int main(int argc, char* argv[])
	{
	
	}

Do not declare main with:

	int main()
	{
	
	}

or with:

	void main()
	{
	
	}

or with:

	main()
	{
	
	}

## Pointers

When declaring a pointer, write the `*` next to the type, as in:

	int* p;

## Variables

Because CS50 uses C99, do not define all of your variables at the very top of
your functions but, rather, when and where you actually need them.

Moreover, scope your variables as tightly as possible. For instance, if `i`
is only needed for the sake of a loop, declare `i` within the loop itself:

	for (int i = 0; i < LIMIT; i++)
	    printf("%d\n", i);

Though it's fine to use variables like `i`, `j`, and `k` for iteration, most
of your variables should be more specifically named. If you're summing some
values, for instance, call your variable `sum`. If your variable's name
warrants two words (e.g., `is_ready`), put an underscore between them, a
convention popular in C though less so in other languages.

If declaring multiple variables of the same type at once, it's fine to
declare them together, as in:

	int quarters, dimes, nickels, pennies;

Just don't initialize some but not others, as in:

	int quarters, dimes = 0, nickels = 0 , pennies;

Also take care to declare pointers separately from non-pointers, as in:

	int* p;
	int n;

Don't declare pointers on the same line as non-pointers, lest it be ambiguous
as to whether the latter was meant to be the former, as in:

	int* p, n;
