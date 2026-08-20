# 03-privesc (Bandit 17, 18, 19, 20, 21, 22, 23, 24)
 

## The concept
When you are acting as a lower account, you have restrictions, because you are a limited user. The objective is to be able to make the role of another user, with more privileges. I learned three different ways to do that during the exercises 17 to 24: using a SUID, cron or brute force. 

## How it works
The SUID is a binary with the S bit, which runs with the identity of the file's owner. It is possible to find SUIDs in the system by using the command "find / -perm -4000", because all the files with the S bit turned on will be identified. It makes the one who uses it be able to do whatever he wants when the SUID wasn't configured with limits, so you act like the root. When someone finds a SUID like that, his search is over, because with that he doesn't need to climb privileges, he already has access to everything. But when the SUID has restrictions, it's still powerful, but not dangerous, because it means it was configured to do a specific function, so he won't give full access to the system, he will just do his specific job and nothing else. To use it, you need to use the command "./SUID ACTION". Cron is a scheduler, and every job that it delivers has its own identity, that is owned by the creator of that job. The cron is a very powerful tool, because, when configured in that way, it is possible to write scripts inside the folders that cron reads. If that folder allows you to write in it (because of the user's permissions), you can write scripts in order to receive something back, as it was done in the level 23. The brute force is used when the amount of possibilities is too big to be tested one by one, so instead of that, you write a command that tries every single one automatically.

## The diagnostic path
In order to find the SUIDs, you use "ls -la", to see the S bit in the files that have it. The scripts from cron are commonly read to understand how they work and what jobs they execute. The main idea behind all of them is "can I use this to get privileges ? what can I influence with this ?"

## Real-world relevance
All this is daily used by hackers when trying to find SUIDs that were badly configured, crons that allow them to introduce scripts in order to gain information, or they simply use the brute force to enter anywhere they need.

## Key commands
- `./SUID ACTION` - used to execute an action with SUID
- `find / -perm -4000` - used to find the SUIDs 
- `ls -la` - shows all the permissions of all the files
- `for i in $(seq -w 0 9999); do echo "PASS $i" | nc HOST PORTA; done` - creates a loop for testing all the possibilities and sends the answer to the service gate, in order to receive the answer