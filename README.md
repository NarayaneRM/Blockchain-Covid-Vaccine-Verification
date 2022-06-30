Blockchain Supply Chain POC: COVID-19 Vaccine Passports
# 1] Goal
Design and implement a system that solves a known problem of trust in the COVID-19 vaccine supply chain.

# 2] Requirements Gathering
## 2.1] Vaccine Cold Chain
![](./imgs/001.png)

*Source: [Vaccine cold chain Q&A*](https://www.gavi.org/vaccineswork/vaccine-cold-chain-qa)*
## 2.2] System Actors
1. **Manufacturer**
   1. process raw materials into vaccines
1. **Distributor**
   1. transports vaccines between locations
1. **Inspector**
   1. performs quality checks on vaccines
   1. performs quality checks on manufacturing plants
1. **Storage Facility**
   1. store vaccines in cold temperatures
1. **Immunizer** (the doctors, nurses
   1. vaccinates people
   1. provides vaccine passport/certificates
1. **Traveller** (the patient)**:**
   1. receives vaccine
   1. receives vaccine certificate
   1. presents vaccine certificate at the border of the destination country
1. **Border Agent**
   1. verifies the vaccine certificates/passports
## 2.3] Problem-Solution Map


|**No.**|**Problems**|**Affected Actors**|**Proposed Solutions**|
| :- | :- | :- | :- |
|1|Vaccine passports can be falsified|- Border Agent|- Cryptographically verify using on-chain data|
|2|Key facilities may not meet quality standards|- All|<p>- Publish inspection results to blockchain</p><p>- Verify presented inspection results</p>|
|3|Vaccine passports may not be recognized by destination countries|<p>- Distributor</p><p>- Traveller</p><p>- Immunizer</p>|- Verify signatures in presented certificates|

## 2.4] Why Blockchain?
1. **Tamper-Proof Provenance**
   1. does the label on the vaccine’s vial accurately represent its contents?
   1. did the vaccine come from an inspected batch?
1. **Credential Issuance & Verification**
   1. cryptographic signatures that are easily verified with on-chain identities
1. **Data Redundancy**
   1. the data can’t be lost even if a Traveller “misplaces” their device
   1. the data can’t be lost even if the vials are damaged
#
# 3] System Design
## 3.1] Flow
1. Inspector issues certificate for batch to Manufacturer
1. ***<batch status updated to MANUFACTURED>***
1. Manufacturer presents certificate to Distributor
1. Distributor verifies each certificate
1. ***<batch status updated to DELIVERING\_INTERNATIONAL>***
1. Distributor presents updated certificate to Storage Facility
1. Storage Facility verifies each batch certificate
1. ***<batch status updated to STORED>***
1. Storage Facility presents certificates to Distributor
1. Distributor verifies each certificate
1. ***<batch status updated to DELIVERING\_LOCAL>***
1. Distributor presents updated certificate to Immunizer
1. Immunizer verifies certificates
1. ***<batch status updated to DELIVERED>***
1. Immunizer vaccinates Traveller and issues vaccine passport
1. ***<certificate issued with status VACCINATED>***
1. Traveller presents vaccine passport to Border Agent
1. Border Agent verifies vaccine passport

## 3.2] User Classifications
![](./imgs/002.png)
## 3.3] Use Cases
1. As an ***Issuer***, I can issue a signature representing a digital certificate for a manufacturer’s plant or storage facility
1. As a ***Prover***, I can present a certificate/signature issued to me
1. As a ***Verifier***, I can validate the signature on the blockchain for a vaccine
### 3.3.1] Out of Scope
- Payments between system agents;
- Dishonest doctors/immunizers;
- Suppliers of raw materials to the manufacturers;
- Image capture & QR code scanning;
- Scalability;
- Distribution to areas without internet access;
- IoT;
- Machine learning;
- Regulatory compliance (e.g. GDPR, HIPAA, etc.); and
- Anything not addressed in this video.

## 3.4] High-level Diagram
### 3.4.1] 3-Tiered Architecture
![](./imgs/003.png)
### 3.4.2] 2-Tiered “dApp” Architecture
![](./imgs/004.png)

##

