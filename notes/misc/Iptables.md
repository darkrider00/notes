- filter table
- nat table
- mangle table
tables/chains are used 

these IP tables are used create firewalls  

![[Pasted image 20240612150209.png]]

![[Pasted image 20240612150354.png]]

-  -l is used to list  -v is for verbose output
- -p is used to set rules for traffic  of inbound and outbound rules

Drop - no ack 
Reject - ack flag that it's rejected

CMD format:
`iptables [-t table ] -[AD] chain rule-spec [options]`

![[Pasted image 20240612151242.png]]

This is how a rule is defined in Linux using iptables
![[Pasted image 20240612151802.png]]

- the ICMP packets we are dropping are now getting accepted via new rule
- always first rule will be triggered first 
- if we want we can specify the location in the command 


![[Pasted image 20240612152648.png]]

`iptables -I INPUT 2 -p tcp--d port110 -j ACCEPT`
this command inserts a rule to accept incoming TCP traffic on port 110 directly before existing rule at 2
-d is used to delete

-F is used to flush 

### default chain policy

- iptables [-t table] -P chain target [options]

example: `iptables -t filter -P INPUT DROP`

-n is used to create new chain 
`iptables -t filtewr -N state`
- custom chain (-X)
- 1st rule is triggered in input chain only instead of custom chain
![[Pasted image 20240612153257.png]]

a new chain state is added to the iptables list

blocking specific ip or website syntax:

`iptables -A INPUT -s www.gitam.edu -j DROP`
for blocking -D

![[Pasted image 20240612155118.png]]

![[Pasted image 20240612155143.png]]

as we can see we can't access gitam.edu website x

you can mention port range to or range of ip address you want to block
- we can limit the number of concurrent connections per ip address
- we can block mac address
- we can keep a log og dropped network packets on IPtables

![[Pasted image 20240612160625.png]]

saving the iptable rules
`iptables-save>~/iptables.rules`

#### service iptables stop
#### service iptables start
#### service iptables restart

