#Objectives

* Get comfortable with Linux.

* Start thinking more carefully.

* Solve some problems in C.


# Appliance

This text assumes you have the appliance up and running. If not, head back to the [Linux problem set](http://prog1.mprog.nl/problem-sets/0-linux) for instructions on how to do so.


# File Manager

Okay, let’s create a folder (otherwise known as a "directory") in which your code for this problem set will soon live. Go ahead and double-click *Home* on John Harvard’s desktop (toward the appliance’s top-left corner). A window entitled *jharvard - File Manager* should appear, indicating that you’re inside of John Harvard’s "home directory" (i.e., personal folder). Then double-click the folder called `Dropbox`, at which point the window’s title should change to *Dropbox - File Manager*. Next select *File* > *Create Folder…* in the window’s top-left corner, input a name of `pset1`, and then click *Create*. (If you misname the folder, control-click the misnamed folder, select *Rename…*, enter a new name, and click *Rename*.) Then double-click that `pset1` folder to open it. The window’s title should change to *pset1 - File Manager*, and you should see an otherwise empty folder (since you just created it).


## Gedit

Okay, go ahead and close any open windows, then select *Menu* > *Accessories* > *gedit*. (Recall that *Menu* is in the appliance’s bottom-left corner.) A window entitled *Untitled Document 1 - gedit* should appear, inside of which is a tab entitled *Untitled Document 1*. Clearly the document is just begging to be saved. Go ahead and type `hello` (or the ever-popular `asdf`) on line 1 of the document, and then notice how the tab’s name is now prefixed with an asterisk (\*), indicating that you’ve made changes since the file was first opened. Select *File* > *Save*, and a window entitled *Save As* should appear. Input `hello.txt` next to *Name*, then click *Home* under *Places*. You should then see the contents of John Harvard’s home directory. Double-click `Dropbox`, then double-click `pset1`, and you should find yourself inside that empty folder you created. Now, at the bottom of this same window, you should see that the file’s default *Character Encoding* is *Unicode (UTF-8)* and that the file’s default *Line Ending* is *Unix/Linux*. No need to change either; just notice they’re there. That the file’s *Line Ending* is *Unix/Linux* just means that *gedit* will insert (invisibly) `\n` at the end of any line of text that you type. Windows, by contrast, uses `\r\n`, and Mac OS uses `\r`, but more on those (delightfully annoying) details some other time.

Okay, click *Save* in the window’s bottom-right corner. The window should close, and you should see that the original window’s title is now *hello.txt (~/Dropbox/pset1) - gedit*. The parenthetical just means that `hello.txt` is inside of `pset1`, which is inside of `Dropbox`, which is inside of `~`, which is shorthand notation for John Harvard’s home directory. A useful reminder is all. The tab, meanwhile, should now be entitled `hello.txt` (with no asterisk, unless you accidentally hit the keyboard again).

Okay, with `hello.txt` still open in *gedit*, notice that beneath your document is a "terminal window" (aka "terminal emulator"), a command-line (i.e., text-based) interface via which you can navigate the appliance’s hard drive and run programs (by typing their name). Notice that the window’s "prompt" is

	jharvard@appliance (~):

which means that you are logged into the appliance as John Harvard and that you are currently inside of ~ (i.e., John Harvard’s home directory). If that’s the case, there should be a `Dropbox` directory somewhere inside. Let’s confirm as much.

Click somewhere inside of that terminal window, and the prompt should start to blink. Type

	cd Dropbox/pset1

followed by Enter to change your directory to `~/Dropbox/pset1`. You should find that your prompt changes to

	jharvard@appliance (~/Dropbox/pset1):

confirming that you are indeed now inside of `~/Dropbox/pset1` (i.e., a directory called `pset1` inside of a directory called `Dropbox` inside of John Harvard’s home directory). Now type

	ls

followed by Enter. You should see `hello.txt`! Now, you can’t click or double-click on that file’s name there; it’s just text. But that listing does confirm that `hello.txt` is where we hoped it would be.

For now, close *gedit* (via *File* > *Quit*) and, with it, `hello.txt`.


# Hello, C

First, a hello from Zamyla if you’d like a tour of what’s to come, particularly if less comfortable. Note that her version of the CS50 Appliance might look a bit different from yours, but not a problem.

<iframe width="711" height="400" src="https://www.youtube.com/embed/HkQD6aw7oDc" frameborder="0" allowfullscreen></iframe>

Shall we have you write your first program? Go ahead and launch *gedit*. (Remember how?) You should find yourself faced with another *Unsaved Document 1*. Go ahead and save the file as `hello.c` (not `hello.txt`) inside of `pset1`, just as before. (Remember how?) Once the file is saved, the window’s title should change to *hello.c (~/Dropbox/pset1) - gedit*, and the tab’s title should change to *hello.c*. (If either does not, best to close *gedit* and start fresh! Or ask for help!)

Go ahead and write your first program by typing these lines into the file (though you’re welcome to change the words between quotes to whatever you’d like):

		#include <stdio.h>

		int main(void)
		{
    		printf("hello, world\n");
		}

Notice how *gedit* adds "syntax highlighting" (i.e., color) as you type. Those colors aren’t actually saved inside of the file itself; they’re just added by *gedit* to make certain syntax stand out. Had you not saved the file as `hello.c` from the start, *gedit* wouldn’t know (per the filename’s extension) that you’re writing C code, in which case those colors would be absent.

Do be sure that you type in this program just right, else you’re about to experience your first bug! In particular, capitalization matters, so don’t accidentally capitalize words (unless they’re between those two quotes). And don’t overlook that one semicolon. C is quite nitpicky!

When done typing, select *File* > *Save* (or hit ctrl-s), but don’t quit. Recall that the leading asterisk in the tab’s name should then disappear. Click anywhere in the terminal window beneath your code, and its prompt should start blinking. But odds are the prompt itself is just

	jharvard@appliance (~):

which means that, so far as the terminal window’s concerned, you’re still inside of John Harvard’s home directory, even though you saved the program you just wrote inside of `~/Dropbox/pset1` (per the top of *gedit*'s window). No problem, go ahead and type

	cd Dropbox/pset1

or

	cd ~/Dropbox/pset1

at the prompt, and the prompt should change to

	jharvard@appliance (~/Dropbox/pset1):

in which case you’re where you should be! Let’s confirm that `hello.c` is there. Type

	ls

followed by Enter, you should see a new file, `hello`, alongside `hello.c` and `hello.txt`.

If, though, upon running **make**, you instead see some error(s), it’s time to debug! (If the terminal window’s too small to see everything, click and drag its top border upward to increase its height.) If you see an error like expected declaration or something no less mysterious, odds are you made a syntax error (i.e., typo) by omitting some character or adding something in the wrong place. Scour your code for any differences vis-à-vis the template above. It’s easy to miss the slightest of things when learning to program, so do compare your code against ours character by character; odds are the mistake(s) will jump out! Anytime you make changes to your own code, just remember to re-save via *File* > *Save* (or ctrl-s), then re-click inside of the terminal window, and then re-type

	make hello

at your prompt, followed by Enter. (Just be sure that you are inside of `~/Dropbox/pset1` within your terminal window, as your prompt will confirm or deny.) If you see no more errors, try running your program by typing

	./hello

at your prompt, followed by Enter! Hopefully you now see precisely the below?

	hello, world

If not, reach out for help!

Incidentally, if you find *gedit*​'s built-in terminal window too small for your tastes, know that you can open one in its own window via *Menu* > *Programming* > *Terminal*. You can then alternate between *gedit* and *Terminal* as needed, as by clicking either’s name along the appliance’s bottom.

Woo hoo! You’ve begun to program!


# CS50 Check

Now let’s see if the program you just wrote is correct! Included in the CS50 Appliance is **check50**, a command-line program with which you can check the correctness of (some of) your programs.

If not already there, navigate your way to `~/Dropbox/pset1` by executing the command below.

	cd ~/Dropbox/pset1

If you then execute

	ls

you should see, at least, `hello.c`. Be sure it’s indeed spelled `hello.c` and not `Hello.c`, `hello.C`, or the like. If it’s not, know that you can rename a file by executing

	mv source destination

where **source** is the file’s current name, and **destination** is the file’s new name. For instance, if you accidentally named your program `Hello.c`, you could fix it as follows.

	mv Hello.c hello.c

Okay, assuming your file’s name is definitely spelled `hello.c` now, go ahead and execute the below. Note that `2014.fall.pset1.hello` is just a unique identifier for this problem’s checks.

	check50 2014.fall.pset1.hello hello.c

Assuming your program is correct, you should then see output like

		:) hello.c exists
		:) hello.c compiles
		:) prints "hello, world\n"

