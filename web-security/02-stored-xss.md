# Stored XSS


## The concept
Stored XSS is really similar to SQL Injection, but it works with a different focus. While SQL Injection focuses on deceiving the database in order to reach the data, the Stored XSS focuses on deceiving the user's browser. It is a way of introducing commands in HTML or JavaScript, with the intention of making the user's browser execute arbitrary attacker code. I am talking specifically about "Stored" because it is a specific branch inside XSS that focuses on the website itself, because the commands stay in the website's database, waiting for the user to get inside it and for their browsers to execute it. 

## How it works
When the attacker uses Stored XSS, what they are actually doing is introducing a malicious input into the page and the browser interprets it as code. In other words, the input stops being just an input and starts being used as a command. The attacker stores the command on the database, then, after each visit from users on the website, the server returns that payload inside the website and the victim's browser executes it. The attack is planned once by the attacker, but it ends working each time it is loaded by each user's browser. Because the payload lives inside the database, everyone who loads that website receives the attack. 

## The diagnostic path
When I actually tried to use Stored XSS, I had to follow a sequence of commands in HTML and JavaScript. The first thing was to find out if it was possible to introduce commands in both languages into the field. The first command used was '<b>teste</b>', which would answer the question by creating or not a "note" inside the lab in bold. I used this command before using JavaScript to verify if the field would accept HTML. I could know that the field accepted HTML because the note was created without the characters '<b>' and '<i>', because they were interpreted by the browser, proving that the field accepted HTML. If the field were safe, the note created would be the same as the command introduced. I also tried to stack more than one tag in the same command, which resulted in the following command: '<b><i>teste</i></b>', which created the field "teste" again, but now in italic words. That also taught me to write the commands in the right way, because you need to do it in that specific way I did, and not in a different way such as '<b><i>teste</b></i>', so it is important to close the command with the same "letter" that you opened it and follow that rule for all the "letters.

Once I knew that the field accepted HTML, I started the real work, that was to create an alert message by using JavaScript. So for that, I used the command '<script>alert('Using XSS')</script>'. Then, I could see the alert box being created and displayed once the browser loaded the page. That means that every person who enters the page, would automatically see that alert box once their browser loaded the payload. 

The command in JavaScript I used is completely safe for all webpages, so it was fine to use it on the lab because the "alert()" just opens a box and does nothing else. It doesn't steal data, doesn't redirect and doesn't execute any action on behalf of the victim. It proves it is possible to execute code without causing damage.

## Real world relevance
Inside a lab, it might look innocent, but when used in real websites, where things are posted, people are accessing, Stored XSS may cause big problems. When a field is not safe and it interprets any HTML or JavaScript command, any person can introduce malicious commands and attack absolutely anyone who access the website, because in Stored XSS, the command stays on the database and is loaded by the browser of all users who access without them even wanting. It can cause, for example, information/cookie theft or redirection to other website.

## Key commands
- `<b>teste</b>` - verify if the field accepts HTML
- `<b><i>teste</i></b>` - stack two different tags in the same command
- `<script>alert('Using XSS')</script>` - execute JavaScript and create the box