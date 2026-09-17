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
