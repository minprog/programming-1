Lecture notes by Andrew Sellergren. [Watch the video.](http://cs50.tv/2013/fall/lectures/1/w/)

## Announcements and Demos

* Devices like Google Glass come with an API, an _application programming interface_, that allow developers to write software for it. For Final Projects, we’ll do what we can to hook you up with loaner hardware so that if you’re interested in writing, say, an Android or iOS app, you’ll have a test device.

* Another such device that comes with an API is Leap Motion. Check out [this video][1] to see how it allows you to control your computer with 3D gestures.

* Section by Friday at noon at [cs50.net/section][2].

* One-time supersections will be held this Sunday. They will be filmed.

	* Less comfortable: Sun 9/15, 2pm, Yenching Auditorium

	* More comfortable: Sun 9/15, 4pm, Yenching Auditorium

* Take advantage of [Office Hours][3]!

* Problem Set 0 is due on Friday. This is a day later than the usual deadline. For Problem Set 1, you’ll have the opportunity to extend the deadline from Thursday to Friday by completing some warm-up exercises.

* Get the CS50 Appliance at [cs50.net/appliance][4]. Problem Set 1’s specification will walk you through setting it up.

## From Last Time

  * To translate source code into object code, we used a compiler. Inside your computer, the CPU knows what the 0’s and 1’s actually mean, whether it be print, add, subtract, etc.

  * We ported our "hello, world" Scratch program to C.

### `hello, world!`

  * Let’s begin to tease apart the syntax of our very first C program:

	    #include <stdio.h>

	    int main(void)
	    {
	        printf("hello, world\n");
	    }

  * The first line that begins with a `#` is called a _preprocessor directive_. In this case, the directive says to include the contents of a file `stdio.h` inside our program. Inside of `stdio.h` is stored the definition of `printf`.

  * `int main(void)` is the equivalent of the "when green flag clicked" puzzle piece in Scratch. We’ll wave our hands at what it actually means for now.

  * Next we have open and close curly braces. These encapsulate related lines of code.

  * The interesting line of code in this program is the `printf` line. Recall that "hello, world " is an example of a _string_. The ` ` is a newline character.

  * How would we print out a double quote? If we simply write a double quote inside the two double quotes that enclose our string, the compiler will freak out. We need to _escape_ it using a backslash, so we write `\"`.

## Programming Constructs in C

### Conditions

  * Conditions in C look like so:

	    if (condition)
	    {
	        // do this
	    }

  * Note the encapsulation provided by the curly braces again. The `//` denotes a comment, a line of English that explains the code.

  * A two-way fork in logic looks like this:

	    if (condition)
	    {
	        // do this
	    }
	    else
	    {
	        // do that
	    }

  * A three-way fork in logic looks like this:

	    if (condition)
	    {
	        // do this
	    }
	    else if (condition)
	    {
	        // do that
	    }
	    else
	    {
	        // do this other thing
	    }

  * The quote strings and variables we’ve been passing to `printf` between the parentheses are known as _arguments_. An argument is a value that influences the behavior of the function.

### Boolean Expressions

  * The Boolean operators "and" and "or" are written as `&&` and `||` in C:

	    if (condition && condition)
	    {
	        // do this
	    }
	    if (condition || condition)
	    {
	        // do this
	    }

  * Note that `&` and `|` have different meaning!

### Switches

  * _Switches_ are another way of implementing forks in logic. Instead of repeated "else if" blocks, you can handle cases like so:

	    switch (x)
	    {
	        case 1:
	            // do this
	            break;

	        case 2:
	            // do that
	            break;

	        default:
	            // do this other thing
	            break;
	    }

### For Loops

  * for loops take the following general structure:

	    for (initializations; condition; updates)
	    {
	        // do this again and again
	    }

  * Within the parentheses after the `for` keyword, there are three parts. Before the first semicolon, we are initializing a variable which will be our iterator or counter, often named `i` by convention. Between the two semicolons, we’re providing a condition which, if true, will cause another iteration of the loop to be executed. Finally, we provide code to update our iterator.

  * A snippet of code to print "hello, world!" ten times would look something like:

	    for (int i = 0; i < 10; i++)
	    {
	        printf("hello, world!\n");
	    }

  * Recall that `i%2B%2B` is shorthand for "increment the value of `i` by 1." This loop continues executing so long as `i &lt; 10`, which happens 10 times.

  * A while loop is functionally equivalent to a for loop, albeit with slightly different syntax. Consider this code that prints out "hello, world!" infinitely:

	    while (true) {
	        print("hello, world\n");
	    }

  * As soon as the condition between the parentheses after `while` evaluates to false, the loop will terminate. In this case, however, `true` will never be false, so the loop continues forever.

  * A do while loop executes before checking the condition it depends on. That means it will always execute at least once. The general structure is as follows:

	    do
	    {
	        // do this again and again
	    }
	    while (condition);

### Variables

  * Syntactically, declaring a variable looks like so:

	    int counter;
	    counter = 0;

  * _Declaring a variable_ means asking the computer for some number of bits in which to store a value, in this case the value of an integer. The second line of code above _assigns_ the value 0 to the variable `counter`. `=` is the assignment operator and instructs the computer to put the right in the left.

  * We can do variable declaration and assignment all in one line:

		int counter = 0;

  * This one is a little easier to read and should be considered best practice.

### Functions

* A _function_ is a piece of code that can take input and can produce output.
  In some cases, a function can be a so-called _black box_. This means that
  the details of its implementation aren’t relevant. We don’t care **how** it
  does what it does, just that it does it.

* Let’s represent `printf` with an actual black box onstage. We can write
  "hello, world" on a piece of paper to represent an argument to `printf`. We
  then place this piece of paper in the black box and, by whatever means, the
  words "hello, world" appear on the screen!

* To make our `hello` program more dynamic, we asked the user for his or her
  name and passed that to `printf`:

	    string name = GetString();
	    printf("hello, %s\n", name);

* `printf` doesn’t return anything; it only has the _side effect_ of printing
  to the screen. `GetString`, on the other hand, returns what the user typed
  in.

* As with `printf`, we don’t necessarily care how `GetString` is implemented.
  We know that when we call it, we’ll be provided with a string after some
  amount of time. We can simulate this by retrieving from the black box a
  piece of paper with a student’s name (Obasi) written on it. We actually
  then make a copy of this string before storing it in `name`.

* Now we have `name` written on one piece of paper which will act as the
  second argument to `printf`. Next we create the first argument by writing
  "hello, %s " on another piece of paper. Finally, we place these two pieces
  of paper in the black box and magically, "hello, Obasi" appears on the
  screen.

* Functions that we implemented in the CS50 Library (`cs50.h`) include:

    * `GetChar`
    * `GetDouble`
    * `GetFloat`
    * `GetInt`
    * `GetLongLong`
    * `GetString`

* Convention holds that C function names are lowercase, but we capitalized
  these just to make it clear that they belong to the CS50 Library.

* A float is a number with a decimal point. A double is a number with a
  decimal point but with more numbers after the decimal point. These types
  returned by CS50 Library function require different number of bits to be
  stored. A `char` requires 8 bits, a `float` requires 32 bits, and a
  `double` requires 64 bits. A `long long` is an integer that is twice as big
  in memory (64 bits) as an `int` (32 bits). More on these types later.

* The CS50 Library also contains two custom types:

    * `bool`
    * `string`

* For convenience, we have created the symbols `true` and `false` to
  represent 1 and 0. Likewise for convenience, we have created a `string`
  type to store strings.

* The actual types of variables available in C are as follows:

    * `char`
    * `double`
    * `float`
    * `int`
    * `long long`

* The `printf` function can take many different formatting characters. Just a
  few of them are:

    * `%c` for `char`
    * `%i` (or `%d`) for `int`
    * `%f` for `float`
    * `%lld` for `long long`
    * `%s` for `string`

* A few more escape sequences:

    * ` ` for newline
    * ` ` for carriage return (think typewriter)
    * `\'` for single quote
    * `\"` for double quote
    * `\` for backslash
    * `` for null terminator

## Hellos and More

### `hello-0.c`

* As before, we’ll open a file in gedit on the Appliance and save it to the
  `jharvard` directory. We’ll call this file `hello-0.c` and write the
  following therein:

	    int main(void)
	    {
	        printf("hello, world\n");
	    }

* When we type `make hello-0` in the terminal window at bottom, we get all
  sorts of compiler errors. At the top of these errors, which tend to
  compound each other, we see:

		...implicitly declaring library function 'printf'...

* This error message may seem overwhelming, but try looking for keywords.
  Right away we notice `printf`. We forgot to include the library that
  contains the definition of `printf`:

	    #include <stdio.h>

	    int main(void)
	    {
	        printf("hello, world\n");
	    }

### `hello-1.c`

* To say hello to the user, we need a variable to store his or her name:

	    #include <stdio.h>

	    int main(void)
	    {
	        string name = "David";
	        printf("hello, %s\n", name);
	    }

* For now, we hardcode the value "David" into the variable `name`. This time
  when we compile (simply hit the up arrow to see previous commands in
  Linux), we get the following error:

		...use of undeclared identifier 'string'

* We need to also include the CS50 Library:

	    #include <cs50.h>
	    #include <stdio.h>

	    int main(void)
	    {
	        string name = "David";
	        printf("hello, %s\n", name);
	    }

* Sigh, still more compiler errors. The topmost one says:

		...multi-character character constant...

* That doesn’t help us too much, but `clang` does point us to the problem are
  with a green caret. Turns out that in C, strings must be delimited by
  double quotes, not single quotes:

	    #include <cs50.h>
	    #include <stdio.h>

	    int main(void)
	    {
	        string name = "David";
	        printf("hello, %s\n", name);
	    }

### `hello-2.c`

* Finally, let’s actually accept dynamic input from the user:

		#include <cs50.h>
		#include <stdio.h>

		int main(void)
		{
		    printf("State your name: ");
		    string name = GetString();
		    printf("hello, %s\n", name);
		}

* This program compiles and functions correctly for normal names like Rob,
  Lauren, and Joseph. What about an empty name? It just prints out "hello, ";
  perhaps we should use a condition and a loop so that we keep prompting the
  user until he provides a non-empty name.

### `adder.c`

* If we want to ask the user for integer input, we can use the `GetInt`
  function:

		#include <cs50.h>
		#include <stdio.h>

		int main(void)
		{
		    // ask user for input
		    printf("Give me an integer: ");
		    int x = GetInt();
		    printf("Give me another integer: ");
		    int y = GetInt();

		    // do the math
		    printf("The sum of %i and %i is %i!\n", x, y, x + y);
		}

* Notice that we don’t need a separate variable to store the sum, we can
  inline `x + y`.

### `conditions-0.c`

* `conditions-0.c` has a subtle bug in it:

		#include <cs50.h>
		#include <stdio.h>

		int main(void)
		{
		    // ask user for an integer
		    printf("I'd like an integer please: ");
		    int n = GetInt();

		    // analyze user's input (somewhat inaccurately)
		    if (n > 0)
		    {
		        printf("You picked a positive number!\n");
		    }
		    else
		    {
		        printf("You picked a negative number!\n");
		    }
		}

* Although this program is syntactically correct (it compiles and runs), it
  is logically incorrect (it declares 0 a negative number).

### `conditions-1.c`

  * To handle the corner case of 0, we need another fork in logic:

		#include <cs50.h>
		#include <stdio.h>

		int main(void)
		{
		    // ask user for an integer
		    printf("I'd like an integer please: ");
		    int n = GetInt();

		    // analyze user's input
		    if (n > 0)
		    {
		        printf("You picked a positive number!\n");
		    }
		    else if (n == 0)
		    {
		        printf("You picked zero!\n");
		    }
		    else
		    {
		        printf("You picked a negative number!\n");
		    }
		}

* Note that to test equality, we use `==`, not `=`, which is the assignment
  operator.

## Teaser

* It turns out that computers cannot express some values perfectly precisely.
  The protagonists in the movie [Office Space][5] take advantage of this
  imprecision to rip off their company Initech. Consider that if banking
  software stores a number like 0.1 improperly, it could mean that there are
  fractions of a cent gained or lost. If you haven’t seen Office Space,
  that’s your homework for the weekend.

[1]: http://www.youtube.com/watch?v=_d6KuiuteIA
[2]: http://cs50.net/section
[3]: http://cs50.net/ohs:
[4]: http://cs50.net/appliance
[5]: http://www.youtube.com/watch?v=G_wiXgRWrIU
