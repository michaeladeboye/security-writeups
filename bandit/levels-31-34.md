## Level 30

**Goal:** From your local machine, clone the git repository at ssh://bandit30-git@bandit.labs.overthewire.org/home/bandit30-git/repo via the port 2220 and find the password for the next level. The password for the user bandit30-git is the same as for the user bandit30

**What worked:**
- Using `git clone` on the repository, while specifying the port 2220 then using the `cat` command on the README file in the copied directory. After that using `git tag` to see the file's tags and `git show` to see the tag message
- 
**New to me:**
- `git tag` allows you to see a files's tags
- `git show <tag_name>` shows more info on the tag such as the tag's message
