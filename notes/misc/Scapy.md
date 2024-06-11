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

send(IP(dst="1.2.3.4")/ICMP())
.
Sent 1 packets.
>>> sendp(Ether()/IP(dst="1.2.3.4",ttl=(1,4)), iface="eth1")
....
Sent 4 packets.
>>> sendp("I'm travelling on Ethernet", iface="eth1", loop=1, inter=0.2)
................^C
Sent 16 packets.
>>> sendp(rdpcap("/tmp/pcapfile")) # tcpreplay
...........
Sent 11 packets.

Returns packets sent by send()
>>> send(IP(dst='127.0.0.1'), return_packets=True)
.
Sent 1 packets.
<PacketList: TCP:0 UDP:0 ICMP:0 Other:1>


sr() is used to know the answers to the packets we sent

ans, ans =  _
ans.sumamry()

