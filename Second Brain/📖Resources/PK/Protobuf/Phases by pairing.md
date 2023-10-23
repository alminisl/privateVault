### Phase 1 - Initiate Pairing Procedure (Vehicle HU) 

To pair a Smartphone with the respective vehicle, the owner shall initiate the pairing through the vehicle HU, in order to activate the SpaaK pairing mode, and SpaaK/WCP NFC communication.

Steps: 

1.  User turns on the ignition
2.  User chooses to add a digital key for the owned vehicle via vehicle HU
3.  HU request SpaaK Module to initiate owner pairing (name it PhoneKey_Req
    = [Add Phone])
Radio >> SGW >> SpaaK
4. SpaaK Module checks existence of SPAKE2+ verifier values  
	a. If SPAKE2+ verifier values does not exist, follow use case PP-03
1. SpaaK requests user via the HU to click on the deep link in the device (name it HU_NTF)
SpaaK >> SGW >> Radio
HU_NTF: Click on link retrieved in device, and follow device native app instructions
6.  SpaaK module shall transition into pairing mode
    1.  SpaaK module shall initiate owner pairing NFC polling
    2.  SpaaK module shall initiate owner pairing BLE advertisement
    3.  SpaaK Module shall remain in pairing mode for upto
        T_PairingModeTimeout timer. Once T_PairingModeTimeout timer
        expires, SpaaK module shall stop the pairing mode
7.  SpaaK module start timer T_OwnerPairing
	a. If timer expires, before owner pairing is complete, SpaaK module shall abort the process, and stop BLE advertisement and NFC polling.




#### Summary 
This use case describes the process of pairing a smartphone with a vehicle using SpaaK pairing mode and NFC communication. The user initiates the pairing process through the vehicle's HU and turns on the ignition. The SpaaK module checks for the existence of SPAKE2+ verifier values and requests the user to click on the deep link in the device to start the pairing process. The SpaaK module then enters pairing mode and starts NFC polling and BLE advertisement. If the owner pairing is not complete within the T_OwnerPairing timer, the SpaaK module aborts the process. The engine start requires a legitimate keyfob or NFC card to be inside the vehicle interior.


### Phase 2 - First Session with NFC Reader

The initial session with the NFC Reader configures the DKFramework and establishes a secure channel between Smartphone and vehicle. This is used to exchange keys and commands.

WCP Wireless Charging Pad
DK - Digital Key?

Steps: 
1. WCP selects CCC DK Framework  
	a. WCP forwards Select_response to SpaaK Module if the device
	present on the WCP is a CCC compliant device
2.  SpaaK Module and Device negotiate CCC Applet version
3.  Device and SpaaK Module perform a SPAKE2+ to create long term shared
    secret on both sides
4.  SpaaKModule provides the device with Digital Key Creation Data [L], which
    includes;
    1.  Vehilce Identity Certificate [K] (tag 7F4Bh)
    2.  Device Configuration (tag 7F4Eh), which includes;
        1.  Tag 7F49h. 7F49h contains the required BLE parameters (IRK, kble_intro, kble_oob).
        2.  Tag D9h The supported Digital Key profile list.
5.  Device Creates Digital Key
6.  Device transfers Digial Key certificate, instance CA certificate, and Device OEM Cerificate to SpaaK Module
7.  SpaaK Module creates Digital Key attestation and send it to Device
8.  SpaaK Module and Device finalize Digital Key creation by indiacting
    successful execution on both sides (OP Flow)

#### Summary 

This use case involves the configuration of the Digital Key framework between a smartphone and a vehicle. The initial session with the NFC Reader establishes a secure channel between the smartphone and the vehicle. The WCP selects the CCC DK framework and negotiates the CCC Applet version with the SpaaK Module and the device. They then perform a SPAKE2+ to create a long-term shared secret on both sides. The SpaaK module provides the device with Digital Key Creation Data, including the Vehicle Identity Certificate, Device Configuration, BLE parameters, and the supported Digital Key profile list. The device creates the Digital Key and transfers the Digital Key certificate, instance CA certificate, and Device OEM Certificate to the SpaaK Module. The SpaaK Module creates Digital Key attestation and sends it to the device, and they finalize Digital Key creation by indicating successful execution on both sides. The LONG_TERM_SHARED_SECRET is created, and crypto material has been exchanged between the smartphone and the vehicle. The Digital Key Identifier enables the identification of the Digital Key within the Vehicle OEM Server system, and it is the SHA-1 hash value over the device public key. Error handling for SpaaK <> NFC Device communication is also specified.


### Phase 3: Second Session with NFC Reader

The second NFC session is executed between vehicle and Digital Key applet, a a standard transaction is performed with the SE Applet.

Steps: 
1. WCP selects CCC Applet  
	a. WCP forwards Select_response to SpaaK Module if the device present on the WCP is a CCC compliant device  
2. SpaaK Module and Device negotiate CCC Applet version  
3. Device and SpaaK Module perform a Standard Transaction as defined in CCC R2 Section 6.3.4  
4. SpaaK Module and Device finalize owner pairing by indiacting successful execution on both sides (OP Flow)  
5. Device send Key Tracking Request ( Device >> Device OEM Server >> Vehicle OEM Server >> Key Tracking Server  
6. SpaaK Module notifies HU of successful owner pairing At this point, Owner pairing is complete  
7. SpaaK Module notifies Stellantis backend if successful owner pairing 
	1. SpaaK >> SGW >> TBM >> Vehicle OEM Server : OwnerPairingPass_Ack
	2.  This step is not required to pass Owner pairing


#### Summary 

This usecase describes the steps involved in the second NFC session between a vehicle and a digital key applet, including the use of a CCC applet and a standard transaction with the SE applet. The digital key is created in the SpaaK module and the smartphone is placed on the wireless charging pad. The WCP selects the CCC applet and forwards a Select_response to the SpaaK module. The SpaaK module and the device negotiate the CCC applet version and perform a standard transaction. The owner pairing is finalized and the device sends a key tracking request. The SpaaK module notifies the HU of the successful pairing and then the Stellantis backend if successful. The post-condition is that a standard transaction is executed. The passage includes remarks on error handling and device communication.



### Phase 4: Finalization of Pairing Procedure 

The finalization step executes a standard transaction using transaction in regular intervals to poll the signaling bitmap indicator for an attestation package in the device. The corresponding bit in the signaling bitmap (SigBmp) is set by the device to indicate to the vehicle the presence of the key tracking attestation.

Steps: 
1.  SpaaK Module and Device exchange ephemeral Keys
2.  Device and SpaaK Module perform a Standard Transaction as defined in
    CCC R2 Section 6.3.4

#### Summary

This usecase involves finalizing the pairing of a digital key with a vehicle by executing a standard transaction between the Uconnect App on a smartphone, Vehicle OEM Backend, and the vehicle. This transaction involves polling for an attestation package in the device by checking a signaling bitmap indicator. The digital key is created in the Spaak Module and a LONG_TERM_SHARED_SECRET exists between the smartphone and vehicle. The SpaaK Module and device exchange ephemeral keys and perform a standard transaction as defined in CCC R2 Section 6.3.4. The KTS_Response content, including the attestation/key tracking receipt and uiBundle, is encrypted using Devx.Enc.PK and signed using ZZ2.SK. The attestation package bit in the signaling bitmap is set by the device to indicate the presence of the key tracking attestation. Error handling for SpaaK <> NFC Device communication is defined in section 5.7.1.