injection flaws- occur because controlled input is interpreted as actual commands or parameters by application 
- depends on technologies 
- how exactly input is interpreted 

**SQL Injection:** This occurs when user controlled input is passed to SQL queries. As a result, an attacker can pass in SQL queries to manipulate the outcome of such queries. 

**Command Injection:** This occurs when user input is passed to system commands. As a result, an attacker is able to execute arbitrary system commands on application servers.

main defence for preventing injection attacks is ensuring that user controlled input is not interpreted as queries or commands. There are different ways of doing this:

- Using an allow list: when input is sent to the server, this input is compared to a list of safe input or characters. If the input is marked as safe, then it is processed. Otherwise, it is rejected and the application throws an error.
  
- Stripping input: If the input contains dangerous characters, these characters are removed before they are processed.

### command Injection 
- occurs when server side code like php in web app makes system call on hosting machine 

 The worst thing they could do would be to spawn a reverse shell to become the user that the web server is running as.  A simple `;nc -e /bin/bash` is all that's needed and they own your server; some variants of netcat don't support the -e option. You can use a list of [these](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md) reverse shells as an alternative.


