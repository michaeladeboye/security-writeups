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
