---
layout: post
title:  "Use CRON schedules when running on Docker"
tags: nifi
---

## Use CRONs

I run NiFi on a docker :whale: container at home, and have noticed that sometimes the container will
restart itself and can cause problems with processors that you have scheduled to run rarely, such as
24 hours.

When NiFi starts, it will run any processor that is set to run unless it is a CRON scheduled processor.
Therefore, if it restarts 10 minutes later, it will run those processors again even if they are
set to run 36 hours later.

![nifi schedule screenshot](/assets/images/kafka-nifi-posts/nifi-scheduling-screenshot.png)

I'm on version 1.19, so this may be not be the case in later versions on Docker. I don't think this is
a bug, and I think it is only a result of slightly lower performance of my home server.