## Desired Features:
- Adapt to Failure
- Performance
- Security
- Communication

## Packet communication issues
- lost
- corrupted
- did not reach destination

![[Pasted image 20240410085434.png]]
- the ==sender sends a message== to the receiver;  
- the receiver ==then sends a short message back== to acknowledge its receipt--- acknowledgement  
- If, in that time, no acknowledgment has been received, the sender concludes that the message has been lost. The sender then simply performs a ==retry of the send==, sending the same message again with hopes that this time, it will get through

## Need to build reliable comm layers
![[Pasted image 20240410085940.png]]
- Acknowledgement may get lost  
- Avoid duplicate reception  
	• ensure that each message is received exactly once by the receiver  
	• Ignore the message if already received

- myriad ways to detect duplicate messages  
	• For example:  
		• the sender could generate a unique ID for each message

==distributed shared memory (DSM)== systems enable processes on different machines to share a large, virtual address space