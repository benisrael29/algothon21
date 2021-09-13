# Assignment 2 Support Code

This is the support code for COMP3702 2021 Assignment 2.

The following files are provided:

**game_env.py**

This file contains a class representing an Untitled Dragon Game level environment, storing the dimensions of the
environment, initial player position, exit position, number of gems and position of each gem, time limit, cost target,
the tile type of each grid position, and a list of all available actions.

This file contains a number of functions which will be useful in developing your solver:

~~~~~
__init__(filename)
~~~~~
Constructs a new instance based on the given input filename.


~~~~~
get_init_state()
~~~~~
Returns a GameState object (see below) representing the initial state of the level.


~~~~~
perform_action(state, action)
~~~~~
Samples an outcome of performing the given 'action' starting from the given 'state', where 'action' is an element of
GameEnv.ACTIONS and 'state' is a GameState object. Returns a tuple (valid, received_reward, next_state, terminal), where
valid is True (if the action is valid) or False (if the action is invalid); received reward is a float representing the
reward received by the agent for this time step (i.e. action cost + any penalties for collision and game over);
next_state is a GameState object, and terminal is True if the episode has terminated (i.e. goal has been reached or game
over has occurred).

Note that perform_action(...) is non-deterministic - it can produce different results based on random chance.

~~~~~
is_solved(state)
~~~~~
Checks whether the given 'state' (a GameState object) is solved (i.e. all gems collected and player at exit). Returns
True (solved) or False (not solved).


~~~~~
is_game_over(state)
~~~~~
Checks whether the given 'state' (a GameState object) results in Game Over (i.e. player has landed on a lava tile).
Returns True (Game Over) or False (not Game Over).


~~~~~
render(state)
~~~~~
Prints a graphical representation of the given 'state' (a GameState object) to the terminal.


**game_state.py**

This file contains a class representing an Untitled Dragon Game state, storing the position of the player and the status
of all gems in the level (1 for collected, 0 for remaining).

~~~~~
__init__(row, col, gem_status)
~~~~~
Constructs a new GameState instance, where row and column are integers between 0 and n_rows, n_cols respectively, and
gem_status is a tuple of length n_gems, where each element is 1 or 0.

~~~~~
deepcopy()
~~~~~
Efficiently creates a deep copy of the GameState instance.


**play_game.py**

This file contains a script which launches an interactive game session when run. Becoming familiar with the game
mechanics may be helpful in designing your solution.

The script takes 1 command line argument:
- input_filename, which must be a valid testcase file (e.g. one of the provided files in the testcases directory)

When prompted for an action, type one of the available action strings (e.g. wr, wl, etc) and press enter to perform the
entered action. Note that the outcomes of actions are non-deterministic - performing the same sequence of actions can
lead to different results on different runs.


**solution.py**

Template file for you to implement your solution to Assignment 1.

You must implement the following method stubs, which will be invoked by the simulator during testing:
    __init__(game_env)
    plan_offline()
    select_action()

Implementing a 'main' method is not required.
    
To ensure compatibility with the autograder, please avoid using try-except blocks for Exception or OSError exception
types. Try-except blocks with concrete exception types other than OSError (e.g. try: ... except ValueError) are allowed.

We recommend you start by implementing value iteration (including developing a transition model), and work to improve
your implementation from here.


**simulator.py**

Run this file to evaluate the performance of the policy generated by your solver for a given input file. You may modify
this file if desired. When submitting to GradeScope, an unmodified version of this file will be used to evaluate your
code.

The return code produced by simulator is your solver's score for the testcase (multiplied by 10 and represented as an
integer).

Simulator seeds random outcomes to produce consistent policy performance between runs - if your code is deterministic
and does not exceed the time limit, simulator will always produce the a consistent score.

The simulator will automatically terminate your solver if it runs over 2x the allowed time limit for any step (on Unix
platforms only - not available on Windows). This feature can be disabled for debugging purposes by setting
DEBUG_MODE = True above.


**visualiser.py**

Run this file to visualise the policy generated by your solver for a given input file. You may modify this file if
desired.

The return code produced by visualiser is your solver's score for the testcase (multiplied by 10 and represented as an
integer).

Visualiser seeds random outcomes to produce consistent policy performance between runs - if your code is deterministic
and does not exceed the time limit, visualiser will always produce the a consistent score.

The visualiser will automatically terminate your solver if it runs over 2x the allowed time limit for any step (on Unix
platforms only - not available on Windows). This feature can be disabled for debugging purposes by setting
DEBUG_MODE = True above.


**testcases**

A directory containing input files which can be used to evaluate your solution.

Testcase files can contain comments, starting with '#', which are ignored by the input file parser. In the provided
testcase files, these comments indicate what each row of information represents.

The provided testcases are designed to be solvable with value iteration. Additional testcases will be provided in the
near future.