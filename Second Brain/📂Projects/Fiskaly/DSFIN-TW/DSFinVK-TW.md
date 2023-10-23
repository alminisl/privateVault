
[[Glossary]]

### QR Code 

- Standardized QR code enables quick check of documents - brings advantage for both financial administration and the company

TODO: Clarify this further

### EDS 

- 3 separate components

#### Integration interface (Einbindungsschnitstelle)

- Essentially the BSI certified technical security gateway to the electornic recording system 

#### Export interface for the TSE 

- in short The BSI TR-03153 - has some predefined requeriments to adhere to 

The data in the interface includes log messages that record all of the events that occur in a TSE/TSS. 
These log messages can be used to track the progression of a transaction and to ensure that the data has not been tampered with. The export interface is required by German law for all businesses that use TSE.

#### Digital interface of the financial administration for taximeters, odometers and additional recording systems (DSFinV-TW)

In Germany, tax authorities require businesses that use taximeters or odometers(**Wegstreckenzähler**) to keep digital records of their transactions. These records must be in a specific format and include all relevant information, such as the date, time, location, and amount of the transaction.

In addition to the data from the  taximeter or odometer,businesses may also need to keep digital records of other information, such as the driver's name and license number. This information is also required to be in a machine-readable format.

The German Federal Central Tax Office (BZSt) has published a digital interface (DSFinV-TW) that businesses can use to export their data. The interface includes a standard format for the data, making it easier for tax authorities to review and verify the records.

Businesses that do not export their data in the DSFinV-TW format must still provide the data to tax authorities upon request. This data must be in a format that allows tax authorities to track the transactions in their entirety.

### Goals of the DSFinV TW 

The goal of the standardization is to define a structure for data from taximeters, odometers, and complementary recording systems. As of January 1, 2024, the use of the legally required unified digital interface (§ 146a AO) will be required for these systems. The standardization is intended to achieve the following goals:

 - Provide a single data source for tax audits and investigations, ensuring that the data can be traced from the basic records to the general ledger (financial accounting).
-  Allow all data recorded in each electronic recording system to be archived in a single system.
 - Simplify the review of structured data from taximeters, odometers, and complementary recording systems that have been transferred to the financial accounting system.

In other words, the standardization will make it easier for tax authorities to verify the accuracy and completeness of data from taximeters, odometers, and complementary recording systems. The standardization will also make it easier for businesses to comply with tax laws.

### Scope

The German government is implementing a new data standard for tax authorities to use to audit businesses that use electronic recording systems. The standard, called DSFinV-TW, requires businesses to export their data in a specific format, including certain mandatory fields and optional fields. The mandatory fields are required to ensure that the data is complete and accurate, while the optional fields can be used to provide additional information that may be helpful for audits.

The standard is designed to make it easier for tax authorities to audit businesses and ensure that they are complying with tax laws. It is also designed to make it easier for businesses to comply with the law, as they will only need to export their data in a single format.

Here is a summary of the key points of the text:

- The German government is implementing a new data standard for tax authorities to use to audit businesses that use electronic recording systems.
- The standard, called DSFinV-TW, requires businesses to export their data in a specific format, including certain mandatory fields and optional fields.
- The mandatory fields are required to ensure that the data is complete and accurate.
- The optional fields can be used to provide additional information that may be helpful for audits.
- The standard is designed to make it easier for tax authorities to audit businesses and ensure that they are complying with tax laws.
- It is also designed to make it easier for businesses to comply with the law.

### Creation of index.xml 

Information on how to create an index.xml file can be found in the document "Additional Information on Data Carrier Delivery" (BMF IV A 4, as of November 28, 2019), which is published as an appendix to the GoBD.

### Usage regulations

1.1.2024

### Data structure
The data from the electronic recording system should be traceable, especially with regard to the completeness check of operating revenue, the calculation of sales tax, and the booked revenue. The basis for data storage is the drives as individual recordings.

The DSFinV-TW is divided into the following areas: 
 - Einzelaufzeichnungsmodul
 - Stammdatenmodul
 
This is to avoid redundant data storage. For this reason, the master data must be stored for each shift. This eliminates the need for complex master data history. To ensure that the master data can be clearly assigned to the respective recording system, it is important to ensure that the shift is ended before a master data change.

