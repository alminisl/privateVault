
```toc
```


## 5.6.3 Root Provisioning (RP)

### UseCase RP-01 Root Crypto Installation at SpaaK Module Plant

**Descriptions**

The following root certificates shall be installed in the ECU

1.  OEM CA Root Certificate [J]
2.  OEM Sub-CA Root Certificate [J1]
3.  OEM CA Root Physical Key Certificate [J_PhysicalKey]
4.  STLA-specific Vehicle OEM Server intermediate CA Certificate [Z1]
5.  STLA-specific KTS server signing certificate [ZZ2] 


**Post Conditions**
• Vehicle contains Root certificates 

### Use case RP-02 Stellantis ECU Identity Certificate Signing Request (at supplier plant)

**Description**

To secure the communication between Backend and vehicle (Z certificate definition), Stellantis relies on mutual authentication and requires a so called “ECU identity certificate” which is different from the CCC vehicle identity certificate. SpaaK Module is required to have an ECU identity key pair.

This use case describes the first of two parts of ECU identity provisioning, that is submitting the ECU identity certificate signing request (CSR) from supplier plant to Stellantis backend.

**Actions**
At SpaaK Module supplier plant
1.  SpaaK Module generates ECU Identity Key Pair
2.  SpaaK Module submits signing request for ECU identity Public Key (CSR)
	a. CSR includes the SpaaK Module serial number as common name. 
3.  ECU supplier plant End of Line tester sends CSR to Stellantis PKI backend
	a. This step can be a batch process (to send multiple modules CSRs at once).

**Post conditions**
• CSR submitted to Stellantis backend 

**Our conclusion:
- These are the Z certificates? (Z1, ZZ2)

## 5.6.4 Pairing Preparation (PP) 

### UseCase PP-01 New Vehicle Identity Provisioning

**Descrption**

In preparation for a new owner pairing, a new vehicle identity must be stored in the vehicle.
-   The vehicle identity consists of the vehicle’s long term key pair  (Private and Public) The public key is certified by the backend and shall include the vehicle ID in the certificate subject name. It needs to be provisioned prior to owner pairing.
-   Vehicle identity shall be changed at every owner change.

##### Actions

Once SpaaK module receives a cyclic CAN message from TBM, indicating the TBM is connected to GSDP, and subscribed in the SpaaK topic

1. SpaaK Module shall verify drmUUID availability  
If drmUUID not available, SpaaK Module shall trigger Remote Service Provisioning (triggered by SpaaK Module) (SP-02), refer to chapter 5.6.12.2. use case SP-02 is performd successfully, SpaaK Module shall continue with the following steps.
2. SpaaK Module verifies the availablity of the Vehicle Identity Certificate
If Vehicle Identity Certificate is not available, SpaaK shall perform the following steps. If Vehicle Identity Certificate is available, SpaaK Module shall not perform the following steps
3. SpaaK Module request Vehicle Identity certificate subject ID (name it VehicleSubjectIdRequest) from Vehicle OEM Server
SpaaK >> SGW >> TBM >> GSDP : VehicleSubjectIdRequest VehicleSubjectIdRequest = SpaakRequest
4. Vehicle OEM Server receives and verifies VehicleSubjectIdRequest
If VehicleSubjectIdRequest verification is successful
5.  Vehicle OEM Server generates Vehicle Identity subject ID (as per CCC
    subject ID definition)
6.  Vehicle OEM Server pushes Vehicle Identity subject ID (name it
    VehicleSubjectIdResponse) to vehicle

GSDP >> TBM >> SGW >> SpaaK: VehicleSubjectIdResponse VehicleSubjectIdResponse = SubjectID || SpaakResponse
7. SpaaK Module receives and verifies VehicleSubjectIdResponse
If VehicleSubjectIdResponse verification is successful
8.  SpaaK Module generates Vehicle Identity key pair
9.  SpaaK Module generates Vehicle Identity CSR
10. SpaaK Module sends Vehicle Identity CSR to Vehicle OEM Server
SpaaK >> SGW >> TBM >> Vehicle OEM Server: VehicleIdentityCSRRequest VehicleIdentityCSRRequest = CSR_file || SpaakRequest
11. Vehicle OEM Server receives and verifies VehicleIdentityCSRRequest

If VehicleIdentityCSRRequest verification is successful

12.  Vehicle OEM Server signs Vehicle Identity CSR
13.  Vehicle OEM Server pushes the Vehicle Identity certificate (i.e. [K]) to the
    vehicle
GSDP >> TBM >> SGW >> SpaaK: VehicleIdentityCSRResponse VehicleIdentityCSRResponse = Certificate || SpaakResponse

14. SpaaK Module receives and verifies VehicleIdentityCSRResponse

If VehicleIdentityCSRResponse verification is successful

15.  SpaaK Module installs Vehicle Identity Certificate    
16.  SpaaK Module reports Vehicle Identity certificate installation status to
    Vehicle OEM Server
SpaaK >> SGW >> TBM >> Vehicle OEM Server: VehicleIdentityCertStatus VehicleIdentityCertStatus = Status: RespEnum || SpaakRequest

