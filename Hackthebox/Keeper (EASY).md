Starting with a nmap scan we have this result 
![](../attachments/Pasted%20image%2020240331145343.png)

When we access the IP address on port 80 via a browser, we can see there is just one link which redirects to `tickets.keeper.htb/rt`. But in order to do that we need to add this IP to our `/etc/hosts` file

10.129.122.221  tickets.keeper.htb  
10.129.122.221  keeper.htb

![](../attachments/Pasted%20image%2020240331145837.png)

i've ried some default passweords and dource code but it wasn't helpful

i've googled and searched in exploit db but found no exploit mentioned in the web page 
![](../attachments/Pasted%20image%2020240331145751.png)

so i searched for default creds for Request tracker 

![](../attachments/Pasted%20image%2020240331150124.png)

![](../attachments/Pasted%20image%2020240331151500.png)

i got loggedin using the default credentials

in the users section i've found lnorgaard user and also a intial password Welcome2023!

![](../attachments/Pasted%20image%2020240331151804.png)

![](../attachments/Pasted%20image%2020240331151945.png)

so i logged into ssh and found the user flag 
![](../attachments/Pasted%20image%2020240331152158.png)

after that we can see a zip file if we extract we get 2 files
![](../attachments/Pasted%20image%2020240331152542.png)

a simple google search led me to this vulnerability
![](../attachments/Pasted%20image%2020240331152515.png)



in the repo we can see this
![](../attachments/Pasted%20image%2020240331152725.png)

to install .net refer here
https://learn.microsoft.com/en-us/dotnet/core/install/linux-scripted-manual#scripted-install

![](../attachments/Pasted%20image%2020240331153718.png)

after using dotnet run dmp file i got the  password 
**dgrød med fløde**.’

after searching this password in google  evry result contained rod med flode so the password must be tht 
![](../attachments/Pasted%20image%2020240331164248.png)

after installing keypass2 in my windows i open passwords.kdbx file with keypass2 
 with password rød med fløde
![](../attachments/Pasted%20image%2020240331164429.png)

i got logged in 
![](../attachments/Pasted%20image%2020240331164516.png)


here after refering to root user notes i found 
![](../attachments/Pasted%20image%2020240331170848.png)


Instead of Passkey2 we can use kpcli 

which is a putty user file  by searching in google Putty-User-Key-File-3
i found this website 
https://www.baeldung.com/linux/ssh-key-types-convert-ppk

![](../attachments/Pasted%20image%2020240331171010.png)

![](../attachments/Pasted%20image%2020240331171137.png)

.ppk file can be converted into id_rsa private key through which we can login ssh with this key 


![](../attachments/Pasted%20image%2020240331170807.png)


i got the root access key is present in root.txt

![](../attachments/Pasted%20image%2020240331171331.png)

machine is pwned 


For using Kpcli refer to 
https://github.com/rebkwok/kpcli
https://kpcli.sourceforge.io/
https://youtu.be/0AafRQIaWmQ?feature=shared

from here you can get the same putty- user key i got with  keypass2 and convert this into rsa private key gen file and log in to ssh and get root access