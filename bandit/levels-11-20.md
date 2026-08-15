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
