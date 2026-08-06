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
