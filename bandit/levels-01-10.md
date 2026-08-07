## Level 0

**Goal:** Use SSH to log into the game

**What worked:**
- ssh bandit0@bandit.labs.overthewire.org -p 2220

**New to me:**
- `-p` sets a non-default SSH port. Default is 22; OverTheWire uses 2220.

## Level 1

**Goal:** Get the password from the readme file in the home directory and use it to log into bandit1

**What worked:**
- Used the ls command to see what files were in the home directory and the cat command printed what was in the readme file
- Used the password found in the readme file to log into bandit1

**New to me:**
- The exit command is used to close the current shell
- Bandit blocks password logins originating from the game server itself.
  Exit back to your own machine before connecting to the next level.

## Level 2

**Goal:** Get the password from a file called - and use it to log into bandit2

**What I tried first:**
- Ran `cat -`. There was no output or error just a blinking cursor. 

**What worked:**
- Prefixing the filename with ./

**New to me:**
- `-` is either an option prefix or interpreted as an instruction to read from standard input
- `--` signals the end of command options, everything after is treated as a positional argument
- `./` means current directory. When used on `-` it turns `-` into a path.
- Use `./` on filenames that begin with a dash

## Level 3

**Goal:** Get the password from a file called "--spaces in file name--" and use it to log into bandit3 

**What worked:**
- Using `--` after the cat command and putting the file in quotes

**New to me:**
- Wrapping a filename that has spaces in it with quotes treats the text as a single argument
- Using `\` before each space strips the special meaning of the space
- Using tab to autocomplete the file or folder name inserts the necessary escape characters or quotes automatically.

## Level 4

**Goal:** Get the password from a hidden file in the inhere directory and use it to log into bandit4 

**What worked:**
- Using `cd` to change to the inhere directory, then `ls -a` to list all the directory contents, then using the `cat` function to obtain the password

**New to me:**
- `ls -A` lists everything in the directory except `.` and `..`
- `ls -a` list everything in the directory

## Level 5

**Goal:** Get the password from the only human-readable file in the inhere directory and use it to log into bandit5 

**What worked:**
- Using `ls -A` to list the directory contents, then using `cat --` on every file until I found the one with the password

**New to me:**
- `reset` resets a terminal session
-  a "human readable file" is a file that can be read by humans i.e. ASCII or Unicode

**Not fully understood**
- What caused the terminal to mess up when I used the `cat` command on the files that weren't human readable

## Level 6

**Goal:** Get the password from a file somewhere in the inhere directory that is human-readable, 1033 bytes in size, and not executable 

**What worked:**
- Using `du -ab` to find which of the files in each of the directories in the inhere directory has a byte size of 1033, then `ls -hA` to find which of the files is human readable and `find -executable` to eliminate the files that are executable.

**New to me:**
- Multiple options can be used simultaneously after a single dash

## Level 7

**Goal:** Find the password which is somewhere on the server and is owned by user bandit7, owned by group bandit6, and 33 bytes in size.

**What I tried first:**
- Ran `find / -user bandit7 -group bandit6 -size33c`. Permission for access was denied.

**What worked:**
- Ran `find -user bandit7 -group bandit6 -size33c` and added `2>/dev/null` at the end to hides all errors, which allowed me to see where the password is

**New to me:**
- `2>/dev/null` hides all error messages
- `/` is the root directory

