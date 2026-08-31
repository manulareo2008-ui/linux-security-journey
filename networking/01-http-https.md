# HTTP/HTTPS

## The concept
HTTP is a way of communicating with the web that allows you to send information from your machine to others, or to allow you to interact with websites in real time.
It is a conversation of request/response, where all the information is human-readable, which makes it dangerous and weak, because someone located halfway along the path that tries to see what is happening can read it easily. I could see it when entering the website "example.com" directly from the terminal using HTTP. 
There is also the HTTPS that does the same as HTTP, but it adds a security layer called TLS, making it more secure than HTTP. 
HTTPS ensures confidentiality, integrity and authenticity because of the TLS layer.

## How it works
The HTTP anatomy works with three parts: 
The request line (it uses the method, the path and the version). For example: "GET / HTTP/1.1";
The headers, with the shape "key: value". For example: "host: example.com";
The empty line. It means that the headers ended and it sends the request.

After sending the HTTP request, there is the response, that also has a specific anatomy:
It reflects the request, showing the status line, the headers, the empty line and the body (the HTML);
Some of the responses show what the headers say (server, Content-Type).

The way the request is answered means what happened:
If the response has the shape "2xx", it means everything worked and the system could bring the information;
If it has the shape "3xx", it means that the user will be redirected, but it doesn't mean the request failed;
If it has the shape "4xx", it means that you did something wrong in the request;
And the last possibility is the shape "5xx", that means that the system has a problem, not your request.

There is also the HTTPS, that works as a HTTP, but adding the TLS layer.
TLS encrypts the communication, making the HTTP more secure and usable to send sensitive information.
Before the information is actually sent, there is something called "handshake", that works like a negotiation between both sides, in order to prove to each other that it is secure to send the information. The server proves who it is by showing a certificate and they have a secret key to encrypt the rest of the conversation.

## The diagnostic path
In order to see with my own eyes the request beeing accepted and getting the "200" response, I had to try 7 times, each one making a little change to the command, always trying to solve the current problem. 
The final command was "printf "GET / HTTP/1.1\nhost: example.com\n\n" | nc example.com 80", that was finally accepted. 
This command makes the request be accepted and gave me the answer that I was expecting: the answer "200" and access to the headers, where I could see the server. 
In the final command, I had to use the command "\n" three times, and each of them is essential. The first one comes after the request line, closing it. The second ends the header "host" line. The third creates an empty line that sends it. Without any of them, the command wouldn't work.

## Real-world relevance
All this knowledge is really important in real world, especially because it helps to prevent cases of:
- Sniffing
- MITM
- Fingerprinting
- Downgrade
All these are examples of how attackers get into your requests and get access to sensitive information without your consent.


## Key commands
- `nc` - opens a raw TCP connection to a host and port.
- `printf | nc` - combination of commands used to do a full request in one single line. "printf" does a similar job to "echo", but it works better for request because it doesn't understand the commands, it only prints them in the exact order you wrote them. Who understands the commands is the system, when the full command is sent by the "nc".