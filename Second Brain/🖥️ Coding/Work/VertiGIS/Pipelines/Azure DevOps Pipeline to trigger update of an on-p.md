https://dev.azure.com/vertigis/Studio/_workitems/edit/190134


# Write down pipelines and how to use them

as Ivan mentioned we have somewhere an example of how to use pipelines 

### First step Adding new Agent

First thing I need to do is add a new agent to the pool which will be my pc in this case. 

**Project Settings > Agent Pool > Select Pool > New Agent**

- After creating the agent pool we have to create the Pipeline
- currently the pipeline i Create is in the Repository and separate branch
- Then we go to the **pipelines** > **new pipeline** 
	- Then we go thru the wizard and select our new pipeline
- Making these changes so far is the must do 

Some changes made today is that I made it so that I can "select" from a radiobutton list values that I want to use. 


Updated pipeline: 

```yml
# --------------------------------------------------------------------------------
# Update the local installation of Engine and Designer
# --------------------------------------------------------------------------------

parameters:
  - name: buildDirectory
    displayName: On-Premise Installation
    type: string
    default: "C:\\VertiGIS Studio Search DVD"
  - name: agentHost
    displayName: Agent Host
    values: 
    - W-WS-ISLAMOVIC
    - W-WS-BARICIC
    - Test

variables:
  buildDir: ${{ parameters.buildDirectory }}
  agentHost: ${{ parameters.agentHost }}

pool:
  name: Vienna Win
  demands:
    - Agent.Name -equals $(agentHost)
steps:
  - task: BatchScript@1
    displayName: Run Update Batch Script
    inputs:
      filename: $(buildDir)\\update.cmd
      workingFolder: $(buildDir)

```



