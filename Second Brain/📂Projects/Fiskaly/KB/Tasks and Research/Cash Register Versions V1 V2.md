
This one is a big one as this tasks is there to make the calls to V1 and V2 compatible. 

```
Create a script that alters all existing Cash Registers of an organization to match with the timestamps on SIGN DE
```

### Description

- Some customers used same `clientId` for V1 and V2 of SignDE.
- Problem is as soon as both of them are in use and were not updated in DSFinV-K accordingly
- there is a script `orderbird-move-revision.ts` takes inputs and creates new 0 revision for Cash Register that is linked to SIgnDe v2. 

Inputs: 
- client id
- tse-id
- datetime

### Goal 

- Go thru all client_ids of an org.
- if revision 0 is linked to SignDe v1 and last one is not cash register needs to be transformed
- if revision 0 is linked to Sign De v2 then this cas register needs to be transformed as well 

**Transformation**

- Read last transaction from SignDE v1 and first from SignDe v2 
	- if last transaction from SignDe v1 was created after the fist v2 this cas register cannot be tranformed. 
	- if Transaction of v2 comes after take that timestamp as the new time_update 
- orderbird-move-revision has all steps to move revision


### FAQ 

how can a client have more then one `client_id` ? 
why is the timestamp important? 



