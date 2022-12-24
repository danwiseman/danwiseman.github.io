---
layout: post
title:  "Using Kafka to Distribute NiFi Tasks"
tags: nifi kafka
---

## What?

Lately I have been using Kafka to help distribute tasks between NiFi progress groups
rather than splitting the flow into each group. For instance, following file ingestion,
the file is saved and a JSON package is created with the file location and some date information.
This JSON package is sent to a kafka topic, for instance, ingestion-status, and is then picked up
by a NiFi consumer that logs this to MongoDB. It is also picked up by a NiFi consumer that grabs the
file and does it's extraction work.