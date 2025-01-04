![[1- dir (listing all the files).png]]

![[2- executing (sysmon64.exe).png]]

![[3- i.png]]

![[4 - sysmon installed and started.png]]

![[5 - checking if the sysmon is running or not.png]]

![[6 -checking in event viewer.png]]

![[7 - operational logs.png]]

![[8 - creating droplet -1.png]]

![[8 - creating droplet -2.png]]

![[8 - creating droplet -3 (recommended settings).png]]

![[8 - creating droplet -4 (password).png]]

![[8 - creating droplet -5 hostname config.png]]

![[9 - creating firewall.png]]

![[10 - adding firewall to our wazuh server.png]]

![[11 adding droplets to firewall -1.png]]

![[11 adding droplets to firewall -2.png]]

![[12 - droplet added.png]]

![[13- ssh login.png]]

![[14 - doing update and upgrade.png]]


Specifications
RAM: 8GB+
HDD: 50GB+
OS: Ubuntu 22.04 LTS

Install Wazuh 4.7
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh && sudo bash ./wazuh-install.sh -a

Extract Wazuh Credentials
sudo tar -xvf wazuh-install-files.tar


https://documentation.wazuh.com/current/quickstart.html

![[15 - installing wazuh.png]]


make sure you copy username and password



Specifications
RAM: 8GB+ (Recommend 16 GB)
HDD: 50+ GB
OS: Ubuntu 22.04 LTS

Installing TheHive 5

Dependences
apt install wget gnupg apt-transport-https git ca-certificates ca-certificates-java curl  software-properties-common python3-pip lsb-release

Install Java
wget -qO- https://apt.corretto.aws/corretto.key | sudo gpg --dearmor  -o /usr/share/keyrings/corretto.gpg
echo "deb [signed-by=/usr/share/keyrings/corretto.gpg] https://apt.corretto.aws stable main" |  sudo tee -a /etc/apt/sources.list.d/corretto.sources.list
sudo apt update
sudo apt install java-common java-11-amazon-corretto-jdk
echo JAVA_HOME="/usr/lib/jvm/java-11-amazon-corretto" | sudo tee -a /etc/environment 
export JAVA_HOME="/usr/lib/jvm/java-11-amazon-corretto"

Install Cassandra
wget -qO -  https://downloads.apache.org/cassandra/KEYS | sudo gpg --dearmor  -o /usr/share/keyrings/cassandra-archive.gpg
echo "deb [signed-by=/usr/share/keyrings/cassandra-archive.gpg] https://debian.cassandra.apache.org 40x main" |  sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list
sudo apt update
sudo apt install cassandra

Install ElasticSearch
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch |  sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
sudo apt-get install apt-transport-https
echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/7.x/apt stable main" |  sudo tee /etc/apt/sources.list.d/elastic-7.x.list
sudo apt update
sudo apt install elasticsearch

***OPTIONAL ELASTICSEARCH***
Create a jvm.options file under /etc/elasticsearch/jvm.options.d and put the following configurations in that file.
-Dlog4j2.formatMsgNoLookups=true
-Xms2g
-Xmx2g

Install TheHive
wget -O- https://archives.strangebee.com/keys/strangebee.gpg | sudo gpg --dearmor -o /usr/share/keyrings/strangebee-archive-keyring.gpg
echo 'deb [signed-by=/usr/share/keyrings/strangebee-archive-keyring.gpg] https://deb.strangebee.com thehive-5.2 main' | sudo tee -a /etc/apt/sources.list.d/strangebee.list
sudo apt-get update
sudo apt-get install -y thehive

Default Credentials on port 9000
credentials are 'admin@thehive.local' with a password of 'secret'


after configuring files we got both up and runnign

![[16 wazuh  installed.png]]

![[17- wazuh dashboard.png]]

![[18- thehive dashboard.png]]

![[19 wazuh passwords.png]]

![[20 wazuh service started in windows vm.png]]

![[21 windows machine has checkin into wazuh successfully.png]]

### new task generate telemetry and ingest into wazuh

security 4688

mimikatz