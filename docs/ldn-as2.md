Overview
========
DDPS notifications are designed to be sent and received using the W3C Linked Data Notifications (LDN) standard. Payloads have a predictable structure, based primarily on Activity Streams 2.0, with some additional vocabularies included for particular properties.    
The notification patterns used for this application, are more domain-specific implementations of the generic patterns described by [Event Notifications in Value-Adding Networks](https://www.eventnotifications.net/){taget="_blank"}.  
An LDN+AS2 notification MUST specify an activity type, expressed in JSON-LD as @type or shortened as type, and its value MUST be the type of AS2 Activity that it describes. Only the subset of AS2 Activity Types shown here are supported:


The activity must contain the following properties:

 * `@context`: This is the JSON-LD 'context' for the activity.
 * `id`: This must be a URI, and the use of URN:UUID is recommended. An HTTP URI may be used, but in such cases the URI should resolve to a resource which represents the activity.
 * `type`: This should include one of the Activity Stream 2.0 Activity Types. It may (depending on the activity) also include a type from the Notify Activity Types vocabulary
 * `origin`: The originator of the activity, typically the service responsible for sending the notification.
 * `object`: This should be the focus of the activity. Other object properties may appear in notifications, as properties of other properties.
 * `target`: The intended destination of the activity, typically the service which consumes the notification.
 
The activity property may (and often will) contain the following properties:

 * `actor`: This identifies the party or process that initiated the activity.
 * `inReplyTo`: This property is used when the notification is a direct response to a previous notification (usually a request) and references the Activity Streams 2.0 activity id of the previous notification.
 * `context`: This identifies another resource which is relevant to understanding the notification.




AS2 Activities that express the state of an Artifact: as:Create, as:Update, as:Remove, as:Announce:  

 * `as:Create`: An Agent created an Artifact that is made available by a Data Node.
 * `as:Update`: An Agent updated an Artifact that is made available by a Data Node.
 * `as:Remove`: An Agent deleted an Artifact that is made available by a Data Node.
 * `as:Announce`: An Agent announces the existence of an Artifact that is made available by a Data Node. Unlike as:Create, which conveys when an Artifact was created, as:Announce merely conveys its existence.

AS2 Activities that pertain to applying value-adding services to an Artifact: as:Offer, as:Accept, as:Reject, as:Announce, and as:Undo:  

 * `as:Offer`: An Agent offers an Artifact to another Agent in order to request the provision of a service.
 * `as:Accept`: An Agent accepts to provide a service that was requested for a specific Artifact by another Agent. This is a reply to a previously received as:Offer.
 * `as:Reject`: An Agent declines to provide a service that was requested for a specific Artifact by another Agent. This is a reply to a previously received as:Offer.
 * `as:Announce`: An Agent announces a Service Result pertaining to an Artifact that is either the result of executing a previously requested service or is volunteered.
 * `as:Undo`: An Agent retracts a prior activity of type as:Offer, as:Accept, as:Reject, or as:Announce.

In addition to these AS2 Activity Types, types ([URI]s) originating from vocabularies chosen by an application domain MAY be specified.  
For `as:object`, one of the core Object Types MUST be expressed. In addition to these Object Types, types ([URI]s) originating from vocabularies chosen by an application domain MAY be specified.  
Both `as:actor`, `as:origin`, and `as:target` SHOULD have an LDN Inbox. The [URL] of the LDN Inbox:  
 * Can be provided as the value of ldp:inbox in the description of these entities in the notification payload;
 * Can be discovered as the link target of a link with the http://www.w3.org/ns/ldp#inbox link relation type provided in the HTTP Link response header of the [URL] of the LDN Inbox.


When sending a notification to a Data Node that pertains to one of the Artifacts it makes available, the LDN+AS2 notification SHOULD include the as:context property and, when included, MUST at least convey the Artifact’s [URL] as its value.  

An LDN+AS2 notification that is sent in response to a previously received notification, MUST include the as:inReplyTo property, and its value MUST be the activity identifier (value of the id property) of the previous notification.  

Data Node requests service
--------------------------
The requirements regarding properties are summarized in the table below and their use is subject to the guidelines provided in [§5 Properties in LDN+AS2 Notifications](https://www.eventnotifications.net/#Activities){target="_blank"}.

```json
{ 
    "@context": [ 
      "https://www.w3.org/ns/activitystreams" ,
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
       "type": [ "Document" , "schema:Dataset" ]
    },
    "target": {     
       "id": "https://data.archive.xyz.net/",
       "inbox": "https://data.archive.xyz.net/inbox/",
       "name": "Data Archive XYZ",
       "type": "Organization"
    }
  }


```

Service Node acknowledges a service request
-------------------------------------------
### Accept
An Agent operating on behalf of a Service Node can send a notification to an Agent operating at the end of a Data Node to acknowledge the receipt of a service request and to indicate whether the service will actually be provided.  
The Data Archive XYZ (Service Node) notifies the ACME Research Institute (Data Node) in a request-response pattern that it **accepts** the offer ACME sent in a previous activity notification.
```json
{ 
    "@context": [ 
      "https://www.w3.org/ns/activitystreams" ,
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
    "inReplyTo" : "urn:uuid:6E5FAF88-A7F1-47A4-B087-77345EBFF495" ,
    "context" : "http://acme.org/artifacts/alice/data-set-2022-01-19.zip" ,
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
           "type": [ "Document" , "schema:Dataset" ]
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
### Reject
The Data Archive XYZ (Service Node) notifies the ACME Research Institute (Data Node) in a request-response pattern that it **rejects** the offer ACME sent in a previous activity notification. 
```json
{ 
    "@context": [ 
      "https://www.w3.org/ns/activitystreams" ,
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
    "inReplyTo" : "urn:uuid:6E5FAF88-A7F1-47A4-B087-77345EBFF495" ,
    "context" : "http://acme.org/artifacts/alice/data-set-2022-01-19.zip" ,
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
           "type": [ "Document" , "schema:Dataset" ]
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

Service Node provides Service Result
------------------------------------
The Service Node has a Service Result available pertaining to the Artifact on the Data Node. The Service Node sends an Announce notification to the Data Node about this fact.
```json
{ 
    "@context": [ 
      "https://www.w3.org/ns/activitystreams" ,
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
    "inReplyTo" : "urn:uuid:6E5FAF88-A7F1-47A4-B087-77345EBFF495" ,
    "context" : "http://acme.org/artifacts/alice/data-set-2022-01-19.zip" ,
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

Data Node cancels prior service request
---------------------------------------
Data Node sends a notification with activity type `as:Undo` to a Service Node canceling its previous Offer notification.
```json
{ 
    "@context": [ 
      "https://www.w3.org/ns/activitystreams" ,
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
            "type": [ "Document" , "schema:Dataset" ]
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