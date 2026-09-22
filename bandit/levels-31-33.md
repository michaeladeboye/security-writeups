## Level 31

**Goal:** From your local machine, clone the git repository at ssh://bandit30-git@bandit.labs.overthewire.org/home/bandit30-git/repo via the port 2220 and find the password for the next level. The password for the user bandit30-git is the same as for the user bandit30

**What worked:**
- Using `git clone` on the repository, while specifying the port 2220 then using the `cat` command on the README file in the copied directory. After that using `git tag` to see the file's tags and `git show` to see the tag message

**New to me:**
- `git tag` allows you to see a files's tags
- `git show <tag_name>` shows more info on the tag such as the tag's message

## Level 32

**Goal:** From your local machine, clone the git repository at ssh://bandit31-git@bandit.labs.overthewire.org/home/bandit31-git/repo via the port 2220 and find the password for the next level. The password for the user bandit31-git is the same as for the user bandit31

**What worked:**
- Using `git clone` on the repository, while specifying the port 2220 then using the `cat` command on the README file in the copied directory. I then created the file `key.txt` which I was told to by the content in the README.md file. After that I used `git add -f` to update that `key.txt` would be part of the next commit, using yhe -f flag to force the file to be committed even though it is normally ignored. I then used `git commit` to save the changes and `git push` to update the change in remote repositories

**New to me:**
- `git commit` saves the currently made changes with a message describing these changes
- `git push` updates local changes in remote repositories. When pushing for the first time, you should also define the branch with `-u`
- `Git Ignore` is a file with the filename ‘.gitignore’. In this file, all file names/extensions that should be ignored by the commit are written
- `git add` updates what files will be part of the next commit. The -f flag forces files to be able to be committed, even when they are normally ignored

## Level 33

**Goal:** Escape the uppercase shell and find the password

**What worked:**
- Used `$0` to break out of the uppercase shell then read the password file `bandit33`

**New to me:**
- `$0` looks at whatever program is running(usually the shell itself)
