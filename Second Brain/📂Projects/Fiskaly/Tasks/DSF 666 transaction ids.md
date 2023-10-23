
[[Code onboarding]]

is kinda finished I have the project running. The current project works using the `docker-compose` present in the projects itself. 

I have now made some changes to the code and implemented the feature. 

- Working on it I discovered that there are a lot of Async things happening due to the MQTT. 
	- this async thingies are being used to insert things into the DB 
- making things challanging is that I have to figure out what is happening on the endpoint I'm working on and It should trigger an error. 

So the plan for now is this: 
	- Add the message 
	- Add the check 
	- Make the check trigger 
	- Think of a way to make this a bit more usable.. 

Currently I've got not context in using the trigger.. so I want to debug it somehow have yet to find a way to do that. 

So the messages in that are in the `Subscribers` are just sent to the DB and nowhere else. So my assumption was wrong. 

Now I have a clearer picture on what happens here. also the `reports` directory has a repository / interfaces and the "business logic" for the reports themselves. 

Finished new PR draft. Now I want to focus on the Debugger. 


