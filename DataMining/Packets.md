# Packet Sniffing & Diablos Network Protocols
Personally I have not delved far into Diablo's Packets and Network Protocols, but I will share what little I do know here. There is also information I'll share pertaining to vanilla D3 because I'd imagine it's largly the same for ROS aswell (though I will strictly note this when I do). And if not, will atleast help push some understanding into how blizzard does things. I will update this if I ever delve farther into it, or if any of you have a greater knowledge of this topic and wish to contribute then please, be my guest.

# Proto Buffers
Blizzard uses Protocol Buffers in its networking code. Protocol Buffers are a way of encoding structured data in an efficient yet extensible format.  
[Read more here...](https://github.com/protocolbuffers/protobuf)

# RPC
Blizzard is using a deprecated RPC implementation that comes with protobuf 2.3. It works like this: there are services provided on both sides of the connection; packets are wrapped by the RPC headers, and there is a basic service attached when the connection starts (connection.proto, which id is 0). The client will ask the server to attach more services using the BindRequest imported_hash and will tell the server that it attached service providers using BindRequest exported_entry (hash and id) so that the server can make requests like LoadModuleRequest to the client. 

### RPC Header

Main header:
```
uint8 service
varint32 method
uint16 requestid
varint64 unknown
varint32 datasize
```
If the service byte is 0xFE (constant RPC call response), the unknown field is not present:
```
uint8 service
varint32 method
uint16 requestid
varint32 datasize
```
The rest of the packet should be at least equal to datasize. Note that messages can be chained in a single packet.


# Packet Details
_(Diablo 3, likely similar for ROS)_  

### Login communication
```
>>> ConnectRequest
<<< ConnectResponse
>>> BindRequest
<<< BindResponse
>>> BindRequest
<<< BindResponse
>>> LogonRequest 
```

### Client->Server packet header 
```c
uint8 service;
varint32 method;
uint16 requestid; // incremental
varint64 unknown;
varint32 datasize;
```

### Service IDs 
* The client does a BindRequest with information (hashes) about a specific service, and then the server returns a BindResponse with an SID.
* These SIDs are later used by the client to communicate with the different services.
* 0x00 is the base service. It does not require binding. 

### Example Packet Logs
[Pastebin](http://web.archive.org/web/20120508130803/http://pastebin.com/18j2mGsx)

# Sources
Credit for a a good majority of this page goes out to a priject that sadly no longer exists. However can still be seen here:  
[WayBack: diablo3dev.com/](http://web.archive.org/web/20120403094443/http://diablo3dev.com/w/Main_Page)
