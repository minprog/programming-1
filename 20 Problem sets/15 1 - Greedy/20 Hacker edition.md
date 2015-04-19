*Please consult your teaching fellow before attempting any hacker edition!*

* Let's ensure that the Appliance is up to date by running **update50** from a Terminal before starting.

# Objectives

* Get comfortable with Linux.

* Start thinking more carefully.

* Solve some problems in C.


# Difference between hacker and normal edition

* Hacker Edition plays with credit cards instead of coins.

* Hacker Edition demands two half pyramids.


# Bad Credit

Odds are you have a credit card in your wallet. Though perhaps the bill does not (yet) get sent to you! That card has a number, both printed on its face and embedded (perhaps with some other data) in the magnetic stripe on back. That number is also stored in a database somewhere, so that when your card is used to buy something, the creditor knows whom to bill. There are a lot of people with credit cards in this world, so those numbers are pretty long: American Express uses 15-digit numbers, MasterCard uses 16-digit numbers, and Visa uses 13- and 16-digit numbers. And those are decimal numbers (0 through 9), not binary, which means, for instance, that American Express could print as many as 10^(15) = 1,000,000,000,000,000 unique cards! (That’s, ahem, a quadrillion.)

Now that’s a bit of an exaggeration, because credit card numbers actually have some structure to them. American Express numbers all start with 34 or 37; MasterCard numbers all start with 51, 52, 53, 54, or 55; and Visa numbers all start with 4. But credit card numbers also have a "checksum" built into them, a mathematical relationship between at least one number and others. That checksum enables computers (or humans who like math) to detect typos (e.g., transpositions), if not fraudulent numbers, without having to query a database, which can be slow. (Consider the awkward silence you may have experienced at some point whilst paying by credit card at a store whose computer uses a dial-up modem to verify your card.) Of course, a dishonest mathematician could certainly craft a fake number that nonetheless respects the mathematical constraint, so a database lookup is still necessary for more rigorous checks.

So what’s the secret formula? Well, most cards use an algorithm invented by Hans Peter Luhn, a nice fellow from IBM. According to Luhn’s algorithm, you can determine if a credit card number is (syntactically) valid as follows:

1. Multiply every other digit by 2, starting with the number’s second-to-last digit, and then add those products' digits together.

2. Add the sum to the sum of the digits that weren’t multiplied by 2.

3. If the total’s last digit is 0 (or, put more formally, if the total modulo 10 is congruent to 0), the number is valid!

That’s kind of confusing, so let’s try an example with Daven’s AmEx: 378282246310005.

1. For the sake of discussion, let’s first underline every other digit, starting with the number’s second-to-last digit:
  378282246310005

  Okay, let’s multiply each of the underlined digits by 2:

  7•2 + 2•2 + 2•2 + 4•2 + 3•2 + 0•2 + 0•2

  That gives us:

  14 + 4 + 4 + 8 + 6 + 0 + 0

  Now let’s add those products' digits (i.e., not the products themselves) together:

  1 + 4 + 4 + 4 + 8 + 6 + 0 + 0 = 27

2. Now let’s add that sum (27) to the sum of the digits that weren’t multiplied by 2:

  27 + 3 + 8 + 8 + 2 + 6 + 1 + 0 + 5 = 60

3. Yup, the last digit in that sum (60) is a 0, so Daven’s card is legit!

So, validating credit card numbers isn’t hard, but it does get a bit tedious by hand. Let’s write a program.

In `credit.c`, write a program that prompts the user for a credit card number and then reports (via `printf`) whether it is a valid American Express, MasterCard, or Visa card number, per the definitions of each’s format herein. So that we can automate some tests of your code, we ask that your program’s last line of output be `AMEX\n` or `MASTERCARD\n` or `VISA\n` or `INVALID\n`, nothing more, nothing less, and that `main` always return `0`. For simplicity, you may assume that the user’s input will be entirely numeric (i.e., devoid of hyphens, as might be printed on an actual card). But do not assume that the user’s input will fit in an `int`! Best to use `GetLongLong` from CS50’s library to get users' input. (Why?)

Of course, to use `GetLongLong`, you’ll need to tell `clang` about CS50’s library. Be sure to put

  #include <cs50.h>

toward the top of `credit.c`. And be sure to compile your code with a command like the below.

  clang -o credit credit.c -lcs50

Note that `-lcs50` must come at this command’s end because of how clang works.

Incidentally, recall that `make` can invoke `clang` for you and provide that flag for you, as via the command below.

  make credit

Assuming your program compiled without errors (or, ideally, warnings) via either command, you can run your program with the command below.

  ./credit

Consider the below representative of how your own program should behave when passed a valid credit card number (sans hyphens), wherein underlined text represents some user’s input.

  jharvard@appliance (~/Dropbox/hacker1): ./credit
  Number: 378282246310005
  AMEX

Of course, `GetLongLong` itself will reject hyphens (and more) anyway:

  jharvard@appliance (~/Dropbox/hacker1): ./credit
  Number: 3782-822-463-10005
  Retry: foo
  Retry: 378282246310005
  AMEX

But it’s up to you to catch inputs that are not credit card numbers (e.g., Lauren’s phone number), even if numeric:

  jharvard@appliance (~/Dropbox/hacker1): ./credit
  Number: 7722574501
  INVALID

