#### Naming Systems Overview:
---

Computers communicate via binary (10110011)

A naming system is used to convert binary into human readable words

==Domain Name System/Services (DNS)== is a common way names are assigned to IPs

#### Naming Systems:
---

The paradox:
- Naming systems are both essential and unnecessary
	- Essential for humans to work with large networks
	- Unnecessary for a network to function

Factors that determine DNS necessity:
- Network Size
- Address Size and Complexity
- User base size and skill

Small networks may not need naming services

#### Naming Architectures:
---

Naming systems can use different types of architectures to identify systems

Flat Name Architecture:
- No internal structure with no clear relationship
- - Example: AJ-PC, Larry-PC, Cooper-PC

![[Pasted image 20230717113542.png]]

Hierarchical Structure:
- Uses a sequence or pattern to name devices
- Example: USA-Sales-AJ, Eurpe-Market-Cooper, etc..

![[Pasted image 20230717113600.png]]

#### Name Resolution Considerations:
---
 Efficiency:
 - Name resolution takes up resources
 - Minimizing name resolution requests is desirable
 - Cashing allows for devices to store locations

Reliability:
- Naming systems must be reliable
- Only one location storing information can be a problem
- Redundancies (Multiple servers) can and should be configured to prevent a single point of failure

#### Early Naming Systems:
---
Basic files contained names and addresses for machines
- Known simply as a host name mechanism

Eventually the files were called host tables

Theses files still exist on systems today

HOSTS files exist on windows and Unix like systems


#### Local Host Table System:
---
Worked well for small, stagnant networks

Larger networks created the need for several entries and updates to the file
- The table grows with each additional device
- Changes to the network require constant changes to the host table
- Bandwidth issues become a concern

Flat naming architecture created naming conflicts

#### Domain Name System:
---
Continually growing and adding networks required a standardized system

A structured, hierarchical system was created 

Networks and names were organized into domains

Several RFCs were written and to move into a standardized, organized approach

DNS is continually evolving to support new addressing (IPV6)

#### DNS Goals:
---
Create a globally scalable, consistent namespace
- Consistent, predictable naming standard
- No duplication regardless of geographic location

Local control over local resources
- Administrator could control the naming of local devices
- Central authorities would not need to approve naming of every object

Distributed design to avoid bottlenecks
- Avoid one central location to store a master database

Application universality
- Support a wide variety of applications

Multiple underlying protocol support
- Support different underlying protocols
- DNS supports more than just IP addresses

Hardware universality
- Any computer system should be able to use the system, not just large servers

#### DNS General Functions
--- 
Naming space 
- One common, consistent, multi-level structure
- Starts from a single root divided into containers (domains), similar to a file system structure

Naming registration
- registration authorities maintain the structure of global DNS

Name resolution
- Client/server hierarchical name resolution process

![[Pasted image 20230717130414.png]]

#### DNS Terminology
---
Root
- top of the DNS name structure
- contains the entire structure
- By default, it has no name (null)

Branch
- Anything connected to the root
- Consists of a domain and all domain object inside

Leaf
- A domain object with nothing underneath

Root Domian: the root of the tree

Top-Level Domains (TLDs)
- Highest-level domain directly under the root
- Somtimes called first-level domains

Second level Domain:
- Located directly under the top level 

Subdomain:
- A domain located below second-level domains
- Can also reference domains further along in the tree

Parent Domain:
- A domain residing above another domain
- The root domain is the parent of top-level domains

Child Domain
- A domain that is the next-level down form a parent domain
- TLDs are children of the root domain

Sibiling Domain
- A domain at the same level as another in a hierarchy
- TLDs are all siblings that share the root as a parent

![[Pasted image 20230717135215.png]]

TLD:
- .com, .net, .gov, etc..

2nd Level domain:
- Weber.edu
- ksl.com
- etc

sub-domain:
- cs.weber.edu
- main.weber.edu

#### Absolute and Relative DNS Specification:
---
Fully Qualified Domain Names (FQDN)
- Domain name that contains the entire domain name (Example: mailserver1.mail.weber.edu)
- FQDNs identify the absolute name of the device starting at the root

Partially Qualified Domain Names (PQDN)
- Name that contains a partial domain name of the device
- Example: mailserver1
- DNS server can append .mail.weber.edu to resolve the FQDN

#### DNS Name Registration:
---
Top level domains must be unique, so the names must be managed
- IANA and ICANN manage these domains

Registration authorities can delegate authority to other organizations
- The .edu TLD must be regulated so no two different entities use the domain
- The weber.edu domain control can be delegated to Weber State University

Top-Level domains should reflect the organization's purpose

#### Common Top-Level Domains:
---
.COM
- Corporations and businesses

.EDU
- Universities and other educational institutions

.GOV 
- Government agencies

.MIL
- Military organizations

.NET 
- internet and networking technology organizations

.ORG
- other organizations, commonly non-profit

MANY others exist, and not all sites conform to these guidelines

#### DNS Zones:
---
DNS groups can be divided into zones

A zone is typically identified by a domain or subdomain name

Zones can be used to divide the responsibility of servers servicing a particular area

A name server with ultimate authority in the zone is considered an authoritative server

Zone information can be transmitted to other servers via zone transfers

![[Pasted image 20230717140754.png]]

#### DNS Disputes
---
Name conflicts
- Many companies my have the same name and want the same domain space

Corporate Warfare 
- Attempting to funnel competitor business to another domain

Cybersquatting
- Individuals recognizing potential value of certain names and registering those for later sale

Deceptive Naming
- Taking advantage of common misspelling of words or using other substituted characters

#### Resolving DNS Disputes
---
Domain Sharing
- Sometimes (rarely), companies may share access to a particular domain name

Domain Name Purchase/Sale
- bigger companies may opt to buy a domain form a smaller company at a not-so-nominal rate

Litigation 
- Lawsuits may result and the decision is left up to courts to decide the outcome.




