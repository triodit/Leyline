Project Leyline
Lora based system for long range communication using a mesh protocol for multi hop communication.
All non-volatile memory usage shall be done in a way that minimizes write events.
Requirements
1.	Small low power radio nodes capable of acting as gateways or as relays
a.	Raspberry Pi Zero, LilyGo TTGO LoRa esp32, or knockoff adafruit LoRa Feather board.
2.	A method of identifying each node
a.	Node ID uint16_t / unsigned short 0 – 65535
b.	Node 0-9 reserved for Admin Use
3.	A method of allowing nodes to identify and rank neighbors
a.	Ping and see who responds
i.	Ping and response should call RSSI
ii.	Responses need to be staggered randomly, or perhaps based on node ID Or based on RX RSSI
iii.	Routing nodes should store data on other routing nodes locally in non-volatile memory.
iv.	Client Nodes should ID the best entry node in volatile memory and there after use that node directly
b.	What do we do if two neighbors are at risk of swapping ranks?  Should we check for that?
i.	Before storing new values check if any two nodes are with in 10% of each other and if they are and they will swap store a volatile counter If that counter gets above say 4-5 ticks without resetting then store a value swap.
4.	A method for allowing nodes to update their neighbors rank and ID
a.	A timer that runs very infrequently that repeats the ping and check the 
5.	A method for new nodes to be added
a.	A broadcast to all nodes in range asking for an ID 
i.	All receiving units take an RSSI of the contacting node and use that to determine response delay
6.	A method for planning connection routes
a.	Routing Nodes should use Flash/EEPROM to remember a list of preferred paths between routing nodes
b.	When a message goes from an access node to a routing node it should be tagged with the ID of the routing node that the message is directed to by the accessing node
c.	If message is a reply,it shall be tagged with both its senders routing entry node and the destinations routing entry node.
d.	All messages their after in this like shall include both end routing nodes.
7.	A fault detection system
a.	Admin Server running on a raspberry pi that logs things like power lose
i.	Nodes should send statues messages to ID 0-9 addresses
ii.	Nodes should use non-volatile memory to track if an admin address is in use.
8.	Security
a.	Special firmware for routing nodes that include password locked/encrypted commands
b.	Ability to use nonvolatile memory to black hole a particular ID’s traffic
c.	Ability to change networks encryption key
d.	Access node to routing node key different from inter routing if possible

