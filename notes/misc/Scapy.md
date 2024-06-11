![[Pasted image 20240611143959.png]]

to install : 
sudo apt install scapy

running: sudo scapy

ttl=time to live
src= source
dst= destination
del = delete 

to view packets  if a is packet
b=raw(a)
b

display captured packets a= rdpcap("path of file")

### generating set of packets 

a=IP(dst="website")
a

multiple ttl values

b = TP(ttl=[1,2,,(5,9)])

c=TCP(dport=[80,443])
[p for p in in a/c]


for more commands refer :
https://scapy.readthedocs.io/en/latest/usage.html