Test out your program with a whole bunch of inputs, both valid and invalid. (We certainly will!) Here are a few card numbers that PayPal recommends for testing:

[https://www.paypalobjects.com/en_US/vhelp/paypalmanager_help/credit_card_numbers.htm](https://www.paypalobjects.com/en_US/vhelp/paypalmanager_help/credit_card_numbers.htm)

Google (or perhaps a roommate’s wallet) should turn up more. (If your roommate asks what you’re doing, don’t mention us.) If your program behaves incorrectly on some inputs (or doesn’t compile at all), time to debug!

If you’d like to check the correctness of your program with **check50**, you may execute the below.

  check50 2014.fall.hacker1.credit credit.c

And if you’d like to play with the staff’s own implementation of *credit* in the appliance, you may execute the below.

  ~cs50/hacker1/credit

Test your program using a bunch of different inputs, both valid and invalid.


# Final steps

* When you are done with `credit.c`, submit it by going over to the [Submit](#submit) tab. Be sure to compile and test one last time before you submit.

* All done!





# Credit

* Let's ensure that the Appliance is up to date by running `update50` from a Terminal before starting.

## `credit.c`
* Odds are you have a credit card in your wallet. Though perhaps the bill does not (yet) get sent to you! That card has a number, both printed on its face and embedded (perhaps with some other data) in the magnetic stripe on back. That number is also stored in a database somewhere, so that when your card is used to buy something, the creditor knows whom to bill. There are a lot of people with credit cards in this world, so those numbers are pretty long: American Express uses 15-digit numbers, MasterCard uses 16-digit numbers, and Visa uses 13- and 16-digit numbers. And those are decimal numbers (0 through 9), not binary, which means, for instance, that American Express could print as many as 10^(15) = 1,000,000,000,000,000 unique cards! (That's, ahem, a quadrillion.)

  Now that's a bit of an exaggeration, because credit card numbers actually have some structure to them. American Express numbers all start with 34 or 37; MasterCard numbers all start with 51, 52, 53, 54, or 55; and Visa numbers all start with 4. But credit card numbers also have a "checksum" built into them, a mathematical relationship between at least one number and others. That checksum enables computers (or humans who like math) to detect typos (e.g., transpositions), if not fraudulent numbers, without having to query a database, which can be slow. (Consider the awkward silence you may have experienced at some point whilst paying by credit card at a store whose computer uses a dial-up modem to verify your card.) Of course, a dishonest mathematician could certainly  craft a fake number that nonetheless respects the mathematical constraint, so a database lookup is still necessary for more rigorous checks.

  So what's the secret formula? Well, most cards use an algorithm invented by Hans Peter Luhn, a nice fellow from IBM. According to Luhn's algorithm, you can determine if a credit card number is (syntactically) valid as follows:

  Multiply every other digit by 2, starting with the number's second-to-last digit, and then add those products' digits together. Add the sum to the sum of the digits that weren't multiplied by 2. If the total's last digit is 0 (or, put more formally, if the total modulo 10 is congruent to 0), the number is valid!

* That's kind of confusing, so let's try an example with Nate's AmEx: 378282246310005. For the sake of discussion, let's first print every other digit in **bold**, starting with the number's second-to-last digit:

  3**7**8**2**8**2**2**4**6**3**1**0**0**0**5

  Okay, let's multiply each of the bold digits by 2:

  7x2 + 2x2 + 2x2 + 4x2 + 3x2 + 0x2 + 0x2

  That gives us:

  14 + 4 + 4 + 8 + 6 + 0 + 0

  Now let's add those products' digits (i.e., not the products themselves) together:

  1 + 4 + 4 + 4 + 8 + 6 + 0 + 0 = 27

  Now let's add that sum (27) to the sum of the digits that weren't multiplied by 2:

  27 + 3 + 8 + 8 + 2 + 6 + 1 + 0 + 5 = 60

  Yup, the last digit in that sum (60) is a 0, so Nate's card is legit!

  So, validating credit card numbers isn't hard, but it does get a bit tedious by hand. Let's write a program.
  
* In `credit.c`, write a program that prompts the user for a credit card number and then reports (via `printf`) whether it is a valid American Express, MasterCard, or Visa card number, per the definitions of each's format herein. So that we can automate some tests of your code, we ask that your program's last line of output be `AMEX\n` or `MASTERCARD\n` or `VISA\n` or `INVALID\n`, nothing more, nothing less, and that main always returns `0`. For simplicity, you may assume that the user's input will be entirely numeric (i.e., devoid of hyphens, as might be printed on an actual card). But do not assume that the user's input will fit in an `int`! Best to use `GetLongLong` from CS50's library to get users' input. (Why?)
  
* Consider the below representative of how your own program should behave when passed a (valid or invalid) credit card number (without hyphens):
  
		jharvard@appliance (~/Dropbox/hacker1): ./credit
		Number: 378282246310005
		AMEX
		
		jharvard@appliance (~/Dropbox/hacker1): ./credit
		Number: 7722574501
		INVALID	
  
* Remember that you can use

		make credit

  to compile your program and then

		./credit

  to run it.
  
* Test your program using a bunch of different inputs, both valid and invalid.
  
* Also, don't forget about `check50` and `style50`!

## Final steps

## Final steps

* When you are done with `credit.c`, submit it by going over to the **Submit** tab. Be sure to compile and test one last time before you submit.

* All done!