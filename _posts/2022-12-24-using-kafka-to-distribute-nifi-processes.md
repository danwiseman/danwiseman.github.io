---
layout: post
title:  "Using Kafka to Distribute NiFi Tasks"
tags: nifi kafka
---

## A possible alternative to multiplying FlowFiles

Lately I have been using Kafka to help distribute tasks between NiFi progress groups
rather than splitting the flow into each group. For instance, following file ingestion,
the file is saved and a JSON package is created with the file location and some date information.
This JSON package is sent to a kafka topic, for instance, ingestion-status

![status to kafka flow](/assets/images/kafka-nifi-posts/flow-send-status-to-kafka.png)

After publishing to Kafka, a NiFi consumer that logs this to MongoDB. It is also picked up by a 
NiFi consumer that grabs the file and does its extraction work. I've found that this results in
less backpressure on flows the can complete relatively quickly. 

> It helps keep each process group independent and allowed to continue in their 
> own pace.

Doing this has also allowed me to send failure status messages to the database for later
investigation and retry processing without impacting successful operations.

