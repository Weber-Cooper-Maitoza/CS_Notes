### Uniform Resource Identifiers (URIs):
---
- General purpose way to refer to many kinds of tcp/ip resources.
- Divided into two categories:
	- ==Uniform Resource Locators (**URLs**)== - refers to a resource thought combination of protocol mechanism and resource location.
	- Uniform Resource Names (**URNs**) - uniquely names a resource without specifying an access protocol or mechanism.
- URNs typical focus on identifying a resource 
- URLs focus on how to access a resource

![[Pasted image 20230724165618.png]]

![[Pasted image 20230724165745.png]]

==Use : after a domain name to specify the port used==

## File Transfer Protocol:
---
- File transfer protocols copy files from one computer to another
- Generally FTP transfers files paying little attention to the file contents
- Another protocol based on the client/server model
- FTP operates with the server-FTP process and the user-FTP process

#### FTP Connections:
- FTP uses a control connection and a data connection
	- Control connection: main logical TCP connection that is created and established throughout the FTP session
	- Data connection: distinct FTP connection is established when data is transferred between devices
- Separating types of traffic allows for flexibility with the protocol, but adds complexity

![[Pasted image 20230724174425.png]]

#### FTP Connection Management:
- The FTP standard specifies two ways to create ftp connections: Active and Passive
- ==Active== connections:
	- Referred to as a *normal* connection
	- The server initiates a data channel connection with the client
- ==Passive== connections:
	- Client tells the server to accept a data connection initiated by the client
	- Server provides an IP and port for the client to use

#### FTP Transmission Modes:
- Stream Mode
	- Data is sent as a continuous stream of unstructured bytes (TCP manages structure)
	- Most common and easiest to implement
- Block Mode
	- Data split into blocks and encapsulated into FTP  records with three-bytes header
- Compressed Mode 
	- Uses run-length encoding to compress information
	- May be redundant due to other TCP compression options

#### FTP Commands:
- Access Control Commands
	- Used as part of the user login and authentication process
- Transfer Parameter Commands
	- Specify parameters for how data transfers should occur (Data type, passive, active, etc)
- FTP Service Commands
	- File operations such as sending, receiving, renaming, deleting, etc
- Full list of commands can be found in Chapter 72

## World Wide Web(www) / HyperText Transfer Protocol (HTTP)
---

#### Components of the web:
- Hypertext Markup Language (HTML)
	- Used to define hypertext documents using *tags*
- Hypertext Transfer Protocol (HTTP)
	- TCP/IP application layer protocol that implements HTML documents and other files
- Uniform Resource Identifiers
	- Used to define labels that identify resources
	- Not specific to the web

![[Pasted image 20230724181326.png]]

#### Web Servers and Web Browsers
- Web servers run special software used to provide documents and files to clients
	- Common servers: Apache, Microsoft IIs, Nginx, many others
- Web browsers allows users to access web documents on web servers

- Servers and browsers are continually evolving to add more conveniences and functionality

#### HTTP Communication
- HTTP communication usually happens via the client/server model
- Clients send HTTP request message to the HTTP server to request various information
- Servers respond to the requests with *HTTP Response* messages
- Messages can be configured in various ways to control how information is transferred

#### HTTP Methods
- GET
	- Requests that the server retrieve a specified resource
- HEAD
	- Identical to GET, but does not request the message body
- Post
	- Allows client to send data to the server for processing
- OPTIONS
	- Allows client to request communication options
- PUT
	- Requests that the server store requested information
- Others

![[Pasted image 20230724195755.png]]

![[Pasted image 20230724195826.png]]

![[Pasted image 20230724195916.png]]

