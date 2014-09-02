# Find

## Getting started

![videoplayer](http://cdn.cs50.net/2012/fall/shorts/linear_search/linear_search-720p.mp4)

![videoplayer](http://cdn.cs50.net/2012/fall/shorts/bubble_sort/bubble_sort-720p.mp4)

![videoplayer](http://cdn.cs50.net/2012/fall/shorts/insertion_sort/insertion_sort-720p.mp4)

![videoplayer](http://cdn.cs50.net/2012/fall/shorts/selection_sort/selection_sort-720p.mp4)

![videoplayer](http://cdn.cs50.net/2012/fall/shorts/gdb/gdb-720p.mp4.mp4)

* Recall that, for the previous problem sets, you started writing programs from scratch, creating your own pset1 and pset2 directories with mkdir. For this problem set, you'll instead download "distribution code" (otherwise known as a "distro"), written by us, and add your own lines of code to it. You'll first need to read and understand our code, though, so this problem set is as much about learning to read someone else's code as it is about writing your own!
  
* Open up a **terminal** and execute the following commands (you might notice that the numbers in this fragment do not match up with the problem set number; however, this is intentional):

		cd ~/Desktop
		wget http://cdn.cs50.net/2013/fall/psets/3/pset3/pset3.zip
		unzip pset3
		rm pset3.zip
		cd pset3
		ls

	which should then display two folders, namely:
	
		fifteen  find

# Searching

* Then, with your **terminal** still open, let's explore the `find` folder:

		cd find

  which should list the following files:
  
		helpers.c helpers.h Makefile find.c generate.c

* Implemented in `generate.c` is a program that uses a "pseudorandom-number generator" (via a function called `rand`) to generate a whole bunch of random (well, pseudorandom, since computers can't actually generate truly random) numbers, one per line. (Cf. [CS50](https://www.cs50.net/resources/cppreference.com/stdother/rand.html)) Compile and run this program per the below.

		make generate
		./generate

  which should then notify you of the program's correct usage:
  
		Usage: generate n [s]

  As this output suggests, this program expects one or two command-line arguments. The first, `n`, is required; it indicates how many pseudorandom numbers you'd like to generate. The second, s, is optional, as the brackets are meant to imply; if supplied, it represents the value that the pseudorandom-number generator should use as its "seed." A seed is simply an input to a pseudorandom-number generator that influences its outputs. For instance, if you seed `rand` by first calling `srand` (another function whose purpose is to "seed" `rand`) with an argument of, say, `1`, and then call `rand` itself three times, rand might return 17767, then 9158, then 39017. (Cf. [CS50](https://www.cs50.net/resources/cppreference.com/stdother/srand.html).) But if you instead seed rand by first calling srand with an argument of, say, `2`, and then call rand itself three times, rand might instead return 38906, then 31103, then 52464. But if you re-seed `rand` by calling srand again with an argument of `1`, the next three times you call `rand`, you'll again get 17767, then 9158, then 39017! See, not so random.
  
* So, go ahead and run this program again, this time with a value of, say, 10 for `n`, as in the below; you should see a list of 10 pseudorandom numbers.

		./generate 10

  Then run that command again. You should see a list of different numbers each time you run the program.
  
  Now, run the program a few times by providing a seed, say, `0`.

		./generate 10 0
		./generate 10 0
		./generate 10 0

  The program returns the same list of numbers each time!

* Now take a look at `generate.c` itself with gedit. (Remember how?) Comments atop that file explain the program's overall functionality. But it looks like we forgot to comment the code itself. Read over the code carefully until you understand each line and then comment our code for us, replacing each `TODO` with **a single phrase** that describes the purpose or functionality of the corresponding line(s) of code. (Know that an `unsigned int` is just an `int that cannot be negative.) And for more details on `rand` and `srand`, recall that you can execute:

		man rand
		man srand

  Once done commenting `generate.c`, re-compile the program to be sure you didn't break anything by re-executing the command below.

		make generate

* Now, recall that `make` automates compilation of your code so that you don't shave to execute `clang` manually along with a whole bunch of switches. Notice, in fact, how `make` just executed a pretty long command for you, per the tool's output. However, as your programs grow in size, `make` won't be able to infer from context anymore how to compile your code; you'll need to start telling `make` how to compile your program, particularly when they involve multiple source (i.e., `.c`) files. And so we'll start relying on "Makefiles," configuration files that tell `make` exactly what to do.

  How did make know how to compile generate in this case? It actually used a configuration file that we wrote. Using gedit, go ahead and look at the file called `Makefile` that's in the same directory as `generate.c`. This `Makefile` is essentially a list of rules that we wrote for you that tells `make` how to build `generate` from `generate.c` for you. The relevant lines appear below.

		generate: generate.c
			`clang` -ggdb -std=c99 -Wall -Werror -o generate generate.c

  The first line tells `make` that the "target" called generate should be built by invoking the second line's command. Moreover, that first line tells `make` that `generate` is dependent on `generate.c`, the implication of which is that `make` will only re-build generate on subsequent runs if that file was modified since make last built `generate`. Neat time-saving trick, eh? In fact, go ahead and execute the command below again, assuming you haven't modified `generate.c`.

  You should be informed that generate is already up to date. Incidentally, know that the leading whitespace on that second line is not a sequence of spaces but, rather, a tab. Unfortunately, make requires that commands be preceded by tabs, so be careful not to change them to spaces with gedit (which automatically converts tabs to four spaces), else you may encounter strange errors! The `-Werror` flag, recall, tells clang to treat warnings (bad) as though they're errors (worse) so that you're forced (in a good, instructive way!) to fix them. Know that you can remove this flag, but that we will check your code with that flag and will certainly notice warnings you hide in this way!
  
* Now take a look at `find.c` with `gedit`. Notice that this program expects a single command-line argument: a "needle" to search for in a "haystack" of values. Once done looking over the code, go ahead and compile the program by executing the command below.

		make find

  Notice, per that command's output, that make actually executed the below for you.

		clang -ggdb -std=c99 -Wall -Werror -o find find.c helpers.c -lcs50 -lm
    
  Notice further that you just compiled a program comprising not one but two `.c` files: `helpers.c` and `find.c`. How did make know what to do? Well, again, open up `Makefile` to see the man behind the curtain. The relevant lines appear below.

		find: find.c helpers.c helpers.h
		    clang -ggdb -std=c99 -Wall -Werror -o find find.c helpers.c -lcs50 -lm

  Per the dependencies implied above (after the colon), any changes to `find.c`, `helpers.c`, or `helpers.h` will compel `make` to rebuild find the next time it's invoked for this target.

  Go ahead and run this program by executing, say, the below.

		./find 13

  You'll be prompted to provide some hay (i.e., some integers), one "straw" at a time. As soon as you tire of providing integers, hit ctrl-d to send the program an EOF (end-of-file) character. That character will compel `GetInt` from the CS50 Library to return `INT_MAX`, a constant that, per `find.c`, will compel `find` to stop prompting for hay. The program will then look for that needle in the hay you provided, ultimately reporting whether the former was found in the latter. In short, this program searches an array for some value. At least, it should, but it won't find anything yet! That's where you come in. More on your role in a bit.

  In turns out you can automate this process of providing hay, though, by "piping" the output of `generate` into `find` as input. For instance, the command below passes 1,000 pseudorandom numbers to find, which then searches those values for 42.

		./generate 1000 | ./find 42

  Note that, when piping output from `generate` into find in this manner, you won't actually see `generate`'s numbers, but you will see `find`'s prompts.

  Alternatively, you can "redirect" `generate`'s output to a file with a command like the below.

		./generate 1000 > numbers.txt

  You can then redirect that file's contents as input to find with the command below.

		./find 42 < numbers.txt

  Let's finish looking at that `Makefile`. Notice the line below.

		all: find generate

  This target implies that you can build both `generate` and `find` simply by executing the below.

    make all

  Even better, the below is equivalent (because `make` builds a `Makefile`'s first target by default).

    make

  If only you could whittle this whole problem set down to a single command! Finally, notice these last lines in `Makefile`:

		clean:
		    rm -f *.o a.out core find generate

  This target allows you to delete all files ending in `.o` or called `core` (more on that soon!), `find`, or `generate` simply by executing the command below.

		make clean

  Be careful not to add, say, `*.c` to that last line in Makefile! (Why?) Any line, incidentally, that begins with `#` is just a comment.

* And now the fun begins! Notice that `find.c` calls search, a function declared in `helpers.h`. Unfortunately, we forgot to implement that function fully in `helpers.c`! (To be sure, we could have put the contents of `helpers.h` and `helpers.c` in `find.c` itself. But it's sometimes better to organize programs into multiple files, especially when some functions are essentially utility functions that might later prove useful to other programs as well, much like those in the CS50 Library.) Take a peek at `helpers.c` with `gedit`, and you'll see that search always returns false, whether or not value is in  values. Re-write search in such a way that it uses linear search, returning `true` if value is in values and `false` if value is not in values. Take care to return `false` right away if `n` isn't even positive.

  When ready to check the correctness of your program, try running the command below.

		./generate 1000 50 | ./find 2008

  Because one of the numbers outputted by `generate`, when seeded with `50`, is `2008`, your code should find that "needle"! By contrast, try running the command below as well.

		./generate 1000 50 | ./find 2013

  Because `2013` is not among the numbers outputted by `generate`, when seeded with `50`, your code shouldn't find that needle. Best to try some other tests as well, as by running `generate` with some seed, taking a look at its output, then piping that same output to `find`, looking for a "needle" you know to be among the "hay".

  Incidentally, note that `main` in `find.c` is written in such a way that find returns `0` if the needle is found, else it returns `1`. You can check the so-called "exit code" with which `main` returns by executing

		echo $?

  after running some other command. For instance, assuming your implementation of search is correct, if you run

		./generate 1000 50 | ./find 2008
		echo $?

  you should see `0`, since `2008` is, again, among the 1,000 numbers outputted by generate when seeded with `50`, and so search (written by you) should return `true`, in which case `main` (written by us) should return (i.e., exit with) `0`. By contrast, assuming your implementation of search is correct, if you run

		./generate 1000 50 | ./find 2013
		echo $?

  you should see `1`.

* When ready to check the correctness of your program officially with `check50`, you may execute the below. Be sure to run the command inside of `~/Desktop/pset3/find`.

		check50 2013.pset3.find helpers.c

  Incidentally, be sure not to get into the habit of testing your code with `check50` before testing it yourself. (And definitely don't get into an even worse habit of only testing your code with `check50`!) Suffice it to say `check50` doesn't exist in the real world, so running your code with your own sample inputs, comparing actual output against expected output, is the best habit to get into sooner rather than later. Truly, don't do yourself a long-term disservice!

  Anyhow, if you'd like to play with the staff's own implementation of `find` in the appliance, you may execute the below.

		~cs50/pset3/find

* If you need help at any time, don't hesitate to ask us!

# Sorting

* Alright, linear search is pretty bad. Recall from Week 0 and Week 3 that we can do better, but first we'd best sort that hay.

  Notice that `find.c` calls `sort`, a function declared in `helpers.h`. Unfortunately, we forgot to implement that function fully too in `helpers.c`! Take a peek at `helpers.c` with `gedit`, and you'll see that `sort` returns immediately, even though `find`'s `main` function does pass it an actual array.

  Now, recall the syntax for declaring an array. Not only do you specify the array's type, you also specify its size between brackets, just as we do for haystack in `find.c`:

		int haystack[MAX];

  But when passing an array, you only specify its name, just as we do when passing haystack to sort in `find.c`:

		sort(haystack, size);

  (Why do we also pass in the size of that array separately?)

  When declaring a function that takes a one-dimensional array as an argument, though, you don't need to specify the array's size, just as we don't when declaring `sort` in `helpers.h` (and `helpers.c`):

    void sort(int values[], int n);

  Go ahead and implement sort so that the function actually sorts, from smallest to largest, the array of numbers that it's passed, in such a way that its running time is in O(n^2), where n is the array's size. Odds are you'll want to implement bubble sort, selection sort, or insertion sort, if only because we discussed them in Week 3. Just realize that there's no one "right" way to implement any of those algorithms; variations abound. In fact, you're welcome to improve upon them as you see fit, so long as your implementation remains in O(n^2). However, take care not to alter our declaration of sort. Its prototype must remain:

		void sort(int values[], int n);

  As this return type of void implies, this function must not return a sorted array; it must instead "destructively" sort the actual array that it's passed by moving around the values therein. As we'll discuss in Week 4, arrays are not passed "by value" but instead "by reference," which means that sort will not be passed a copy of an array but, rather, the original array itself.

  Although you may not alter our declaration of sort, you're welcome to define  your own function(s) in `helpers.c` that `sort` itself may then call.

  We leave it to you to determine how best to test your implementation of `sort`. But don't forget that `printf` and, per Week 3's first lecture, `gdb` are your friends. And don't forget that you can generate the same sequence of pseudorandom numbers again and again by explicitly specifying generate's seed. Before you ultimately submit, though, be sure to remove any such calls to `printf`, as we like our programs' outputs just they way they are!

<iframe width="711" height="400" src="http://www.youtube.com/embed/U8k-0StE1Ik" frameborder="0" allowfullscreen></iframe>

  There's no `check50` for this one!

* Now that `sort` (presumably) works, it's time to improve upon search, the other function that lives in `helpers.c`. Recall that your first version implemented linear search. Rip out the lines that you wrote earlier (sniff) and re-implement search as Binary Search, that divide-and-conquer strategy that we employed in Week 0 and again in Week 3. You are welcome to take an iterative or, per Week 4, a recursive approach. If you pursue the latter, though, know that you may not change our declaration of search, but you may write a new, recursive function (that perhaps takes different parameters) that search itself calls. **When you submit this problem set, only submit the Binary Search version of `search`; do not submit your linear search version.**

<iframe width="711" height="400" src="http://www.youtube.com/embed/7DSRJj7qfP8" frameborder="0" allowfullscreen></iframe>

## Final steps

* When you are done with `generate.c`, `find.c`, and `helpers.c`, submit them by going over to the **Submit** tab. Be sure to compile and test one last time before you submit.

* All done!
