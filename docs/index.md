DICE Digital Preservation Service (DDPS)
==============================

!!! warning "Work In Progress"

    This document is currently **under development**, which means **"Work in Progress"**. It is carried out in the context of the [DICE project]{target="_blank"} (Data Infrastructure Capacities for EOSC),
    funded by the EU's Horizon 2020 project call H2020-INFRAEOSC-2018-2020 under Grant Agreement no. 101017207.


Introduction
--------
This document describes the functional and technical requirements for the DICE Digital Preservation Service (DDPS).  
The document is meant as a guide on how to implement the Long Term Preservation Service between a short to mid term data repository and a long term preservation (LTP) Archive.
All the open web standards used and the specifications and the profiles will be documented here.

DICE Digital Preservation Service
---------------------------------
The technical specification for long-term-archiving notifications have been developed by DICE Task 4.3: Long Term Preservation.<p />
It will focus on the following web standards:  

- [Linked Data Notification](https://www.w3.org/TR/ldn/){target=_blank} (W3C) => Notification protocol
- [Activity Streams 2](https://www.w3.org/TR/activitystreams-core/){target=_blank} (W3C) => [Vocabulary](https://www.w3.org/TR/activitystreams-vocabulary){target=_blank} / Contents (payload)
- [Signposting]{target=_blank} => Navigational

[DICE Digital Preservation Service Technical Requirements](tech-requirements.md) 



This document gives an overview of the DICE Digital Preservation Service (DDPS) architecture. The schema below displays all the components of the service and how they relate and interact to
each other. The notation used is not a formal one and is intended to be self-explanatory.

![Overview](architecture-overview.png)

1. An LTP request will be sent from a B2SHARE landing page to the Archival Bot’s inbox, conveying the URL of the landing page of the dataset.
2. The Archival Bot will poll the LDN Inbox for such requests.
3. The Archival bot visits the landing page URL, discovers a Link Set provided via Signposting, and retrieves it.
4. The Archival Bot parses the Link Set to obtain URLs for object files and metadata, and then retrieves those.
5. The Archival Bot deposits an archival package containing metadata and object files to the LTP-archive.
6. The Archival Bot reports back on the status of the deposit.

Actors
------

* **Repository User** - an authenticated user of the repository system, typically a researcher who curates or deposits data.

Components
----------
Please see the [Service components](components.md) for further details.

[yEd]: https://www.yworks.com/products/yed
[Signposting]: https://www.signposting.org/
[//]: # ([DICE project]: https://www.dice-eosc.eu/)
[DICE project]: {{ hyperlink.ext.dice }}