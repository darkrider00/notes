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

#### Active command injection
Blind command injection occurs when system command made to the server does not return response to the user in HTML DOC

Active command injection return response to user 

![[Pasted image 20250110200221.png]]

In pseudocode, the above snippet is doing the following:

1. Checking if the parameter "commandString" is set

2. If it is, then the variable `$command_string` gets what was passed into the input field

3. The program then goes into a try block to execute the function `passthru($command_string)`.  You can read the docs on `passthru()` on [PHP's website](https://www.php.net/manual/en/function.passthru.php), but in general, it is executing what gets entered into the input then passing the output directly back to the browser.

4. If the try does not succeed, output the error to page.  Generally this won't output anything because you can't output stderr but PHP doesn't let you have a try without a catch.

reference : https://www.php.net/manual/en/function.passthru.php
The **passthru()** function is similar to the [exec()](https://www.php.net/manual/en/function.exec.php) function in that it executes a `command`. This function should be used in place of [exec()](https://www.php.net/manual/en/function.exec.php) or [system()](https://www.php.net/manual/en/function.system.php) when the output from the Unix command is binary data which needs to be passed directly back to the browser.

A common use for this is to execute something like the pbmplus utilities that can output an image stream directly. By setting the Content-type to `image/gif` and then calling a pbmplus program to output a gif, you can create PHP scripts that output images directly.

#### Return Values [¶](https://www.php.net/manual/en/function.passthru.php#refsect1-function.passthru-returnvalues)

Returns **`[null](https://www.php.net/manual/en/reserved.constants.php#constant.null)`** on success or **`[false](https://www.php.net/manual/en/reserved.constants.php#constant.false)`** on failure.

#### Errors/Exceptions [¶](https://www.php.net/manual/en/function.passthru.php#refsect1-function.passthru-errors)

Will emit an **`[E_WARNING](https://www.php.net/manual/en/errorfunc.constants.php#constant.e-warning)`** if **passthru()** is unable to execute the `command`.

Throws a [ValueError](https://www.php.net/manual/en/class.valueerror.php) if `command` is empty or contains null bytes.



command to find How many non-root/non-service/non-daemon users are there?

`awk -F: '($3 >= 1000 && $3 < 65534) && $7 !~ /nologin|false/' /etc/passwd | wc -l`

### Explanation of the Command:

1. **`awk -F:`**: Use `:` as the field delimiter to parse the `/etc/passwd` file.
2. **`($3 >= 1000 && $3 < 65534)`**: Only consider users with a UID (User ID) in the range 1000 to 65533.
    - UID 0 is for `root`.
    - UIDs below 1000 are typically for system/service/daemon users.
    - UIDs 1000+ are for regular users.
    - UID 65534 is often reserved for `nobody`.
3. **`$7 !~ /nologin|false/`**: Exclude accounts with shells like `/sbin/nologin` or `/bin/false` (indicating disabled accounts).
4. **`/etc/passwd`**: The file listing user account details.
5. **`wc -l`**: Count the number of lines, giving the total number of matching users.


