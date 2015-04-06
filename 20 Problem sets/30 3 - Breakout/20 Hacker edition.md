**Please consult your teaching fellow before attempting any hacker edition!**


For this hackers edition implement the normal edition, only with a few twists:

* Implement **find** with an O(n) sorting algorithm.

* Implement breakout.c such that the angle at which the ball bounces off the paddle depends on where the ball strikes the paddle; we leave it to you to decide on a formula. 

* Implement at least 2 of the following features into your breakout.c:
	* Implement God Mode whereby, if the program is run with **./breakout GOD**, the game ignores the user’s mouse movements and instead moves the paddle itself in perfect lockstep with the ball along its (horizontal) x-axis so that the ball never misses the paddle.
	* Implement a shrinking-paddle mechanism whereby the paddle’s width decreases as bricks are broken; we leave it to you to decide on a formula.
	* Implement a variable-scoring mechanism whereby bricks higher in the game’s grid are worth more points than are bricks lower in the game’s grid; we leave it to you to decide on a formula.
	* Implement a variable-velocity mechanism whereby the ball’s velocity (along one or both axes) increases as bricks are broken; we leave it to you to decide on a formula.
	* Implement lasers, whereby clicking the mouse button during gameplay results in the paddle shooting one or two laser beams upward toward bricks, whereby those beams can destroy them just like the ball can. However, if a beam strikes the ball itself, gameplay must end.