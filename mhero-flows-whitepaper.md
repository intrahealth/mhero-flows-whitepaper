**IntraHealth International**

# **mHero Workflows White Paper: Use cases for short messaging and FHIR with mHero**

**Revision 0.1 - Draft**

Author: IntraHealth International

Contact: [GitHub Issue](https://github.com/intrahealth/mhero-flows-whitepaper/issues/new/choose)

# Forward

This is a white paper of IntraHealth International.

This white paper is published [here](https://github.com/intrahealth/mhero-flows-whitepaper/blob/main/mhero-flows-whitepaper.md)

Comments are welcome. Please submit a [GitHub Issue](https://github.com/intrahealth/mhero-flows-whitepaper/issues/new/choose).

**CONTENTS**
* [1 Introduction](#1-introduction)
* [2 Short Messaging](#2-short-messaging)
* [3 mHero and Health Worker Registries](#3-mhero-and-health-worker-registries)
* [4 Summary of Workflows](#4-summary-of-workflows)
* [5 Synchronizing Practitioners](#5-synchronizing-practitioners)
* [6 Structured Data Capture](#6-structured-data-capture)


## 1 Introduction
[mHero](https://www.mhero.org) is a two-way, mobile phone-based communication system that connects ministries of health and health workers. It uses data from existing local health information systems to deliver messages via locally popular communication channels. It reduces the barriers that can exist between health workers and their support systems, playing a critical role in ensuring effective and efficient responses, particularly in a crisis.

Health officials can use mHero to:
* **Communicate** both routine and urgent messages to health workers. 
* **Target messages** to health workers based on cadre, location, or skill set. 
* **Collect critical information** that powers resilient health systems, including stock levels, routine and one-time assessments, and validation of health worker and facility data.
* **Build capacity** and **provide support** to health workers, to give them the information, skills, and encouragement to deliver quality health services.
 
**mHero is not a new technology.** Instead, it is a new way to connect data from existing technologies to allow for targeted, real-time communication. It does so by using global interoperability standards for health information exchange. In other words, mHero can help platforms speak in a common language and easily share data.

[IntraHealth International](https://www.intrahealth.org) and [UNICEF](https://www.unicef.org) created mHero in August 2014 to support health-sector communication during the Ebola outbreak in Liberia. The original version of mHero connected Liberia's health workforce information system, [iHRIS](https://www.ihris.org), with [RapidPro](https://app.rapidpro.io), a platform that delivers basic text and audio messages. The use of RapidPro made it possible to reach most Liberian frontline health workers using only basic mobile phones.

Since the end of the Ebola crisis, the Ministry of Health and Social Welfare in Liberia has integrated the platform into its health information system infrastructure to meet ongoing communication needs for various health services. Several other countries have also tested or deployed mHero, including for COVID-19 response purposes.

The technology behind mHero has also evolved since the initial deployment in Liberia. Both advancements in technology, as well as varying conditions and needs in other countries, inspired IntraHealth to make mHero more interoperable. It can operate with other communication platforms and any health information systems compliant with the global Fast Healthcare Interoperability Resources (FHIR) standards.

mHero’s origin and ongoing use and development illustrate how the platform is **flexible**, **scalable**, and **sustainable** by governments in low- and middle-income countries.


## 2 Short Messaging


## 3 mHero and Health Worker Registries


## 4 Summary of Workflows

### Use Case: Sync RapidPro contacts and groups with point of service systems
* **Example**: Verifying in the CHW registry the phone numbers of CHWs who register women for age- and stage-based messaging.
* **Short description**: mHero as a connector that syncs contacts between RapidPro and point of service systems in FHIR standard.
* **Technical description**: mHero runs as a microservice that syncs (one-way in either direction, or two-way) contacts and groups between RapidPro and point of service systems in FHIR standard. The sync can occur in the background or by manual trigger via an end point.

### Use Case: Broadcast one-way messages using contacts from the health worker registry (or other registry) and IDs from the facility registry
* **Example**: Notifying vaccinators about vaccine delivery dates at the facility where they are based.
* **Short description**: mHero acts as a connector that syncs contacts between RapidPro and FHIR registry, and stores facility IDs.The HAPI FHIR Server then acts as a webhook for matching facility IDs.
* **Technical description**: mHero does contact syncing as above, and additionally can provide the facility IDs for the health worker (or other contact). The API for webhook queries is the HAPI FHIR Server.


### Use Case: Broadcast one-way messages originated within POS system

* **Example**: Sending reporting reminder to data managers who have not submitted weekly report.
* **Short description**: mHero syncs contacts and a module within the POS system is used to compose messages and trigger the sending which is done through RapidPro channels.
* **Technical description**: Contact sync happens as above. mHero interface enables composing messages, selecting contacts to receive the message, specifying the frequency and timing of sending, and triggering the sending.

### Use Case: Collect aggregate, routine data and push to POS system

* **Example**: Collecting daily reports of numbers of patients vaccinated.
* **Short description**: mHero syncs contacts. Reporting data must be formally mapped using mHero configurations.
* **Technical description**: Contact (demographic data) sync happens as above except for custom contact fields which must be mapped.Simple, unstructured data will be converted to FHIR Questionnaire Response and Communications resources. Form-oriented data must be mapped between RapidPro and POS system (registry/DHIS2). A data manager must map RapidPro flows to DHIS2 indicators/registry fields. This must be done for each questionnaire intended to be sent.

### Use Case: Contact initiated data submission 

* **Example**: Case-based reporting by health workers (eIDSR)
* **Short description**: mHero syncs contacts. Reporting data must be formally mapped using mHero configurations. Data can be submitted to multiple systems triggering other messaging or other actions.
* **Technical description**: Contact sync happens as above. Structured SMS flows are mapped between RapidPro and DHIS2 (and/or other POS systems). New case reports initiate flow to collect other information about the case; this information can be submitted to other systems as well (i.e. lab system) and notifications can be set up to alert people or offices (i.e. District Surveillance Officer) about new cases reported.


### Use Case: Both contacts (existing and new) and the system can initiate two-way messaging to submit/collect data can be pushed to DHIS2 and other POS systems

* **Example**: Polls on vaccine acceptance/hesitancy, self-reporting of vaccine doses received.
* **Short description**: mHero syncs existing contacts. Reporting data must be formally mapped using mHero configurations. In addition to the above, CasePro can be used independently for unstructured data.
* **Technical description**: Contact (demographic data) sync happens as above except for custom contact fields which must be mapped.Simple, unstructured data will be converted to FHIR Questionnaire Response and Communications resources. Form-oriented data must be mapped between RapidPro and DHIS2 (or other POS system). A data manager must map RapidPro flows to DHIS2 indicators/registry fields. This must be done for each questionnaire intended to be sent. In addition to the above, CasePro is used independently for "help desk" type support. Ad-hoc messages to the help desk are not mapped, but are available in FHIR Communication resources.



# 5 Synchronizing Practitioners


# 6 Structured Data Capture
