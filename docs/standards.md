
Open Web Standards
==============================

!!! warning "Living Document (WIP)"

    This document is currently **under development**, which means **"Work in Progress"**.  
    It is carried out in the context of the [DICE project]{target="_blank"} (Data Infrastructure Capacities for EOSC), funded by the EU's Horizon 2020 project call H2020-INFRAEOSC-2018-2020 under Grant Agreement no. 101017207.


Open web standards specifications used within the project are:

### Linked Data Notification
W3C Linked Data Notification (LDN) is an HTTP-based notification (push) protocol. It will be used for repository/archive communication. 
### Activity Streams 2
W3C Activity Streams 2 (AS2) provides a foundational vocabulary for messaging about activities that involve web resources. A message profile inspired by notifications used in the COAR Notify project and the UGent Researcher Pod project will be used for LDN notifications exchanged by repositories and archives.
### Signposting
Signposting is a REST/HATEOAS “follow your nose” (navigational) approach to make the scholarly web more friendly to machines; it leverages IETF RFCs and IANA-registered link relation types. Typed links (HTTP Link header and/or HTML <link>) are used to allow machines to uniformly navigate scholarly artefacts irrespective of the repository they reside in. The FAIR Signposting Profile is a lightweight, yet powerful approach to increase the FAIRness of scholarly objects. It will be used by repositories as a means to allow archives to determine which web resources need to be retrieved in response to an on-demand archiving request.

[DICE project]: {{ hyperlink.ext.dice }}