17. Vehicle OEM Server receives and verifies VehicleIdentityCertStatus

If VehicleIdentityCertStatus verification is successful  

18. Vehicle OEM Server acknowledge receiving the SpaaK Module Vehicle
Identity certificate status to the vehicle
GSDP >> TBM >> SGW >> SpaaK: C2VUsecaseCompletionAck
19. SpaaK Module receives and verifies C2VUsecaseCompletionAck

**Open questions**

- What is GDPS? 
- What is DigitalKeyServer? 
- What is DigitalKeyTrackingServer?


#### Findings - Follow up questions

Also documented in [[Followup]]

The sequence diagram - make new diagram with the cloud details. 
- VehicleIdentityCSRResponse, do we need all these responses? 
- What is VehicleSubjectIDRequest
	- VehicleIdCSRRequest
- CAEnabled = false 

##### Pki 
- Add ECU Ids to PKI before doing anything make clear
- PKI needs to be able to validate the CSR / SignCSR 

#### Delta 
5.6.4.1 New Vehicle Identity Provisioning 
- 5.  Vehicle OEM Server generates Vehicle Identity subject ID (as per CCC subject ID definition) or TBE? 

###  5.6.4.2 SPAKE2+ Parameters Provisioning (triggered by Vehicle OEM server)

#### Use Case ID PP-02

**Description**
In preparation for a new owner pairing, new SPAKE2+ verifier values must be stored in the vehicle. It needs to be provisioned prior to owner pairing. In addition, certain scenarios (e.g. error handling use cases) may require the Vehicle OEM server to push SPAKE2+ verifier values to the vehicle.

#### Findings 
- Renew Vehicle ID endpoint 
- Saving the verifiers to DB for the ECU ID 
- We also need to know the K Certificate from the vehicle from the begining 
- Ending status? 


### 5.6.4.3 SPAKE2+ Parameters Provisioning (triggered by SpaaK Module)

#### Use Case PP-03

**Description**

In the following scenarios;
1.  Owner key termination use cases  
2.  Deletion of previously used SPAKE2+ verifires
		a. This occurs when owner pairing fails > 7 times  
3. SpaaK detects lack of SPAKE2+ verifier values during owner pairing
New SPAKE2+ verifier values must be stored in the vehicle. Thus, SpaaK Module shall request it from the Vehicle OEM Server.

#### Status 
**TODO**



### [[5.6.5 Owner Smartphone Key Pairing (OP)]]

**Description**

CCC divides the Owner Pairing Flow into 4 technical phases.
-   Phase 0: Preparation
-   Phase 1: Initiate pairing procedure on vehicle and device
-   Phase 2: First session with NFC reader
-   Phase 3: Second session with NFC reader
-   Phase 4: Finalization of pairing procedure

The actual execution steps to complete the pairing via NFC are described in the following use cases:

1.  OP-01: User initiates pairing from Uconnect App (in Smartphone)   
2.  OP-02: User initiates pairing from Vehicle (in HU)
3.  OP-03 – OP-05: CCC Owner Pairing Phases 2 – 4 are executed
4.  OP-06: BLE activation & first approach


### UseCase OP-01a - Mobile app - Initial Pairing procedure

#### Notes 
- Vos generates the pairing password and uses it to be sent from Backend to Phone app 


#### VOS
- The VOS gets the Pairing password from the DIGITALKEYSERVER
- The VOS Validates service is provisioned
- The VOS validates user is owner 
- The VOS validates the pairing password wasn't delivered to the mobile app 
- The VOS returns the pairing password to the GDSP services and it will be passed to Mobile App 
- The VOS makrs the pairing password as delivered 
- The VOS generates the pairing password deep link 
- The VOS marks pairing password as delivered to mobile app 
- IF the password is never delivered try again 
- IF Error in any steps above send Error, reason to the mobile app 


#### TBE (new)
- The TBE recieves a Reqiest for the pairing password 
- the TBE validates the userAuthorization
- The TBE sentds back the Pairing password - Deep link URL to the Mobile app 


### UseCase OP-01b -  - Pairing password request via Customer Portal / Hotline, retrieved in email

**Description**

The owner pairing password retrieval via Customer Portal / Hotline, by receiving an email with deep URL for pairing password

#### VOS

- The VOS recieves a password Pairing request
- The VOS sends the pairing password URL to the GSDP_Services


#### TBE (new)

- The TBE will validate the user authorization 
- The TBE will response with Authorization successful if everything is fine
- The TBE will response with Report failure if the Authorization fails 

#### Helpcenter? 

- The HC will recievers a Owner pairing password reqeust
- The HC will request the User to authorize 
- The HC will accept the user authorization
- The HC will send the pairing password URL via email
- IF there is an issue on the cloud side the HC will Report a failure to user 

![[Pasted image 20230404142845.png]]


### 5.6.5.3.2 Phase 3: Second Session with NFC Reader 

### VOS / TBE
- Recieves a Status message from the Vehicle 
