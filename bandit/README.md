# OverTheWire: Bandit

Writeups for [Bandit](https://overthewire.org/wargames/bandit/), OverTheWire's beginner Linux wargame. Each level means SSHing into the next account with a password you find on the current one. I completed the full wargame.

## Writeups
Levels are grouped about 10 per file, with one section per level.

| File | Levels |
|---|---|
| [levels-01-10.md](levels-01-10.md) | 1–10 |
| [levels-11-20.md](levels-11-20.md) | 11–20 |
| [levels-21-30.md](levels-21-30.md) | 21–30 |
| [levels-31-34.md](levels-31-33.md) | 31–33 |

## What it covers
- **Linux basics**: navigating the filesystem, hidden files, weird filenames, `find` by size, owner, and permissions
- **Text processing**: `grep`, `sort`, `uniq`, `strings`, `base64`, `tr` (ROT13)
- **Hexdumps and compression**: reversing a hexdump with `xxd` and unpacking layered gzip, bzip2, and tar archives
- **Networking**: `nc`, `openssl s_client`, and port scanning with `nmap`
- **SSH**: logging in with private keys and running commands when the shell logs you out
- **Privilege and automation**: setuid binaries, cron jobs, and the scripts they run
- **Git**: digging through commit history, branches, and tags for credentials
- **Shell escapes**: breaking out of a restricted shell and a pager
