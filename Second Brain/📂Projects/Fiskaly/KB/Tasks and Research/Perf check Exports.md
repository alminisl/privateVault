
![[Pasted image 20230907162720.png]]
![[Pasted image 20230907162916.png]]

## Performance testing
### Steps made: 

- Create a MasterCashRegister and then create a CPC 
- If you check in the codebase, upsertCashREgister use case test, I created something like that. 
- https://dsfinvk.fiskaly.dev/api/v1/_docs/#operation/upsertCashRegister 
- console.profile()/console.profileEnd()
- Tested with the External Cash Register works like a charm! 


Done some flame graphs and investigation on the performance of our [[Export consumer]]. 

The conclusion is that currently - Using a external cash register shows us that there is a IO issue with the `highland` package and our IO takes a long time. However, this does not seem to be the biggest issue. 

#### TODO: 
I need to run a new performance test however this one with a REAL cash register connected to signDE.

### Conclusion

The performance impact could be ignored if we fix the Requests that are going to SignDe. The SignDe is going to be the biggest issue however the PostCPC should maybe fix it. 

Todo: Update this after we have a POC of the postCPC