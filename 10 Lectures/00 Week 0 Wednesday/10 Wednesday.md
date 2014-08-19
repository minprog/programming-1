Lecture notes by Andrew Sellergren. [Watch the video.](http://cs50.tv/2013/fall/lectures/0/w/)

## Announcements and Demos

  * [This is CS50.][1]

  * 73% of CS50 students have no prior computer science experience! You’re not alone!

## Binary

  * At the lowest level of computers, information is represented by electricity. You can think of the transistors that store this information as desk lamps that can be either on or off. The off state represents the number 0 and the on state represents the number 1.

  * To represent larger numbers, we use more than one desk lamp or transistor. Each desk lamp corresponds to a single bit of information. Just as each lamp has two possible states (on and off), each bit can take two possible values (1 and 0). With 2 desk lamps, we can represent 2 * 2 = 4 possible values. With 3 desk lamps, we can represent 2 * 2 * 2 = 8 possible values.

  * Writing binary numbers is identical to writing the decimal numbers that you’re familiar with. A number like 123 can be broken out like so:

        100's   10's   1's

        1       2      3

  * In binary, the 100’s, 10’s, and 1’s columns are replaced with 4’s, 2’s, and 1’s columns. Only the numbers 0 and 1 are allowed in each column.

        4's    2's   1's

        1      1     1

  * With 1 * 4, 1 * 2, and 1 * 1, we represent the number 7.

## ASCII

  * Now that we have binary to represent numbers, we need a way to represent alphabetic characters. Enter ASCII, an encoding system which represents every alphabetic character with a given number. For example, an uppercase "A" is represented by the number 65 and an uppercase "Z" is represented by the number 90.

  * With this encoding system, we can begin to spell out words. If we bring 8 volunteers on stage, we can allow each of them to represent a single bit. Together, they represent a number that we can map to a letter. When a volunteer raises her hand, her digit is a 1. Otherwise, her digit is a 0. After three rounds of this, we can represent the numbers 66, 79, and 87, or, according to our ASCII chart, the characters B, O, and W. And with that, our volunteers take a bow!

## Overview

  * It’s worth noting that this is _Introduction_ to Computer Science _I_. There’s also an Introduction to Computer Science II, so you’re in the right place if you have no prior knowledge of the subject matter (or even if you do).

  * CS50 is now offered with a SAT/UNS grading option! It’s far more important to engage with the material than to worry about grades. Learn more at the [FAQ][2].

  * CS50 is an introduction to the intellectual enterprises of computer science and the art of programming.

## Algorithms

### The Famous Phonebook Example

  * Back in the days when phone numbers weren’t stored in cell phones, you might have actually had to look them up in a phonebook. How did you go about that? If you wanted to look up someone with the last name "Smith," you could flip through the phonebook one page at a time. You don’t need to be a computer scientist to know that this is an inefficient approach.

  * Instead, we could start by flipping to the middle of the phonebook. Now we break the problem into two. Since we know that "Smith" isn’t in the left half of the alphabet, we can literally tear the phonebook in half, throw away the left half of the phonebook, and leave ourselves with only the right half. Once again, we flip to the middle and find ourselves at "R." We can again throw away the left half. As we continue tearing the book in half and throwing away pieces of it, we will eventually be left with a single page on which the name "Smith" appears (assuming it was there in the first place).

  * How do these two approaches compare in terms of their times to solve the problem? In the graph below, the first steep line (`n` in red) represents the approach of turning one page at a time. The second steep line (`n/2` in yellow) represents a slightly improved approach of turning two pages at a time. The curve (`log n` in green) represents our "tear and throw away" approach. As the size of the problem grows, the time to solve that problem doesn’t grow nearly as fast. In the context of this problem, `n` is the number of pages in the phonebook. As we go from 500 to 1000 to 2000 pages in the phonebook, we need only tear the phonebook in half one or two more times.

![Linear and logarithmic runtimes.][3]

### Counting People

  * In order to illustrate programming examples, we’ll often use _pseudocode_. Pseudocode is English-like syntax meant to represent a programming language. Check out [this TED-Ed video][4] which introduces the concept of an algorithm using pseudocode.

  * Let’s take a look at another problem: counting the number of students in this lecture hall. We can solve this problem using a very simple algorithm:

    1. stand up and assign yourself the number 1

    2. pair off with someone standing, add your numbers together, and adopt the sum as your new number

    3. one of you should sit down; the other should go back to step 2

  * This algorithm gives us 637, which is close to the correct number of 729. Hooray! Using the algorithm above, we got to this number much faster (in only 9-10 steps) than we would have if we had pointed to each person individually (729 steps). Why is it so much faster? Each execution of the algorithm cuts the problem in half, just like in the phonebook example. Even if there were 4 billion students in the lecture hall, it would only take us 32 executions of this algorithm to count them all!

### Steganography

  * Steganography is the art of hiding information within images. Although it appears to be random noise, this image is actually of something much more interesting:

![Iron puzz le steganogram.][5]

  * The actual code for hiding information in this picture is something like the following:

	    im = new SimpleImage("iron-puzzle.png");
	    for (x = 0; x &lt; im.getWidth(); x%2B%2B) {
	            for (y = 0; y &lt; im.getHeight(); y%2B%2B) {
	                    // code for each x,y pixel here
	            }
	    }


  * This code may look like gibberish to you, but it’s actually not that hard to break down. Line 1 simply opens up an image. Lines 2 through 4 walk through the dots that make up the image. Now let’s add some lines of code that remove all of the blue and green from these dots and bump up the red by a factor of ten:

	    im = new SimpleImage("iron-puzzle.png");
	    for (x = 0; x &lt; im.getWidth(); x%2B%2B) {
	      for (y = 0; y &lt; im.getHeight(); y%2B%2B) {
	        im.setBlue(x, y, 0);
	        im.setGreen(x, y, 0);
	        red = im.getRed(x, y);
	        im.setRed(x, y, red * 10);
	      }
	    }
	    print(im);

  * Don’t worry too much about the details of this syntax, for now. Just allow yourself to be wowed by the result:

![The Eiffel Tower.][6]

## Teasers

  * Now, allow yourself to be wowed with what you might accomplish in the next twelve weeks! Check out [wrdly][7], a CS50 Final Project written by former students Sierra, Daniel, and Sam.

  * [CS50 Courses][8] is a tool for all your course shopping needs!

  * For your real shopping needs, check out the [CS50 Market][9]!

  * [CS50 2x][10] is a Chrome extension for watching Harvard iSites videos at double speed.

## The Course

### Lectures

  * 1pm - 2pm (sometimes 2:30pm), Mondays and Wednesdays (sometimes Fridays)

### Simultaneous Enrollment

  * Head to  if you want us to support you in your petition to the Ad Board to take a class that conflicts with CS50.

### Sections

  * We offer three distinct tracks for those that are less comfortable, more comfortable, and somewhere in between in their already-existing knowledge of computer science.

### Problem Sets

  * Problem Sets come in two editions: standard and Hacker. If you want a little extra challenge out of these projects, try the Hacker Edition.

  * You have late days that will be provided to you for turning in problem sets after the deadline.

  * The lowest score of your problem sets will be dropped, as well, but see the syllabus for fine print.

  * To give you a sense of where we’re going in the course, check out last year’s problem sets:

    * Scratch

    * C

    * Crypto

    * Scramble

    * Forensics

    * Mispellings

    * Huff’n Puff

    * C$50 Finance

  * Two years ago, students implemented [CS50 Shuttle][11], a fun game in which the player transports staff members to various destinations on campus.

### Office Hours

  * Held Monday through Thursday, 8pm to 11pm, in the Leverett, Pfoho, Eliot, and Annenberg dining halls.

  * This year, we’ll have a new format for office hours featuring a table with a few staff members who can host a more intimate conversation.

### Walkthroughs

  * Zamyla will be releasing weekly videos that literally walk you through the problem set. She will give you hints and starting points for the various problems along the way. Walkthroughs intend to answer the question, "Where do I begin?"

### Post-mortems

  * After each problem set, we’ll release short videos that present representative solutions and point out the good and the bad.

### Tutoring

  * As resources permit, we’ll pair up staff and students for 1-on-1 assistance.

### CS50 Hackathon

  * The Hackathon gives you a chance to fulfill the programmer stereotype by staying up all night coding! Food and fun will be provided.

### CS50 Fair

  * The CS50 Fair is your chance to show off your Final Project to all of Harvard!

### Our Mission Statement

  * What ultimately matters in this course is not so much where you end up relative to your classmates but where you, in Week 12, end up relative to yourself in Week 0.

   [1]: http://www.youtube.com/watch?v=8plnFoXnVoo
   [2]: https://www.cs50.net/faqs/cs50
   [3]: runtimes.png
   [4]: http://www.youtube.com/watch?&amp;v=6hfOvs8pY1k
   [5]: iron_puzzle.png
   [6]: iron_solution.png
   [7]: http://www.youtube.com/watch?v=55MuhuzC5Dw
   [8]: http://courses.cs50.net
   [9]: http://market.cs50.net
   [10]: http://cs50.net/2x
   [11]: http://shuttle.cs50.net
  