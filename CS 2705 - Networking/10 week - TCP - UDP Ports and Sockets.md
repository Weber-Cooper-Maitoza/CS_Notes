
#### TCP and UDP Overview
- TCP and UDP are Transport layer protocols
- Work to address some shortcomings of IP 
	- connectionless, unreliable, and unacknowledged
- TCP is a connection-oriented protocol that allows simultaneous connections to a single IP 
	- Contains error correction and ==windowing==  
- UDP is connectionless like IP  
	- Does little more than add ports to transmissions

#### TCP and UDP Application  
- Software that requires reliable transport of information uses TCP  
	- Common protocols: HTTP, FTP, SMTP, SSL, etc  
- Software that does not require data to get there (then why send it??)  
	- Streaming/live broadcasts  
	- Common protocols: DNS, TFTP, SNMP, DHCP (Dynamic host protocol)
	- Many UDP protocols send short/small 
#### TCP and UDP Comparisons


![[Screenshot 2023-07-11 at 7.28.46 AM.png]]

## Connections:

- Utilize the client/server model of operation  
	- Client: requesting device  
	- Server: responding device  
- Uses asymmetric communication  
	- Source port and destination port usually different  
- Multiple application transmissions ==multiplexed== and ==demultiplexed== using a single IP address  
	- Use ports to share a an IP connection

![[Pasted image 20230711073432.png]]

![[Pasted image 20230711073534.png]]

#### Port Assignment
- Much like IP Addresses, many ports have been reserved for specific use:
	- Well-Known Ports: Port 0 - 1023
	- Registered Ports: Port 1024 - 49151
	- Private/Dynamic Ports: 49152 - 65535
- Static port assignment typically happens on a server device
- Dynamic port generation usually happens when a request is sent to a serving device

![[Pasted image 20230711074004.png]]

#### Sockets  
- Port numbers are indicated by a number following a colon of an address  
- ==The IP address and port used combine to make up a socket  ==
	- HTTP server socket: 137.190.8.10:==443==  
- Sockets are created on both the client and the server  
	- Client socket: 192.168.1.25:==2345==  
	- ==High port number on client==
	- Random port generated on the client side

![[Pasted image 20230711074521.png]]

#### NETSTAT In terminal
For mac-os use `netstat -nf inet`

####  UDP Characteristics
- unreliable protocol just like IP
	- Sometimes referred to as a wrapper protocol due to simply adding basic information to messages
- Sends data one-way with no persistent connection
- Provides an optional checksum and ICMP error reporting
- Beneficial for certain applications:
	- Exchanges that value performance over reliability
	- Short/small data exchanges

#### TCP Characteristics  
- Connection-oriented  
- Bidirectional connection establishment  
- Keeps track of data that has been sent and received (reliable)  
- Acknowledgement of transmissions  
- Stream-oriented so applications don’t have to divide data into chunks  
- Managed data flow to ensure smooth 

#### Data Packaging: Segments
- TCP process data streams from applications and divides the data int segments
- IP treats the segments as all other messages and transmits them to the destination
- ==Sequence numbers are added to keep track of the order of data==
> Because packets may not arrive in the exact order they were sent, TCP uses _____________ to reassemble submissions in the correct order.
> - **sequence numbers**
- The receiving device reassembles the packets back into a byte stream

![[Pasted image 20230711085005.png]]

#### Windowing and Acknowledgement
- Acknowledgements are used to verify successful receiving of data segments  
- Multiple bytes are sent, and the last segment received is acknowledged to the sender  
- TCP can gradually increase or decrease the number of bytes sent  
	- This is known as Windowing (or a sliding window)  
- If the window increases too much, acknowledgements go missing  
	- The window would then be lessened to accommodate

![[Pasted image 20230711090834.png]]

#### Three-way Handshake  
• When establishing a connection, TCP uses a three-way handshake process  
• SYN and ACK messages are used in this process  
	- SYN: Synchronize message  
	- ACK: Acknowledgement message  
• SYN, SYN+ACK, ACK process is on the next slide  
• After connections are complete, FIN messages are used to terminate connections

![[Pasted image 20230711091450.png]]