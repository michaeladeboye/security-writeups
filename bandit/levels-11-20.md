## Level 11

**Goal:** Find the password stored in the file data.txt which contains base64 encoded data

**What worked:**
- Ran `base64 -d data.txt` which outputted the decoded data from data.txt

**New to me:**
- The `base64` encodes binary data into plain text

## Level 12

**Goal:** Find the password stored in the file data.txt where the ROT13 substitution cipher has been applied

**What I tried first:**
- Ran `tr data.txt` which outputted an error message

**What worked:**
- Ran `cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'` which took the output from `cat data.txt` and translated it out of ROT13

**New to me:**
- The `tr` command needs 2 strings to be given to translate
- The `tr` command needs to be passed data from the output of a previous application

## Level 13

**Goal:** Find the password stored in the file data.txt which is a hexdump of a file that has been repeatedly compress

**What worked:**
- Created a temporary directory using `mktemp -d`, copied data.txt over to it using `cp`, and changed its name using `mv`
- Ran `xxd -r` on the file to revert it from hexdump format
- Ran `xxd (filename) | head` to see whether the file was compressed using `bzip2`/`gzip`, or if there was a file in it.
- Changed the file extension to either `.gz` or `.bz2` depending on the on what it was
- Used `gzip -d` or `bzip2 -d` on the file to decompress it
- When a file contained another file I used `tar -xf` to extract the file

**New to me:**
- `tar -xf` extracts a file from within another file
- `gzip` and `bzip2` compress files
- Each file type has its own file signature that can be seen when viewing a hexdump of the file

## Level 14

**Goal:** Get the private SSH key and use it to log in to the next level

**What I tried first:**
- I first attempted to use `scp` on the bandit14 file which did not work because I was in Bandit and you cannot ssh from inside the level and I was supposed to copy the private key

**What worked:**
- I logged out of the level and copied the `sshkey.private` file using `scp`
- I then changed the permissions on the `sshkey.private` file using the `chmod` command to be able to read, write, and execute the file
- I then used the `ssh` command with the `-i` option using `sshkey.private` as its argument and the destination being the next level

**New to me:**
- The `-i` option for the `ssh` command selects the file  from which the private key for public key authentication is read

## Level 15

**Goal:** Submit the password of the current level to port 30000 on localhost

**What worked:**
- I used the `nc` command with the with the the destination as localhost and the port as 30000

**New to me:**
- The `nc` command allows to read and write data over a network connection.

## Level 16

**Goal:** Submit the password of the current level to port 30001 on localhost using SSL/TLS encryption

**What worked:**
- I used the openssl command `s_client` with the -connect option while specifying localhost as the host and port 30001 as the port to connect while using SSL/TLS

**New to me:**
- openssl commands need to be specified by putting openssl before the command
- to see an openssl command's man page, you must enter `openssl-(command)` ex: `open-ssl-s_client`
- `s_client` implements a generic SSL/TLS client which connects to a remote host using SSL/TLS.

## Level 17

**Goal:** Retrieve the credentials for the next level by submitting the password of the current level to a port on localhost in the range 31000 to 32000 that speaks SSL/TLS

**What I tried first:**
- I used the `nc` command with the -z option in order to scan for ports with a listening server which worked but did not tell me which ports spoke SSL/TLS

**What worked:**
- I used the `nmap` command with the -sV option to see the service and the -p option to specify the port range
- I then submitted the password of the current level to the correct port using `s_client -connect` as well as the `-quiet` flag which outputted a private key
- I copied the private key, logged out, created a file and put the private key into that file
- I then used the `ssh` command with the `-i` option using the file I created as its argument and the destination being the next level

**New to me:**
- `nmap` determines what hosts are available on the network and what services those hosts are offering, as well as much more


