#### Email History:
---
- Electronic mail predates TCP/IP and the internet with usage on ARPANet
- Early messages were transmitted and received on main frame computing devices
- One of the first email protocols documents was published in 1971 (RFC 196)
	- The Mail Box Protocol
- Several revisions to the protocol happened during the same year

#### Email Protocol Evolution:
---
- During the mid 1970's several protocol developments took place
	- Mail Transfer Protocol (MTP) used features form FTP and Telnet to transfer messages
	- Unix-to-Unix Copy Protocol was developed for Unix systems and Usenet communications
- In 1981, Simple Mail Transfer Protocol (SMTP) defined transfer of mail without FTP

#### Basic Steps of Email Communication:
---
- Mail Composition
	- User creates an email that contains a body and a header, which contains addressing information
- Mail Submission
	- ==Mail is sent to an email server using the SMTP Protocol==
- Mail Delivery
	- Mail server looks DNS information of intended recipient and sends the message accordingly
- Mail Receipt and Processing
	- Recipient mail server accepts the message and stores it in the appropriate mailbox
- Mail Access and Retrieval
	- Intended recipient checks with local server to determine if any mail has arrived
- Some of these steps may not be preformed (Local versus remote transmission)

#### Common Mail Protocols:
---
- SMTP 
	- Simple Mail Transfer Protocol
	- Sends email
- POP (and POP3)
	- Post Office Protocol
	- Retrieves email
- IMAP (and IMAP4)
	- Internet Message Access Protocol
	- Retrieves email ( and synchronizes better than POP)

![[Pasted image 20230731110345.png]]

#### Email Client Settings:
---
- IMAP = Port: 993
- SMTP = Port: 465 (SSL) or ==587== (TLS)
- POP = Port: 995

==be wary of ports: 25, 110, 143== NON SECURED

#### Email Addressing:
---
- Email is user-based, not machine-based
	- ﻿﻿Addressing must then also be user-based
- ﻿﻿Much like computers use DNS to identify devices, email also relies heavily on DNS
- The address consists of a user and domain
	- ﻿﻿Example: ajhepler@weber.edu
	- ﻿﻿User names may contain some special characters
- ﻿﻿The weber.edu domain hosts a mail server to support @weber.edu addresses
- ﻿﻿What about studentname@mail.weber.edu?

#### Email Features:
---
- Address Books
	- Database of email address contacts
- Multiple Recipient Addressing
	- One message can be sent to multiple people (instead of a physical envelope per person)
- Mailing Lists
	- Large groups of users can be emailed by sending a message to a single address

#### Email Structure:
---
- ﻿﻿Emails have a header that contains message-specific details:
	- ﻿﻿Origination Date
	- ﻿﻿Originator Fields
	- ﻿﻿Destination address Fields
	- ﻿﻿Identification Fields
	- ﻿﻿Informational Fields
	- ﻿﻿Resent Fields
	- ﻿﻿Trace Fields
- ﻿﻿These fields can be viewed in most modern email systems (with a little investigation)

#### MIME:
---
- ﻿﻿Multipurpose Internet Mail Extensions
- ﻿﻿Early email consisted of text-only messages
- ﻿﻿As email has evolved, the need for more a more-enhanced option surfaced
- ﻿﻿MIME allows for graphics, videos, files, and other media to be included in messages
- ﻿﻿MIME information is included in email headers

#### MIME Headers:
---
- ﻿﻿MIME-Version
	- ﻿﻿Identifies message as MIME-encoded
	- ﻿﻿Indicates a version (1.0 currently)
- ﻿﻿Content-Type
	- ﻿﻿Describes the type(s) of data in the message
- ﻿﻿Content-Transfer-Encoding
	- ﻿﻿Specifies the type of encoding used (Non-ASCIl)
- ﻿﻿Content-ID
	- ﻿﻿Optional field to specify a MIME identification code
- ﻿﻿Content-Description
	- ﻿﻿Optional field to add a text description
- ﻿﻿Others

#### SMTP Overview:
---
- ﻿﻿Original email standards utilized existing protocols, piecing together a solution
- ﻿﻿SMTP transfers messages between email  
    servers
- ﻿﻿Early email transfers before DNS were sent via a process called relaying
	- ﻿SMTP routing information was included with the email address and specified a sequence of servers
- ﻿﻿Uses well-known port number 25 ==unsecured==

#### Email using DNS:
---
- ﻿﻿DNS servers added the functionality of a mail ==exchanger (MX)== record to map addresses
- ﻿﻿SMTP server can use an MX record to route email instead of hopping between servers
	- ﻿﻿This allows for a direct connection
	- ﻿﻿More secure than email relaying (spam)
- ﻿﻿SMTP traffic can be routed in the same way other IP packets are routed

![[Pasted image 20230731122010.png]]

![[Pasted image 20230731122034.png]]

#### Email Access and Retrieval Models:
---
- ﻿﻿Online Access Model
	- ﻿﻿All machines have constant access to mailboxes
- ﻿﻿Offline Access Model
	- ﻿﻿User establishes a connection to his or her mailbox and downloads messages to a device
	- ﻿﻿All activity can then be done offline
- ﻿﻿Disconnected Access Model
	- ﻿﻿Hybrid of Online and Offline
	- ﻿﻿User downloads messages to view later and any changes are synchronized when connectivity resumes

#### Post Office Protocol (POP/POP3)
- ﻿﻿Maps closest to the offline model of email access methods
- ﻿﻿Email is downloaded to a computer and deleted from the server
	- ﻿﻿Typically used with an email client instead of a web browser
- ﻿﻿Synchronization across devices becomes a challenge with POP
- ﻿﻿Uses well-known port number 110 ==Unsecured==

![[Pasted image 20230731123104.png]]

![[Pasted image 20230731123136.png]]

#### Internet Message Access Protocol (IMAP/IMAP4):
---
- ﻿﻿More robust protocol than POP3 which allows for a more enhanced command structure
- ﻿﻿Synchronizes mailboxes across devices for email consistency
- ﻿﻿Currently a preferred method over POP3 as more devices are constantly connected
- ﻿﻿Creates a better experience when mixing web-and software-based clients
- ﻿﻿Uses well-known port number 143 ==unsecured==

The process of an email server needing to map out the entire path of SMTP servers from source to destination is known as __________.
- ==Relaying==

