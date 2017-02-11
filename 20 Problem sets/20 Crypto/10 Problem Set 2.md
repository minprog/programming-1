# Problem Set 2: Crypto

##  Objectives

* Become better acquainted with functions and libraries.
* Dabble in cryptography.

## tl;dr

0. Watch [Week 2's lecture](/lectures/week-2).

1. Infer a user's initials from their name with `initials.c`.

2. Choose two adventures:

	- Implement Caesar's cipher.

	- Implement Vigenère's cipher.

	- Crack passwords.

3. Submit your code.

4. Submit a form.
{:start="0"}

## Help

For help with Week 2 and Problem Set 2:

- Read carefully through the specs.

- Attend the tutorial on Monday.

- Watch Zamyla's walkthroughs herein.

- Attend office hours.

## Reminders

Per [Week 2's lecture](/lectures/week-2):

- Use `help50` as needed.

- Use `eprintf` as needed.

- Use `debug50` as needed.

## Getting Started

Alright, here we go again!

Log into `cs50.io` and execute

	update50

within a terminal window to make sure your workspace is up-to-date. If you somehow closed your terminal window (and can't find it!), make sure that Console is checked under the View menu, then click the green, circled plus (+) in CS50 IDE's bottom half, then select New Terminal.

Next, execute

	mkdir ~/workspace/pset2/

at your prompt in order to make a directory called `pset2` in your workspace directory. Take care not to overlook the space between `mkdir` and `~/workspace/pset2` or any other character for that matter! Keep in mind that `~` denotes your home directory, `~/workspace` denotes a directory called `workspace` therein, and `~/workspace/pset2` denotes a directory called `pset2` within `~/workspace`.

Now execute

	cd ~/workspace/pset2/

to move yourself into (i.e., open) that directory. Your prompt should now resemble the below.

	~/workspace/pset2/ $

If not, retrace your steps and see if you can determine where you went wrong. You can actually execute

	history

at the prompt to see your last several commands in chronological order if you'd like to do some sleuthing. You can also scroll through the same one line at a time by hitting your keyboard's up and down arrows; hit Enter to re-execute any command that you'd like.

## What to Do

1. Implement either of:

- [Initials](http://docs.cs50.net/problems/initials/less/initials.html), less comfortable

- [Initials](http://docs.cs50.net/problems/initials/more/initials.html), more comfortable

2. Implement any two (2) of:

- [Caesar](http://docs.cs50.net/problems/caesar/caesar.html), less comfortable

- [Vigenere](http://docs.cs50.net/problems/vigenere/vigenere.html), less comfortable

- [Crack](http://docs.cs50.net/problems/crack/crack.html), more comfortable

## How to Submit

For this problem set, we'll be using a new submission system based on GitHub, a popular site for storing code. Recall that for Problem Set 0 you signed up (hopefully!) for an account on github.com. The new system's still in "beta" (a testing phase), so please forgive any bugs! We'll keep an eye on CS50 Discuss and email over the weekend in case anything goes wrong so that we can fix right away!

### Step 1 of 4

Execute

	update50

again to ensure that your IDE is up-to-date.

### Step 2 of 4

Recall that you were asked to implement the less-comfortable or more-comfortable version of `initials`.

Be sure that `initials.c` is in `~/workspace/pset2/initials`, as with:

	cd ~/workspace/pset2/initials/
	ls

Recall that you were asked to implement any two (2) of `caesar`, `vigenere`, and `crack`.

If you implemented `caesar`, be sure that `caesar.c` is in `~/workspace/pset2/caesar/`.

If you implemented `vigenere`, be sure that `vigenere.c` is in `~/workspace/pset2/vigenere/`.

If you implemented `crack`, be sure that `crack.c` is in `~/workspace/pset2/crack/`.

If not sure how to confirm or fix something, do just reach out to the staff!

### Step 3 of 4

Below, add the relevant files to the submission form, and press submit!

If you run into any trouble, email <help@mprog.nl>!

You may resubmit any problem as many times as you'd like.

This was Problem Set 2.

## FAQs

### command not found

If you execute, e.g.,

	submit50 initials

and see

	bash: submit50: command not found

odds are you haven't run `update50` again, per Step 1 of 4. Do just re-run `update50`!

### Not a directory

If you execute, e.g.,

	cd ~/workspace/pset2/initials/

and see

	bash: cd: /home/ubuntu/workspace/pset2/initials/: Not a directory

odds are you don't have a `pset2/` directory inside of `~/workspace/` and/or you don't have an `initials/` directory inside of `~/workspace/pset2/`. Check as much using `ls` (remember how?) or poke around your IDE's file browser at left. Make sure that:

- you have a `pset2/` directory inside of `~/workspace/`,

- you have an `initials/` directory inside of `~/workspace/pset2/`, inside of which is `initials.c`,

- you have an `caesar/` directory inside of `~/workspace/pset2/`, inside of which is `caesar.c`,

- you have an `vigenere/` directory inside of `~/workspace/pset2/`, inside of which is `vigenere.c`, and/or

- you have an `crack/` directory inside of `~/workspace/pset2/`, inside of which is `crack.c`.
