
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

### Dot 
Suppose a PHP file like this exists on the server:

`// vuln.php <?php include("uploads/" . $_GET['file'] . ".php"); ?>`

You visit this URL:

`http://example.com/vuln.php?file=test`

What happens?

PHP sees:

`include("uploads/test.php");`

It loads that file if it exists.

✅ So far so good.

---

## 😈 The Hacker’s Trick (4096-byte Truncation)

Now, here’s the **trick hackers discovered**:

PHP has a **limit of 4096 bytes** for a file path.

If a path is longer than that, PHP **cuts off (truncates)** anything beyond 4096 bytes **silently**, without showing an error.
So:
#### Let's say you do:

`http://example.com/vuln.php?file=aaaaaaa...aaaaaa (4067 'a's)`
Internally PHP creates this string:

`"uploads/" + "aaaaa...aaaa" (4067 'a's) + ".php" = total 4075 bytes`

Oops! That’s **too long** — longer than 4096 bytes.
So PHP cuts it:
`"uploads/aaaa...aaaa"  ← exactly 4096 bytes`

The `.php` at the end? ❌ GONE — it's **cut off**.
PHP then tries to include this file:
``uploads/aaaaa...aaaaa   (no `.php`)``

If this file exists on the server, PHP will **include it**.

---

## 😕 So... What’s the Confusing Part?

You asked:

> "If I give such a long filename, will the file really exist? Can the request work?"

Let me answer that clearly:

---

## ✅ FINAL EXPLANATION (KID-FRIENDLY)

### 🍕 Imagine you're ordering pizza:
You call the pizza shop and say:

> "Hi, I want to order a **MargaritaWithExtraExtraExtraExtra...ExtraCheese** pizza."

The guy on the phone has a limit of 4096 letters. He can only write that much on his order screen. So when you say too many "Extra"s, he cuts off everything after 4096 characters.

So instead of:
`MargaritaWithExtraExtraExtra...ExtraCheese (full name)`

He sees:

`MargaritaWithExtraExtraExtra...(cut after 4096 letters)`

He now checks:

> ❓“Do we have a pizza with this shortened name?”

If yes → He bakes it. 🍕
If no → He says “Sorry, we don’t have this.” ❌

---

## 🧁 In PHP terms:

- You give a long filename (like many "aaaaa")
    
- PHP adds `.php` to it
    
- The total path becomes **longer than 4096 bytes**
    
- PHP **cuts off everything after 4096 bytes**
    
- So `.php` is removed!
    
- PHP now **checks if a file with the remaining name exists**
If that file exists → it gets **included** ✅  
If it doesn’t exist → you get an **error** ❌

---

## 🧠 Hacker’s Goal:

1. Create or guess a file with **no extension** (like `uploads/hackfile`)
2. Trick PHP into **cutting off** `.php`
3. PHP now includes `uploads/hackfile` instead of `uploads/hackfile.php`
    

---

## 🧪 TL;DR (Super Simple)

- PHP can only handle **4096 bytes** for filenames.
- Anything longer is **cut off**.
- If you craft a long enough path, the `.php` at the end can be **cut off**.
- If the remaining path **exists as a file**, PHP includes it. ✅
- If not, you get an error. ❌


## The Real Goal of the Attack:

> You’re **not** using the payload to “open” a normal, short file like `uploads/admin`.

You are using the payload to:

- Trick PHP into loading a **very long filename**
    
- That **you created (or controlled)** ahead of time
    
- Where the `.php` part gets **cut off** at 4096 bytes
    
- So that **PHP includes your file**, even though the code seems to restrict file names to `.php`
    

---

## 🔐 Why This Is Useful to Hackers:

Because many apps do this:

`include("uploads/" . $_GET['file'] . ".php");`

…thinking they’re safe because only `.php` files can be loaded.

But with this truncation trick, if the attacker can:
- Upload a file with a long name (e.g., via upload bypass)
- Or trick the server to create a long log file, image, or error file

Then they can later:

- Trigger a path > 4096 bytes
- Cause PHP to cut off `.php`
- Load their file with **any extension or no extension at all**
    

---

## 💡 So Yes — You’re Creating the Long-Named File **First**

Then using the payload to **load it** by pushing `.php` off the edge.

This is why attackers often **combine** this trick with:

- File upload bypasses
- LFI (Local File Inclusion)
- Log poisoning
- Other creative write primitives
    


