---
title: Microservices - Hell’s Kitchen Nightmares Edition
author: martin
date: 2024-01-13 16:30:00 
categories: [Microservices]
tags: [Microservices, Cloud, Architecture, Scaling, Distributed]
---

![well oiled kitchen](./images/working-kitchen.webp)

Let’s talk about kitchens, specifically restaurant kitchens. They’re a textbook example of efficiency and speed perfected. A key element of this speed and efficiency is how they’re broken down into areas that specialize in different domains. It  starts with the very beginning of the meal creation process with prep chefs and continues onto different areas such as butchers, grill chefs, and more...all the way through to pastry chefs for dessert. 

Just as important as the chef’s specialized skills, is the workspace itself is specially designed to serve the needs of that domain. And of course, the chefs have 100% ownership and accountability of their space. They decide the kitchen equipment they need, and ensure it’s well taken care of to keep it running smoothly. 

All these chefs and unique sections of the kitchen work together in a well choreographed dance to get you a delicious multi-course meal. These patterns are well established in the food industry, and no one would build a large restaurant without taking this design into account. There’s a good reason, it’s because they work well and provide an overall better product for customers and better work environment for kitchen staff.

Over the past 15-20 years, the tech industry has taken this model and applied it to building web applications using microservices. The idea of making things smaller, more discrete, and therefore more manageable is not really a new idea. It’s a pattern Linux has been using effectively since the beginning with its command line tools. Microservices simply take that design and bring it up the stack to the application layer. 

However, to hear it from DHH (creator of Ruby and Basecamp), microservices are dying because they’re a terrible idea and no one other than a few big tech companies should be implementing them. I won’t boost his SEO rankings and link to his posts here, you can find them if you want, but the gist of it is that distributed computing is hard and requires tooling, skills, money, and use-cases that only the largest tech companies have/need. He asserts that most companies don’t need that level of complexity and should only deploy monoliths. 

