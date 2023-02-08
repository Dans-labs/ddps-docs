# DICE Digital Preservation Service


## Introduction
This document defines the general requirements for creating and using the DICE Digital Preservation Service (DDPS).
Technical specification and documentation may be found <u>here</u>.

The technical specification for long-term-archiving notifications are being developed by DICE Task 4.3: Long Term Preservation.  
It will make use the following open web standards:

* [Linked Data Notification](https://www.w3.org/TR/ldn/) (W3C) => Notification protocol
* [JSON-LD 1.1](https://www.w3.org/TR/json-ld/#introduction) (Serialisation)
* [Activity Streams 2 Core](https://www.w3.org/TR/activitystreams-core/) (W3C)
	* [ActivityStreams 2.0 Vocabulary](https://www.w3.org/TR/activitystreams-vocabulary)
	* [ActivityStreams 2.0 Terms](https://www.w3.org/ns/activitystreams)
* [Activity Vocabulary](https://www.w3.org/TR/activitystreams-vocabulary)
* [FAIR Signposting Profile](https://signposting.org/FAIR/)  => Navigational




Within this document, the following namespace prefix bindings are used:


| Prefix 		   | Namespace  |
|:------------- |:---------------|
| as     		   | https://www.w3.org/ns/activitystreams# |
|ldp	|http://www.w3.org/ns/ldp# |
| ddps     | http://some.example.org/ns/ddps# |

Examples of notification payloads use [JSON-LD] as syntax.  

## Activity Diagram

![](https://mermaid.ink/img/eyJjb2RlIjoic2VxdWVuY2VEaWFncmFtXG4gICAgYXV0b251bWJlclxuICAgIFxuICAgIGFjdG9yIGFsaWNlIGFzIEFsaWNlXG4gICAgcGFydGljaXBhbnQgcmVwbyBhcyBXZWIgUmVwb3NpdG9yeVxuICAgIHBhcnRpY2lwYW50IGJvdCBhcyBBcmNoaXZhbCBCb3RcbiAgICBwYXJ0aWNpcGFudCBhcmNoaXZlIGFzIExUUCBEYXRhIEFyY2hpdmVcblxuICAgIGFsaWNlLT4-cmVwbzogTG9naW4gb24gbGFuZGluZ3BhZ2VcbiAgICBhbGljZS0-PnJlcG86IFJlcXVlc3QgZm9yIExUUFxuICAgIHJlcG8tPj5hcmNoaXZlOiBTZW5kIChMRE4pIGFzMjpPZmZlciBub3RpZmljYXRpb24gPExhbmRpbmdwYWdlIHwgTGluayBTZXQ-XG4gICAgcmVwby0-PnJlcG86IFNldCBzdGF0dXM6IFwiTFRQIGluIHJlcXVlc3RcIlxuICAgIGxvb3AgUG9sbCBMRE4gaW5ib3hcbiAgICAgICAgYm90LT4-YXJjaGl2ZTogR2V0IChMRE4pIGFzMjpPZmZlclxuICAgIGVuZFxuICAgIGJvdC0-PmJvdDogQ2hlY2sgdmFsaWRpdHkgb2YgTEROIGFzMjpPZmZlclxuICAgIFxuICAgIGFsdCBWQUxJRDogQWNjZXB0IGFzMjpPZmZlclxuICAgICAgICBib3QtPj5yZXBvOiBTZW5kIChMRE4pIGFzMjpBY2NlcHRcbiAgICAgICAgcmVwby0-PnJlcG86IFVwZGF0ZSBzdGF0dXM6IFwiTFRQIGluIHByb2dyZXNzXCJcbiAgICBvcHQgTGFuZGluZ3BhZ2UgVVJMIG9ubHlcbiAgICAgICAgYm90LT4-cmVwbzogSFRUUCBIRUFEIChTaWducG9zdGluZylcbiAgICAgICAgcmVwby0tPj5ib3Q6IExpbmsgU2V0IExvY2F0aW9uXG4gICAgZW5kXG4gICAgYm90LT4-cmVwbzogSFRUUCBHRVQgTGluayBTZXQgKFNpZ25wb3N0aW5nKVxuICAgICUlbm90ZSByaWdodCBvZiBib3Q6IEhhXG4gICAgYm90LT4-cmVwbzogSFRUUCBHRVQgTGluayBTZXQgb2JqZWN0cyAoU2lnbnBvc3RpbmcpXG4gICAgYm90LT4-YXJjaGl2ZTogSFRUUCBQT1NUL1BVVCBEYXRhU2V0IG9iamVjdHNcbiAgICBib3QtPj5yZXBvOiBTZW5kIChMRE4pIGFzMjpBbm5vdW5jZVxuICAgIHJlcG8tPj5yZXBvOiBVcGRhdGUgc3RhdHVzOiBcIkxUUCBBcmNoaXZlZFwiXG5cbiAgICBlbHNlIElOVkFMSUQ6IHJlamVjdCBhczI6T2ZmZXJcbiAgICAgICAgYm90LT4-cmVwbzogU2VuZCAoTEROKSBhczI6UmVqZWN0XG4gICAgICAgIHJlcG8tPj5yZXBvOiBDbGVhciBMVFAgc3RhdHVzXG4gICAgZW5kXG4iLCJtZXJtYWlkIjp7InRoZW1lIjoiYmFzZSIsInRoZW1lVmFyaWFibGVzIjp7Im1haW5Ca2ciOiIjQjRCRkQ4IiwiYWN0b3JCa2ciOiIjRURGMUZDIiwiYWN0b3JCb3JkZXIiOiIjNjk3RkIyIiwiYWN0b3JUZXh0Q29sb3IiOiIjMkEzNzU3Iiwibm90ZVRleHRDb2xvciI6IiNGOEY4RjgiLCJub3RlQmtnQ29sb3IiOiIjMkEzNzU3IiwiZm9udFNpemUiOiIxNnB4In19LCJ1cGRhdGVFZGl0b3IiOmZhbHNlLCJhdXRvU3luYyI6dHJ1ZSwidXBkYXRlRGlhZ3JhbSI6ZmFsc2V9)

1. The user of the **Web Repository** needs to be loged in.
2. User hits "LTP" button on the landingpage of the dataset that he/she owns. Otherwise no button will be available.
3. The **Web Repository** sends a Linked Data Notification`as2:Offer`to the LDN`ldp:inbox`of the **LTP Data Archive**. The payload should hold the landingpage URL related to the Dataset. This way, associated resources of the dataset can be found by using FAIR Signposting discovery methods (9). If, for some reason, the landingpage URL is not available at this point, the URL of the Link Set must be supplied. This way the **Archival Bot** can directly access the serialized Link Set (11) holding all Typed Links, without using Signposting discovery methods.  
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
    "ddps:ReviewAction"
  ]
}
```
4. The **Web Repository** marks the landingpage of the dataset that a request for Long Term Archiving is <span style="font-family:Courier New; font-size:1.1em;">pending</span>. 
5. The`as2:Offer`in the LDN`ldp:inbox`of the **LTP Data Archive** is picked up by the **Archival Bot** 
6. **Archival Bot** determines if this`as2:Offer`is valid against known rules. (e.g: registered domain, etc). It will either accept(7) or reject(16) the`as2:Offer`
7. **Archival Bot** sends an`as2:Accept`notification to the LDN`ldp:inbox`of the **Web Repository**.  
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
8. The **Web Repository** updates the status of the landingpage from <span style="font-family:Courier New; font-size:1.1em;">request pending</span> to <span style="font-family:Courier New; font-size:1.1em;">Long Term Archiving in progress</span>. 
9. (...)


## Activities
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