Lecture notes by Andrew Sellergren. [Watch the video.](http://cs50.tv/2013/fall/lectures/4/m/)

## Announcements and Demos

We seem to have caused some confusion with our coupon code policy. Apologies!
What we meant was to incentivize you to start your problem sets early. To
explain it more clearly:

* by default, psets are due on Thu at 12pm

* if you start early, finishing part of pset by Wed at 12pm (and receive a
  coupon code), you can extend your deadline for rest of pset to Fri at 12pm

* coupon-code problem still required even if not completed by Wed at 12pm

## From Last Time

We talked a little more high level about searching and sorting. Bubble sort,
for example, gets its name from the way that large numbers bubble up toward
the end of the list. We visualized bubble sort using [this website](http://www.cs.smith.edu/~thiebaut/java/sort/).

We quantified the efficiency of searching and sorting algorithms using big O
notation. Bubble sort was said to take $$n^2$$ steps in the worst case, where n
was the size of the input.

Selection sort gets its name from selecting the smallest number on each
walkthrough of the list and placing it at the front. Unfortunately, selection
sort also took $$n^2$$ steps in the worst case.

Insertion sort involved sorting the list in place, but required shifting
elements of the "sorted list" to the right whenever a smaller number needed
to be placed in the middle of it. It too took $$n^2$$ steps.

What's the best sorting algorithm? Why not [ask President Obama](http://www.youtube.com/watch?v=k4RRi_ntQc8)?

When talking about the running time of algorithms, $$O$$ represents the upper
bound, the worst case, whereas $$\Omega$$ represents the lower bound, the
best case. For bubble sort, selection sort, and insertion sort, the worst
case was that the list was in exactly reverse order and the best case was
that the list was already sorted. Whereas bubble sort (with a variable
tracking the number of swaps) and insertion sort only took n steps in the
best case, selection sort still took $$n^2$$ steps.

So we say that bubble sort, selection sort, and insertion sort are all
$$O(n^2)$$. Linear search is $$O(n)$$. Binary search is $$O(log n)$$. Finding
the length of an array is in $$O(1)$$, a.k.a. constant time, if that length
is stored in a variable. `printf` is also $$O(n)$$ since it takes $$n$$ steps
to print $$n$$ characters.

Bubble sort and insertion sort are $$\Omega(n)$$. Linear search and binary
search are $$\Omega(1)$$ because the element we're looking for might just be
the first one we examine.

One algorithm we mentioned briefly was merge sort. Merge sort is both
$$\Omega(n log n)$$ and $$O(n log n)$$, so we say it is $$\Theta(n log n)$$.

### Merge Sort

To see how merge sort compares to the other algorithms we've looked at so
far, check out this animation. Notice that bubble sort, insertion sort, and
selection sort are the three worst performers! The flip side is that they are
relatively easy to implement.

We can describe merge sort with the following pseudocode:

	On input of n elements:
	    If n < 2
	        Return.
	    Else:
	        Sort left half of elements.
	        Sort right half of elements.
	        Merge sorted halves.

If `n` is less than 2, then it's either 0 or 1 and the list is already sorted.
This is the trivial case.

If `n` is greater than or equal to 2, then what? We seem to be copping out
with a circular algorithm. Two of the steps begin with the command "sort"
without giving any indication as to how we go about that. When we say "sort,"
what we actually mean is reapply this whole algorithm to the left half and
the right half of the original list.

Will this algorithm loop infinitely? No, because after you've halved the
original list enough times, you will eventually have less than 2 items left.

Okay, so we're halving and halving and halving until we have less than 2
items and then we're returning. So far, nothing seems sorted. The magic must
be in the "Merge sorted halves" step.

One consideration with merge sort is that we need a second list for
intermediate storage. In computer science, there's generally a tradeoff
between resources and speed. If we want to do something faster, we may need
to use more memory.

To visualize merge sort, let's bring 8 volunteers on stage. We'll hand them
numbers and sit them down in chairs so that they're in the following order:

	4 2 6 1 3 7 5 8

The bold numbers are the ones we're currently focusing on. Merge sort says to
first sort the left half, so let's consider:

	4 2 6 1 3 7 5 8

Now we again sort the left half:

	4 2 6 1 3 7 5 8

And again:

	4 2 6 1 3 7 5 8

Now we have a list of size 1, so it's already sorted and we return.
Backtracking, we look at the right half of the final two-person list:

	4 2 6 1 3 7 5 8

Again, a list of size 1, so we return. Finally, we arrive at a merge step.
Since the elements are out of order, we need to put them in the correct order
as we merge:

	_ _ 6 1 3 7 5 8
	
	2 4 _ _ _ _ _ _

From now on, the bottom line will represent the second list we use for
intermediate storage. Now we focus on the right half of the left half of the
original list:

	_ _ 6 1 3 7 5 8
	
	2 4 _ _ _ _ _ _

We insert these two numbers in order into our intermediate list:

	_ _ _ _ 3 7 5 8
	
	2 4 1 6 _ _ _ _

Now we merge the left and right half of the intermediate list:

	_ _ _ _ 3 7 5 8
	
	1 2 4 6 _ _ _ _

Finally, we can insert the intermediate list back into the original list:

	1 2 4 6 3 7 5 8

And we're done with the "Sort left half" step for the original list!

Repeat for the right half of the original list, skipping to the "Sort left
half" step:

	1 2 4 6 _ _ 5 8
	
	_ _ _ _ 3 7 _ _

Sort right half:

	1 2 4 6 _ _ _ _
	
	_ _ _ _ 3 7 5 8

Merge:

	1 2 4 6 _ _ _ _
	
	_ _ _ _ 3 5 7 8

Move the right half back to the original list:

	1 2 4 6 3 5 7 8

Now, merge the left half and the right half of the original list:

	_ _ _ _ _ _ _ _
	
	1 2 3 4 5 6 7 8

And ta-da!

	1 2 3 4 5 6 7 8

Merge sort is $$O(n log n)$$. As before, the $$log n$$ comes from the
dividing by two. The $$n$$ thus must come from the merging. You can
rationalize this by considering the last merge step. To figure out which
number to place in the intermediate array next, we point our left hand at the
leftmost number of the left half and our right hand at the leftmost number of
the right half. Then we walk each hand to the right and compare numbers. All
told, we walk through every number in the list, which takes n steps.

Check out [Rob's visualization](http://www.youtube.com/watch?v=EeQ8pwjQxTM)
of merge sort. You can even hear [what sorting algorithms sound like](http://www.youtube.com/watch?v=t8g-iYGHpEA).

A function that calls itself is using recursion. In the above pseudocode, we
implemented merge sort using recursion.

### A Little Math

To show mathematically that merge sort is $$O(n log n)$$, let's use the
following notation:

	T(n) = 0, if n < 2

So far, all this says is that it takes 0 steps to sort a list of 1 or 0
elements. This is the so-called base case.

	T(n) = T(n/2) + T(n/2) + n, if n > 1

This notation indicates that the rest of the algorithm, the *recursive case*,
i.e. sorting a list of n elements, takes as many steps as sorting its two
halves, each of $$n / 2$$ elements, plus an extra $$n$$ steps to do the
merging.

Consider the case where $$n = 16$$:

	T(16) = 2 * T(8) + 16
	T(8)  = 2 * T(4) + 8
	T(4)  = 2 * T(2) + 4
	T(2)  = 2 * T(1) + 2
	T(1)  = 0

Since the base case, where a list of 0 or 1 is already sorted, takes 0 steps,
we can now substitute 0 in for $$T(1)$$ and calculate $$T(2)$$:

	T(2) = 2 * 0 + 2
	     = 2

Now we can substitute 2 in for T(2) and so on until we get:

	T(16) = 2 * 24 + 16
	T(8)  = 2 * 8  + 8
	T(4)  = 2 * 2  + 4
	T(2)  = 2 * 0  + 2
	T(1)  = 1

Thus, $$T(16)$$ is 64. This number is actually $$n log n$$. Dividing the list
successively accounts for $$log n$$, but the additional $$n$$ factor comes
from the merge step.

Here again with merge sort we've returned to the idea of "divide and conquer"
that we saw in Week 0 with the phonebook example.

In case you want to know what recursion is, try Googling it and checking out
the "Did you mean" suggestion. Hooray for geek humor!

## More with Recursion

### `sigma-0.c`

Let's write a program that sums up the numbers 0 through n, where n is
provided by the user. We start with some boilerplate code to get a positive
integer from the user using a do-while loop:

	#include <cs50.h>
	#include <stdio.h>

	int main(void)
	{
	    int n;
	    do
	    {
	        printf("Positive integer please: ");
	        n = GetInt();
	    }
	    while (n < 1);
	}

Recall the sigma symbol ($$\Sigma$$) which stands for sum. It makes sense,
then, to call our summing function sigma:

	#include <cs50.h>
	#include <stdio.h>

	int main(void)
	{
	    int n;
	    do
	    {
	        printf("Positive integer please: ");
	        n = GetInt();
	    }
	    while (n < 1);

	    int answer = sigma(n);

	    printf("%i\n", answer);
	}

Now we need to define `sigma`:

	#include <cs50.h>
	#include <stdio.h>

	int sigma(int m);

	int main(void)
	{
	    int n;
	    do
	    {
	        printf("Positive integer please: ");
	        n = GetInt();
	    }
	    while (n < 1);

	    int answer = sigma(n);

	    printf("%i\n", answer);
	}

	int sigma(int m)
	{
	    if (m < 1)
	    {
	        return 0;
	    }

	    int sum = 0;
	    for (int i = 1; i <= m; i++)
	    {
	        sum += i;
	    }
	    return sum;
	}

This is pretty straightforward. First, we do some error checking, then we
iterate through all numbers 1 through m, summing them up as we go. `sum += i`
is functionally equivalent to `sum = sum + i`.

Don't forget that we need to declare sigma before main if we want to
implement sigma after main!

When we compile and run this, it seems to work! What happens when we mess
with it by inputting a very large number? Turns out that if our sum becomes
so large that an int doesn't have enough bits for it, it will be confused for
a negative number.

### `sigma-1.c`

Let's try to approach the same problem using recursion.

Our implementation of main doesn't change. `sigma`, however, now looks like
this:

	int sigma(int m)
	{
	    if (m <= 0)
	    {
	        return 0;
	    }
	    else
	    {
	        return (m + sigma(m - 1));
	    }
	}

You might worry that this implementation will induce an infinite loop.
However, the first if condition represents a base case in which sigma doesn't
call itself.

## Teaser

### `noswap.c`

Consider the following code that claims to swap the values of two integers:

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

Seems reasonable, right? Unfortunately, when we compile and run this, we get
this output:

	x is 1
	y is 2
	Swapping...
	Swapped!
	x is 1
	y is 2

Obviously, the numbers haven't really been swapped. We'll find out why next
time!
