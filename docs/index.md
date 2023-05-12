Digital Preservation Service (DPS)
========================================

!!! warning "Living Document (WIP)"

    This document is currently **under development**, which means **"Work in Progress"**.  
    Don’t cite this document other than as work in progress.  
    It is carried out in the context of the [DICE project]{target="_blank"} (Data Infrastructure Capacities for EOSC), funded by the EU's Horizon 2020 project call H2020-INFRAEOSC-2018-2020 under Grant Agreement no. 101017207.


Introduction
------------
Within the DICE project, task 4.3 created a Long Term Preservation (LTP) template and accompanying guidance that data services and repositories can use to develop their own LTP policy.
The LTP policy should clarify to the users what is or can be guaranteed by the service, for how long and by whom.
The policy template contains articles that distinguish between outsourced services and services hosted in-house.  
This file documents the functional requirements and technical specifications for a service that implements such an LTP policy in which the archive is outsourced; the Digital Preservation Service (DPS).  
It is meant as a guide on how to implement an example long-term preservation Service between a short to midterm data (web)repository service and a long-term preservation (LTP) archive.  
The implementation adheres to documented community conventions for the use of [W3C Linked Data Notifications](https://www.w3.org/TR/ldn/){target=_blank} (LDN) and [Activity Streams 2](https://www.w3.org/TR/activitystreams-core/){target=_blank} (AS2) to integrate repository systems with long-term (LTP) archives, in a distributed, resilient and web-native architecture.  
The standards used, and the application profile documented here, are implementations of the generic patterns described by [Event Notifications in Value-Adding Networks]{target=_blank}, that details a profile for using Linked Data Notifications with ActivityStreams2 payloads in value-adding networks.  

[//]: # (The the [COAR Notify Protocol]&#40;https://notify.coar-repositories.org/&#41;{target=_blank} is also strongly aligned with the [Event Notifications in Value-Adding Networks]{target=_blank} Profile and provides notification patterns that are more specific implementations of the generic patterns described by [Event Notifications in Value-Adding Networks]{target=_blank}.)


The Digital Preservation Service
---------------------------------

## Use cases
### 1. Single record archiving
A single dataset will be transferred to a LTP-Archive on demand, according to the repository LTP Policy, by an authenticated repository dataset owner.

### 2. (Auto) Archive Community records
All records within a repository community could be auto-archived, according to a community archival agreement.  
Opt-out/in option could be offered to the dataset owner.  
This use case is a variant of use case 1 and is not worked out in this document, but it could easily be derived from the previous use case.


## Technical motivation
###### Asynchronous
The intended communication style among Nodes is point-to-point, requiring no centralized hubs.
Interactions among Nodes (Service Nodes and Data Nodes) are necessarily asynchronous because certain notification patterns do not require a response ("fire and forget") and, in patterns that do, such as requesting an action, the time between a request and the announcement of the Action Result is unpredictable, as the recipient may complete tasks at its own pace.
Pushing any data at any moment to an archive might cause resource problems at the server side.
Therefore, it is push-oriented, with only the relevant Nodes being updated about new information as it becomes available.
###### Lightweight
This proposal is lightweight. It does take relatively little resources to implement, both from the client as from the server side.
###### Multi-purpose
The LDN+AS2 notifications approach can also be used for other purposes with the same investment. For example the peer reviewing service [COAR Notify](https://notify.coar-repositories.org/){target=_blank}, which is also strongly aligned with the [Event Notifications in Value-Adding Networks]{target=_blank} Profile.
###### Open Web Standards
This specification is built using Open Web Standards only. Because of its obvious benefits like larger audience and community, forward compatibility with browsers and cost savings; no patents or licensing. 

## Open Web Standards

Below is a list of the open web standards that will be used for the core implementation of the Digital Preservation Service.

#### Linked Data Notification
W3C [Linked Data Notification](https://www.w3.org/TR/ldn/){target=_blank} (LDN) is an HTTP-based notification (push) protocol. It will be used for repository/archive communication. 
#### Activity Streams 2.0
W3C [Activity Streams 2](https://www.w3.org/TR/activitystreams-core/){target=_blank} (AS2) provides a foundational vocabulary for messaging about activities that involve web resources. A message profile will be used for LDN notifications payload exchanged by repositories and archives.  
Within this documentation, the Linked Data Notifications (LDN) with ActivityStreams2 (AS2) payloads will be reffered to as: 'LDN+AS2 notifications'.  
The notification payloads should use JSON-LD as default syntax, but other RDF syntaxes may be used.
#### Signposting
[Signposting]{target=_blank} is a REST/HATEOAS “follow your nose” (navigational) approach to make the scholarly web more friendly to machines; it leverages IETF RFCs and IANA-registered link relation types. Typed links (HTTP Link header and/or HTML <link>) are used to allow machines to uniformly navigate scholarly artefacts irrespective of the repository they reside in. The [FAIR Signposting Profile](https://signposting.org/FAIR/){target=_blank} is a lightweight, yet powerful approach to increase the FAIRness of scholarly objects. It will be used by repositories as a means to allow archives to determine which web resources need to be retrieved in response to an on-demand archiving request.


## Namespaces
Within this document, the following namespace prefix bindings are used:

| Prefix | Namespace                               | Name                                                         |
|:-------|:----------------------------------------|:-------------------------------------------------------------|
| `as`   | https://www.w3.org/ns/activitystreams#  | W3C ActivityStreams 2.0                                      |
| `ldp`  | http://www.w3.org/ns/ldp#               | W3C Linked Data Platform (LDP) Vocabulary                    |
| `sorg` | https://schema.org/                     | Schema.org                                                   |
| `ietf` |http://www.iana.org/assignments/relation/| The Internet Engineering Task Force (IETF)                   |

In our example LDN+AS2 notifications we use JSON-LD as syntax, in which we don’t explicitly write the prefixes.  



## DPS Architecture
### Main components
##### Web Repository
This is the short- to midterm repository system. In the DPS this repository system is used for depositing, storing and disseminating datasets / digital objects.  
The **Web Repository** must support Signposting and have an LDN inbox for handling LDN+AS2 notifications.   
In the Event Notifications in Value-Adding Networks specification, this is also refered to as the Data Node. 
##### LTP Archive
A Long-term Preservation Archive where datasets/digital objects can be preserved and archived.
The archive must provide a deposit endpoint. Depending on your system, this can either be internal or external. For example a REST API or SWORD enpoint.
##### Archival Bot
Middleware server that takes care of the LDN+AS2 notifications communication between the **Web repository** and the **LTP Archive**.    
It must support Signposting and have an LDN inbox.  
This middleware component can be implemented in several ways, depending on your architecture. It might be part of the LTP Archive application itself (built-in) or as a plug-in (internal). It may also run as a micro-service that interacts with the Archive (external).  
The external variant can also be extended with 'rule engine' functionality. Depending on certain business rules, it can send the archival deposit to different endpoints in the required format.
In the Event Notifications in Value-Adding Networks specification, this is also refered to as the Servive Node. 

### High level Architecture Overview
The schema below displays the components of the preservation service and how they relate and interact with each other. The notation used is not a formal one and is intended to be self-explanatory.
![Overview](architecture-overview.jpg)

1. An LTP request will be sent from a **Web Repository** landing page to the **Archival Bot**’s inbox, conveying the URL of the landing page of the dataset.
2. The **Archival Bot** will poll the LDN Inbox for such requests.
3. The **Archival Bot** visits the landing page URL, discovers a Link Set provided via Signposting, and retrieves it.
4. The **Archival Bot** parses the Link Set to obtain URLs for object files and metadata, and then retrieves those.
5. The **Archival Bot** deposits an archival package containing metadata and object files to the **LTP Archive**.
6. The **Archival Bot** reports back on the status of the deposit.


### Activity Diagram Use Case #1
The activity diagram below shows the interactions involved in use case #1. The numbers in the diagram correspond to the nummers given in the description below.
[![](https://mermaid.ink/img/pako:eNqtVW1r2zAQ_iuHRkgHHaPd1nZmFPK6Fkwb8tJ98RfFvjhaHcmT5dIu5L_v5JdGdlLYYPGXWM9z95zuJD9bFqoImcc6na2Qwniw7WYY5lqYFx-fMOl60E2UyrB7Cl2zxg12ve6SF-8BKxYeuBZ8mWAWMAoP2IYL2X-M6S1g7_qf--PhVcAsm4dG6VdkNByfjQcuonSEugQvvl6O--cOOMdnM1CJqvDz3qfLL5clLpXBFjy-ss8eJtE3gldKmpn4jbb2gJ1dpM8B2-12nU4gM_yVowxxKHis-SaQQD-eGyXzzZIKLd6rVVsi8ESECDyDXm7WqiKkXBsRipRLAxpTZfEfuIQp_c8Ehb0c8pbKFGl0uBZPPIG-MockXqCFnj-fwJAbXkVgIKuybEEfrq-trge-ioUEJSHhMhIyTnmMx3hTu-_MwIq2RJlLioWIQZV5MEMZwYk_vHtP4ufe_WqFGqjNYiVCbgQpfPP3ErCY-teNJKXMDA1khps8s523W9CVcIpFcMDKKJUaGHAaRFKXVq4fVt5kNTfQ3oStfCEjdYDWTciovjfqquouQ2mx7jddlBSoLyDkUj3vM5NgLTtRSdKmFBlavMEaw0eg4YuIriKoVRH02u7G4UsMPPT82yEUkAe9MMTUtMl7gbr_jSmWQW90Y5FG3GBrXHSYUq1ijVlWj6qtcTMn3s2oN4STmYglnXhDDXzfUqn37Av5WBwLX5XnyN3lQdrvo_k-4kj6TsfefNAiXhvbv0Lihv9NNrX8iaHJjmUtA6u7V8VO7mfzj5PFvLiDTvyhVLvnUqqcjuyR23G049X1jmy7q6OTZAi3d43xT9Gq_-P4y6D_cxnYKdugJhuIyFi2FqicovzIWvegj6-z3nKQcuqOj4BrJDXsuAm4dtLEa08B11QaFNc6wHWHmtX2F3ANxiU5LnM00TGvsdgukDvqWV6MfBRZU2DeitNoT5n1m9mLDJlndI41qbKkirX7A_bDcPQ?type=png)](https://mermaid.live/edit#pako:eNqtVW1r2zAQ_iuHRkgHHaPd1nZmFPK6Fkwb8tJ98RfFvjhaHcmT5dIu5L_v5JdGdlLYYPGXWM9z95zuJD9bFqoImcc6na2Qwniw7WYY5lqYFx-fMOl60E2UyrB7Cl2zxg12ve6SF-8BKxYeuBZ8mWAWMAoP2IYL2X-M6S1g7_qf--PhVcAsm4dG6VdkNByfjQcuonSEugQvvl6O--cOOMdnM1CJqvDz3qfLL5clLpXBFjy-ss8eJtE3gldKmpn4jbb2gJ1dpM8B2-12nU4gM_yVowxxKHis-SaQQD-eGyXzzZIKLd6rVVsi8ESECDyDXm7WqiKkXBsRipRLAxpTZfEfuIQp_c8Ehb0c8pbKFGl0uBZPPIG-MockXqCFnj-fwJAbXkVgIKuybEEfrq-trge-ioUEJSHhMhIyTnmMx3hTu-_MwIq2RJlLioWIQZV5MEMZwYk_vHtP4ufe_WqFGqjNYiVCbgQpfPP3ErCY-teNJKXMDA1khps8s523W9CVcIpFcMDKKJUaGHAaRFKXVq4fVt5kNTfQ3oStfCEjdYDWTciovjfqquouQ2mx7jddlBSoLyDkUj3vM5NgLTtRSdKmFBlavMEaw0eg4YuIriKoVRH02u7G4UsMPPT82yEUkAe9MMTUtMl7gbr_jSmWQW90Y5FG3GBrXHSYUq1ijVlWj6qtcTMn3s2oN4STmYglnXhDDXzfUqn37Av5WBwLX5XnyN3lQdrvo_k-4kj6TsfefNAiXhvbv0Lihv9NNrX8iaHJjmUtA6u7V8VO7mfzj5PFvLiDTvyhVLvnUqqcjuyR23G049X1jmy7q6OTZAi3d43xT9Gq_-P4y6D_cxnYKdugJhuIyFi2FqicovzIWvegj6-z3nKQcuqOj4BrJDXsuAm4dtLEa08B11QaFNc6wHWHmtX2F3ANxiU5LnM00TGvsdgukDvqWV6MfBRZU2DeitNoT5n1m9mLDJlndI41qbKkirX7A_bDcPQ)

### LDN+AS2 notification payloads

The LDN payloads that are involved in the activity diagram above, have been composed of the specifications in both [Event Notifications in Value-Adding Networks]{target=_blank} and [COAR Notify]{target=_blank}.   
For a profound understanding of this application profile one should also look into these specifications.
Prior to each example payload, the requirements of the properties used are listed in a table. The JSON-LD properties @id and @type (mapped to 'id' and 'type' in the notification by the @context property) represent the mandatory identifier for the activity and the activity type respectively.  
The activity identifier (@id) is distinct from the notification identifier, which is the URI minted by the LDN Receiver when the LDN+AS2 notification that describes the activity is received in its LDN Inbox.
Notice that all payloads include the [COAR Notify context file](https://notify.coar-repositories.org/schema/notify.json){target=_blank} (@context). This context file defines commonly used namespaces in this profile as listed in table 1, and also includes the COAR Notify vocabulary. 
The [activitystreams context file](https://www.w3.org/ns/activitystreams){target=_blank} also includes namespace prefixes used in the examples.

1. The <b>Author</b> logs in into the landingpage of the dataset that it owns on the **Web Repository** (authorized user).
2. The authorized <b>Author</b> presses an archival-button, to start a Long Term Preservation (LTP) request for this dataset on the landingpage.
3. The **Web Repository** (Data Node) sends a Linked Data Notification (LDN) Offer `as:Offer` to the LDN inbox `ldp:inbox` of the **Archival Bot** (Service Node). The payload MUST hold the landingpage URL `sorg:AboutPage` of the scholary object/dataset. This is by convention in both Event Notifications and COAR Notify. Also, providing the PID as a `ietf:cite-as` relation, together with the landing page URL is mandated by both specifications. This way all the associated resources can be found and retrieved by using FAIR Signposting discovery methods (12).

#### *as:Offer (3)*:  
In this example, the request for an LTP archival request is initated by the authorized author, 'Some Author' (identified in the payload as the actor). The origin identifies the system that sends the message on behalf of the actor.   

| Requirements | Properties                              |
|:-------------|:----------------------------------------|
| Required     | `@id`, `@type`, `as:actor`, `as:object` |
| Optional     | `as:origin`, `as:target`                |


```json
{
    "@context": [
        "https://www.w3.org/ns/activitystreams",
        "https://purl.org/coar/notify"
    ],
    "id": "urn:uuid:78a30582-ef0f-11ed-a05b-0242ac120003",
    "type": "Offer",
    "actor": {
        "id": "https://orcid.org/0000-0003-4405-7546",
        "name": "Some Author",
        "type": "Person"
    },
    "origin": {
        "id": "https://b2share.eudat.eu",
        "name": "EUDAT B2SHARE Web Repository",
        "inbox": "https://b2share.eudat.eu/inbox/",
        "type": "Service"
    },
    "object": {
        "id": "https://b2share.eudat.eu/records/1c42a67a73e9424b8192ba65c81077e1",
        "ietf:cite-as": "https://doi.org/10.23728/b2share.1c42a67a73e9424b8192ba65c81077e1",
        "type": [
            "sorg:AboutPage",
            "sorg:Dataset"
        ]
    },
    "target": {
        "id": "https://archivalbot.data-stations.nl/",
        "inbox": "https://archivalbot.data-stations.nl/inbox/",
        "name": "DANS Archival Bot",
        "type": "Service"
    }
}
```

<ol start="4">
	<li>The <b>Web Repository</b> flags the status on the landingpage of the scholary object/dataset to &quot;LTP Request Pending&quot;.   
	<li>Option: The <b>Author</b> cancels the LTP request, by pressing the "Cancel LTP" button on the landing page.
	<li>Option: In response to action (5), the <b>Web Repository</b> sends a Linked Data Notification (LDN) Undo<code>as:Undo</code> to the LDN inbox<code>ldp:inbox</code>of the <b>Archival Bot</b> (Service Node).
	<li>Option: In response to action (5), the <b>Web Repository</b> cleares the LTP status/flag on the landingpage, on behalf of the <b>Author</b>.
</ol>

#### *as:Undo (6)*:
In this payload, the as:object holds the original as:Offer message that needs to be undone.

| Requirements | Properties                              |
|:-------------|:----------------------------------------|
| Required     | `@id`, `@type`, `as:actor`, `as:object` |
| Optional     | `as:origin`, `as:target `               |


```json
{
    "@context": [
        "https://www.w3.org/ns/activitystreams",
        "https://purl.org/coar/notify"
    ],
    "id": "urn:uuid:82eaace6-3bf3-4b8b-b168-15d1a46fb668",
    "type": "Undo",
    "actor": {
        "id": "https://orcid.org/0000-0003-4405-7546",
        "name": "Some Author",
        "type": "Person"
    },
    "origin": {
        "id": "https://b2share.eudat.eu",
        "name": "EUDAT B2SHARE Web Repository",
        "inbox": "https://b2share.eudat.eu/inbox/",
        "type": "Service"
    },
    "object": {
        "id": "urn:uuid:78a30582-ef0f-11ed-a05b-0242ac120003",
        "type": "Offer",
        "actor": {
            "id": "https://orcid.org/0000-0003-4405-7546",
            "name": "Some Author",
            "type": "Person"
        },
        "origin": {
            "id": "https://b2share.eudat.eu",
            "name": "EUDAT B2SHARE Web Repository",
            "inbox": "https://b2share.eudat.eu/inbox/",
            "type": "Service"
        },
        "object": {
            "id": "https://b2share.eudat.eu/records/1c42a67a73e9424b8192ba65c81077e1",
            "ietf:cite-as": "https://doi.org/10.23728/b2share.1c42a67a73e9424b8192ba65c81077e1",
            "type": [
                "sorg:AboutPage",
                "sorg:Dataset"
            ]
        },
        "target": {
            "id": "https://archivalbot.data-stations.nl/",
            "inbox": "https://archivalbot.data-stations.nl/inbox/",
            "name": "DANS Archival Bot",
            "type": "Service"
        }
    },
    "target": {
        "id": "https://archivalbot.data-stations.nl/",
        "inbox": "https://archivalbot.data-stations.nl/inbox/",
        "name": "DANS Archival Bot",
        "type": "Service"
    }
}
```

<ol start="8">
	<li>The <code>as:Offer</code>in the LDN<code>ldp:inbox</code>of the <b>LTP Data Archive</b> is picked up by the <b>Archival Bot</b>  
	<li>The <b>Archival Bot</b> checks the validity of the <code>as:Offer</code>. It checks against known rules, like registered domain, RDF format/SHACL validation, etc. It will either accept (10) or reject (19) the<code>as:Offer</code>   
	<li>The <b>Archival Bot</b> sends an<code>as:Accept</code>notification to the LDN<code>ldp:inbox</code>of the <b>Web Repository</b>.
</ol>  

#### *as:Accept (10)*:

This payload, the as:object holds the original as:Offer message that is accepted and has a reference to the URI of the initial request (as:inReplyTo)

| Requirements | Properties                              |
|:-------------|:----------------------------------------|
| Required     | `@id`, `@type`, `as:actor`, `as:object` |
| Recommended  | `as:context`, `as:inReplyTo`            |
| Optional     | `as:origin`, `as:target`                |


```json
{
    "@context": [
        "https://www.w3.org/ns/activitystreams",
        "https://purl.org/coar/notify"
    ],
    "id": "urn:uuid:0cd58f07-69aa-4dd3-bc19-7b7de0f3550a",
    "type": "Accept",
    "actor": {
        "id": "https://archivalbot.data-stations.nl/",
        "inbox": "https://archivalbot.data-stations.nl/inbox/",
        "name": "DANS Archival Bot",
        "type": "Service"
    },
    "origin": { // superfluous? Leave out?
        "id": "https://archivalbot.data-stations.nl/",
        "inbox": "https://archivalbot.data-stations.nl/inbox/",
        "name": "DANS Archival Bot",
        "type": "Service"
    },
    "inReplyTo": "urn:uuid:78a30582-ef0f-11ed-a05b-0242ac120003",
    "context": "https://b2share.eudat.eu/records/1c42a67a73e9424b8192ba65c81077e1",
    "object": {
        "id": "urn:uuid:78a30582-ef0f-11ed-a05b-0242ac120003",
        "type": "Offer",
        "actor": {
            "id": "https://orcid.org/0000-0003-4405-7546",
            "name": "Some Author",
            "type": "Person"
        },
        "origin": {
            "id": "https://b2share.eudat.eu",
            "name": "EUDAT B2SHARE Web Repository",
            "inbox": "https://b2share.eudat.eu/inbox/",
            "type": "Service"
        },
        "object": {
            "id": "https://b2share.eudat.eu/records/1c42a67a73e9424b8192ba65c81077e1",
            "ietf:cite-as": "https://doi.org/10.23728/b2share.1c42a67a73e9424b8192ba65c81077e1",
            "type": [
                "sorg:AboutPage",
                "sorg:Dataset"
            ]
        },
        "target": {
            "id": "https://archivalbot.data-stations.nl/",
            "inbox": "https://archivalbot.data-stations.nl/inbox/",
            "name": "DANS Archival Bot",
            "type": "Service"
        }
    },
    "target": {
        "id": "https://b2share.eudat.eu",
        "name": "EUDAT B2SHARE Web Repository",
        "inbox": "https://b2share.eudat.eu/inbox/",
        "type": "Service"
    }
}
```
<ol start="11">
	<li>The <b>Web Repository</b> updates the status of the landingpage from &quot;Request Pending&quot; to &quot;Long Term Archiving in progress&quot;.    
	<li>The <b>Archival Bot</b> will retrieve the Link Set URL from the <b>Web Repository</b> landing page, by either HTTP header or HTML <head> of the landingpage URL, as is described by [Signposting]{target="_blank"}.  
	<li>The Link Set location is returned by the <b>Web Repository</b>.  
	<li>The <b>Archival Bot</b> retrieves the seriailized Link Set from the <b>Web Repository</b>.  
	<li>The <b>Archival Bot</b> retrieves the content resources from the <b>Web Repository</b> that are listed in the Link Set.    
	<li>The <b>Archival Bot</b> prepares and deposits all content resources to the the <b>LTP Data Archive</b> deposit endpoint.  
	<li><b>Archival Bot</b> sends an <code>as:Announce</code> notification to the LDN<code>ldp:inbox</code>of the <b>Web Repository</b> to inform about the creation of the archive artifact.
</ol>

#### *as:Announce (17)*:

In this payload, the as:object announces the creation of the archived artefact.

| Requirements | Properties                                               |
|:-------------|:---------------------------------------------------------|
| Required     | `@id`, `@type`, `as:actor`, `as:object`, `as:inReplyTo`  |
| Recommended  | `as:context`                                             |
| Optional     | `as:origin`, `as:target`                                 |


```json
{
    "@context": [
        "https://www.w3.org/ns/activitystreams",
        "https://purl.org/coar/notify"
    ],
    "id": "urn:uuid:4a6b8761-3365-4379-a2cf-1fb012f1c2d8",
    "type": "Announce",
    "actor": {
        "id": "https://archivalbot.data-stations.nl/",
        "inbox": "https://archivalbot.data-stations.nl/inbox/",
        "name": "DANS Archival Bot",
        "type": "Service"
    },
    "origin": { // superfluous? Leave this out?
        "id": "https://archivalbot.data-stations.nl/",
        "inbox": "https://archivalbot.data-stations.nl/inbox/",
        "name": "DANS Archival Bot",
        "type": "Service"
    },
    "inReplyTo": "urn:uuid:78a30582-ef0f-11ed-a05b-0242ac120003",
    "context": "https://b2share.eudat.eu/records/1c42a67a73e9424b8192ba65c81077e1",
    "object": {
        "id": "urn:uuid:CF21A499-1BDD-4B59-984A-FC94CF6FBA86",
        "type": "Relationship",
        "subject": "https://b2share.eudat.eu/records/1c42a67a73e9424b8192ba65c81077e1",
        "relationship": "http://www.iana.org/assignments/relation/archives", //TODO: is this the right link relation?
        "object": ["https://dans.knaw.nl/dd-vault-catalog/catalognumber123456", "https://www.persistent-identifier.nl/urn:nbn:nl:ui:13-r6a-812"] //TODO: Can we also relate to a PID?
    },
    "target": {
        "id": "https://b2share.eudat.eu",
        "name": "EUDAT B2SHARE Web Repository",
        "inbox": "https://b2share.eudat.eu/inbox/",
        "type": "Service"
    }
}
```

<ol start="18">
	<li>The <b>Web Repository</b> updates the status of the landingpage from 'Long Term Archiving in progress' to 'Long Term Archived', including a link to the archived artefact.    
	<li><b>Archival Bot</b> sends an <code>as:Reject</code> notification to the LDN <code>ldp:inbox</code> of the <b>Web Repository</b>.  
</ol>

#### *as:Reject (19)*:

This payload, the as:object holds the original as:Offer message that is rejected by the Archival Bot and has a reference to the URI of the initial request (as:inReplyTo)

| Requirements | Properties                              |
|:-------------|:----------------------------------------|
| Required     | `@id`, `@type`, `as:actor`, `as:object` |
| Recommended  | `as:context`, `as:inReplyTo`            |
| Optional     | `as:origin`, `as:target`                |

```json
{
    "@context": [
        "https://www.w3.org/ns/activitystreams",
        "https://purl.org/coar/notify"
    ],
    "id": "urn:uuid:2a74a606-42c8-4e26-88b9-0f14e7b79d82",
    "type": "Reject",
    "actor": {
        "id": "https://archivalbot.data-stations.nl/",
        "inbox": "https://archivalbot.data-stations.nl/inbox/",
        "name": "DANS Archival Bot",
        "type": "Service"
    },
    "origin": { // superfluous? Leave out?
        "id": "https://archivalbot.data-stations.nl/",
        "inbox": "https://archivalbot.data-stations.nl/inbox/",
        "name": "DANS Archival Bot",
        "type": "Service"
    },
    "inReplyTo": "urn:uuid:78a30582-ef0f-11ed-a05b-0242ac120003",
    "context": "https://b2share.eudat.eu/records/1c42a67a73e9424b8192ba65c81077e1",
    "object": {
        "id": "urn:uuid:78a30582-ef0f-11ed-a05b-0242ac120003",
        "type": "Offer",
        "actor": {
            "id": "https://orcid.org/0000-0003-4405-7546",
            "name": "Some Author",
            "type": "Person"
        },
        "origin": {
            "id": "https://b2share.eudat.eu",
            "name": "EUDAT B2SHARE Web Repository",
            "inbox": "https://b2share.eudat.eu/inbox/",
            "type": "Service"
        },
        "object": {
            "id": "https://b2share.eudat.eu/records/1c42a67a73e9424b8192ba65c81077e1",
            "ietf:cite-as": "https://doi.org/10.23728/b2share.1c42a67a73e9424b8192ba65c81077e1",
            "type": [
                "sorg:AboutPage",
                "sorg:Dataset"
            ]
        },
        "target": {
            "id": "https://archivalbot.data-stations.nl/",
            "inbox": "https://archivalbot.data-stations.nl/inbox/",
            "name": "DANS Archival Bot",
            "type": "Service"
        }
    },
        "id": "https://b2share.eudat.eu",
        "name": "EUDAT B2SHARE Web Repository",
        "inbox": "https://b2share.eudat.eu/inbox/",
        "type": "Service"
}
```
<ol start="20">
	<li>The <b>Web Repository</b> cleares the LTP status on the landingpage, because the <code>as:Offer</code> was not accepted by the <b>Archival Bot</b> because the business rules in (9) where not met.  
</ol>

Acknowledgements
----------------

!!! info "Aligned Projects"

    [Event Notifications in Value-Adding Networks]{target=_blank} <br />
    [COAR Notify Protocol](https://notify.coar-repositories.org/){target=_blank}

!!! info "Data Infrastructure Capacities for EOSC"

    The specifications for long-term-archiving notifications is carried out in the context of the [DICE project]{target="_blank"} (Data Infrastructure Capacities for EOSC), funded by the EU's Horizon 2020 project call H2020-INFRAEOSC-2018-2020 under Grant Agreement no. 101017207.  
    It is developed by Task 4.3: "Long Term Preservation", as part of the working package 4 (WP4): "Integration with other services & platforms", and published in the joint WP4 Deliverable: "D4.3 Final integration with other services & platforms".


[Signposting]: https://www.signposting.org/
[DICE project]: {{ hyperlink.ext.dice }}
[Event Notifications in Value-Adding Networks]: https://www.eventnotifications.net/
[COAR Notify]:https://notify.coar-repositories.org/