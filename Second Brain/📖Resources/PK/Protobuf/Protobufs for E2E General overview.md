#later  #protobuf #tbe #python 

```toc
```


Current open questions from our side: 

- Do we need all the messages?  
![[Pasted image 20230310163308.png]]

We only have the OP_INIT and OP_SPAKE2.. 

- Also question what should we use to communicate between TBE and Backend? 
![[Pasted image 20230310163752.png]]

Also research how and why protobufs work. 

## Dos and donts 

https://protobuf.dev/programming-guides/dos-donts/

## javascript and protobuf library

[GitHub - protobufjs/protobuf.js: Protocol Buffers for JavaScript (& TypeScript).](https://github.com/protobufjs/protobuf.js/)

### Acronyms

APAC Asia Pacific region  
BEV Battery Electric Vehicle  
BCM Body Control Module  
BLE Bluetooth Low Energy  
CCC Car Connectivity Consortium  
CSR Certificate Signing Request  
DFMEA Design Failure Mode and Effect Analysis DVP Design Validation Plan  
ECU Electronic Control(ler) Unit  
EMEA Europe Middle East Africa region  
FCA Fiat Chrysler Automobile  
GCSB Global Cyber-Security Bridge  
GSDP Global Service Delivery Platform  
HU Head Unit  
ICE Internal Combustion Engines  
IOD Ignition-Off Draw  
LATAM Latin America region  
LF Low Frequency  
NAFTA North America Free Trade Associated region NFC Near field Communication  
PASE Passive Start and Entry  
PEKG Passive entry Keyless Go  
PKI Public Key Infrastructure  
RFHM Radio Frequency Hub Module  
RSSI Received Signal Strength Indicator  
SDP Service Delivery Platform  
SGW Security Gateway  
SOW Statement of Work  
SpaaK Smartphone as a Key  
TBM Telematics Box Module  
UHF Ultra High Frequency  
UWB Ultra-Wide Band  
WCP Wireless Charging Pad


## Pairing preparation - Charlotte

### Steps 
1. SPAAK recieves CAN message from TBM / TBE
	- Is connected to GSDP?
	- Subscribes int he SPAAK to topic
2. SPAAK verifys drmUUID availability
	- if UUID not available - 5.6.12.2 (find in docu)
		- SPAAK requests GSDP to update SPAAK service provisioning status
	- if yes - Continue 
3. SPAAK verifies the availability of the Vehicle Identity Certs
	- If Available will not perform next steps
	- If Not available perform next steps
4.  SpAAK request Vehicle Identify Certs subjectID (VehicleSubjectIdRequest)
5.  VOS recieves verifies VehicleSubjectIdRequest 
	 - if successfull 
6. VOS generates Vehicle Identity subject ID (as per CCC)
7. VOS server pushed Vehicle Identity subject ID to vehice (VehicleSubjectIdResponse), GSDP >> TBM >> SGW >> SpaaK: VehicleSubjectIdResponse VehicleSubjectIdResponse = SubjectID || SpaakResponse
8. Spaak Module Recieves and verifies VehicleSubjectIdResponse 
	- if VehicleSubjectIdResponse successfull verified
9. Spaak module generated Vehicle identity key pair 
10. Spaak module generates vehicle identity CSR 
11. Spaak module sends Vehicle idtentity CSR to VOS 
	- SpaaK >> SGW >> TBM >> Vehicle OEM Server: VehicleIdentityCSRRequest VehicleIdentityCSRRequest = CSR_file || SpaakRequest
12. VOS Server recieves and verifies VehicleIdentityCSRRequest 
	 - VehicleIdentityCSRRequest verification is success 
13. VOS signs Vehicle Identify CSR / SignCSR  
14. VOS pushed the vehicle idtentity certificate (K) to the vehicle 
15. SPAAK module reviews and verifies VehicleIdentityCSRResponse
16. SPAAK module installs Vehicle Identity Certificate 
17. Spaak Module reports Vehicle Identity Certificate installation status to the VOS 
18. Vehicle oem server recieves and verifies VehicleIdentityCertStatus 
19. VOS acknowledges recieveng the spaak module vehicle identity certificate status to the vhiccle 
20. Spaak module recieves and verivies C2CUsecaseCompletionAck 


#### Summary 
 usecase (PP-01) for preparing a new vehicle identity to be stored in a vehicle in preparation for a new owner pairing. The vehicle identity consists of the vehicle's long-term key pair and a public key certified by the backend, which includes the vehicleID in the certificate subject name. The use case involves several steps, including verifying the availability of the Vehicle Identity Certificate, requesting and generating a Vehicle Identity key pair and CSR, and installing the Vehicle Identity Certificate. The document also includes details on actor roles, preconditions, and post conditions.


## Stelantis implementation details

### [[5.6.5 Owner Smartphone Key Pairing (OP)]]

### [[5.6.5.3.4 BLE Activation & First Approach]]