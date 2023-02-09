# DICE Digital Preservation Service

## Introduction
This document defines the Functional and Technical requirements for creating and using the DICE Digital Preservation Service (DDPS).
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

| Prefix 		   | Namespace  |
|:------------|:---------------|
| `as`     		   | https://www.w3.org/ns/activitystreams# |
| `ldp`	        |http://www.w3.org/ns/ldp# |
| `ddps`        | http://some.example.org/ns/ddps# |
| `so`          | https://schema.org/|

Examples of notification payloads use [JSON-LD] as syntax.  


## Use cases
### 1. Single record archiving
A single record will be archived on demand, according to the LTP Policy.
### 2. Community's records
All records with a B2SHARE community will be auto-archived, according to a community archival agreement(?).

## Activity Diagram Single record archiving

![](https://mermaid.ink/img/eyJjb2RlIjoic2VxdWVuY2VEaWFncmFtXG4gICAgYXV0b251bWJlclxuICAgIFxuICAgIGFjdG9yIGFsaWNlIGFzIEFsaWNlXG4gICAgcGFydGljaXBhbnQgcmVwbyBhcyBXZWIgUmVwb3NpdG9yeVxuICAgIHBhcnRpY2lwYW50IGJvdCBhcyBBcmNoaXZhbCBCb3RcbiAgICBwYXJ0aWNpcGFudCBhcmNoaXZlIGFzIExUUCBEYXRhIEFyY2hpdmVcblxuICAgIGFsaWNlLT4-cmVwbzogTG9naW4gb24gbGFuZGluZ3BhZ2VcbiAgICBhbGljZS0-PnJlcG86IFJlcXVlc3QgZm9yIExUUFxuICAgIHJlcG8tPj5hcmNoaXZlOiBTZW5kIChMRE4pIGFzMjpPZmZlciBub3RpZmljYXRpb24gPExhbmRpbmdwYWdlIHwgTGluayBTZXQ-XG4gICAgcmVwby0-PnJlcG86IFNldCBzdGF0dXM6IFwiTFRQIGluIHJlcXVlc3RcIlxuICAgIGxvb3AgUG9sbCBMRE4gaW5ib3hcbiAgICAgICAgYm90LT4-YXJjaGl2ZTogR2V0IChMRE4pIGFzMjpPZmZlclxuICAgIGVuZFxuICAgIGJvdC0-PmJvdDogQ2hlY2sgdmFsaWRpdHkgb2YgTEROIGFzMjpPZmZlclxuICAgIFxuICAgIGFsdCBWQUxJRDogQWNjZXB0IGFzMjpPZmZlclxuICAgICAgICBib3QtPj5yZXBvOiBTZW5kIChMRE4pIGFzMjpBY2NlcHRcbiAgICAgICAgcmVwby0-PnJlcG86IFVwZGF0ZSBzdGF0dXM6IFwiTFRQIGluIHByb2dyZXNzXCJcbiAgICBvcHQgTGFuZGluZ3BhZ2UgVVJMIG9ubHlcbiAgICAgICAgYm90LT4-cmVwbzogSFRUUCBIRUFEIChTaWducG9zdGluZylcbiAgICAgICAgcmVwby0tPj5ib3Q6IExpbmsgU2V0IExvY2F0aW9uXG4gICAgZW5kXG4gICAgYm90LT4-cmVwbzogSFRUUCBHRVQgTGluayBTZXQgKFNpZ25wb3N0aW5nKVxuICAgICUlbm90ZSByaWdodCBvZiBib3Q6IEhhXG4gICAgYm90LT4-cmVwbzogSFRUUCBHRVQgTGluayBTZXQgb2JqZWN0cyAoU2lnbnBvc3RpbmcpXG4gICAgYm90LT4-YXJjaGl2ZTogSFRUUCBQT1NUL1BVVCBEYXRhU2V0IG9iamVjdHNcbiAgICBib3QtPj5yZXBvOiBTZW5kIChMRE4pIGFzMjpBbm5vdW5jZVxuICAgIHJlcG8tPj5yZXBvOiBVcGRhdGUgc3RhdHVzOiBcIkxUUCBBcmNoaXZlZFwiXG5cbiAgICBlbHNlIElOVkFMSUQ6IHJlamVjdCBhczI6T2ZmZXJcbiAgICAgICAgYm90LT4-cmVwbzogU2VuZCAoTEROKSBhczI6UmVqZWN0XG4gICAgICAgIHJlcG8tPj5yZXBvOiBDbGVhciBMVFAgc3RhdHVzXG4gICAgZW5kXG4iLCJtZXJtYWlkIjp7InRoZW1lIjoiYmFzZSIsInRoZW1lVmFyaWFibGVzIjp7Im1haW5Ca2ciOiIjQjRCRkQ4IiwiYWN0b3JCa2ciOiIjRURGMUZDIiwiYWN0b3JCb3JkZXIiOiIjNjk3RkIyIiwiYWN0b3JUZXh0Q29sb3IiOiIjMkEzNzU3Iiwibm90ZVRleHRDb2xvciI6IiNGOEY4RjgiLCJub3RlQmtnQ29sb3IiOiIjMkEzNzU3IiwiZm9udFNpemUiOiIxNnB4In19LCJ1cGRhdGVFZGl0b3IiOmZhbHNlLCJhdXRvU3luYyI6dHJ1ZSwidXBkYXRlRGlhZ3JhbSI6ZmFsc2V9)


1. The user of the **Web Repository** needs to be logged in.
2. User hits "LTP" button on the landingpage of the dataset that he/she owns. Otherwise no button will be available.
3. The **Web Repository** sends a Linked Data Notification`as2:Offer`to the LDN`ldp:inbox`of the **LTP Data Archive**. The payload should hold the landingpage URL (PID) related to the scholary object/Dataset. This way, associated resources of the dataset can be found by using FAIR Signposting discovery methods (9). If, for some reason, the landingpage URL/PID is not available at this point, the URL of the Link Set for this scholary object must be supplied. This way the **Archival Bot** can directly access the serialized Link Set (11) holding all Typed Links, without using Signposting discovery method(s).
```json
    {
      "@context": [
        "https://www.w3.org/ns/activitystreams",
        "https://purl.org/dice/ltp"
      ],
      "actor": {
        "id": "https://b2share/",
        "name": "repository.org",
        "type": ""
      },
      "id": "urn:uuid:0370c0fb-bb78-4a9b-87f5-bed307a509dd",
      "object": {
        "id": "https://research-organisation.org/repository/dataset/201203/421/",
        "ietf:cite-as": "https://doi.org/10.5555/12345680",
        "type": "sorg:AboutPage",
        "url": {
          "id": "https://research-organisation.org/repository/dataset/201203/421/content.pdf",
          "media-type": "application/pdf",
          "type": [
            "Dataset",
            "sorg:ScholarlyObject"
          ]
        }
      },
      "origin": {
        "id": "https://research-organisation.org/repository",
        "inbox": "https://research-organisation.org/repository/inbox/",
        "type": "Service"
      },
      "target": {
        "id": "https://sample.com/system",
        "inbox": "https://sample.com/system/inbox/",
        "type": "Service"
      },
      "type": [
        "Offer",
        "ddps:ArchiveAction"
      ]
    }
```

4. The **Web Repository** marks the landingpage of the scholary object/dataset that a request for Long Term Archiving is pending.    
5. The`as2:Offer`in the LDN`ldp:inbox`of the **LTP Data Archive** is picked up by the **Archival Bot**  
6. **Archival Bot** determines if this`as2:Offer`is valid against known rules. (e.g: registered domain, etc). It will either accept(7) or reject(16) the`as2:Offer`    
7. **Archival Bot** sends an`as2:Accept`notification to the LDN`ldp:inbox`of the <b>Web Repository</b>.  

<u>*Example JSON-LD payload*</u>:


```json
{
  "@context": [
    "https://www.w3.org/ns/activitystreams",
    "https://purl.org/dice/ltp"
  ],
  "actor": {
    "id": "https://b2share/",
    "name": "Some repo",
    "type": ""
  }, (...)
```

<ol start="8"><li>The <b>Web Repository</b> updates the status of the landingpage from request pending to Long Term Archiving in progress.    
<li>**OPTION** Signposting; The <b>Archival Bot</b> will request the Link Set URL from the **Web Repository** by either HTTP header or HTML <head> of the landingpage URL (PID).  
<li>The Link Set location is returned by the <b>Web Repository</b>.  
<li>The **Archival Bot** retrieves the seriailized Link Set from the <b>Web Repository</b>.  
<li>The **Archival Bot** retrieves the content resources from the <b>Web Repository</b> that are listed in the Link Set.    
<li>The **Archival Bot** prepares and sends all content resources to the the **LTP Data Archive**.  
<li>**Archival Bot** sends an `as2:Announce` notification to the LDN`ldp:inbox`of the <b>Web Repository</b>.  
<li>The <b>Web Repository</b> updates the status of the landingpage from Long Term Archiving in progress to Long Term Archived, including a link to the archive (?).    
<li>**Archival Bot** sends an `as2:Reject` notification to the LDN `ldp:inbox` of the <b>Web Repository</b>.  
<li>The <b>Web Repository</b> cleares the LTP status of the landingpage, because the as:Offer was not accepted by the **Archival Bot**.  
</ol>

## LDN Activities
A notification is sent by a actor to inform another actor about an activity. An Activity is some action that occurred, pertaining to a certain artefact in the network. Activities are described by the notification payload.

Notification payloads are expressed in [activitystreams-vocabulary] and use [JSON-LD] as default syntax (other RDF syntaxes are allowed as well). A payload is uniquely identified, indicates the type of activity it is describing, and includes some descriptive metadata about the activity.

### Types of activities
Notification payloads apply the [ActivityStreams 2.0 vocabulary](https://www.w3.org/TR/activitystreams-vocabulary). Therefore, the notification payload MUST be typed as an`as:Activity`or as one of its more specialized subtypes.  

|Activity Type | Context|
|:----|:----|
|[`as:Offer`](https://www.w3.org/TR/activitystreams-vocabulary#dfn-offer)| (...)|
|[`as:Accept`](https://www.w3.org/TR/activitystreams-vocabulary#dfn-accept)| (...)|
|[`as:Announce`](https://www.w3.org/TR/activitystreams-vocabulary#dfn-announce)| (...)|
|[`as:Reject`](https://www.w3.org/TR/activitystreams-vocabulary#dfn-reject)| (...)|
|`as:xxx`| (...)|

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
