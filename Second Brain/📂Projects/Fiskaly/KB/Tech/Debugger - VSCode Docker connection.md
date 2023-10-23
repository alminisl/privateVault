
Figure out if its possible to run the consumers using the debugger.. 

Ask maybe chatGPT? 

Not sure why the consumers won't start and run the debugger for me. For now I want to google that. 


I also have to think about a better way to write my daily notes. 
Currently working with obsidian like this is kinda weird, I will probably have to watch people do it makes it a bit more understandable. 


Current debugger config: 

```json
{

"name": "Docker: Attach to App",

"type": "node",

"request": "attach",

"port": 9229,

"address": "localhost",

"localRoot": "${workspaceFolder}",

"remoteRoot": "/app",

"protocol": "inspector"

},

{

"name": "Start Closing Prep Consumer",

"type": "node",

"request": "launch",

"runtimeExecutable": "${workspaceFolder}/node_modules/.bin/ts-node-dev",

"runtimeArgs": [

"--inspect=9239",

"--respawn",

"${workspaceFolder}/src/consumers/closings/closingPrep"

],

"internalConsoleOptions": "openOnSessionStart",

"sourceMaps": true,

"protocol": "inspector"

}
```


Currently what I'm thinking about is to make this process more streamlined. I want to make the debugging process a little bit more easy.

### Current implementation 

- I change the dockerfile and I change the launch.json
- Then I restart and then the debugger is running

This is bad as it involves a lot of manual steps to make it work 


### Possible solutions to this 


- Expose all ports
- Make a dockerfile improvement

For simplicities sake I will add debug ports for every service: 
![[Pasted image 20230714104249.png]] 

For these I will then create launch.json files and see what happens. 

### Results 

- Currently not all are working.. investigatingh


### Webstorm 

Works as easy as adding the configurations. Is it possible to share those in the repo? 