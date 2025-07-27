
https://owasp.org/www-project-web-security-testing-guide/v42/4-Web_Application_Security_Testing/07-Input_Validation_Testing/11.1-Testing_for_Local_File_Inclusion

- usually means include a file and exploiting dynamic file inclusion
- vuln occurs due to the use of supplied input 

it can also lead to:

- Code execution on the web server
- Code execution on the client-side such as JavaScript which can lead to other attacks such as cross site scripting (XSS)
- Denial of Service (DoS)
- Sensitive Information Disclosure

- including files that are already present on the server ,exploit vulnerble inclusion 
- the path to the file should be included (if no sanitization) allows directory traversal charcters such as ../ 
- comes in also other technologies like JSP, ASP

`http://vulnerable_host/preview.php?file=example.html`

- instead of file name we can write script directly include the input parameter 
http://vulnerable_host/preview.php?file=../../../../etc/passw

If the above mentioned conditions are met, an attacker would see something like the following:

```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
alex:x:500:500:alex:/home/alex:/bin/bash
margo:x:501:501::/home/margo:/bin/bash
...
```

Consider the following piece of code:

```
<?php include($_GET['file'].".php"); ?>
```

Simple substitution with a random filename would not work as the postfix `.php`

### Null Byte Injection
- null terminator or null byte 
- 0 present in many character sets 
-  `http://vulnerable_host/preview.php?file=../../../../etc/passwd%00` would ignore the `.php` extension being added to the input filename,

### Path and Dot Truncation
- 