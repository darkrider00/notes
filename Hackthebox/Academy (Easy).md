
Starting with Nmap
![](../attachments/Pasted%20image%2020240331223815.png)


we won't be able to connect to the website using only ip address so we can access the website after adiing the website in /etc/hosts

![](../attachments/Pasted%20image%2020240331223953.png)

The POST request to register a new user is interesting:

![](../attachments/Pasted%20image%2020240331225045.png)


While the `uid` (user id) and double password fields are expected, `roleid` is interesting. I’ll register again, but this time I’ll use Burp proxy to intercept the POST and change `roleid` to 1.

![](../attachments/Pasted%20image%2020240331225505.png)

after changing the role everythign works same but this time it logged in to admin panel 

here's the homepage of dev-staging-01
![](../attachments/Pasted%20image%2020240331230121.png)


![](../attachments/Pasted%20image%2020240331230200.png)

we found the app name and app key 

google search about larvel exploit led e to this
https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/laravel

there are exploits in github where we can clone them and exploit them on the ip directly

after a bit of research i've found this 
https://www.rapid7.com/db/modules/exploit/unix/http/laravel_token_unserialize_exec/

i fired up msfconsole ot use the exploit
![](../attachments/Pasted%20image%2020240331232245.png)

after setting Rhost Lhost options and running we got a terminal
![](../attachments/Pasted%20image%2020240331233056.png)

we used python3 -c 'import pty;pty.spawn("bash")' to beautify the terminal 

![](../attachments/Pasted%20image%2020240331233910.png)

from the above we can login with user cry0l1t3
`cr0l1t3` user was a member of the `adm` group. On a typical Linux system, this group is responsible for system administration and, notably, monitoring.
so loggedin with cry0l1t3 user and got the user flag
![](../attachments/Pasted%20image%2020240331235258.png)

using log inspection tool using the `aureport` tool I was able to find credentials for the `mrb3n` user

![](../attachments/Pasted%20image%2020240331234551.png)


i logged in with mrb3n user and run the comamnds

TF=$(mktemp -d)
echo '{"scripts":{"x":"/bin/sh -i 0<&3 1>&3 2>&3"}}' >$TF/composer.json
sudo composer --working-dir=$TF run-script x

/bin/sh -i 0<&3 1>&3 2>&3

i got root access and got the rootflag

![](../attachments/Pasted%20image%2020240331235459.png)


i pwned the machine 