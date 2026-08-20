# Restricted Shell Escapes (Bandit 25, 26, 33)


## The concept
The levels 25, 26 and 32 were about getting out of a restricted shell, where I had to understand the concepts to make it possible. A restricted shell prevents you from running commands the way you normally would, it acts like a jail, but the jail has flaws that let you escape it. The jail can be restricted in different ways, as we can see on the bandit game, because levels 25 and 26 were about trying to get into the shell again, where the jail was the shell itself. Level 32 was about finding an input that lets you leave a restricted shell that puts all the letters you type into uppercase.

## How it works
The main idea of all the three levels were about leaving a restricted shell, each one with its own details that made them different between each other. In the level 25, it was necessary to enter in Bandit26 with an specific secret key that was previously found, but in the moment of logging in, the level set you off because of the restricted shell, so it was necessary to let only some lines on the page, so you would enter the "more" page, and some lines wouldn't be shown on the page, so it would open a line where you could insert the commands ":set shell=/bin/bash" and right after ":shell". After that, you would be able to search for the password of the level as you always do when you are logged at the right user, because the commands opened a shell, where you could write the commands to find the password. The level 26 was basically the same as the previous level, with the addition of the SUID that was necessary to get the password of Bandit27, with the command "./SUID cat XXXXXX". The level 32 was a bit different, because it was necessary to leave a shell that converted all the commands to capital words, so no command was accepted by the shell, but by writing "$0", the shell would go back to its normal way and let you get off the jail, letting you get the password of the Bandit33.

## The diagnostic path
Similar levels, different endings to each other. In the level 25 and 26, the fact of tying to get in by suing localhost was blocking me to continue, so it was necessary to log in by the inside, using the same command that was always used to enter. I discovered that by using the command "ssh -v" and reading until the authentication line that showed the problem. The level 32 was different, but at the same time similar, because all three had jails where I had to leave. I identified the jail in this case by looking at how the commands were identified by the shell, so once I understood that all commands were being identified as capital letters, I just had to enter the write command to leave the jail and have the normal shell.

## Real-world relevance
All three levels represent an important skill to have when working with cibersecurity, because sometimes it will be necessary to work with restricted shells and different types of jails, where you will need to leave them.

## Key commands
- `ssh -i <key>` — log in with a private key instead of a password
- `ssh-keygen -y -f <key>` — check the private key is valid and has no passphrase
- `ssh -v` — read the handshake, look for "Authenticated ... using publickey"
- `chmod 600 <key>` — fix key permissions (SSH refuses loose ones)
- `scp -P 2220 ...` — copy the key to the local machine (note: -P uppercase)
- `:set shell=/bin/bash` then `:shell` — escape from vim into a real shell
- `./SUID cat xxxxx` — view what is inside a file using a SUID
- `$0` — get off the restrictive jail