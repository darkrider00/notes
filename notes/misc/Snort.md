signature based intrusion detection system 

BRO, smart -open source tools

- network based intrusion detection system
- takes corresponding action if signature matches

to build a intrusion detection system
winpcap - java language windows
lipcap - c language linux 

detection will try to match signatures and if it matches it will from the packet 

sniffer - just capturing packets (lipcap)
packet logger - logs packets
ids mode - create alerts for the logs that matched signature

if u r expecting particular traffic u can whitelists them and generate alerts in them 

`snort -vde`
running snort in sniffer mode

`snort -dev -l ./log` stores logs in log file in root directory 

`sudo -c /etc/snort.conf -l /var/log/snort -A console`

-c specified configuing file
-a alert
-l logs