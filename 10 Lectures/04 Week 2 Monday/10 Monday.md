Lecture notes by Andrew Sellergren. [Watch the video.](http://cs50.tv/2013/fall/lectures/2/m/)

## Announcements and Demos

* If you're interested in teaching computer science to local middle school
  students, either now or sometime in the future, head to
  [DLP.io/volunteer][1].

* Sections begin this coming Monday, Tuesday, and Wednesday. You'll hear
  later this week via e-mail about your assignment and how to change it if
  necessary.

* Problem Set 1 is due this Thursday. Included in the specification are
  instructions for how to extend the deadline to Friday as well as how to use
  the CS50 Appliance and tools like `check50` and `style50`.

* Problem set scores are calculated as follows:

    * scope * (correctness * 3 %2B design * 2 + style * 1)

        Scope captures how much of the problem set you bit off. Correctness
        implies whether your program works as per the specification. Design
        is a subjective assessment of the approach you took to solve the
        problem. Style refers to the aesthetics of your code: are your
        variables named descriptively, is your code indented properly?

    * each axis ranges from 1 to 5:

	    * 5 - best

	    * 4 - better

		* 3 - good

		* 2 - fair

		* 1 - poor

		Never fear that a 3 out of 5 is a 60% and thus failing! A 3 out of 5 is just what it says: good.

* A word on academic honesty. This course has the distinction of having sent
  more students to the Ad Board than any other course. We're very good at
  detecting _dishonesty_. We compare all problem sets pairwise against each
  other across this year and all prior years. If you can Google a solution,
  so can we. This year, we've rephrased our statement on academic honesty to
  capture the spirit of appropriate collaboration:

    * This courses's philosophy on academic honesty is best stated as "be
      reasonable."

    * Generally speaking, when asking for help, you may show your code to
      others, but you may not view theirs, so long as you and they respect
      this policy's other constraits.

    * See [cs50.net/syllabus][2] for examples of "reasonable" and
      "unreasonable" behavior.

    * If you're absolutely stuck and at your breaking point, reach out to
      David or the heads directly. Don't resort to unreasonable behavior!

## From Last Time

* We introduced a few data types in C:

    * `char`
    * `double`
    * `float`
    * `int`
    * `long long`

* A `char` is an ASCII character. Recall in Week 0 our 8 volunteers who came
  on stage and raised their hands to represent bits. Together, they
  represented an entire byte, which, thanks to ASCII, can represent an
  alphabetical character. With 8 bits, it is possible to represent `2^{8}`,
  or 256, different characters. To represent the whole of the alphabet in a
  language such as Arabic, we need an encoding system other than ASCII. More
  on that later.

* An `int` is an integer. On most computers, an `int` requires 32 bits and
  thus can represent roughly `2^{32}`, or 4 billion, different numbers.

* A `long long` requires 64 bits and can represent even bigger numbers than
  an `int`.

* The `float` and `double` types, which require 32 bits and 64 bits,
  respectively, store numbers with decimal points.

* One problem you may have already picked up on is that we have a finite
  number of bits that we can use to represent an infinite number of numbers.

### Floating Points

#### `floats-0.c`

* Let's write a short program we'll call `floats-0.c`:

		#include <stdio.h>

		int main(void)
		{
		    float f = 1 / 10;
		    printf("%.1f\n", f);
		}

* Here we're simply trying to store the value 0.1 in a `float` and print it
  out. Don't forget `stdio.h`! The `.1` in front of `f` means that we want to
  print only one decimal place.

* When we compile and run this program, however, we see 0.0 printed to the
  screen. Where is the bug? Let's try printing two decimal places by writing
  `%.2f`. Nope, we get 0.00.

* The problem is that we're dividing one integer by another. When you do
  this, the computer assumes that you want another integer in response. Since
  0.1 is not an integer, the computer actually truncates it, throwing away
  everything after the decimal point. When we actually store the resulting
  integer in a `float`, it gets converted to a number that has a decimal
  point.

#### `floats-1.c`

* To fix this, we could turn the integers into floating points like so:

		#include <stdio.h>

		int main(void)
		{
		    float f = 1.0 / 10.0;
		    printf("%.1f\n", f);
		}


#### `floats-2.c`

* Alternatively, we could explicitly _cast_, or convert, the numbers 1 and 10
  to floating points before the division:

	    #include <stdio.h>

	    int main(void)
	    {
	        float f = (float) 1 / (float) 10;
	        printf("%.1f\n", f);
	    }

* Since characters are represented as numbers via ASCII, we can use casting
  to convert between `char` and `int`. Similarly, we can cast between
  different types of numbers.

* What if we change `%.1f` to `.10f` or `.20f`? We don't get exactly 0.1, but
  rather 0.1 with some numbers in the far right decimal places. Because the
  `float` type has a finite number of bits, we can only use it to represent a
  finite number of numbers. At some point, our numbers become imprecise.

* Don't think that this imprecision is a big deal? Perhaps [this video][3]
  will convince you otherwise.

* As we'll find out later in the semester, MySQL requires you to specify how
  many bits it should use to store values.

## More From Last Time

* Check out [last week's notes][4] for the syntax we used for conditions,
  Boolean expressions, switches, loops, variables, and functions in C.

* Recall that `printf` was a function that had no return value (or at least
  none that we cared about), but only a _side effect_, that of printing to
  the screen.

## do-while

One type of loop we didn't look closely at is the do-while loop. Let's write
a program that insists that the user give a positive number:

		#include <stdio.h>

		int main(void)
		{
		    printf("I demand that you give me a positive integer: ");
		    int n = GetInt();
		    if (n <= 0)
		    {
		        printf("That is not positive!\n")
		    }
		}

But now if the user hasn't given us a positive number, we need to copy and
paste the `GetInt()` call into another branch of logic to re-prompt her. But
what if she *still* hasn't given us a positive number? Obviously this could go
on forever, so we probably need some kind of loop instead. Let's try a
do-while loop:

		#include <stdio.h>

		int main(void)
		{
		    do
		    {
		        printf("I demand that you give me a positive integer: ");
		        int n = GetInt();
		    }
		    while (n <= 0);
		    printf("Thanks for the %d!\n", n);
		}

Notice how much improved this is! When we try to compile, though, we get an
"implicit declaration" error. We need to include the CS50 Library.

### Scope

Even after adding `#include <cs50.h>` we get "unused variable n" and
"undeclared identifier n" errors. It would seem that we are in fact using the
variable n when we check whether it's less than or equal to zero. Likewise it
would seem that `n` is not "undeclared" since we initialized it within the do
block. What's wrong then? Because we're declaring `n` inside the do block,
within the curly braces, its scope is limited to that block. Outside of those
curly braces, `n` effectively doesn't exist. What we need to do is declare
`n` outside the loop but set its value within the loop like so:

		#include <cs50.h>
		#include <stdio.h>

		int main(void)
		{
		    int n;
		    do
		    {
		        printf("I demand that you give me a positive integer: ");
		        n = GetInt();
		    }
		    while (n <= 0);
		    printf("Thanks for the %d!\n", n);
		}

If we compile and run this program, we find that it works!

Let's try banging on it a little. What happens if we type a character instead
of a number? We get a "Retry: " prompt. Since this doesn't appear in our
program above, it presumably comes from some error checking in the CS50
Library. When you call `GetInt()`, we at least make sure that what you get in
return is an `int`, not a `string` or a `char`.

A suboptimal solution to this problem of scope would have been to declare a
*global variable* like so:

Scratch actually implemented global variables as variables declared for "all
sprites."

Global variables are generally considered poor design.

Note that declaring a variable and not using it is not strictly an error.
However, for CS50, we've cranked up the error checking of the compiler as a
pedagogical exercise. You may have noticed a series of flags that are passed
to `clang` automatically when you type `make`. Two of those flags are `-Wall`
`-Werror` which mean "make all warnings into errors."

## Strings

There's a lot more going on under the hood with strings than we've let on so
far. Consider the following program:

		#include <cs50.h>
		#include <stdio.h>
		#include <string.h>

		int main(void)
		{
		    printf("Please give me a string: ");
		    string s = GetString();
		    for (int i = 0; i < strlen(s); i++)
		    {
		        printf("%c\n", s[i]);
		    }
		}

`strlen` returns the length of the string it is passed. Thus, we seem to be
looping through the characters of the string.

It turns out that strings are stored as characters back-to-back in memory. We
can access those characters using the square bracket notation, so `s[0]` gets
the first letter, `s[1]` gets the second letter, and so on.

This program prints the characters of the user-provided string, one line at a
time!

## Teaser

Check out the first
[jailbreak](http://cdn.cs50.net/2013/fall/lectures/2/m/src2m/iUnlock.c) of
the iPhone, the
[winner](http://cdn.cs50.net/2013/fall/lectures/2/m/src2m/holloway.c) of an
obfuscated C contest, and a [very pretty program](http://cdn.cs50.net/2013/fall/lectures/2/m/src2m/thadgavin.c)!



