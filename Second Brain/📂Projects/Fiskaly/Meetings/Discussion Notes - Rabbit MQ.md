
![[Pasted image 20230712133638.png]]

- nameless exchange - routing keys = que name 

**Exchange**

- Exchange type specifices Routing rules and attributes
- acting as adresses
- Bindings

Direct Exchange 
Route Exchange 
 - Routing key taxi.eco.large
Topic Exchange 


https://www.mailerq.com/blog/disable-consumer-timeouts-in-rabbitmq-3-8-15-and-higher 

https://www.rabbitmq.com/reliability.html

### Motive
- Large exports, take a lot of time 
- How many consumers? 
	- Consumer goes down if the timeout is reached
	- 10 replicas for for export queues
- Current exports crash when updating

### Goals
- Before we start 
	- Get beefy exports 
	- Get to know the Exports and how much they are 

- Goals
	- handling exports 
	- better tracking/monitoring

- Approaches
	- Increase the timeout
	- Early ACK
		- would cause the consumer to process multiple messages at the same time
		- concert consumer to async funcs
		- Early Ack 2 - adds redis and a middlewear.. 
		- event emitter
			- Emitting events - Observer that handles the events for the exports
		- Set timeout that acts like an alaram
		- Batching - Multiple batches of exports

### What todo 
-  

### Approaches

### QA 
- Radical question - rewrite in another language? 
