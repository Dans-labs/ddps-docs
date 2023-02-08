DICE Digital Preservation Service Architecture
==============================

Overview
--------
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


```python
def fn():
    pass
```
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
