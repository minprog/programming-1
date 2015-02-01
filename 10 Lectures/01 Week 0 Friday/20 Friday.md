Lecture notes by Andrew Sellergren. [Watch the video.](http://cs50.tv/2013/fall/lectures/0/f/)

## Announcements and Demos

  * Not sure about CS50? Don't take our word for it, listen to [Chi][1].

## From Last Time

  * We used desk lamps to represent transistors, both of which exist in one of two states: off and on. The off state corresponds to 0 in binary and the on state corresponds to 1 in binary.

  * We then used students to represent 0 and 1 in binary. A raised hand meant 1 and a hand at the side meant 0. With 8 students, we had 8 bits, called a byte. Together, these 8 bits signified numbers large enough to represent alphabetical characters using the ASCII encoding system.

  * We defined an algorithm as a series of instructions that can be executed to achieve a goal. Two goals we had were to count the number of students in the lecture hall and to find the name Smith in a phonebook. In case you missed it, here's [footage][2] of David tearing the phonebook in half.

  * We conveyed our algorithms in pseudocode, syntax meant to generically represent a programming language. The first pseudocode we looked at was for counting people in a room one at a time. To do this, we introduced a _variable_ `n`. A variable is a storage container, a chunk of some number of bits of memory, in which we can put values, images, words, etc. We also introduced a _loop_ so that we could execute the same logic multiple times. The "for each" syntax is common in describing a loop, as is indenting any lines of code that should execute within the loop:

	    let n = 0
	    for each person in room
	      set n = n %2B 1

  * With this algorithm in hand, we tried a few representative inputs to see if we got the desired outputs. For inputs of 0 and 2 people in the room, we got the correct outputs 0 and 2.

  * To make our algorithm a little more efficient, we modified it to count by twos instead of ones:

	    let n = 0
	    for each pair of people in room
	      set n = n %2B 2

  * Unfortunately, this code breaks when there is an odd number of people in the room. To redress this, we added a _condition_ after the loop:

	    let n = 0
	    for each pair of people in room
	      set n = n %2B 2
	    if 1 person remains then
	      set n = n %2B 1

## Introduction to Programming

### C

  * Henceforth, we'll be writing mostly _source code_, which, unlike pseudocode, must adhere to the syntax of the programming language in which it's written. We'll be writing this source code within the CS50 Appliance, a piece of software that gives the illusion of an operating system called Linux running within your computer's normal environment.

  * Whether you have a Mac or a PC, you can use any number of text editors to write source code.
[Although if you use `emacs` you're just wrong.]
Using the text editor gEdit, let's write a short program in C:

	    #include <stdio.h>

	    int main(void)
	    {
	        printf("hello, world!");
	    }

  * At the bottom of gEdit is a terminal window that we can use to execute a command that will, as its name suggests, make our program:

        make hello


  * `make` looks for a file named `hello.c` and passes it to a _compiler_ named `clang`. Once it's done so, we can execute this command to see "hello, world!" printed to the screen:

        ./hello


  * Given how much this arcane syntax gets in the way of the underlying programming concepts, we're going to set aside C for now. Instead, we'll be using a graphical programming language named Scratch.

### Scratch

  * To start working with Scratch, you'll need to login and register at MIT's [website][3]. Instructions for this are detailed in specification for Problem Set 0.

  * Once you click Create to start a new project, take note of the following layout:

    * At far left is the stage, where the program will be carried out.

    * In the middle is the “palette” of puzzle pieces, which represent programming statements. Programs will be composed by putting puzzle pieces together in a particular order.

    * At bottom left are sprites, or characters that will carry out your instructions.

    * To the right of the palette is the scripts area, where puzzle pieces must be dragged and strung together.

  * The puzzle pieces under the Control category are curved on the top so that they don't interlock with any other pieces. This is because they denote the start of a program.

  * We can recreate our very simple C program in Scratch using the "say" puzzle piece. `[hello, world.sb2`][4] is equivalent to `hello.c`, only a little more colorful.

  * Note that Scratch is also a standalone program that you can download to write and execute code.

  * Yes, `[hello, world.sb2`][4] is pretty simple, but take a look at [Scratch, Scratch Revolution][5] to see what is possible in Scratch. The footage you see through Vanessa's eyes is from Google Glass. Thanks, Google!
