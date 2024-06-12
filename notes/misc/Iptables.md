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
`iptables -I INP`


