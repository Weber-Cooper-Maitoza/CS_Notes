#### The Need for Network Security:
---
- ﻿﻿Most protocols in the TCP/IP stack were not built with security as a high priority
- ﻿﻿Widespread adoption at an accelerated rate put many devices in many different places
- ﻿﻿With more people involved in design and development, flaws are inevitable
- ﻿﻿As data has become more valuable, the likelihood for theft has also increased

#### Hackers/Hacking:
---
- ﻿﻿The term hacker did not always come with a negative connotation
- ﻿﻿A hacker would modify a technology to do something it was not designed for
	- ﻿﻿An example would be to enhance functionality
- ﻿﻿Some early hackers did not always have good intentions
- ﻿﻿A few of these hackers were arrested in high-profile stories and litigation

## Different Types of Attacks:
---
- Spoofing
	- "*The act of masking who you are and pretending to be someone else*"
- Man-in-the-Middle
	- "*Put a device in-between a valid connection to listen in*"
	- ARP Cache Poisoning
	- Wireless Access Points
- Denial of Service
	- "*Group of people deny service to a group or server*"
- Brute Force
	- "*Tries every possible outcome to unlock passwords*"
- Malware
	- "*Malintent software*"
- Zero-Day Exploits
- Social Engineering
	- "*Trying to take advantage of the "human" aspect of technology*"

#### Spoofing:
---
- ﻿﻿Pretending to be something or someone you are not
- ﻿﻿MAC addresses and IP addresses can be spoofed to manipulate network devices
	- ﻿﻿MAC filtering on routers
- ﻿﻿Email addresses can be spoofed so that the sender appears to be legitimate
- ﻿﻿Web pages can also be spoofed to appear to be legitimate

#### Man-in-the-Middle:
---
![[Pasted image 20230807115929.png]]

#### Denial of Service (DOS):
---
- ﻿﻿Disrupts access to network devices or services
	- ﻿﻿This can be intentional or unintentional
- ﻿﻿This type of attack is often-used to prevent access to certain web sites
- ﻿﻿Several separate devices are sometimes configured to participate in the same attack
	- ﻿﻿Distributed Denial of Service (DDoS)
- ﻿﻿DoS attacks can be physical or digital

![[Pasted image 20230807120500.png]]

#### Brute Force:
---
- ﻿﻿Uses every possible combination of data in an attempt to gain access
- ﻿﻿Several thousand attempts per second (or more) may be achieved
	- ﻿﻿Failed login thresholds combat this problem
- ﻿﻿Not all attacks happen on live devices
- ﻿﻿Brute force attacks can happen on storage drives, files, packet captures, and more

#### Malware:
---
- ﻿﻿Any type of software designed with malicious or destructive intent
- ﻿﻿Comes in the form of phishing emails, bad links, phony sites, and more
- ﻿﻿Can be introduced intentionally or unintentionally
- ﻿﻿Viruses, worms, Trojan horses, and rootkits are all types of malware

- ﻿﻿Virus
	- ﻿﻿Malicious code included with a program that infects and replicates to other files and hardware
- ﻿﻿Trojan Horse
	- ﻿﻿Software that may perform a certain function, but has another hidden, damaging function
- ﻿﻿Worm
	- ﻿﻿Code designed to replicate through a network
- ﻿﻿Rootkit
	- ﻿﻿Code that uses low-level operating system functions to hide itself from detection

#### Zero-Day Exploits:
---
- ﻿﻿Type of exploit that takes advantage of unpatched software
- ﻿﻿Unidentified vulnerabilities in software can be shared with other malicious hackers
- ﻿﻿Several recent cybersecurity incidents involve unpatched exploits
- ﻿﻿Some vulnerabilities are reported to vendors
- Others may be held ransom and/or sold online

#### Social Engineering:
---
- ﻿﻿Most effective type of network attack
- ﻿﻿Takes advantage of the human element involved in a digital ecosystem
- ﻿﻿Common Social Engineering tactics
	- ﻿﻿Phishing: attempting to trick a user into providing sensitive information  
	- Physical: attempting to gain access via physical means (documents, key codes, ID badges, etc)
- ﻿﻿Dedicated attackers may use many methods over a long time period to achieve the desired access

## Encryption:
---
- ﻿﻿Many devices and technologies make use of encryption to secure connections
	- ﻿﻿Scrambles data making it unreadable to unauthorized users
- ﻿﻿Encryption happens with protocols, devices, files, and connections
- ﻿﻿Some types of encryption can happen with passwords, or special files called certificates
- ﻿﻿PKI - Public Key Infrastructure
	- ﻿﻿Establishes private and public key pairs to verify the identity of users and devices

#### Securing Protocols:
---
Many early protocols now have secure options
- ﻿﻿HTTP -> HTTPS
	- ﻿﻿Uses Secure Sockets Layer (SSL) encryption
- ﻿﻿FTP -> SFTP or FTPS
	- ﻿﻿SFTP uses the Secure Shell (SSH) protocol
	- ﻿﻿FTPS uses SSL
- ﻿﻿IMAP/POP3/SMTP
	- ﻿﻿Uses SSL or Transport Layer Security (TLS) encryption
- ﻿﻿Telnet -> SSH
	- ﻿﻿Try to not use telnet. Ever.

## Securing Remote Access:
---
- ﻿﻿Local networks can be extended virtually anywhere in the world
- ﻿﻿Secure access to networks takes place using Virtual Private Networks (VPNs)
- ﻿﻿A VPN connection creates a tunnel from an end device to a network using the Internet
- ﻿﻿Multiple encryption algorithms can be used to secure the communication channel

#### Protecting Networks:
---
- ﻿﻿An effective cybersecurity plan includes a layered approach (defense in depth)
- ﻿﻿Firewalls can help prevent unauthorized users from accessing a network
- ﻿﻿Content filters can prevent unwanted files from entering the network
- ﻿﻿Policies and procedures can help reduce the number of threats introduced into a network
- ﻿﻿End-user education can help prevent social engineering and other types of attacks

## Future of Networking and Security:
---
- ﻿﻿A vast number of devices are being developed as Internet-enabled
- ﻿﻿More technology developed by humans will lead to more possible vulnerabilities
	- ﻿﻿Internet of Things
- ﻿﻿Practicing secure coding habits can minimize the likelihood of software being exploited
- ﻿﻿Share knowledge of best-practices to prevent intrusions or virus infections
- ﻿﻿Keep security in mind in your day-to-day use of network-enabled devices