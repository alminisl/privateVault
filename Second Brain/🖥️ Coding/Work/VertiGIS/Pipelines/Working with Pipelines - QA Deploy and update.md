## Build pipelines

w-qas-client2 - q$client24qcheck
q$client24qcheck


On Premise installation for Designer 

goal: 

update.cmd 
	- Stop all services
	- Get new artifacts
	- Start all services


Working on the on prem installation and so far so good now I need to figure out some of the 

- The ideal usecase would be to have a script that would just update the onPrem installation. 

Feedback: 

> you can have an agent PUSH to the on prem server
there are a couple of ways to push
or you can have the on prem server subscribe to some feed about artifacts and PULL the latest artifact
generally PULL is more secure but is sometimes more complex
PUSH could be as simple as provide an SSH key to a CI server and have the CI server trigger after build to push the artifact and install it
I think in azure you would do a notification hub and have something on prem subscribed for notifications
(high level, i don't have experience with azure notification hub, only the AWS equivalent)

- Also found out about the `Releases` tab in the Pipelines
	- https://docs.microsoft.com/en-us/azure/devops/pipelines/release/deploy-pull-request-builds?view=azure-devops
	

## Research

>if you're using azure yaml pipelines then you want environments and add your machine as a resource (install az pipelines agent)

The current URL: https://vertigis.visualstudio.com/fe504507-9847-46cb-9eac-59eb5b821c9c/_apis/build/builds/40575/artifacts?artifactName=build&api-version=7.0&%24format=zip 

This one needs to be configured so that I can use `curl` and then get the `zip` file and essentially deployt it / unzip it somewhere. (The solution was that I needed the PAT)

PAT - is generated in MS Azure Devops, icon by the profile photo. 

### Research links
- Some information about the API URL https://developercommunity.visualstudio.com/t/download-url-of-artifact/394251 
- URL: https://docs.microsoft.com/en-us/rest/api/azure/devops/build/artifacts/get?view=azure-devops-rest-4.1
- PAT and how to use it with CURL: https://stackoverflow.com/questions/62563443/cannot-access-azure-devops-api-using-pat-in-curl-command-in-bash-script

### Success

Get the latest build folder and data
```bash
 curl -u :toia27lri3jiwq37it2wykk3yzxm6gvrulmjsb7ma25pyrdbd3gq "https://vertigis.visualstudio.com/fe504507-9847-46cb-9eac-59eb5b821c9c/_apis/build/builds/40575/artifacts?artifactName=build&api-version=7.0&%24format=zip" -o build.zip
```

Get the latest build Id 
```bash
https://vertigis.visualstudio.com/fe504507-9847-46cb-9eac-59eb5b821c9c/_apis/build/latest/133?branchName=main&api-version=6.0-preview.1
```


# Working powershell script

```bash
$PAT = 'toia27lri3jiwq37it2wykk3yzxm6gvrulmjsb7ma25pyrdbd3gq'
$B64Pat = [Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes("`:$PAT"))
$currDir = Get-Location

$headers = @{
  Authorization = 'Basic ' + $B64Pat
}

# get the latest designer build ID 
$designerResult = Invoke-RestMethod -Method GET -Headers $headers -ContentType "application/json" -Uri "https://vertigis.visualstudio.com/fe504507-9847-46cb-9eac-59eb5b821c9c/_apis/build/latest/133?branchName=main&api-version=6.0-preview.1"

# get the latest engine build id
$engineResult = Invoke-RestMethod -Method GET -Headers $headers -ContentType "application/json" -Uri "https://vertigis.visualstudio.com/fe504507-9847-46cb-9eac-59eb5b821c9c/_apis/build/latest/182?branchName=main&api-version=6.0-preview.1"

echo $designerResult.id
echo $engineResult.id

$designerUri =  "https://vertigis.visualstudio.com/fe504507-9847-46cb-9eac-59eb5b821c9c/_apis/build/builds/" + $designerResult.id + "/artifacts?artifactName=build&api-version=7.0&%24format=zip"
$engineUri = "https://dev.azure.com/vertigis/fe504507-9847-46cb-9eac-59eb5b821c9c/_apis/build/builds/" + $engineResult.id + "/artifacts?artifactName=fts-modules&api-version=7.0&%24format=zip"

echo $designerUri
echo $engineUrl

# 1. DOWNLOAD THE BUILDS

# download the build for designer
$buildDesigner = Invoke-RestMethod -Method GET -Headers $headers -ContentType "application/json" -Uri $designerUri -o designerbuild.zip

# download the build for the engine
$buildEngine = Invoke-RestMethod -Method GET -Headers $headers -ContentType "application/json" -Uri $engineUri -o enginebuild.zip

# 2. UNZIP THE BUILDS

# unzip the designer build
Expand-Archive -Path designerbuild.zip -DestinationPath ./designerbuild -Force
# unzip the engine build
Expand-Archive -Path enginebuild.zip -DestinationPath ./enginebuild -Force

# 3. DELETE THE CURRENT FILES

# Delete the current content of webapp folder in Designer
Get-ChildItem -Path $currDir/Designer/webapp -Directory | Remove-Item -Recurse

# Delete the current content of the Engine fts-modules folder
Get-ChildItem -Path $currDir/Engine/bin/fts-modules -Exclude ".env" -Recurse -Force | ForEach  { $_.Delete()}

# 4. COPY THE NEW FILES

# Copy the content of build folder to webapp folder in Designer
Get-ChildItem -Path $currDir/designerbuild/* -Recurse | Move-Item -Destination $currDir/Designer/webapp

# Copy the contet of enginebuild folder to fts-modules folder in Engine
Get-ChildItem -Path $currDir/enginebuild/* -Recurse | Move-Item -Destination $currDir/Engine/bin/fts-modules

# 5. CLEANUP

# Cleanup of the build.zip and build folder
Remove-Item -LiteralPath $currDir/designerbuild -Force -Recurse
Remove-Item -LiteralPath $currDir/enginebuild -Force -Recurse
Get-ChildItem -Path $currDir -Filter '*.zip' | Remove-Item

```

# Adding Engine

To the above script I still have to add the Engine stuff however I have to check if the same build id is being used. 

Engine URL to get the latest IDs:  "https://vertigis.visualstudio.com/fe504507-9847-46cb-9eac-59eb5b821c9c/_apis/build/latest/182?branchName=main&api-version=6.0-preview.1"
`"https://vertigis.visualstudio.com/fe504507-9847-46cb-9eac-59eb5b821c9c/_apis/build/latest/182?branchName=main&api-version=6.0-preview.1"`



# Testing 

- Try to test it on different locations on disk if everything works fine. 


# For future reference

```bash
Get-ChildItem -Path $currDir/Designer/webapp -Include *.* -Recurse -Force | ForEach  { $_.Delete()}
 Get-ChildItem  $currDir/Designer/webapp  -Recurse | Remove-Item -Force -Recurse
 (Get-ChildItem $currDir/Designer/webapp -Recurse -Force ).Delete()
```
