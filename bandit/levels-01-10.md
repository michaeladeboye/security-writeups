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
- Using then `ls -A` to list the directory contents, then using `cat --` on every file until I found the one with the password

**New to me:**
- `reset` resets a terminal session
-  a "human readable file" is a file that can be read by humans i.e. not binary data

**Not fully understood**
- What caused the terminal to mess up when I used the `cat` command on the files that weren't human readable
- why when I entered `ls -h` it listed all the files as human readable

