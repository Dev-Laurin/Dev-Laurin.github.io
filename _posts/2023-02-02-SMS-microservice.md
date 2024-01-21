---
layout: post
author: Laurin
title: SMS Microservice
img: 
description: Creating a SMS microservice for OneLogin
tags: Javascript RabbitMQ NodeJS SMS
category: work
toc: false 
end_date: 2023-07-16
---

While working at OneLogin I was tasked with creating a way to send SMS otp codes through multiple SMS providers. The solution? Create a new microservice (or rather a worker) to handle SMS and pull the responsibility out of the monoliths. By decoupling functionality, we were building a microservice architecture that would be easier to maintain and allow efficient code-reuse.

I created a worker, using our internal middleware, to handle the RabbitMQ SMS exchange and allow our services and monoliths to send a simple request instead of re-implementing sending SMS code everywhere. This also allowed us to add new SMS providers other than Twilio easily, saving our customers millions of dollars. 

It's not to say that this project was without bumps though. Upon testing we found errors that would have ended up in production. I had some lessons reinforced in the process. 

1. Communication is key, no matter how embarassing finding bugs can be, you have to communicate quickly with your team and managers to get it fixed. 
2. Rushing into fixing bugs is a bad idea. Even if it's incredibly stressful, make sure you take the time to think things through, you don't want to introduce more bugs. 
3. Bugs happen, and having a mitigation plan is key to giving you time to fix those bugs. Having something as simple as a backup db or a way you can rollback, is mandatory for production. This is why version control and automated environment spin up is so useful.

The most severe bug we found was actually in our environment and was unrelated to the SMS code. It was preventing customers in certain regions from logging in. We rolled back the release and I proactively began troubleshooting to fix the issue. With help from the right people, I created a solution and tested it without interferring with production. The release then was able to go out only a day late. 

Other than the environment issue, we ended up fixing a lot of bugs before the code hit production (thank you QE for finding those!), but still had a few smaller ones after release. However, we worked with support closely and produced fixes quickly for the effected customers. 

Overall I learned a lot owning this worker/microservice (fixing bugs in production, RabbitMQ messaging, better logging for troubleshooting) and it reinforced the reasons behind why we do what we do (version control, logging, testing, controls around production). These things are rather obvious if you've been programming for awhile, but it always feels different when you experience it when something goes wrong. 