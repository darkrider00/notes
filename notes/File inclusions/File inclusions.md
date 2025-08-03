
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
    


template engine : 
![[Pasted image 20250803104235.png]]

the template engines take input do the changes to the static webpage the gives us the final webpage other wise everytime we interact with a webpage it need to change the index.php file or about file and give is the final output 

The most common place we usually find LFI within is templating engines. In order to have most of the web application looking the same when navigating between pages, a templating engine displays a page that shows the common static parts, such as the `header`, `navigation bar`, and `footer`, and then dynamically loads other content that changes between pages.

Otherwise, every page on the server would need to be modified when changes are made to any of the static parts. This is why we often see a parameter like `/index.php?page=about`, where `index.php` sets static content (e.g. header/footer), and then only pulls the dynamic content specified in the parameter, which in this case may be read from a file called `about.php`.

As we have control over the `about` portion of the request, it may be possible to have the web application grab other files and display them on the page.

 LFI may also allow attackers to execute code on the remote server, which may compromise the entire back-end server and any other servers connected to it.


All vulnerabilities can occur in PHP , NodeJS,Java,.net and others
- each have different approach to include the files in webserver 
- they share common thing (loading a file from specific path)

example if the page contains ?language=es we can change it to en or tn something and access a different language page 

- if we have ability to read the files then we can use it to read other files and do remote code execution 

**PHP:**
- include() - used to load the local or remote file page
- if it doesnt sanitize the input then it leads to local file inclusion 


```php
if (isset($_GET['language'])) {
    include($_GET['language']);
}
```

- language parameter is directly passed in the include function so whatever parameter we pass in the language parameter it will be loaded on the page 

if we had control over the path passed into them. Such functions include `include_once()`, `require()`, `require_once()`, `file_get_contents()`, and several others as well.


**NodeJS**

```javascript
if(req.query.language) {
    fs.readFile(path.join(__dirname, req.query.language), function (err, data) {
        res.write(data);
    });
}
```

- parameter passed in the url gets used by the readfile function and written in http response 
- the `render()` function in the `Express.js` framework. The following example shows how the `language` parameter is used to determine which directory to pull the `about.html` page from:

```js
app.get("/about/:language", function(req, res) {
    res.render(`/${req.params.language}/about.html`);
});
```

we can change the URL to show a different file instead.

**JAVA**
```jsp
<c:if test="${not empty param.language}">
    <jsp:include file="<%= request.getParameter('language') %>" />
</c:if>
```
- include function take a file or page url as its argument then renders the object into front end template 
- import fucntion may be used to render local file or a url
```jsp
<c:import url= "<%= request.getParameter('language') %>"/>
```

.**NET**
- Response.WriteFile function works very similarly to all of our examples
```cs
@if (!string.IsNullOrEmpty(HttpContext.Request.Query['language'])) {
    <% Response.WriteFile("<% HttpContext.Request.Query['language'] %>"); %> 
}
```

 `@Html.Partial()` function may also be used to render the specified file as part of the front-end template, similarly to what we saw earlier:

```cs
@Html.Partial(HttpContext.Request.Query['language'])
```

**READ VS EXECUTE**
-  `some of the above functions only read the content of the specified files, while others also execute the specified files`

|**Function**|**Read Content**|**Execute**|**Remote URL**|
|---|:-:|:-:|:-:|
|**PHP**||||
|`include()`/`include_once()`|✅|✅|✅|
|`require()`/`require_once()`|✅|✅|❌|
|`file_get_contents()`|✅|❌|✅|
|`fopen()`/`file()`|✅|❌|❌|
|**NodeJS**||||
|`fs.readFile()`|✅|❌|❌|
|`fs.sendFile()`|✅|❌|❌|
|`res.render()`|✅|✅|❌|
|**Java**||||
|`include`|✅|❌|❌|
|`import`|✅|✅|✅|
|**.NET**||||
|`@Html.Partial()`|✅|❌|❌|
|`@Html.RemotePartial()`|✅|❌|✅|
|`Response.WriteFile()`|✅|❌|❌|
|`include`|✅|✅|✅|

if we had access to the source code in a whitebox exercise or in a code audit
- these actions helps us in identifying potential File Inclusion vulnerabilities, especially if they had user-controlled input going into them.
- Even if we were only able to read the web application source code, it may still allow us to compromise the web application, as it may reveal other vulnerabilities as mentioned earlier, and the source code may also contain database keys, admin credentials, or other sensitive information


**BASIC LFI**
- ![[Pasted image 20250803111702.png]]

![[Pasted image 20250803111709.png]]

![[Pasted image 20250803111719.png]]

Two common readable files that are available on most back-end servers are `/etc/passwd` on Linux and `C:\Windows\boot.ini` on Windows. 

```php
include($_GET['language']);
```

, if we try to read `/etc/passwd`, then the `include()` function would fetch that file directly. However, in many occasions, web developers may append or prepend a string to the `language` parameter.

 `language` parameter may be used for the filename, and may be added after a directory, as follows
```php
include("./languages/" . $_GET['language']);
```



![[Pasted image 20250803112000.png]]

 we can add `../` before our file name, which refers to the parent directory.

specify our absolute file path (e.g. `../../../../etc/passwd`), and the file should exist:

![[Pasted image 20250803112039.png]]

if we were at the root path (`/`) and used `../` then we would still remain in the root path. So, if we were not sure of the directory the web application is in, we can add `../` many times, and it should not break the path (even if we do it a hundred times!).

```
**Tip:** It can always be useful to be efficient and not add unnecessary `../` several times, especially if we were writing a report or writing an exploit. So, always try to find the minimum number of `../` that works and use it. You may also be able to calculate how many directories you are away from the root path and use that many. For example, with `/var/www/html/` we are `3` directories away from the root path, so we can use `../` 3 times (i.e. `../../../`).
```


 On some occasions, our input may be appended after a different string.
 it may be used with a prefix to get the full filename, like the following example:

```php
include("lang_" . $_GET['language']);
```

f we try to traverse the directory with `../../../etc/passwd`, the final string would be `lang_../../../etc/passwd`, which is invalid:

![[Pasted image 20250803112234.png]]

we can prefix a `/` before our payload, and this should consider the prefix as a directory, and then we should bypass the filename and be able to traverse directories:

![[Pasted image 20250803112305.png]]

```
**Note:** This may not always work, as in this example a directory named `lang_/` may not exist, so our relative path may not be correct. Furthermore, `any prefix appended to our input may break some file inclusion techniques` we will discuss in upcoming sections, like using PHP wrappers and filters or RFI.
```

if we try to read `/etc/passwd`, then the file included would be `/etc/passwd.php`, which does not exist:

![[Pasted image 20250803112407.png]]

**Exercise:** Try to read any php file (e.g. index.php) through LFI, and see whether you would get its source code or if the file gets rendered as HTML instead.


 a web application may allow us to download our avatar through a URL like (`/profile/$username/avatar.png`).

we craft a malicious LFI username (e.g. `../../../etc/passwd`), then it may be possible to change the file being pulled to another local file on the server and grab it instead of our avatar.


we would be poisoning a database entry with a malicious LFI payload in our username. Then, another web application functionality would utilize this poisoned entry to perform our attack (i.e. download our avatar based on username value). This is why this attack is called a `Second-Order` attack.

Developers often overlook these vulnerabilities, as they may protect against direct user input (e.g. from a `?page` parameter), but they may trust values pulled from their database, like our username in this case. If we managed to poison our username during our registration, then the attack would be possible.