[For my job, too!]


  * Now take a look at [Cookie Love Story][6] and think about what programming constructs you might use to implement it. In Scratch, as in most programming languages, for example, there exists the concept of _events_ that trigger some piece of source code to execute.

  * Before we go any farther, let's talk about some computer science jargon: a _statement_ is an action that we give to the computer to perform. In the context of Scratch, statements begin with verbs like "say," "play," and "wait."

  * So far we've only made use of statements, which are direct imperatives given to the computer. But if we want to introduce logic into our program, we'll need boolean expressions and conditions.

    * _Boolean expressions_ are those that have only two possible values: true or false, yes or no, on or off, 1 or 0. No matter how you say it, it's a simple variable. In Scratch, boolean expressions are represented as hexagons and are written as yes-or-no questions such as "touching mouse-pointer?," "mouse down?" or comparisons such as less-than, equal-to, or greater-than. In CS50 Courses, boolean expressions are used to implement the checkboxes for CUE score greater-than and "doesn't conflict with Courses I'm Taking."

    * _Conditions_ are forks in the logic of a program that execute depending on whether or not certain criteria are met. The if and if-else blocks in Scratch are examples of conditions that depend on Boolean expressions.

  * Also available to you in Scratch are loops, variables, and functions. More on those later.

  * By replacing the "say" block with a "play" block we can turn "hello, world" into [meow][7]. To make the program more interesting, we can add an if condition such that the cat will meow [approximately half the time][8]. The condition says, "pick a random number between 1 and 10 and if that number is less than 6, have the cat meow." If we want the cat to meow forever without having to click the green flag over and over again, we appropriately [use the forever block][9].

  * In [pet the cat][10], we combine a loop and a condition so that the cat will meow only if the mouse pointer is touching it or, in other words, if we are petting it. In [don't pet the cat][11], we add an extra condition (using the `else` keyword) so that the cat will meow indefinitely, but will roar if we touch it with the mouse pointer. In these, we have the beginnings of a game!

  * The [hi hi hi][12] program hints at the concept of _threading_, which involves multiple scripts executing simultaneously. In the logic of one of these scripts, we see that if a variable named `muted` is 0, we play the sound. Recall that 0 is equivalent to false, so this makes sense: if the script is not muted, it should play sound. The second script actually sets the variable `muted`: to 1 if it's currently 0 or to 0 if it's currently 1. This variable setting occurs when we press the space bar. Note that variables in programs should have descriptive names, as with `muted` here. These two scripts are sharing a _state_ between them: whether or not the program is muted.

  * So-called _infinite loops_, which sometimes signal a bug in the source code, are not always a bad thing. Take [counting sheep][13], for example, in which an infinite loop is used to increment a variable indefinitely.

  * Say we want to implement a program in which a cat coughs three times.

    * We could do this as in [cough-0][14] by duplicating statements (you can actually right click to do this), but it's not the most elegant solution.

    * The obvious way to clean this up is to use a repeat block, as in [cough-1][15]. This is better design because if we want to change the number of times the cat coughs, we simply change a variable rather than duplicating an entire statement. If you find yourself copying and pasting code, you should ask yourself if there's a better way to do it.

    * Our program would be even cleaner if we had our own cough block. We can do this in Scratch by clicking on More Blocks and Make a Block. As soon as we name it "cough," a curved puzzle piece reading "define cough" appears in the scripts window. Now we steal the "say" and "wait" blocks from our loop and link them to this "define cough" piece. In doing so, we've defined a _function_. Under More Blocks, a new purple block called "cough" has appeared. Take a look at the this implementation in [cough-2][16].

  * Now, say we want to implement a program in which a cat coughs and also sneezes.

    * Saying "achoo" is very similar to saying "cough," so we don't want to copy and paste the definition of the cough function and change the word that's said. Better would be to implement a higher-level function that takes inputs, also known as _arguments_. To do this in Scratch, click More Blocks and Make a Block, then expand the More Options menu. Thus, in [cough-4][17], we have a function which takes two arguments called `word` and `n`, or what should be said and how many times it should be said, respectively.

    * We're moving fast, but the take-away is that common functionality can be factored out so that code isn't repeated unnecessarily.

  * To revisit the concept of threading, consider the [threads][18] program. Here, we have two different scripts associated with two different sprites, a cat and a bird. For the cat, we begin by placing him in a given spot on the stage and orienting him in a random direction. Then we begin a loop whereby if he touches the bird, then the game ends; otherwise, we orient him toward the bird and advance him one step. For the bird, we move him around the stage three steps at a time. Effectively, then, the cat is chasing the bird until he catches him. If we increase the number of steps that the cat takes compared to the bird, the cat will catch the bird all the more quickly.

  * Another programming construct we'll become familiar with soon is that of _arrays_. Arrays are collections of related variables.

  * Events are another method of communicating between sprites. The [events][19] program leverages events to play the game of Marco Polo. Thus far, our sprites haven't really been communicating with each other. But in this game of Marco Polo, one sprite is saying "Marco," and the other is listening for him to say it so that she can say "Polo" in response. The second sprite is listening for the event which the first sprite broadcasts.

  * Even complex games like [Frogger][20] can be implemented using the concepts we've already been exposed to, e.g. events, conditions, statements. You can even use the webcam to trigger actions, as in [Move the Butterfly][21].

  * The objective of Problem Set 0 is for you to have fun playing around with Scratch. Make something interesting, interactive, artistic, fun. Don't feel like you need to implement Scratch Scratch Revolution, but hopefully you'll be proud of what you make, enough to show it off to your friends and family once you've uploaded it to MIT's website.

  * We leave you with [Raining Men][22]. While you enjoy it, think about how you might implement it!

   [1]: http://www.youtube.com/watch?v=SMrp9P2iuPs
   [2]: http://www.youtube.com/watch?v=P4fcOLN9heU
   [3]: http://scratch.mit.edu
   [4]: http://scratch.mit.edu/projects/12196962/
   [5]: http://scratch.mit.edu/projects/12199021/
   [6]: http://scratch.mit.edu/projects/12199076/
   [7]: http://scratch.mit.edu/projects/12199089
   [8]: http://scratch.mit.edu/projects/12199096
   [9]: http://scratch.mit.edu/projects/12199099/
   [10]: http://scratch.mit.edu/projects/12199100/
   [11]: http://scratch.mit.edu/projects/12199106/
   [12]: http://scratch.mit.edu/projects/12199112/
   [13]: http://scratch.mit.edu/projects/12198996
   [14]: http://scratch.mit.edu/projects/12197173/
   [15]: http://scratch.mit.edu/projects/12197255/#editor
   [16]: http://scratch.mit.edu/projects/12197294/
   [17]: http://scratch.mit.edu/projects/12197698/
   [18]: http://scratch.mit.edu/studios/247678/
   [19]: http://scratch.mit.edu/projects/12199034/
   [20]: http://scratch.mit.edu/projects/12199081/
   [21]: http://scratch.mit.edu/projects/10016382
   [22]: http://scratch.mit.edu/projects/10003491
  