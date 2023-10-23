#brainstorm

#todo: Move to separate note  
## Meeting brainstorm ideas 

- Upsert CR
	- Quiet complicated to pick a version of signDE. 
	- they dont upsert when they NEED to upsert 
	- manipulating cash register to fix stuff - baad 
	- Upserting might not work in edge cases 

- Insert cpc 
	- Not knowing what the issue with the timeouts is 
		- http timeouts 
		- rabbitMQ timeouts?
		- assumption - why do we have timeouts?
	- validating data - transactions - is the transaction there or not 
		- later we query data requesting the smae information not validating
	- Does not prepare data for exports

- Exports 
	- untgles data 
		- slow queries
	- takes a long time to connect to SignDe 
		- check if this has big perf impacts
	- Redundant checks
	- IO issues 
		- Memory mounting - io improvements?
#### Solutions
- Cash register
	- Must have a valid state, revision should have all the info we need 
		- if its linked to signDE v1 - v2
		- separating the cash registers? 
		- revision we can connect to different clients v1 and v2 
	- Cash Register - Does he have clients in 2 versions? 
	- define time_creation + time_update of the revision
	- if last revision is connected to SignDe v2 no check against v1

- Find solution to profile in production or track some functions which are executing
	- Improve the tracing and what happens

- PostCPC 
	- solution to exports