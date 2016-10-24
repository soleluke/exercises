#WuLUG Workshop: tmux, the terminal multiplexer
**tmux** is a program which allows the user to multiplex their terminal sessions, or have mutliple, separate terminal sessions open within one terminal window. Whether you are in a tty or an ssh session, tmux can help you get your work done, faster
This workshop is available at https://github.com/soleluke/exercises

##Exercise 1: Basic usage
1. Log into the system and open up a terminal
2. Do`$ tmux`
  * Notice the green bar at the bottom. This tells you what you are currently running in your session

3. Press <kbd>Ctrl</kbd>+<kbd>b</kbd>, then <kbd>d</kbd> to detach from the session

##Exercise 2: Multiplexing
####Part A: Panes
1. Do `$ tmux attach`
  to re-attach to your session from exercise 1
2. Press <kbd>Ctrl</kbd>+<kbd>b</kbd>, then <kbd>Shift</kbd>+<kbd>5</kbd>
  * Note: this has created a second 'pane' in your window
3. Press <kbd>Ctrl</kbd>+<kbd>b</kbd>, then <arrow-key> to switch to the pane in that direction.
  * What happens if there is no pane in that direction?
4. Press <kbd>Ctrl</kbd>+<kbd>b</kbd>, then <kbd>x</kbd>, then <kbd>y</kbd> at the prompt (located in the bar at the bottom)
5. Press <kbd>Ctrl</kbd>+<kbd>b</kbd>, then <kbd>Shift</kbd>+<kbd>'</kbd>
  * This is has also created a second pane. What is different this time?
6. Again, you can use <kbd>Ctrl</kbd>+<kbd>b</kbd> and an arrow key to switch panes.
  * Try <kbd>Ctrl</kbd>+<kbd>b</kbd>, then <kbd>Shift</kbd>+<kbd>'</kbd> now. What happens?

####Part B: Windows
Up until now, we've been working in one window. Lets change that

1. Press <kbd>Ctrl</kbd>+<kbd>b</kbd>, then <kbd>c</kbd> to create a new window
  * Notice how the bottom bar has changed
2. You can do any of the pane commands from part A in this window
3. Press <kbd>Ctrl</kbd>+<kbd>b</kbd>, then <kbd>n</kbd> or <kbd>p</kbd> to go to the next or previous window, respectively
4. Press <kbd>Ctrl</kbd>+<kbd>b</kbd>, then <kbd>Shift</kbd>+<kbd>7</kbd> to kill a window.
5. Kill all your windows
  * What happens?

####Part C: Sessions
Let's expand past one session

1. Since you should have killed your session after killing all your windows in part c, do `$ tmux` to start a new session
2. Run `watch ls` in this session
  * Notice how the bar at the bottom has changed
3. Press <kbd>Ctrl</kbd>+<kbd>b</kbd>, then <kbd>Shift</kbd>+<kbd>;</kbd>, then type *new* and press <kbd>Enter</kbd>
  * What happened?
4. Press <kbd>Ctrl</kbd>+<kbd>b</kbd>, then <kbd>s</kbd>. This is the list of your sessions. Move back to the first session using the arrow keys, then press <kbd>Enter</kbd> to select it
  * Notice that your **watch** command that you ran before making the new session is still running
  * Notice the numbers in brackets []. This is the size of the screen [<num-of-cols>,<num-of-rows>]. Try resizing your terminal window after attaching to one, then bring the list back up and see how the numbers change
5. Press <kbd>Ctrl</kbd>+<kbd>c</kbd> to stop the watch command, then run `$ exit` to kill this session
6. Run `$ tmux ls` to list your sessions from the terminal
  * How many sessions do you see?
  * Notice the label of the session (it should just be a number). How can we make this more descriptive?
7. Run `$ tmux attach`again to attach to your session
8. Press <kbd>Ctrl</kbd>+<kbd>b</kbd>, then <kbd>Shift</kbd>+<kbd>4</kbd> then replace the current name with a different one at the prompt in the bottom bar (ex. 'test')
  * Notice how the bottom bar has changed
9. Press <kbd>Ctrl</kbd>+<kbd>b</kbd>, then <kbd>d</kbd> to detach again
10. Run `$ tmux ls` again to see the change in the list
11. To begin a session with a given name, run `$ tmux new -s <session-name>`. Lets make another session called test2.
12. Press <kbd>Ctrl</kbd>+<kbd>b</kbd>, then <kbd>s</kbd> to list the sessions again.
13. Detach from this session. Run `$ tmux attach -t test2` to attach to the session named test2. Kill both sessions by killing all windows.

##Miscellaneous
* Press <kbd>Ctrl</kbd>+<kbd>b</kbd>, then <kbd>t</kbd>. Press any key within the pane to get out of big clock mode
* Sockets: You can use sockets with tmux to do a variety of things. To set up a tmux session using a socket, run:

  ```
  	$ tmux -S ~/tmux-socket new
  ```
  This will have auto-attached you to the new session. Detach from the session using <kbd>Ctrl</kbd>+<kbd>b</kbd>, then <kbd>d</kbd>

  To attach to a session in a socket, run:

  ```
  	$ tmux -S ~/tmux-socket attach
  ```
* Send-keys: you can send keys to tmux targets from outside sessions. use `$ tmux send-keys -R -t <target> <key>` to send any combination of keys into the tmux session. You can also send keys to panes within a session by targeting a pane instead of a session
* [Cheat sheet](https://gist.github.cm/MohamedAlaa/2961058) - https://gist.github.com/MohamedAlaa/2961058 (was used extensively for reference within the exercise)