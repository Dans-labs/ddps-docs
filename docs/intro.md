# Digital Preservation Service

!!! warning "Living Document (WIP)"

    This document is currently **under development**, which means **"Work in Progress"**.  
	Don’t cite this document other than as work in progress.  
    It is carried out in the context of the [DICE project]{target="_blank"} (Data Infrastructure Capacities for EOSC), funded by the EU's Horizon 2020 project call H2020-INFRAEOSC-2018-2020 under Grant Agreement no. 101017207.


## Introduction
This document defines the Functional and Technical requirements for creating and using the Digital Preservation Service (DPS).
This document is work in progress.

The technical specifications for long-term-archiving notifications are being developed within DICE Task 4.3: Long Term Preservation.  
It will use the following open web standards:

* [Linked Data Notification](https://www.w3.org/TR/ldn/){target="_blank"}" (W3C) => Notification protocol
* [JSON-LD 1.1](https://www.w3.org/TR/json-ld/#introduction){target="_blank"} (Serialisation)
* [Activity Streams 2 Core](https://www.w3.org/TR/activitystreams-core/){target="_blank"} (W3C)
	* [ActivityStreams 2.0 Vocabulary](https://www.w3.org/TR/activitystreams-vocabulary){target="_blank"}
	* [ActivityStreams 2.0 Terms](https://www.w3.org/ns/activitystreams){target="_blank"}
* [Activity Vocabulary](https://www.w3.org/TR/activitystreams-vocabulary){target="_blank"}
* [FAIR Signposting Profile](https://signposting.org/FAIR/){target="_blank"} => Navigational


## Namespaces
Within this document, the following namespace prefix bindings are used:

| Prefix 	 | Namespace                              | Name                                      |
|:---------|:---------------------------------------|:------------------------------------------|
| `as2`    | https://www.w3.org/ns/activitystreams# | W3C ActivityStreams 2.0                   |
| `ldp`    | http://www.w3.org/ns/ldp#              | W3C Linked Data Platform (LDP) Vocabulary |
| `so`     | https://schema.org/                    | Schema.org                                |

Examples of notification payloads use [JSON-LD] as syntax.
In our example LDN+AS2 payloads we use [JSON-LD] as syntax. In these examples we don’t explicity write the prefixes.
The @context element in JSON-LD defines a mapping from the terms to [URI]-s.


## Use cases
### 1. Single record archiving
A single record will be archived on demand, according to the LTP Policy.
### 2. Community's records
All records with a B2SHARE community will be auto-archived, according to a community archival agreement(?).

## Activity Diagram Single Record Archiving

[![](https://mermaid.ink/img/pako:eNqtVdtO20AQ_ZXRVlFAoqqgLVCrQsqFFKQIolzoi1829jjZ4uy66zWCpvn3zvpC1o6RWqnkBe-ZmTM7lz1bFqgQmcc6na2Qwniw7aYYZFqYlzE-Ydz1oBsrlWL3BLpmjRvset0lz799lh88cC34MsbUZ-Tusw0Xsv-4oi-fvet_6o-Glz6z1jwwSr8i18PR6WjgIkqHqAvw_MvFqH_mgHN8NgMVqxI_6328-HxR4FIZbMCjS_vbw0T6hnOkpJmJX2hz99npefLss91u1-n4MsWfGcoAh4KvNN_4EuiPZ0bJbLOkRPPv8tSmCDwWAQJPoZeZtSoNEq6NCETCpQGNibL4d1zClP5PBbm9HNotlcnD6GAtnngMfWUOjXiO5nzj-QSG3PDSA31ZpmUTen91ZXk9GKuVkKAkxFyGQq4SvsI2u6m9d2ogoitR5MLEQmRBmXkwQxnC0Xh4d0zkZ959FKEGKrOIRMCNIIavi-mYCPc8v8dCPpKjuaqFKwjpGFLDTZbaHtjL6DKFBPMIPiu8VGJgwKklcZVkcX54h7pV_SrN69g7LGSoDtCqHCnl90ZeZd6FKx1WlaeVSYAqBEIu1fM-MhFWtBMVx02TPELDbrDG4BFoDERISwkqyp1eC18bw9jAQ298O4Qc8qAXBJiYpvGeoKp_rZ-F0xvVWCQhN9hoF41VotVKY5q6rbqN3BEAmol2_ps5xbi57g3haCZWkvbCkM9xI4OqHtUk0TwX09ZaOifyt-v53qmFodOxTwRosVobW96c5Yb_TTS1_IGBSduiFo7lkpa-k_vZ_MNkMc-X1fE_pGq2REqV0US3LE9rQ8p3ILTdKMsTpwi3d7XpmKJl_8fpKJz-z66wE7ZBTXoRkgJtLVBKSvEaW5mhV9o5b0hNMfqO4ICrOBXsyA64ulPHK_EBV31qJq7GgCsjlVVTiMBVItfIkaPWQG2iZLGdL3dUsyxv-XVo1YN5EafWnjArTLMXGTDP6Awro1K7SqvdH8l6frQ?type=png)](https://mermaid.live/edit#pako:eNqtVdtO20AQ_ZXRVlFAoqqgLVCrQsqFFKQIolzoi1829jjZ4uy66zWCpvn3zvpC1o6RWqnkBe-ZmTM7lz1bFqgQmcc6na2Qwniw7aYYZFqYlzE-Ydz1oBsrlWL3BLpmjRvset0lz799lh88cC34MsbUZ-Tusw0Xsv-4oi-fvet_6o-Glz6z1jwwSr8i18PR6WjgIkqHqAvw_MvFqH_mgHN8NgMVqxI_6328-HxR4FIZbMCjS_vbw0T6hnOkpJmJX2hz99npefLss91u1-n4MsWfGcoAh4KvNN_4EuiPZ0bJbLOkRPPv8tSmCDwWAQJPoZeZtSoNEq6NCETCpQGNibL4d1zClP5PBbm9HNotlcnD6GAtnngMfWUOjXiO5nzj-QSG3PDSA31ZpmUTen91ZXk9GKuVkKAkxFyGQq4SvsI2u6m9d2ogoitR5MLEQmRBmXkwQxnC0Xh4d0zkZ959FKEGKrOIRMCNIIavi-mYCPc8v8dCPpKjuaqFKwjpGFLDTZbaHtjL6DKFBPMIPiu8VGJgwKklcZVkcX54h7pV_SrN69g7LGSoDtCqHCnl90ZeZd6FKx1WlaeVSYAqBEIu1fM-MhFWtBMVx02TPELDbrDG4BFoDERISwkqyp1eC18bw9jAQ298O4Qc8qAXBJiYpvGeoKp_rZ-F0xvVWCQhN9hoF41VotVKY5q6rbqN3BEAmol2_ps5xbi57g3haCZWkvbCkM9xI4OqHtUk0TwX09ZaOifyt-v53qmFodOxTwRosVobW96c5Yb_TTS1_IGBSduiFo7lkpa-k_vZ_MNkMc-X1fE_pGq2REqV0US3LE9rQ8p3ILTdKMsTpwi3d7XpmKJl_8fpKJz-z66wE7ZBTXoRkgJtLVBKSvEaW5mhV9o5b0hNMfqO4ICrOBXsyA64ulPHK_EBV31qJq7GgCsjlVVTiMBVItfIkaPWQG2iZLGdL3dUsyxv-XVo1YN5EafWnjArTLMXGTDP6Awro1K7SqvdH8l6frQ)

1. The <b>Author</b> logs in into the landingpage of the dataset that it owns on the **Web Repository** (authorized user).
2. The authorized <b>Author</b> presses an archival-button, to start a Long Term Preservation (LTP) request for this dataset.
3. The **Web Repository** (DataNode) sends a Linked Data Notification (LDN) Offer`as2:Offer`to the LDN inbox`ldp:inbox`of the **Archival Bot**. The payload MUST hold the landingpage URL of the scholary object/dataset. All associated resources can be found by using FAIR Signposting discovery methods (12). If, for some reason, the landingpage URL/PID is not available at this point, the URL of the Link Set for this scholary object must be supplied. This way the <b>Archival Bot</b> can directly access the serialized Link Set (14) holding all Typed Links, without using Signposting discovery method(s).

*Example JSON-LD as2:Offer payload (3)*:

```json
{
    "@context": [
        "https://www.w3.org/ns/activitystreams",
        {"schema": "https://schema.org/"}
    ],
    "id": "urn:uuid:6E5FAF88-A7F1-47A4-B087-77345EBFF495",
    "type": "Offer",
    "actor": {
        "id": "https://acme.org/profile/card#us",
        "inbox": "https://acme.org/inbox/",
        "name": "ACME Research Institute",
        "type": "Organization"
    },
    "origin": {
        "id": "https://acme.org/system",
        "name": "ACME Research Institute System",
        "type": "Application"
    },
    "object": {
        "id": "http://acme.org/artifacts/alice/data-set-2022-01-19.zip",
        "type": [
            "Document",
            "schema:Dataset"
        ]
    },
    "target": {
        "id": "https://data.archive.xyz.net/",
        "inbox": "https://data.archive.xyz.net/inbox/",
        "name": "Data Archive XYZ",
        "type": "Organization"
    }
}
```


<ol start="4">
	<li>The <b>Web Repository</b> flags the status on the landingpage of the scholary object/dataset to &quot;LTP Request Pending&quot;.   
	<li>OPT: The <b>Author</b> cancels the request.
	<li>OPT: The <b>Web Repository</b> sends a Linked Data Notification (LDN) Undo<code>as2:Undo</code>the LDN inbox<code>ldp:inbox</code>of the <b>Archival Bot</b>.
	<li>OPT: The <b>Web Repository</b> cleares the LTP status on the landingpage, on behalf of the <b>Author</b>.
</ol>

*Example JSON-LD as2:Undo payload (6)*:


```
{
    "@context": [
        "https://www.w3.org/ns/activitystreams",
        {"schema": "https://schema.org/"}
    ],
    "id": "urn:uuid:70892B92-001E-40C8-B4E8-B70BBC334419",
    "type": "Undo",
    "actor": {
        "id": "https://acme.org/profile/card#us",
        "inbox": "https://acme.org/inbox/",
        "name": "ACME Research Institute",
        "type": "Organization"
    },
    "origin": {
        "id": "https://acme.org/system",
        "name": "ACME Research Institute System",
        "type": "Application"
    },
    "object": {
        "id": "urn:uuid:6E5FAF88-A7F1-47A4-B087-77345EBFF495",
        "type": "Offer",
        "actor": {
            "id": "https://acme.org/profile/card#us",
            "inbox": "https://acme.org/inbox/",
            "name": "ACME Research Institute",
            "type": "Organization"
        },
        "origin": {
            "id": "https://acme.org/system",
            "name": "ACME Research Institute System",
            "type": "Application"
        },
        "object": {
            "id": "http://acme.org/artifacts/alice/data-set-2022-01-19.zip",
            "type": [
                "Document",
                "schema:Dataset"
            ]
        },
        "target": {
            "id": "https://data.archive.xyz.net/",
            "inbox": "https://data.archive.xyz.net/inbox/",
            "name": "Data Archive XYZ",
            "type": "Organization"
        }
    },
    "target": {
        "id": "https://data.archive.xyz.net/",
        "inbox": "https://data.archive.xyz.net/inbox/",
        "name": "Data Archive XYZ",
        "type": "Organization"
    }
}
```

<ol start="8">
	<li>The <code>as2:Offer</code>in the LDN<code>ldp:inbox</code>of the <b>LTP Data Archive</b> is picked up by the <b>Archival Bot</b>  
	<li>The <b>Archival Bot</b> checks the validity of the <code>as2:Offer</code>. It checks against known rules, like registered domain, RDF format/SHACL validation, etc. It will either accept(10) or reject(19) the<code>as2:Offer</code>   
	<li>The <b>Archival Bot</b> sends an<code>as2:Accept</code>notification to the LDN<code>ldp:inbox</code>of the <b>Web Repository</b>.
</ol>  

*Example JSON-LD as2:Accept payload (10)*:


```json
{
    "@context": [
        "https://www.w3.org/ns/activitystreams",
        {"schema": "https://schema.org/"}
    ],
    "id": "urn:uuid:9C0ED771-B7F3-4A50-8A92-72DF63215BCB",
    "type": "Accept",
    "actor": {
        "id": "https://data.archive.xyz.net/",
        "inbox": "https://data.archive.xyz.net/inbox/",
        "name": "Data Archive XYZ",
        "type": "Organization"
    },
    "origin": {
        "id": "https://data.archive.xyz.net/system",
        "name": "XYZ Archiving Department",
        "type": "Application"
    },
    "inReplyTo": "urn:uuid:6E5FAF88-A7F1-47A4-B087-77345EBFF495",
    "context": "http://acme.org/artifacts/alice/data-set-2022-01-19.zip",
    "object": {
        "id": "urn:uuid:6E5FAF88-A7F1-47A4-B087-77345EBFF495",
        "type": "Offer",
        "actor": {
            "id": "https://acme.org/profile/card#us",
            "inbox": "https://acme.org/inbox/",
            "name": "ACME Research Institute",
            "type": "Organization"
        },
        "origin": {
            "id": "https://acme.org/system",
            "name": "ACME Research Institute System",
            "type": "Application"
        },
        "object": {
            "id": "http://acme.org/artifacts/alice/data-set-2022-01-19.zip",
            "type": [
                "Document",
                "schema:Dataset"
            ]
        },
        "target": {
            "id": "https://data.archive.xyz.net/",
            "inbox": "https://data.archive.xyz.net/inbox/",
            "name": "Data Archive XYZ",
            "type": "Organization"
        }
    },
    "target": {
        "id": "https://acme.org/profile/card#us",
        "inbox": "https://acme.org/inbox/",
        "name": "ACME Research Institute",
        "type": "Organization"
    }
}
```

<ol start="11">
	<li>The <b>Web Repository</b> updates the status of the landingpage from &quot;Request Pending&quot; to &quot;Long Term Archiving in progress&quot;.    
	<li>OPT: Signposting; The <b>Archival Bot</b> will request the Link Set URL from the <b>Web Repository</b> by either HTTP header or HTML <head> of the landingpage URL (PID).  
	<li>The Link Set location is returned by the <b>Web Repository</b>.  
	<li>The <b>Archival Bot</b> retrieves the seriailized Link Set from the <b>Web Repository</b>.  
	<li>The <b>Archival Bot</b> retrieves the content resources from the <b>Web Repository</b> that are listed in the Link Set.    
	<li>The <b>Archival Bot</b> prepares and sends all content resources to the the <b>LTP Data Archive</b>.  
	<li><b>Archival Bot</b> sends an <code>as2:Announce</code> notification to the LDN<code>ldp:inbox</code>of the <b>Web Repository</b>.
</ol>

*Example JSON-LD as2:Announce payload (17)*:


```
{
    "@context": [
        "https://www.w3.org/ns/activitystreams",
        {"schema": "https://schema.org/"}
    ],
    "id": "urn:uuid:ED0E06DA-4294-43C0-8E87-800558E4045B",
    "type": "Announce",
    "actor": {
        "id": "https://data.archive.xyz.net/",
        "inbox": "https://data.archive.xyz.net/inbox/",
        "name": "Data Archive XYZ",
        "type": "Organization"
    },
    "origin": {
        "id": "https://data.archive.xyz.net/system",
        "name": "XYZ Archiving Department",
        "type": "Application"
    },
    "inReplyTo": "urn:uuid:6E5FAF88-A7F1-47A4-B087-77345EBFF495",
    "context": "http://acme.org/artifacts/alice/data-set-2022-01-19.zip",
    "object": {
        "id": "urn:uuid:CF21A499-1BDD-4B59-984A-FC94CF6FBA86",
        "type": "Relationship",
        "subject": "http://acme.org/artifacts/alice/data-set-2022-01-19.zip",
        "relationship": "https://www.iana.org/memento",
        "object": "https://data.archive.xyz.net/data/memento/21daF1921"
    },
    "target": {
        "id": "https://acme.org/profile/card#us",
        "inbox": "https://acme.org/inbox/",
        "name": "ACME Research Institute",
        "type": "Organization"
    }
}
```

<ol start="18">
	<li>The <b>Web Repository</b> updates the status of the landingpage from Long Term Archiving in progress to Long Term Archived, including a link to the archive (?).    
	<li><b>Archival Bot</b> sends an <code>as2:Reject</code> notification to the LDN <code>ldp:inbox</code> of the <b>Web Repository</b>.  
</ol>

*Example JSON-LD as2:Reject payload (19)*:


```
{
    "@context": [
        "https://www.w3.org/ns/activitystreams",
        {"schema": "https://schema.org/"}
    ],
    "id": "urn:uuid:ED4CB09E-F74C-44E8-AA0D-BA74CDE0CDC7",
    "type": "Reject",
    "actor": {
        "id": "https://data.archive.xyz.net/",
        "inbox": "https://data.archive.xyz.net/inbox/",
        "name": "Data Archive XYZ",
        "type": "Organization"
    },
    "origin": {
        "id": "https://data.archive.xyz.net/system",
        "name": "XYZ Archiving Department",
        "type": "Application"
    },
    "inReplyTo": "urn:uuid:6E5FAF88-A7F1-47A4-B087-77345EBFF495",
    "context": "http://acme.org/artifacts/alice/data-set-2022-01-19.zip",
    "object": {
        "id": "urn:uuid:6E5FAF88-A7F1-47A4-B087-77345EBFF495",
        "type": "Offer",
        "actor": {
            "id": "https://acme.org/profile/card#us",
            "inbox": "https://acme.org/inbox/",
            "name": "ACME Research Institute",
            "type": "Organization"
        },
        "origin": {
            "id": "https://acme.org/system",
            "name": "ACME Research Institute System",
            "type": "Application"
        },
        "object": {
            "id": "http://acme.org/artifacts/alice/data-set-2022-01-19.zip",
            "type": [
                "Document",
                "schema:Dataset"
            ]
        },
        "target": {
            "id": "https://data.archive.xyz.net/",
            "inbox": "https://data.archive.xyz.net/inbox/",
            "name": "Data Archive XYZ",
            "type": "Organization"
        }
    },
    "target": {
        "id": "https://acme.org/profile/card#us",
        "inbox": "https://acme.org/inbox/",
        "name": "ACME Research Institute",
        "type": "Organization"
    }
}
```

<ol start="20">
	<li>The <b>Web Repository</b> cleares the LTP status on the landingpage, because the <code>as2:Offer</code> was not accepted by the <b>Archival Bot</b> because the business rules in (9) where not met.  
</ol>


## LDN Activities
A notification is sent by a actor to inform another actor about an activity. An Activity is some action that occurred, pertaining to a certain artefact in the network. Activities are described by the notification payload.

Notification payloads are expressed in [activitystreams-vocabulary] and use [JSON-LD] as default syntax (other RDF syntaxes are allowed as well). A payload is uniquely identified, indicates the type of activity it is describing, and includes some descriptive metadata about the activity.

### Types of activities
Notification payloads apply the [ActivityStreams 2.0 vocabulary](https://www.w3.org/TR/activitystreams-vocabulary). Therefore, the notification payload MUST be typed as an`as2:Activity`or as one of its more specialized subtypes.  

|Activity Type | Context|
|:----|:----|
|[`as2:Offer`](https://www.w3.org/TR/activitystreams-vocabulary#dfn-offer)| (...)|
|[`as2:Accept`](https://www.w3.org/TR/activitystreams-vocabulary#dfn-accept)| (...)|
|[`as2:Announce`](https://www.w3.org/TR/activitystreams-vocabulary#dfn-announce)| (...)|
|[`as2:Reject`](https://www.w3.org/TR/activitystreams-vocabulary#dfn-reject)| (...)|
|`as2:xxx`| (...)|

## B2SHARE Long Term Archiving Module

To be implemented. Main question here is how B2SHARE should preserve state of the archiving status of a scholary object?  
Two options may be recognized:
1. By polling the LT-Archive (B2SHARE must hold state of the LT-Archive location/identifier).
2. By reading it's own LDN-Inbox, which should be implemented in the LTA Module.

## B2SHARE Signposting Module 
Open Pull Request: https://github.com/EUDAT-B2SHARE/b2share/pull/1813  

According to the latest update of the [FAIR Signposting Profile](https://signposting.org/FAIR/), the `type` for a landingpage needs to be revised. It should contain both `so:AboutPage` as well as the type of the scholary work the `so:AboutPage` represents, i.e: `so:Dataset`.  
This way child content resources of the scholary object will inherit this `type` and do not explicitly need to declare it again (?).  
If the Link Set is discoverable by either HTTP HEAD or HTML <header> it will adhere to Signposting Level 1. To achief Level 2, the content resources need to expose a Link Set too, by using the HTTP Link header approach, which is not (yet) the case.  

[Open issue](https://docs.google.com/document/d/1UKK1Q6CIFRgdmcmxLoILVxEF9f2QHAqcRLVCuOoV0eE): Type (as Link relation Type) i.e. file description is not present in the B2SHARE (meta)data model. This element can therefore not be extracted and added to the linkset.  
Q: How can `type` be available from the output example below?

### B2SHARE Signposting Module output example

http://localhost:5000/api/linkset/7646043f7a784b5597e257e9f5d7450f/json

```json
{
  "linkset": [
    {
      "anchor": "http://localhost:5000/records/7646043f7a784b5597e257e9f5d7450f",
      "cite-as": [
        {
          "href": "https://doi.org/10.15497/A675341C-F705-4136-B7C3-B9C14B556186"
        }
      ],
      "describedby": [
        {
          "href": "https://citation.crosscite.org/format?style=bibtex&doi=10.15497/A675341C-F705-4136-B7C3-B9C14B556186",
          "type": "application/x-bibtex"
        }
      ],
      "item": [
        {
          "href": "http://localhost:5000/api/files/9d5cb5d6-9a5b-4819-bd45-48e9f7984ed0/myfile",
          "type": "application/octet-stream"
        },
        {
          "href": "http://localhost:5000/api/files/9d5cb5d6-9a5b-4819-bd45-48e9f7984ed0/myfile-ver0",
          "type": "application/octet-stream"
        },
        {
          "href": "http://localhost:5000/api/files/9d5cb5d6-9a5b-4819-bd45-48e9f7984ed0/myfile-ver1",
          "type": "application/octet-stream"
        },
        {
          "href": "http://localhost:5000/api/files/9d5cb5d6-9a5b-4819-bd45-48e9f7984ed0/myfile-ver2",
          "type": "application/octet-stream"
        },
        {
          "href": "http://localhost:5000/api/files/9d5cb5d6-9a5b-4819-bd45-48e9f7984ed0/myfile-ver3",
          "type": "application/octet-stream"
        }
      ],
      "license": {
        "href": "http://creativecommons.org/licenses/by/4.0/"
      },
      "type": [
        {
          "href": "https://schema.org/AboutPage"
        }
      ]
    },
    {
      "anchor": "http://localhost:5000/api/files/9d5cb5d6-9a5b-4819-bd45-48e9f7984ed0/myfile",
      "collection": [
        {
          "href": "http://localhost:5000/records/7646043f7a784b5597e257e9f5d7450f",
          "type": "text/html"
        }
      ]
    },
    {
      "anchor": "http://localhost:5000/api/files/9d5cb5d6-9a5b-4819-bd45-48e9f7984ed0/myfile-ver0",
      "collection": [
        {
          "href": "http://localhost:5000/records/7646043f7a784b5597e257e9f5d7450f",
          "type": "text/html"
        }
      ]
    },
    {
      "anchor": "http://localhost:5000/api/files/9d5cb5d6-9a5b-4819-bd45-48e9f7984ed0/myfile-ver1",
      "collection": [
        {
          "href": "http://localhost:5000/records/7646043f7a784b5597e257e9f5d7450f",
          "type": "text/html"
        }
      ]
    },
    {
      "anchor": "http://localhost:5000/api/files/9d5cb5d6-9a5b-4819-bd45-48e9f7984ed0/myfile-ver2",
      "collection": [
        {
          "href": "http://localhost:5000/records/7646043f7a784b5597e257e9f5d7450f",
          "type": "text/html"
        }
      ]
    },
    {
      "anchor": "http://localhost:5000/api/files/9d5cb5d6-9a5b-4819-bd45-48e9f7984ed0/myfile-ver3",
      "collection": [
        {
          "href": "http://localhost:5000/records/7646043f7a784b5597e257e9f5d7450f",
          "type": "text/html"
        }
      ]
    }
  ]
}
```

[DICE project]: {{ hyperlink.ext.dice }}
