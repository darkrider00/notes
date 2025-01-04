- got to google and type install Splunk universal forwarder installation


![[Pasted image 20240524112726.png]]

got to download universal forwarder and login to your splunk account if you are not logged in 

![[Pasted image 20240524112851.png]]

install according to your device specifications

![[Pasted image 20240524113214.png]]

you can change path in customize options and thin window appears 
- here the ssl certificate means certificates needed for the server to trust Splunk (if you want to send logs to the server)
- if you don't want this you skip this by clicking on next

After clicking next you will see this window
![[Pasted image 20240524113649.png]]

if you want to use system in your computer itself then you have to choose local system
- if it's within organization and the client is also member of domain (group of computer then you have to choose domain account).

![[Pasted image 20240524113944.png]]

- now you have a choice of selecting which logs you want to collect in your local machine
- the same option you will in the server too
- if it's server then you can enable AD too
- you have to be careful while selecting performance monitor options 

As of now I'm selecting application logs, security logs, system logs and setup logs and CPU load from performance monitor

next give some username and password 

![[Pasted image 20240524114557.png]]

next
![[Pasted image 20240524114917.png]]

in the real word there are group of servers that are connecting logs and those servers are controlled by deployment server
- if receiving logs are in different machine and controller is in different machine then you have to enter the deployment server and port you can mention it or default port is 8089

![[Pasted image 20240524115447.png]]

basically what we are saying is 
To your receiving client at this particular port.
I'm going to send the logs from this machine.

1. Perform one of the following steps depending upon your requirements:
    
    - In the **Deployment Server** pane, enter a host name or IP address and management port for the deployment server that you want the universal forwarder to connect to and select **Next**.
        
    - In the **Receiving Indexer** pane, enter a host name or IP address and the receiving port for the receiving indexer that you want the universal forwarder to send data to and select **Next**.
The above will be the case only if server is at one location and indexer at one location

![[Pasted image 20240524120840.png]]

if you login the Splunk in the quick links section you can see add data and click on forward option to setup for setting up receiving  port got to forwarding and receiving option in settings and you will see this

![[Pasted image 20240524121306.png]]
and click on configure receiving and if the default port is set it's okay other click on add new to setup port and the same thing you need to give while installing Splunk forwarder in the below window and logs will be forwarded to that particular port 

![[Pasted image 20240524121111.png]]

i've given my host ip and and default port and click on next and install and it will be installed 

![[Pasted image 20240524121748.png]]


![[Pasted image 20240524121451.png]]

![[Pasted image 20240524123237.png]]

the universal forwarder is installed successfully on our local machine 

for more information refer : https://docs.splunk.com/Documentation/Forwarder/9.2.1/Forwarder/InstallaWindowsuniversalforwarderfromaninstaller
