
## BASICS
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

#### Challenges

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


## Virutualization
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

 
 ## Storage and Virtual Machines and Networks in the Cloud
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


Cloud storage 
- standard storage -accessd frequently 
- nearline storage - accessed once per month 
- coldline storage - accessed every 90 days 
- archive storage - once a year

![[Pasted image 20250314185035.png]]

auto class- based on access pattreens optimises features access

![[Pasted image 20250314185121.png]]

![[Pasted image 20250314185455.png]]

![[Pasted image 20250314185648.png]]

Firestore

![[Pasted image 20250314185733.png]]

![[Pasted image 20250314185818.png]]

![[Pasted image 20250314185828.png]]

![[Pasted image 20250314185953.png]]


## containers in the cloud 

![[Pasted image 20250314193607.png]]

Kubernetes
- open source platform for managing containerized workloads
- makes it easy to orchestrate many containers on many hosted microservices and deploy rollouts and roll backs
- set of APIs to deploy containers on set of nodes called a cluster
- divides into primary set of components that run as the control plane and set of nodes that run containers
- describe as set of applications and how they should interact with each other and kubernetes figures how to make them happen 
![[Pasted image 20250314194652.png]]

pod -smallest unit in kubernetes that u can create or deploy 
represents your running applications or your entire app 
- generally u have only one container per pod
![[Pasted image 20250314194809.png]]

provides unique IP
command > kubectl
![[Pasted image 20250314194841.png]]

Kubernetes creates a Service with a fixed IP address for your Pods, and a controller says "I need to attach

an external load balancer with a public IP address to that Service so others outside the cluster can access it."

In GKE, the load balancer is created as a network load balancer.

To scale :
![[Pasted image 20250314194931.png]]

![[Pasted image 20250314195020.png]]

if you want to apply new changes 

GKE - google hosted managed kubernetes service in the cloud 
- consits of multiple machine 

![[Pasted image 20250314195149.png]]

GKE manages all the control plane components for us 

- still exposes ip address
- Node configuration and management depends on the type of GKE mode you use.
- With the Autopilot mode, which is recommended, GKE manages the underlying infrastructure such as node configuration, autoscaling, auto-upgrades, baseline security configurations, and baseline networking configuration.
- With the Standard mode, you manage the underlying infrastructure, including configuring the individual nodes.

![[Pasted image 20250314195302.png]]


![[Pasted image 20250314195310.png]]

helps us 
![[Pasted image 20250314195345.png]]



![[Pasted image 20250314195412.png]]

![[Pasted image 20250314195429.png]]

In Kubernetes, a group of one or more containers is called a pod. Containers in a pod are deployed together. They are started, stopped, and replicated as a group.The simplest workload that Kubernetes can deploy is a pod that consists only of a single container.



Cloud run 

![[Pasted image 20250314195632.png]]

Process

![[Pasted image 20250314195703.png]]

Source flow 

![[Pasted image 20250314195743.png]]


The pricing model on Cloud Run is unique; as you only pay for the system resources you use
while a container is handling web requests, with a granularity of 100ms, and when it’s starting or shutting down.

The price of container time increases with CPU and memory.
A container with more vCPU and memory is more expensive.
You can use Cloud Run to run any binary, as long as it’s compiled for Linux sixty-four bit.

![[Pasted image 20250314195848.png]]

in cloud run 


devlopment in cloud :
![[Pasted image 20250314195935.png]]

Cloud Run functions is a lightweight, event-based, asynchronous compute solution that allows you to create small, single-purpose

functions that respond to cloud events, without the need to manage a server or a runtime environment.

These functions can be used to construct application workflows from individual business logic tasks.

![[Pasted image 20250314200015.png]]

cloud run functions are asynchronous use http invokation for synchronization 


## PROMPT Engineering 

Generative AI encompasses a broader range of models capable of generating various types of content beyond just text, while LLM specifically refers to a subset of generative AI models focusing on language tasks.
 - Generative artificial intelligence, which is commonly referred to as gen AI, is a subset of artificial intelligence
 - that is capable of creating text, images, or other data using generative models, often in response to prompts.
 - a prompt is a specific instruction, question, or cue given to a computer
 ![[Pasted image 20250314202451.png]]


![[Pasted image 20250314202525.png]]


![[Pasted image 20250314202642.png]]

![[Pasted image 20250314202711.png]]

![[Pasted image 20250314202728.png]]

wrong ans - hallucinations 
no real time info or dont have req data 
can work on what they see
![[Pasted image 20250314202856.png]]


![[Pasted image 20250314203051.png]]

![[Pasted image 20250314203121.png]]

![[Pasted image 20250314203212.png]]


![[Pasted image 20250314203246.png]]

![[Pasted image 20250314203307.png]]

![[Pasted image 20250314203313.png]]

![[Pasted image 20250314203326.png]]

![[Pasted image 20250314203339.png]]

![[Pasted image 20250314203353.png]]

### VPC networks 

- Virtual private cloud is virtual version of physical network 
- provides connectivity for your compute engine and VM instances
- inbuilt pass through network load balencers and internal application load balaencers
- distributes traffic from google cloud external load balencers to backends
- u can create a route to send packets (we need to make sure that firewall is allowing our packets)
- project can contain multiple vpc networks
- start with default network (auto mode VPC network(has one subnet))

![[Pasted image 20250319204219.png]]

VPC networks are isolated by default
- uses internal ip to communicate within and external ip to outside
- Multiple Network interfaces are used when a single instance needs to act as a network appliance for tasks like load balencing and IDS/IPS

example project : 
![[Pasted image 20250319204952.png]]

![[Pasted image 20250319205133.png]]

![[Pasted image 20250321164211.png]]

Network Service Tier :
![[Pasted image 20250321164352.png]]

www.gcpn.com

![[Pasted image 20250321164531.png]]

![[Pasted image 20250321164635.png]]

## VPC netwrok peering 
- allows private connectivity across two VPC
- across organizations
- within the same project
- across different projects

![[Pasted image 20250321165117.png]]

- u can peer computer engne, kubernetes , app engine flexible environments
- peered VPC networks remain administratively separate 
- no subnet IP ranges overlap across peered VPC networks
- Transitive peering is supported
- Each side Peering is supported independently 

![[Pasted image 20250321165256.png]]

![[Pasted image 20250321165414.png]]

Custom routes
- help achieve a desired granularity that cannot be achieved with default route
- sharing routes and dynamic with peered VPC networks learn routes directly from their peered networks
- if a custom route in peered network is updated your VPC network automatically learns and uses the updated custom toute
- we can import and export routes

![[Pasted image 20250321165643.png]]