Due to the complexity of the representation, it is necessary to define several CSV files. 

- Fahrten.csv
- Fahrten_Zahlarten.csv
- Schicht.csv
- TSE_Transaktionen.csv
- Stamm_Unternehmen.csv
- Stamm_Fahrzeuge.csv
- Stamm_Personal.csv
- Stamm_Kunden.csv
- Stamm_TSE.csv 

<< ADD TABLES HERE >>

### Taxameter and odometer(Wegstreckenzähler)

Taxameters and odometers are types of recording systems that are required by law in Germany. They are both required to be certified to comply with the "MID?" directive, which ensures that they are accurate and reliable.

- A taxameter is a meter that measures the distance traveled by a vehicle. It is required by law in Germany for taxis and rental cars.
-  A taxameter must be certified to comply with the "MID?" directive, which is a European regulation that sets standards for meters and other measuring devices.
- A taxameter system consists of the meter itself, a display, a mileage sensor, and any other components that are integrated with the meter.
- Any other systems that are used with a taxameter, such as an accounting system, are not considered part of the taxameter system.

**Odometer / Wegstreckenzahler**

- An odometer is a meter that measures the distance traveled by a vehicle. It is required by law in Germany for all vehicles.
-  An odometer must be certified to comply with the MID directive.
- An odometer system consists of a display, a mileage sensor, and any other components that are integrated with the odometer.
- Any other systems that are used with an odometer, such as an accounting system, are not considered part of the odometer system.

**Terminology**

-  A transaction is a unit of data that is recorded in a TSS/TSE.
-  A business transaction is an event that affects the financial records of a business.
-  An other process is an event that is not a business transaction, but is still important for the proper functioning of the TSS/TSE.


### Definition of the data structures for transfer to the security module

Each transaction or other process is represented by a startTransaction and a finishTransaction. The startTransaction marks the beginning of the event, and the finishTransaction marks the end.

The data in each transaction or other process is represented by a processType and a processData. The processType identifies the type of data, and the processData contains the actual data.

The processTypes are as follows:

- Einschalten-V1: The ERS is turned on.
- Fahrer-V1: A driver is logged in or out.
- Frei-V1: The ERS is switched to the "Free" mode.
- Fahrtbeleg-V1: A ride is started or ended.
- Pause-V1: The ERS is switched to the "Pause" mode.
- Ausschalten-V1: The ERS is turned off.
- SonstigerVorgangTW: An other process occurs.


The processData for each processType is as follows:

- Einschalten-V1: Empty
- Fahrer-V1: Empty
- Frei-V1: The total distance traveled
- Fahrtbeleg-V1:
    - Taxikennung: The vehicle identification number
    - Tarifkennung: The tariff identification number
    - Fahrttyp: The type of ride (tariff or other)
    - Fahrtbeginn: The start time of the ride
    - Fahrtende: The end time of the ride
    - zurückgelegte Strecke: The distance traveled
    - Fahrpreis: The fare
    - Zuschlag: The surcharge
    - in Rechnung gestellte Gesamtsumme: The total amount billed
    - Brutto-Steuerumsätze: The gross sales for each tax rate
    - Zahlungen: The payments made for the ride
- Pause-V1: Empty
- Ausschalten-V1: Empty
- SonstigerVorgangTW: Specific data for the other process

The data in the processData fields is formatted as follows:

- **Dates and times** are in the ISO 8601 format (YYYY-MM-DDThh:mm:ss).
- **Numeric values** are formatted with a decimal point and two decimal places.
- **Strings** are formatted with the ASCII character set.

The data is transferred to the TSS in a binary format.

The data in the transaction is formatted as follows:

- **System**
    - Prefix (e.g., "T" for taxi meter or "W" for odometer/Wegstreckenzählern)
    - Manufacturer name
    - Model name
- **Zählwerksdaten** (odometer data)
    - Total distance traveled
    - Total number of passengers
    - Total amount of fares charged
- **allgemeine Daten** (general data)
    - Constant of the odometer sensor (in impulses per kilometer)
    - Date of backup
    - Taxi identification number
    - Current time
    - Tariff identification number