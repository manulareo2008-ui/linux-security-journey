# The basics (Bandit 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10)


## The concept
The first 10 levels are the foundational levels, they have the objective of showing the players the basic commands they will use until the last level. Those levels are basically about reading files from the terminal. The big difficulty about those levels is not technical, it is about understanding where you need to look in order to find answers and learn to ignore useless files with weird names, restrictions or because they are among useless trash. 

## How it works
They teach about reading files with the commands "ls", "ls -a", "ls -l", "ls -la", "cd", "cat" and "pwd", reading files with problematic names (those that start with a dot), how to look inside files that start with a "-" using "cat ./ FILE" and how to read files with spaces among the words in the name (for example, to look inside the file "--look inside here--", you need to use the command 'cat "./--look inside here--"').

## The diagnostic path
When the command "cat" doesn't show the content you need, the problem is not the command, it's in the file, so you need to use commands like "ls" or "ls -a" to find the right file before reading anything.

## Real-world relevance
All these are the basics of the Linux world. When working with Linux, you definitely need to know all this.

## Key commands
- `ls` - used to list the files
- `ls -a` - used to list all the files, including the hidden ones
- `ls -l` - used to look at the permissions of the file
- `ls -la` - used to look at the permissions of all files, including the hidden ones
- `cat` - used to read the content of a file
- `pwd` - used to read the file path
- `file` - used to show the type of content of a file
- `find` - used to search for files by filters (name, size, permission, owner)