The catalyst for his post was [this article](https://www.primevideotech.com/video-streaming/scaling-up-the-prime-video-audio-video-monitoring-service-and-reducing-costs-by-90) from the Prime Video team discussing a change in their architecture from serverless Step Functions to containers. To begin with, I would argue that the article itself incorrectly uses the term "monolith" Taking a few microservices hooked up to AWS Step Functions and combining them into a single container may or many not technically be a monolith, but it’s definitely not a monolith in the way the industry thinks about them (think: massive Rails apps like GitHub, Shopify, etc).

I won’t spend anymore time talking about DHH, but there is one concern that he raised that is not entirely off base and worth addressing.

For the purpose of this discussion, let’s set aside any discussions about specific monolith vs microservices as it relates to specific applications and whether it’s a good fit from an architecture perspective (performance, etc). Instead let’s take a best case scenario and imagine we have an engineering team that has determined microservices are a perfect fit for them and they’d love to get started building some. What they may or may not know, is this team now has a lot of work ahead of them.

## No CAP, All Tooling

Your first instinct might be to say "distributed computing is hard" and point to all the academic articles about how hard distributed computing is. However, from personal experience and observing the industry, many of the struggles with microservices come well before we even get to [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem).

### Builder Tooling

The problems start from the very beginning on the developer’s machine, continue on through CI/CD, and persists through service operation. Let’s itemize what it takes to build a new microservice from scratch.

First we need frameworks to cover the following areas:
- API business logic - Spring (Java), ASP.NET, NestJS, etc
- Testing
- Linting
- Build packaging
- Infrastructure as code

Then we need a number of services:
- CI/CD server(s)
- Application servers
- Database servers (managed or unmanaged)
- Logging
- Tracing
- Alerting/Error monitoring
- End user monitoring
- Performance/resource utilization dashboards

All of this, and that’s just for our first service. Now what happens when we need our second service?

Now engineering teams are looking at having to replicate this entire stack over to another service, if nothing else, that involves even more time. However in many/most cases, there’s more to it than that. These teams probably will need their services to communicate in some way. 

### Intra-service Communication

With service integration needs, we’ve now added the following requirements:
- Service discovery (DNS, Zookeeper, Consul, etc)
- Service to service authorization (I see you trying to give open access just because your servers are on the same internal network)
- Cross-service tracing/monitoring
- Integration testing from both local environments and as a pre-prod gate
- Event driven architecture integration and observability
- Service versioning standards (and strong practices)

#### Story Time: Intra-service challenges

Early in my cloud career, I worked for a large financial enterprise company helping them start their cloud journey migrating an on-prem .NET monolith to AWS microservices. This was circa 2015, when microservices tooling was still quite immature. Docker was barely a thing, and the best tooling available was still the open source components from Netflix's tech stack. 

Besides struggling with building all the tooling from scratch (see above), we ran into many challenges with building, deploying, and monitoring cross-service features and dependencies. We found ourselves having to deploy the entire suite of microservices that composed the application, all at once, at the end of every sprint. As you can imagine, this resulted in much system instability every time services were promoted to new environments. The severe lack of stability resulted in our front-end lead suggesting that we should tag all of our microservices on every deploy to prod and track them all collectively as one, ironically, monolithic version. In the famous words: "It was at this moment that we knew, we f'ed up."

We had been treating our microservices as a monolith while attempting to deploy them as individual components. Coincidentally, I heard a similar story from one of our partners at the time during their microservices journey. And I've heard the story repeated many times since then by other engineering teams.

It's so important to treat each service as a completely isolated component. It needs to be able to be tested and deployed that way too. That means it needs strong versioning practices, such as [semantic versioning](https://semver.org/), and strong integration testing practices to ensure API contracts are not broken between releases. 

## The Biggest Gaps

In theory, there are solutions in the market to address this entire list. In practice, the coverage is not even close to 100%. I won’t go through the entire list but there are some notable gaps.

### Project (repo) management

Historically, tools such as [CookieCutter](https://cookiecutter.readthedocs.io/en/stable/) have attempted to solve the profliferation of repos to support microservices. However, these are one and done solutions. Recently a new tool has come on the scene called [Projen](https://projen.io) that attempts to abstract repo configuration into a global tool and published as a package in a central artifact repo. More tools like this will be needed to support multi-repo microservice designs.

### User authorization

You might be screaming at the screen saying "OAuth2!". OAuth2 does a fine job of authentication, but comes up short at authorization. OpenID tokens attempted to resolve some of these deficiencies, however it’s still only scratching the surface for requirements.

A tool like the [Open Policy Agent](https://www.openpolicyagent.org) is really the best example of attempting to address what’s needed. However, as of the last time I checked, implementation is still complicated and adoption in application frameworks is still mostly non-existent. From a developer experience perspective, the [OPA policy syntax](https://www.openpolicyagent.org/docs/latest/#example) really pales in comparison to something like [Django permissions](https://docs.djangoproject.com/en/5.0/topics/auth/default/#the-permission-required-decorator). This makes the arguments for microservices even more challenging.

### Infrastructure as code

It might be surprising to see this called out given how long IaC has been around, but this is still a major pain point. Correctly configuring cloud services still requires a lot of specialized skills. Even for those with required skills, the most common framework for IaC, Terraform, is a significant amount of code for a basic service. This does vary by cloud provider, but regardless, it’s a heavy lift for a new service.

The lone bright spot here is the AWS CDK with its powerful L2 and L3 constructs and developer friendly language compatibility.

### Observability

I’m going to bundle this into one section, because I think this can be summed up quite simply. Technically, there’s tooling out there that can cover most, if not all observability and instrumentation needs. However, even within a single observability tool, such as Datadog, it’s still a lot of work to configure it correctly (alarms, metrics, etc) and create a single pane of glass.

## What’s the solution?

Coming back to the kitchen example, we know this is solvable given enough time and investment. However, given my most recent discovery and experience with the game Overcooked, I won’t be so overzealous to say it’s an *easy* problem. But step one is acknowledging we have a problem and shining a light on potential gaps and solutions for investment to happen.

All that said, even with the heavy initial lift, microservices still offer a better overall application architecture and engineering experience for any team over 5 people. And the more we build, the more we can help people building tooling create better solutions for us. In the meantime, let’s not throw out the distributed kitchens with the burnt pizzas.

![kitchen on fire](./images/kitchen-on-fire.gif)
