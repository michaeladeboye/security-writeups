## Level 21

**Goal:** Use the setuid binary in the homedirectory to make a connection to localhost on the specified port. read a line of text from the connection and compare it to the password in the previous level. If the password is correct, the password for the next level will be transmitted

**What worked:**
- I used the `echo` command to write the password from the last level and piped it to `nc -l -p 1200 &`. This creates a listening server with the message of the password of the last level
- I then used the setuid binary on port 1200 and recieved the password for the next level

**New to me:**
- Putting the `&` symbol at the end of a command tells linux to run it in the background

## Level 22

**Goal:** Find the password from a program is running automatically at regular intervals from cron. Look in /etc/cron.d/ for the configuration and see what command is being executed

**What worked:**
- I listed the items in the `/etc/cron.d directory` and used the `cat` command on the file that corresponds with the level. I then ran the `cat` command on the file  was referenced in the file that contained the instructions for the cron program. Lastly I ran the `cat` command on the file that the cron program was writing the password to

**New to me:**
- Cron is a time-based job scheduler
- There are multiple folders that contain cronjobs

## Level 23

**Goal:**  Find the password from a program running automatically at regular intervals from cron. Look in /etc/cron.d/ for the configuration and see what command is being executed

**What I tried first** 
- I listed the items in the `/etc/cron.d directory` and used the `cat` command on the file that corresponds with the level. I then ran the `cat` command on the file  was referenced in the file that contained the instructions for the cron program and tried to run the `cat` command on the file that the cron program was writing the password to. That did not work because variables were used rather than a filename

**What worked:**
- After running the `cat` command on the file  was referenced in the file that contained the instructions for the cron program, I ran `echo I am user $bandit23 | md5sum | cut -d ' ' -f 1` which runs the script which creates the file that has the password. From there, I ran the `cat` command on the file and got the password

**New to me:**
- Variables in bash scripting contain a value
- The syntax`var_name=var_value` is used to declare a variable in bash scripting
- The syntax `var_name=$(command)` saves the output of a command in a variable
- `$var_name` accesses the value of an existing variable

## Level 24

**Goal:**  Find the password from a program running automatically at regular intervals from cron. Look in /etc/cron.d/ for the configuration and see what command is being executed. Create a shell script to get the password

**What worked:**
- Using the `cat` command on the cronjob file that corresponds with the level as well as the bash script that the cronjob file refrences. I then created a script that writes the password from bandit24 to a file I can read. Finally, I changed the permissions on that script and ran it by copying the script file to the folder that the other bash script refrences

**New to me:**
- A script can refrence and execute another script
- To run a file inside a directory, the directory must have the execute permission
- Bash scripts begin with `#!/bin/bash`

## Level 25

**Goal:**  A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. Use brute force to find the pincode

**What worked:**
- Created a bash script that connected to port 30002 using the `nc` command and ran a loop which wrote the password of bandit24 as well as every number combination between 0000 and 9999 to stdout one by one until it was correct

**New to me:**
- In bash, data flows from left to right through a pipe `|`. Meaning the output generator (In this case the loop) comes before the command that reads the input(In this case `nc`)

## Level 26

**Goal:** The shell for user bandit26 is not /bin/bash, but something else. Find out what the shel for user bandit26 is, how it works and how to break out of it.

**What worked:**
- I first use the `cat` command on `/etc/passwd` to find the shell used for bandit26. I then copied the private ssh key to a file on my local machine. After that I made the terminal window small so that `more` would not fill the screen and exit and used `ssh` with the `-i` option, refrencing the file with the private key. I then pressed v to open the file inside the vim editor. Next I entered command mode and ran these two commands. `:set shell=/bin/bash` and `:shell`. Once I did this I used the cat command on the bandit26 file and got the password

**New to me:**
- The `v` shortcut in `more` automatically opens the current file in the system's default text editor (vim)
- The `:shell` command in `vim` tells the editor to temporarily pause itself and open a command prompt for the user
