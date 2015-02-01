Lecture notes by Andrew Sellergren. [Watch the video.](http://cs50.tv/2013/fall/lectures/1/m/)

## Announcements and Demos

  * Next time you're milling about the Science Center, take a gander at the [Mark I][1], one of the very first electromechanical computers capable of long self-sustained computation. Check out [this giant calculator][2]. From this same Mark I computer comes the term "bug" that we take for granted. One of the engineers discovered an actual moth in the machine that was causing some incorrect calculations. The moth was then taped to a log book for posterity's sake.

  * To help make the class feel a bit more intimate, we'll be gathering most Fridays at Fire and Ice in Harvard Square for a casual lunch. If you're interested, RSVP [here][3].

  * Avail yourself of the following resources at [cs50.net/lectures][4] to aid you in your quest through CS50:

    * videos

      * If you click the icon at the bottom right in the video player, you'll see a searchable full transcript of the lecture.

    * slides

    * examples

    * walkthroughs

      * To illuminate some of the more complex examples from lecture, we offer walkthroughs of those examples. Check out the first round [here][5].

    * scribe notes

      * Welcome to the scribe notes! This is your canonical source of notes for each lecture so that you don't have to scribble down anything while listening to David. This is also your canonical source for jokes made at David's expense.

  * Sectioning starts Wednesday. This Sunday [[Sunday Sunday Someday!][6]] we'll offer a one-time supersection led by the course heads and available on video afterward.

  * It's time to introduce our inimitable course heads: Lauren Carvalho, Rob Bowden, Joseph Ong, R.J. Aquino, and Lucas Freitas. Feel free to reach out to them at [heads@cs50.net][7].

  * Problem Set 0 has been released!

  * [Office Hours][8] will begin soon! There really are no dumb questions. [Except for once when David asked me what's the deal with the internet and cats. Duh.]


  * [CS50 Discuss][9] is the course's forum where you can post any and all questions you have. We'll monitor it during lecture so that if you have a question about something David says, you can post it and we'll try to respond in realtime.

  * If you come into this course with little or no prior background in computer science or you'd just like to have the safety net of being able to call it quits when you're 90% done with a problem set on a Thursday night, you should consider taking the course SAT/UNS. Trust us, you'll still learn plenty!

## From Last Time

  * In Scratch, we worked with purple puzzle pieces starting with verbs like "say" that represented _statements_.

  * The blue hexagonal puzzle pieces that ended in question marks we deemed _boolean expressions_.

  * We used these boolean expressions inside of _conditions_, which represented branches in our program's logic.

  * The puzzle pieces that contain the words "repeat" and "forever" are examples of _loops_.

  * We wrote our own _functions_ using the purple curved puzzle pieces containing the word "define." A function is a chunk of code that we want to use over and over again without having to copy and paste.

## From Scratch to C

  * Recall that source code looks something like the following:

		int main(void)
		{
			printf("hello, world");
		}

  * The blue "say" puzzle piece from Scratch has now become `printf` and the orange "when green flag clicked" puzzle piece has become `main(void)`.

  * However, source code is not something a computer actually understands. To translate source code into something the computer understands, we'll need a _compiler_. A compiler is a program that takes source code as input and produces 0's and 1's, a.k.a. object code, as output.

  * We won't trouble ourselves with knowing the exact mapping between a series of 0's and 1's and the "print" command. Rather, we'll content ourselves with writing instructions at a higher level that can be translated to a lower level. This is consistent with one of the themes of the course: layering on top of the work of others.

  * Statements are direct instructions, e.g. "say" in Scratch or `printf` in C.

  * The "forever" loop from Scratch can be recreated with a `while (true)` block in C. The "repeat" loop from Scratch can be recreated with a `for` block in C.

  * Note that in C just as in Scratch, there are multiple ways of achieving the same goals.

  * In C, a loop that increments a variable and announces its value would look like so:

	    int counter = 0;
	    while (true)
	    {
	        printf("%i", counter);
	        counter++;
	    }

  * Here we declare a variable named `counter` and then create an infinite loop that prints its value then increments it.

  * Boolean expressions are much the same in C as in Scratch. The less-than (``) operators are the same. One difference is that the "and" operator is represented as `&amp;&amp;` in C.

  * Conditions in C look much the same as they do in Scratch:

	    if (x < y)
	    {
	        printf("x is less than y");
	    }
	    else if (x > y)
	    {
	        printf("x is greater than y");
	    }
	    else
	    {
	        printf("x is equal to y");
	    }


## `hello, world!`

  * The CS50 Appliance is software running inside of your normal computer's environment that simulates the environment of another operating system, namely Fedora Linux. At the bottom left of the Appliance window are three icons for gedit, Chrome, and Terminal. Since we can code in any text editor, let's start by opening gedit.

  * In gedit, there are three main divisions of the window:

    * on the left, the source code pane

    * on the right, the actual text editor, where we write code

    * on the bottom, the terminal, where we run commands

  * Note that all of your files by default save to the `jharvard` directory, which is unique to your Appliance and is not shared with other students. All of your files in the `Dropbox` subdirectory are automatically backed up in the cloud. In this directory, we'll save our file as `hello.c`.

  * Now let's quickly rewrite that first program in C:

	    #include <stdio.h>

	    int main(void)
	    {
	        printf("hello, world!");
	    }

  * To actually run this program, we click on the terminal at the bottom of gedit. To begin, we're in the `jharvard` directory. On other operating systems, we can simply double click on another directory in order to open it. But in the terminal, we can only use the keyboard. So to get to the `Dropbox` folder, we instead type `cd Dropbox`. Now if we type `make hello`, we see a bit of cryptic syntax, but afterward, we can run `./hello` and see our program execute successfully.

  * A single dot (`.`) refers to the current directory. Typing `./hello` instructs the computer to look for a program named `hello` in the current directory. Type `ls` to see the contents of the current directory. In green, you'll see `hello`, which is the executable program that we just compiled. Recall that we use a _compiler_ to translate the source code above into the object code that the computer can actually understand.

## Linux Commands

  * As an aside, here's a short list of Linux commands that you'll find useful:

    * `ls`

      * stands for "list," shows the contents of the current directory

    * `mkdir`

      * stands for "make directory," creates a new folder

    * `cd`

      * stands for "change directory," the equivalent of double clicking on a folder

    * `rm`

      * stands for "remove," deletes a file

    * `rmdir`

      * stands for "remove directory," deletes a directory

## Compiling

  * When we type `make hello` in the terminal, the command that actually runs is as follows:

		clang -ggdb3 -00 -std=c99 -Wall -Werror hello.c -lcs50 -lm -o hello

  * `make` is not actually a compiler, but rather a program that shortcuts these options to the compiler, which in this case is `clang`. The shorter version of the command above is:

		clang -o hello hello.c

  * `-o` is a switch or flag, an option that influences the behavior of the program. In this case, the value provided after `-o` is `hello`, which becomes the name of the executable that the compiler creates. We could've typed `-o hihihi` and our executable would then have been named `hihihi`. The flags that we pass to a program are special examples of _command-line arguments_.

## User Input

  * To make our program more interesting, let's try asking the user for a name and saying hello to her. To do this, we need a place to store the user's name, i.e. a variable. A variable that stores a word or a phrase is known as a _string_. Let's call this variable `name`:

        #include <stdio.h>

	    int main(void)
	    {
	        string name;
	        name = GetString();
	        printf("hello, David");
	    }


  * Before we ask the user for her name, the variable `name` has no value. We shouldn't print it out as such.

  * `GetString` is a function provided in the CS50 Library written by the staff. `GetString` takes in user input and passes it back to your program as a string. The `=` in this case is an assignment operator, meaning place in the left side the value of the right side.

  * Now when we try to compile this program, we get all sorts of errors. When the compiler prints out this many errors, it's a good idea to work your way through them from top to bottom because the errors at bottom might actually have been caused by the errors at the top. The topmost error is as follows:

		hello.c:5:5 error: use of undeclared identifier 'string': did you mean 'stdin'?

  * No, we didn't mean `stdin`! However, the variable type `string` is actually not built in to C. It's available via the CS50 Library. To use this library, we actually need to tell our program to include it like so:

	    #include <cs50.h>
	    #include <stdio.h>

	    int main(void)
	    {
	        string name;
	        name = GetString();
	        printf("hello, David\n");
	    }


  * When we compile and run this, the program appears to do nothing: the cursor simply blinks. This is because it's waiting for the user to type something. When we type "Rob," the program still prints out "hello, David," which isn't quite what we intended. Let's add a line to clarify to the user that he's supposed to type something:

		#include <cs50.h>
		#include <stdio.h>

		int main(void)
		{
		    string name;
		    printf("What is your name?");
		    name = GetString();
		    printf("hello, David\n", );
		}


  * When we run the program, nothing seems to have changed. Oops, we forgot to recompile.

  * One thing we can improve is to add a newline between the question and the blinking cursor. We do this by adding the ` ` character.

  * What we really want is to print out the user-provided name, which is stored in `name`. Thus, we nee to pass `name` to `printf` like so:

	    #include <cs50.h>
	    #include <stdio.h>

	    int main(void)
	    {
	        string name;
	        printf("What is your name?\n");
	        name = GetString();
	        printf("hello, %s\n" name);
	    }

  * What's between the parentheses after `printf` are the _arguments_ that we pass it. Here, we pass two arguments. `%s` is a placeholder for the second argument, `name`, which gets inserted into the first argument.

  * In addition to the CS50 Library, we're including `stdio.h`, the library the contains the definition of `printf`.

## Loops

  * Let's write a silly little program with an infinite loop:

	    #include <cs50.h>
	    #include <stdio.h>

	    int main(void)
	    {
	        while (true)
	        {
	            printf("I am a buggy program");
	        }
	    }

  * Since the loop condition `true` is always true, the loop continues executing indefinitely. Compiling and running this program prints a whole lot of text to the terminal! You don't need to restart your Appliance to stop the program, just type Ctrl%2BC.

  * Now let's write a counter program:

	    #include <cs50.h>
	    #include <stdio.h>

	    int main(void)
	    {
	        for (int i = 0; i < 100; i++)
	        {
	            printf("I can count to %i\n", i);
	        }
	    }

  * Ignore the cryptic syntax for now, but know that this program counts (very fast) to 100. What if we made a mistake and typed `i &gt;= 0` instead of `i &lt; 100` as the second loop condition? We would unintentionally induce an infinite loop. On Wednesday we'll see if this program has finished!

[1]: http://en.wikipedia.org/wiki/Harvard_Mark_I
[2]: http://www.youtube.com/watch?v=Uw1-UtwXtGw
[3]: http://cs50.net/rsvp
[4]: http://cs50.net/lectures
[5]: https://www.cs50.net/lectures/0/f/examples
[6]: http://www.youtube.com/watch?v=dChdT_XKmWc
[7]: mailto:heads%40cs50.net
[8]: http://cs50.net/ohs
[9]: http://cs50.net/discuss
