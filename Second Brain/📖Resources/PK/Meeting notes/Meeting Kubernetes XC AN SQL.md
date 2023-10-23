## Meeting XC NA Kubernetes

- pki folder ca_templates / data / json 
- regresions uberpruft ob alles funktioniert
- initial data load - init_services
- neuen - sind auf anderen repo / pk etwas devops 
- Devops repo is not much active

#### DB Lock 
- New version has a fix - 8.4.1 
	- Init container - no worker so it does not gert locked

#### key slot counter
- 8.4.0 has key slot counter
- client credentials - API Client token can also be used 
- Details Wolfi

#### SBOD
- fms-0 
- dos
- vos

#### Error: owner_digital_key_long_term..
- no info about this one from XC 

#### Error Signature can't be verified

- sbod / sbfd - users and devices anlegen
	- have to have devices with the name in the DOS DB - Devices table
- sending the components all around the components.. find out where the signature is thrown then we can figure out a solution
- SBOD ? Nothing can found in SBOD 
- VOS Sigunature public key should be checked
- Enviroment variable VOS? Not understanding this part... 
- Download owner pairing bundle
	- Regression script works with timeouts, if its too long it can fail sleep long / short timeouts 
- Private/Public Signature - OwnPrivate sigunature key 

- Owner pairing bundle has been successfully verified. 
- Bugfixes in 8.4.1 - 8.4.2