where each :) means your program passed a check (i.e., test). You may also see a URL at the bottom of check50's output, but that’s just for staff (though you’re welcome to visit it).

If you instead see :\| or :( smileys, it means your code isn’t correct! For instance, suppose you instead see the below.

		:( hello.c exists
		  \ expected hello.c to exist
		:| hello.c compiles
		  \ can't check until a frown turns upside down
		:| prints "hello, world\n"
		  \ can't check until a frown turns upside down

Because **check50** doesn’t think `hello.c` exists, as per the red smiley, odds are you uploaded the wrong file or misnamed your file. The other smileys, meanwhile, are yellow because those checks are dependent on `hello.c` existing, and so they weren’t even run.

Suppose instead you see the below.

		:) hello.c exists
		:) hello.c compiles
		:( prints "hello, world\n"
		  \ expected output, but not "hello, world"

Odds are, in this case, you printed something other than `hello, world\n` verbatim, per the spec’s expectations. In particular, the above suggests you printed `hello, world`, without a trailing newline (`\n`).

Know that check50 lets you check your work’s correctness before you submit your work. Once you actually submit your work (per the directions at this spec’s end), our staff will use check50 to evaluate your work’s correctness officially.


# CS50 Style

In addition to **check50**, the CS50 Appliance comes with **style50**, a tool with which you can evaluate your code’s style vis-à-vis our [style guide](http://prog1.mprog.nl/resources/style-guide). To run it on, say, `hello.c`, execute the below:

	style50 hello.c

You should see zero or more lines of suggestions. Yellow smileys indicate warnings that you should consider addressing. Red smileys indicate errors that you should definitely address.

*If you instead see **java: command not found**, execute **sudo apt-get -y install default-jre-headless** (which will install software that we forgot to install for you!), then try again.*

*Note that **style50** is still a work in progress (a "beta" version, so to speak), so best to consult our [style guide](http://prog1.mprog.nl/resources/style-guide) for official guidance.*


# Shorts

Curl up with Nate’s short on libraries. Be sure you’re reasonably comfortable answering the below when it comes time to submit this problem set’s form!

<iframe width="711" height="400" src="https://www.youtube.com/embed/ED7QtgXDShY" frameborder="0" allowfullscreen></iframe>

* What's a library?

* What role does
		
		#include <cs50.h>

	play when you write it atop some program?

* What role does

		-lcs50

	play when you pass it as a "command-line argument" to **clang**? (Recall that **make**, the program we’ve been using to compile programs in lecture, simply calls **clang** with some command-line arguments for you to save you some keystrokes.)

Curl up with at least two other shorts at [https://cs50.harvard.edu/shorts/1](). Some additional questions may be in your future!


# Hello again, C

Before forging ahead, you might want to review some of the examples that we looked at in Week 1’s lectures and take a look at a few more, the "source code" for which can be found at [https://cs50.harvard.edu/lectures/1](). Allow me to take you on a tour, though feel free to forge ahead on your own if you’d prefer. Not to worry if your appliance also looks a bit different from mine.

<iframe width="711" height="400" src="https://www.youtube.com/embed/bQnyxpf0vk0?list=PLhQjrBD2T380JCGC3qD3nGpqt8iIjx2fV" frameborder="0" allowfullscreen></iframe>


# Itsa Mario

Toward the end of World 1-1 in Nintendo’s Super Mario Brothers, Mario must ascend a "half-pyramid" of blocks before leaping (if he wants to maximize his score) toward a flag pole. Below is a screenshot.

  ![Mario!](pset11.png)

Write, in a file called `mario.c` in your `~/Dropbox/pset1 directory`, a program that recreates this half-pyramid using hashes (`#`) for blocks. However, to make things more interesting, first prompt the user for the half-pyramid’s height, a non-negative integer no greater than `23`. (The height of the half-pyramid pictured above happens to be `8`.) If the user fails to provide a non-negative integer no greater than `23`, you should re-prompt for the same again. Then, generate (with the help of `printf` and one or more loops) the desired half-pyramid. Take care to align the bottom-left corner of your half-pyramid with the left-hand edge of your terminal window, as in the sample output below, wherein underlined text represents some user’s input.

		jharvard@appliance (~/Dropbox/pset1): ./mario
		Height: 8
		       ##
		      ###
		     ####
		    #####
		   ######
		  #######
		 ########
		#########

Note that the rightmost two columns of blocks must be of the same height. No need to generate the pipe, clouds, numbers, text, or Mario himself.

By contrast, if the user fails to provide a non-negative integer no greater than `23`, your program’s output should instead resemble the below, wherein underlined text again represents some user’s input. (Recall that `GetInt` will handle some, but not all, re-prompting for you.)

		jharvard@appliance (~/Dropbox/pset1): ./mario
		Height: -2
		Height: -1
		Height: foo
		Retry: bar
		Retry: 1
		##

To compile your program, remember that you can execute

	make mario

or, more manually,

	clang -o mario mario.c -lcs50

after which you can run your program with the below.

	./mario

If you’d like to check the correctness of your program with **check50**, you may execute the below.

	check50 2014.fall.pset1.mario mario.c

And if you’d like to play with the staff’s own implementation of mario in the appliance, you may execute the below

	~cs50/pset1/mario

Not sure where to begin? Not to worry. A walkthrough awaits!

<iframe width="711" height="400" src="https://www.youtube.com/embed/z32BxNe2Sfc" frameborder="0" allowfullscreen></iframe>


# Final steps

* When you are done with `mario.c`, submit it by going over to the [Submit](#submit) tab. Be sure to compile and test one last time before you submit. (Note that you do not have to submit `hello.c`.)

* All done!
