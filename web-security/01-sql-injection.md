# SQL Injection


## The concept
SQL is one of the most popular languages used to talk to databases. SQL injection works with SQL, but in a specific way: it uses that same language to turn what the user writes — from data into commands that will be executed by the database. It works because the app concatenates the raw input in the query, without separating data from commands. When successful, it allows the attacker to read, change or destroy the data that they wouldn't be able to touch.

## How it works
As I said in the concept, the data turns into commands by writing it precisely. An example of SQL injection structure: "SELECT [column] FROM [table] WHERE [condition]". This command allows the attacker to get into the user account without the password. The actual injected input would be: "admin'--". It works because the input is concatenated without sanitization, `admin'--` fits in and comments out the rest of the query, including the password check, so the password verification never actually happens, allowing you to get into the user's account just by having their username.

## The diagnostic path
The first thing I did when trying to enter the admin account without having access to the password was using the command "admin'-- ", which made the database accept my entry without verifying the password, because the line that guarantees that the password is correct never actually worked because of the "-- " inside the command, so all I needed was to know that the account name was "admin".

Then, I used the command "ORDER BY N", starting with number 1 and keep adding 1 to it until the error happened. When the error happens, it means we found the number of columns, because the last number that worked = number of columns. For example, if I try "ORDER BY 4" and the error happens, it means the number of columns is 3. 

Before the last command, it is important to see which positions appear on screen, and for that, we use the command "UNION SELECT 1, 2, 3". When the result is shown on screen, we can see the numbers 2 and 3 with their respective contents, but the number 1 doesn't return any result, meaning that the first one is going to be just "1" inside the following command, and the results from the numbers 2 and 3 will be placed in their respective place in the command.

After seeing what fits in every column, we can finally look for the information that we always wanted by using the command "UNION SELECT 1, username, password FROM users". We can only use this command now because of all the other steps we followed, which were giving us information to keep going and using more commands based on the previous information collected. 

## Real-world relevance
SQL injection allows attackers to leak, change or even destroy real data, credentials, client data or even an entire database. It is something extremely important and any mistake can be hard to solve.
When I did the exfiltration, the password appeared in pure text (admin: admin123), what is considered a vulnerability caused by insecure password storage.
When a credential is leaked, it doesn't stop there. If a hacker could get a password, he may be able to get many more of them, because people often reuse the same password across different systems, the attacker can try it elsewhere. And after that, many other crucial information from all the users he got the password from. It is an exponential problem and it needs to be treated as one.

## Key commands
- `admin'--` 
- `ORDER BY N`
- `UNION SELECT 1,2,3`
- `UNION SELECT 1, username, password FROM users`