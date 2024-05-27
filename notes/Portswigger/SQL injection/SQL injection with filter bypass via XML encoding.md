![[Pasted image 20240527101209.png]]

The above image is lab description
from the above description 
-  we know that there is a database that contains username and password 
- to solve the lab we have to retrieve the username and password and login to their account.

Let's take a look at the hint 

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

