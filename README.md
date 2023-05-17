# dps-docs
Documentation site for the Digital Preservation Service (DPS).  

This work is carried out in the context of the [DICE project](https://www.dice-eosc.eu/) (Data Infrastructure Capacities for EOSC), funded by the EU's Horizon 2020 project call H2020-INFRAEOSC-2018-2020 under Grant Agreement no. 101017207. <br />
It is developed by Task 4.3: "Long Term Preservation", as part of the working package 4 (WP4): "Integration with other services & platforms", and published in the joint WP4 Deliverable: "D4.3 Final integration with other services & platforms".

Introduction
------------
Within the DICE project, task 4.3 created a Long Term Preservation (LTP) template and accompanying guidance that data services and repositories can use to formulate their own LTP policy.
The LTP policy should clarify to the users what is or can be guaranteed by the service, for how long and by whom.
The policy template contains articles that distinguish between outsourced services and services hosted in-house.  
This file documents the functional requirements and technical specifications for a service that implements such an LTP policy in which the archive is outsourced; the Digital Preservation Service (DPS).  
It is meant as a guide on how to implement an example long-term preservation Service between a short to midterm data (web)repository service and a long-term preservation (LTP) archive.  
The implementation adheres to documented community conventions for the use of [W3C Linked Data Notifications](https://www.w3.org/TR/ldn/) (LDN) and [Activity Streams 2](https://www.w3.org/TR/activitystreams-core/) (AS2) to integrate repository systems with long-term (LTP) archives, in a distributed, resilient and web-native architecture.  
The standards used, and the application profile documented here, are implementations of the generic patterns described by [Event Notifications in Value-Adding Networks](https://www.eventnotifications.net/), that details a profile for using Linked Data Notifications with ActivityStreams2 payloads in value-adding networks.  
The the [COAR Notify Protocol](https://notify.coar-repositories.org/) is strongly aligned with the Event Notifications in Value-Adding Networks Profile and provides notification patterns that are more specific implementations of the generic patterns described by Event Notifications in Value-Adding Networks.

