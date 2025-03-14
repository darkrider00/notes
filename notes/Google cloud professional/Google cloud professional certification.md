cloud - network of data centers

instead of describing a complex web of software , servers, computers, networks, and security systems  we use one word called cloud 

on premises
- on prem
- hardware and software hosted within org
- traditional way for managing IT infra
- req physical space , expert personnel , often require more computing resources 

private cloud
- infra is dedicated to single organization 
- single-tenant or corporate cloud 
- hosted within org or at org own data center ,
- or third party facilitator
- for private data

public cloud 
- on demand third party service provider where on demand computing services and infra managed by  third party provider
- shared to tenants
- multi cloud infra 
- a apartment has many tenants and each tenant is living private 
- no need to acquire, manage 
types:
 1. IAAS - compute and storage services
 2. PAAS - development and deployment 
 3. SAAS - services to get access to software on subscription basis

hybrid cloud
- mostly this and multi are same
- applications run in diff env  
Multi cloud
- mostly companies follow this
- combing both physical and diff organization 
- at least 2 cloud providers like google cloud Ans amazon web services etc. (takes key strengths of different cloud providers)


Due to those 
we have - scalable 
flexible 
AGILE -develop and deploy fast 
strategic value 
secure -due to depth of mech 
cost effective - only pay for what they use 

- save costs, faster sec, reduction of management load , focusing on new capabilities (digitalization is made easy)

### Challenges

- best at understanding and using data 
- best tech infra 
- creating a hybrid workplace 
- know their data, systems is secure 
- prioritize sustainability 

Five capabilities
- Data - for AI and analyzing (data driven org)
- open infra - choose to modernize , bring services to physical locations
	 1. open standard - particular specifications and guidelines eg: http protocol to send specific info 
	 2. open source - publicly accessible 
- collaborations-  workspaces , communication and collaboration Eg: google apps
- Trust - helps org protect what's imp using security protocols and mechanisms
- Sustainable Technology 

![[Pasted image 20241123160327.png]]

Google cloud framework base 
- short term tactical
- mid term strategic 
- long term transformational obj 

cloud maturity assessment helps to establish where an organization is currently regarding the cloud adoption recognized by google cloud

after cloud maturity has been assessed and actions have been recommended it's easy to scope and structure a cloud adaption program using the framework


Review of section :

- digital infra is important for technology evolution and cost effectiveness
- 2 or more types are used by single organization 


Total cost of ownership 
on premises -  higher than cloud (power, cooling maintenance, support services)
switching from capital expenditure to operating expenses 
capital - buy once and benefit several years




AI and ML in cloud 

- used for prediction 
- requires more complex models for making accurate predictions

quality is assed on 
- completeness - all req data is present or not 
- uniqueness - should be unique (no duplicates)
- timeliness - up to date  and timely and relavent
- validity - conforms set of predefined standards (type and format)
- accuracy - correctness of the data 
- consistency - uniform and doesn't contain any contradictory information 

anything model can't see it doesn't exist

![[Pasted image 20250212114703.png]]

explainable AI - google tool

building ML models
- BigQuery ML - Use SQL queries to create and execute machine learning models in BIg Query
     - model trained access using SQL familiar to data analysts , less tools requires
     - integrates with vertex AI
     - deployed to end points for online prediction

- Pre trained APIs - leverage model that have already built and trained by google 
     - less customization 
     - suitable when u don't have data
     - analyzing images videos 
     - analyzes in google public cloud
     - vision API , Natural language API (discover syntax text and diff categories, cloud translation API , speech to text API vice versa ,video intelligence API)

- Auto ML - no code solution to build ML models on vertex AI
    - vertex Ai and unified AI 
    - used vertex AI and Auto Ml to build end to end models
    - Auto ML choose best models suitable for model
    - saves time 
    - AutoML vision API , Auto ML NLP API

- Custom training -  code your own ML environment have control over ML

![[Pasted image 20250212120133.png]]

- tools for image processing and all

TensorFlow - open platform for ML
- tensor processing unit 
- implented across google cloud products

AI solutions aimed to solve specific business needs
- contact center AI
     - provides model for handling customer care 
     - saved in database and exported to further analysis
- Discovery AI
     - to select optimal products for the search , relevance and likely to make sale
- Document AI 
- Cloud Talent Solution

AI can take 3 to 36 months to to build 
- pre trained API dont need training is done
- expertise required while selecting model 
- effort required to build AI solutions



computing - computing power 
- virtualization allows mutliple resources to run on same hardware 

![[Pasted image 20250307211925.png]]

containerization 
- only virtualize operating systems 
- faster , less memory 

kubernetes
- open source cluster management system that provides automated container orchestration
- application reliability
- fast and more agile

serverless computing 
- automatically provisioned behind the scenes
- function as a service
- you write code and cloud provider does everything else

google cloud uses Open APIs

![[Pasted image 20250307212631.png]]

Anthos - modify existing application and run it on anywhere 

![[Pasted image 20250307212856.png]]


