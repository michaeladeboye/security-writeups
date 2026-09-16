## Level 21

**Goal:** Use the setuid binary in the homedirectory to make a connection to localhost on the specified port. read a line of text from the connection and compare it to the password in the previous level. If the password is correct, the password for the next level will be transmitted

**What worked:**
- I used the `echo` command to write the password from the last level and piped it to `nc -l -p 1200 &`. This creates a listening server with the message of the password of the last level
- I then used the setuid binary on port 1200 and recieved the password for the next level

**New to me:**
- Putting the `&` symbol at the end of a command tells linux to run it in the background
