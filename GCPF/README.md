# GCP (Related to my JECP project) (2nd CHAPTER IS IMPORTANT)

1. Fundamental concepts - Compliance requirements, resource hierarchy, cost optimization, geographical segmentation strategy.
2. Advance security practices - IAM, infra security, N/W security, data security, security operations.
3. Data management - Object storage on GCP (SQL, NOSQL)

### 1. Fundamental concepts

#### 1(a) GC Compliance => (Rules, regulations, legalities)

#### 1(b) Resource hierarchy 
`ORG` => `departments` => `teams` => `product` 

`ORG` => `folder` => `project` => `resources`

Project[dev project, test project, prod project] => Resources [CS bucket, App engine service, compute engine instance]

IAM (Identity & access management) - Who can do what on which resource.

#### 1(c) Cost optimization

Billing setup in GCP - Based on diff service classes, Consumption based model, Application on discount

Pricing - Hourly, monthly, yearly, commitment(1y/3y)

Cost optimization strategies - Enable GuardRails(billing alerts), using discount(commitment plans), optimism workLoad(use cloud native service, reduce hardware).

#### 1(d) Google n/w infra (geographical segmentation strategy)

Regions => ZONES => n/w edge location => countries and territories

Zonal OR regional (compute engines) || Multinational(dual OR multi region) || global(vpc n/w)

----

### 2. Advance security practices

Infra & services - Compute, IAM & security, n/w, Storage & DB, IOT, BigData, cloud AI, Data transfer, management tool

#### 2(a) IAM

Set resource hierarchy correctly to avoid security risks.
Underlying resources inherit policy permissions from parent resource

ORG Node => Root node represents your org(yourBusiness.com)- some services may not available if ORG node not created.

Folder Node => map properly (HR folder for HR department like that)

Project Node => Child of org or folder node, contains all resources

Service node => Actual GC services e.g. compute engine, BigQuery, storage bucket

**IAM Policies** => Create policies to apply on resource to control access

3 Factor makes up a policy
- Members => users, employee OR service account OR google group
- Roles => collection of permissions, compute admin, 
- Logic conditions => Extra constraints (Access during office hours only)

Policy applied in 2ways => 1. Transitive inheritance 2. Direct Assignment

If resource "z" moves from project A  to project B then polices of project B will be applicable from now.

**Role Type**
- Basic => Owner, editor, viewer
- Predefined(Best practices) => Compute admin, app engine etc.
- Custom => Require high maintenance

**IAM Best practices**
- Give bare minimum permission to user, pgm or process 
- Seperate service account for each user/service & give only necessary permissions
- **Manage resource using project(isolated)**
- Utilize google group instead individual role
- Rotate user managed service acc keys regularly

**NOTE :** Access control for google cloud resource is managed by IAM policies

#### 2(b) Infrastructure security

Computing Services - GC Engine/ GCE (Create VMs), App engine(web mobile backend), k8s engine(container service), cloud f/n, cloud run, VMWARE engine

- GCE => IaaS, create & manage VMs, Customer is responsible for full config (creation of VM, OS, RAM, PROCESSOR, update security patches (Use preemptive VM to save cost(auto on/off))

- App engine => PaaS, reliable & high performance, build,develop& host web app.

HOW to create VM in GCE
- Give details(name, region, zone, machine config), OS, API Access, HTTP Traffic. After installing any web server (NGINX) - external IP of VM internal IP of VM

**Infra security best practices**
- Secure n/w using firewall, load balancer OR encrypt
- Isolate your PROD resource from internet(Isolate from public use, cut use of public IP)
- Apply principle of least privilege (IAM recommended)
- Enable log collection & monitor your VM

#### 2(c) N/W Scurity

**VPC(Virtual private network):** A virtual version of on-premise physical n/w. Benefits => It is considered a global resource, flexible & scalable, sharable, isolation

=> To create VPC you must create a Project

VPC is a cloud service that allow create & manage resources in logically isolated virtual n/w (Isolated PVT n/w within a public cloud) 

**NOTE :** Each project has its own VPC(isolated from other env), we can create separate env for dev, testing and prod. Associate your VPC to a VM.

- VPC is made up of subnets
- Firewall controls the n/w traffic flow & enforce at VM level
- VPC Peering allow internal resource to connect other VPC

**Firewall Rules =>** Allow or deny n/w traffic connections to & from your VM. Firewall rules are stateful(bidirectional) & always enforced . Enforced at VM level & VPC defined at n/w level. 
Firewall rules are applied all the time either VM is on/off.

SMTP (PORT 25) - Always blocked on GC.
DHCP (PORT 67) - ALways allowed.

**SUBNET =>** It let you create own pvt cloud topology within GCP. N/W are global resource & subnet are regional resource.

Additonal VPC n/w tools => Load balancer, cloud armor, C security command center, C identity aware proxy.

#### 2(d) DATA SECURITY (Bucket - container for data)

CSEK - Customer supplied encryption keys
SMEK - Customer managed encryption keys

Data encryption option
- We have various encryption algo, data is encrypted before written to disk, google do not handle client side encryption.

Data security best practices

- Store data in region closest to your application user, don not share credentials, use TLS (HTTPS) protocol to transport your data.

----

### 3. Data management

#### 3(a). Object storage on GCP

Features of object storage- Config obj lifecycle management, multiple redundancy options (store data in multiple locations). We can turn on object versioning from CLI.

How to migrate data in cloud storage => Create project then create bucket, drag&drop data or push from CLI/CLOUD SHELL

#### 3(b) Relational DB

Bare metal solution, cloudSQL, cloud spanner
Cloud spanner is global(horizontally scalable), cloud SQL is regional (mySQL, pgSQL, sqlServer)

#### 3(c) NON-Relational DB

Cloud BigTable(Steaming data, IOT, low latency, no hierarchy, no in-memory), fireStore(collection)

#### 3(d) Data warehouse (Big query)

Why use big query instead of cloud SQL OR cloud Spanner => used to query very big data & data analysis [BigQuery is serverless]
