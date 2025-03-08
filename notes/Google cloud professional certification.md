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