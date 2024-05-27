![[Pasted image 20240527101209.png]]

The above image is lab description
from the above description 
-  we know that there is a database that contains username and password 
- to solve the lab we have to retrieve the username and password and login to their account.

Let's take a look at the hint 

## hint
`A web application firewall (WAF) will block requests that contain obvious signs of a SQL injection attack. You'll need to find a way to obfuscate your malicious query to bypass this filter. We recommend using the [Hackvertor](https://portswigger.net/bappstore/65033cbd2c344fbabe57ac060b5dd100) extension to do this.`

the website :
![[Pasted image 20240527103159.png]]
I've turned on the burp proxy now let's navigate through the website.
let's check for inputs fields in the website for sql injection 

![[Pasted image 20240527113835.png]]

here there is a input field if we click on view details of any product 

now let's take a look at http history that is recorded in the burpsuite
![[Pasted image 20240527114009.png]]

here the server is requesting the product id and it is communicating with back so let's send this to repeater .

![[Pasted image 20240527114215.png]]


![[Pasted image 20240527114334.png]]

here's when we click on check stock then we are getting the number units present at that location we can definitely inject some payloads here
 let's send this to repeater too 
 
![[Pasted image 20240527115321.png]]

in this when we input the product id we are getting number of units present
 let's add `UNION SELECT NULL` to product id to determine number of columns.

![[Pasted image 20240527115659.png]]

we got attack detected that's why they gave us a hint about WAF in the hint section

- we need to obfusacate the input so that it will bypass the firewall , we need to install hackvetor extension to install hackvector extension  go to extensions tab and go to bwapp store and search for hackvector extension as mentioned in [[SQL injection with filter bypass via XML encoding#hint]]

![[Pasted image 20240527120459.png]]

- click on install to install the hack vector extension 
- for more information on the hack vector extension refer [[Hackvector extension]]

![[Pasted image 20240527121136.png]]

as we can see hack vector extension has been installed and loaded we can see it in the repeater section
- to use the hackvector select the payload you've already written and right click on it and select extensions and select encode using hex entities and then send the request.

![[Pasted image 20240527121548.png]]

![[Pasted image 20240527121619.png]]

as you can see hex entities tags are added to the payload we've selected 

and Boom !

![[Pasted image 20240527122135.png]]

we dind't get any attack detected in the response tab 
we successfully bypassed the WAF with this extension 
- now let's add another null to the statement to see if there are 2 columns 
![[Pasted image 20240527122405.png]]
we got 0 units that means only one column is present in the table 

let's build  a payload now to retrieve the username and password table 

`1 UNION SELECT username || '~' || password FROM users`

- let's breakdown this payload we've built union select is used to select and we are selecting username 
-  **`||`**: This is the string concatenation operator in SQL (specifically in databases like SQLite and PostgreSQL). It concatenates two or more strings.
- **`'~'`**: This is a tilde character being used as a delimiter (to separate username and password)
- and passwords from table users

![[Pasted image 20240527122849.png]]

in this lab we are looking for admin account so let's login with these details 



we got our username and passwords 