-------
#### IPv6 Addressing:

- 128-bit addresses displayed in hextets, hex octets, or words
- no classful boundaries
- reserved/ Special Addresses:
	- Reserved addresses have 0s as the first 8 bits 00::
	- :: Unspecified address
	- ::1 Local loopack address
- Link-Local and Site-Local are private addresses
	- Link-Local: FE8, FE9, FEA, FEB 
	- Site-Local: FEC,FED,FEE,FEF
- Multicast Address:
	- starts with FF::

#### IPv6 Address Types and Terms:

- Unicast Address
	- Send traffic to a single device
- Multicast Address
	- Send traffic to multiple devices
- Anycast Address
	- Send traffic to any one device in a group
- Broadcast removed from IPv6
- EUI-64
	- Incorporates MAC address into IPv6 Address
	- (Insert FFFE in between MAC Address)

```
[6E-18-BC-E9-E9-D7]

first 24 bits: 6E-18-BC
last 24 bits: E9-E9-D7

fit FF-FE inbetween first and last 24 bits:
[6E18:BCFF:FEE9:E9D7]

Change the 7th bit *6E*:
0110 1100
6C

Final:
[6C18:BCFF:FEE9:E9D7]
```

#### IPv4 Subnetting:

- Subnetting breaks bigger networks into smaller networks
- More networks results in fewer hosts per network
- Finding network information can e done using the number of network or host bits
- 2<sup>n</sup> - 2 is used for hosts, 2<sup>n</sup> for networks
- Network ID, first host, last host, and broadcast address exist for each subnet

- Subnet masks can be expressed in prefix form
	- Slash notation or CIDR notation
	- Classful subnet mask prefixes: /8, /16, /24
- Prefix represents the number of network bits in a subnet mask (consecutive 1s in a subnet mask)
	- Host bits can be calculated by subtracting the prefix length from 32 (32 - "/24" = 8 host bits )
	- Classless Inter-Domain Routing (CIDR)
		- Allows for subnet masks to deviate from a classful subnet mask
		- Example classless prefixes: /12, /21, /27, etc...

#### ARP:

- Address Resolution Protocol
- Used to map physical addresses to logical addresses
- If a physical address for a device is unknown, an ARP request is sent
	- May be sent to FF-FF-FF-FF-FF-FF (broadcast)
- Address mappings are stored in a ARP cache or ARP table
- Dynamic entries should be refreshed on a regular basis

#### RARP:

- Reverse Address Resolution Protocol
- Used when a device needs to know an IP address and has a MAC address
	- Some devices my not immediately know their own IP address
- Messages are formatted the same, but the operation is preformed in the opposite
- Has been largely replaced by DHCP

#### IPv4 Packets:

IPv4 Packets contain many fields:
- Time-to-live (TTL)
- Type of service (TOS)
- Protocol
- Source and Destination Address
- Options
- Others
Time to Live decrements by one as it hops through routers
- prevents endless propagation of traffic (routing loops)

#### Packet Transmission:

Layer 2 devices use a Maximum Transmission Unit (MTU) to determine maximum size
- Common ethernet MTU: 1,500 bytes
- MTU may be different based on protocol in use
Frames that exceed the maximum size are fragmented
Receiving device reassembles the transmission in the proper order

#### Routing:

Any traffic not destined for the local network is sent to a router (Default Gateway).
Routers use routing protocols to learn routes to different networks.
Routing tables are used to store locations of remote networks.
Several small networks can be summarized with supernetting/route aggregation.

#### NAT:

Network Address Translation

Different NAT Types:
- Static NAT: One-to-one mapping of an outside IP to an inside IP
- Dynamic NAT: Shared use of one or more IP addresses (usually a pool)
- NAT Overload/ PAT: Uses source and destination ports to share use of IP addresses

One of the main reasons IPv4 is still in use