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