compute engine - scalable high performance network engines
Vmware engine - fully managed vm engine on google cloud
Bare metal - enables specalized workloads to cloud 

container
google kubernetes engine
- group of compute engines to perform a structure 

![[Pasted image 20250307213115.png]]

cloud run
- allow users to build application with their choice of tools languages and dependencies and deploy them

![[Pasted image 20250308110321.png]]

Apeege -API
![[Pasted image 20250308111808.png]]


 
![[Pasted image 20250308191340.png]]

service infra security - service deployment layer
- encrypted of inter service communication 

User identity layer 
- user identity 
- encryption at rest 

internet communication layer
- Google Front End ("GFE")
- Denial of service 

Operational security layer
- Intrusion detection
- reducing insider risk 
- employee Universal second factor
- Software development practices


cloud.google.com/products/calculator 

 rate quota and Allocation Quota

![[Pasted image 20250308193125.png]]

4 levels 
level 1 - resources 
- vms cloud storgae buckets bgi query 
level 2 - Projects 
- resources are organised into projects
- managing APIs 
- using google cloud services  like 
level 3 - folders
- projects are organised into folders and sub folders
level 4 - organisation node
- encompassess all the projects in the organisation

policies are inherited downroad 

folders let u assign policies to resources at a level of granualrity you choose

project ID -  unique globally, assigned by google cloud but mutable during creation, Immutable after creation

Project Name - need not be Unique
- chosen by u
- mutable

Project number - unique
- assigned by google cloud
- Immutable

Resource manager tool 
- gather list of projects
- create update delete recover projects
- access trough RPC API REST API

We can use folders to group projects 


IAM - can apply policies that define who can do what on which resources

- account
- group
- service account 
- other

to use a VM u should be able to start stop delete pause the VM u can group all these and give it as permission

Basic 
- owner,edito viewr , billing admin
Predefined
- compute engine
     - a group or person can do specific set of actions 
     Predefined actions: 
     - compute .instance.delete
     - compute.instance.get
     - compute.instance.list
     - compute.instance.setMachineType
     - compute.instance.start

Custom 
- if we want some users to start and stop compute engine virtual machines but not reconfigure them 
- you willl need the manage the permissions that define cutom tole u have created

Service Account :
lets say u have an application running in a VM, that needs to store data in cloud storage , but you dont want anyone on internet to have access to that data, , you can create a service account to authenticate that VM to cloud storage 

- named with email address
- access with cryptographic keys 
- need to be managed 
- it can have IAM policies

 Google cloud console can be accessed through
 - google cloud console
     -  simple web based GUI
     - easily find resources check health 
     - facility to quickly find resources and connect instances
 - cloud SDK
     - set of tools manage resources and applications in google cloud
     - cloud CLI interfacefor google cloud Products and services
     - bq -A command -line tool for BigQuery
     - debain based VM
     - all tools are installed and maintained
 - APIs
     - offer APIs that allow code to written to control them 
     - explorer shoes what  APIs are availble in what versions
     - provides cloud client and google API client libraries
     - lang represented : JAVA, PYTHON , PHP, C#, Go, Nodejs
 - Google cloud APP
     - satart stop SSH to connect into compute engine
     - start stop cloud SQL instances
     - administer applications deployed on app engine
     - upto date billing info
     - customizable graphs


VPC 
- secure induvidual private cloud computing model hosted with public cloud
- run code , store data, host website , anythign else that can be done on ordinary private cloud
- hosted by remotely by public cloud provider

VPC networks 
- connect google cloud resources to each other and to the internet 
- segmenting networks
- using firewall to restrict access to instances
- creating static cloud roues to forward traffic to specific destinations 

size of subnet can be expanded and used worldwide


![[Pasted image 20250314173717.png]]

this capablity can be used to build solutions that are resilient to disruptions and retain a simple network layout

compute engines bills by second
commited use discounts
preemptible and spot VMS
 != compute engine VM
![[Pasted image 20250314174018.png]]
pay for what u need 
has Auto scaling 

VPC compatiblities 
- has routing tables
- no router provising or managing 
- restrict acess to instances
- add firewall rules

vpc peering connection b/w 2 vpcs can be established 

Cloud load balencer  

![[Pasted image 20250314174534.png]]

![[Pasted image 20250314174553.png]]

Cloud DNS
- managed DNS runs on same infra as google
- low latencty high availability 

edge caching
![[Pasted image 20250314174712.png]]

using of caching servers to store content closer to end users

connecting networks to google VPC
- using cloud VPN
- direct peering - puts router in same public data center as google point of presence
    -  uses a router to exchange traffic between networks
- carrier peering 
     - direct access from on premises network through service provider networks
     - not covered by google service level agreement 
 - dedicated interconnect 
     - one or more direct connection to google
 - partner interconnect
    - cant reach a dedicated interconnect coloaction facility 
    - useful if data doesnt need a warrent
- cross cloud connect
     - establish high bandwidth dedicated connectivity b/w google cloud and another cloud service provider
     - 