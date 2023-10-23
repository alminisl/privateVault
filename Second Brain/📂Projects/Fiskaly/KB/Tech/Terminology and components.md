
Goal of this document should be the understanding and collection of information about the Terminology and the use cases of the 


### TSS 

**Technical Security System**

TSS is indentified by a tss_id. 
`tss_id` is UUIDv4 standard comlient. 
creating a new TSS state is set to `"CREATED"` - Response will have a PUK. Store that. 
Admin will need the PUK to set the ADMIN PIN. 

### Client 

Creating a client and associating it with a TSS. (`api/v2/tss/tss_id/client/client_id`)

Default state is set to `"REGISTERED"` Only client in this state can use the TSS. 

`client_id` must be generated UUIDv4. 

Only one `client_id` for one T`SS. 

### Cash register 

Cash register is characterized by the ability to both electronically accept incoming orders and to complete the payment process electornically.

There is also the Master-Slave arhcitecture where we can have a master Cash Register and then slaves to it. 

### Cash Point Closing 

Cash closing 

