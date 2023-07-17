---
layout: post
author: Laurin
title: SMS Microservice
img: assets/images/.png
description: Creating a SMS microservice for OneLogin
tags: Javascript RabbitMQ NodeJS SMS
category: work
---

While working at OneLogin I was tasked with creating a way to send SMS otp codes through multiple SMS providers. The solution? Create a new microservice (or rather a worker) to handle SMS and pull the responsibility out of the monoliths. By decoupling functionality, we were building a microservice architecture that would be easier to maintain and allow efficient code-reuse.

I created a worker, using our internal middleware, to handle the RabbitMQ SMS exchange and allow our services and monoliths to send a simple request instead of re-implementing sending SMS code everywhere. This also allowed us to add new SMS providers other than Twilio easily, saving our customers millions of dollars. 

It's not to say that this project was without bumps though. Upon testing we found errors that would have ended up in production. I learned some lessons in the process. 

1. During this time I learned communication was key, no matter how embarassing finding bugs can be, you have to communicate quickly with your team and managers to get it fixed (I already knew that, but implementing it can be tough). 
2. I also learned that rushing into fixing bugs is a bad idea. I ended up introducing new bugs because I didn't slow down to think things through thoroughly (Also knew that, but really felt it through experience). Even if it's incredibly stressful, make sure you take the time to think things through. 
3. Bugs happen, and having a mitigation plan is key to giving you time to fix those bugs. Having something as simple as a backup db or a way you can rollback, is mandatory for production. This is why version control and automated environment spin up is so useful.

The biggest bug we found was actually in our environment and was unrelated to the SMS code. It was preventing customers in certain regions from logging in. We rolled back the release and I proactively began troubleshooting and fixing the issue. With help from the right people, I created a solution and tested it without interferring with production. The release then was able to go out only one day late. 

Other than the environment issue, we ended up fixing a lot of bugs before the code hit production, but still had a few smaller ones after release. However, we worked with support closely and produced fixes quickly for the effected customers. 

Overall I learned a lot owning this worker/microservice (fixing bugs in production, RabbitMQ messaging, better logging for troubleshooting) and it was a lot of fun creating and integrating it into our system.