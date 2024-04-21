---
title: Two-Pizza Government - Can the DevOps Model Fix America?
author: martin
date: 2024-04-21 01:00:00 
categories: [DevOps, Politics]
tags: [DevOps, Amazon, Politics]
---

![guardrails](./images/guardrails.jpg)

According to many surveys ([Gallup](https://news.gallup.com/poll/548120/record-low-satisfied-democracy-working.aspx), [Pew](https://www.pewresearch.org/politics/2022/06/06/americans-views-of-government-decades-of-distrust-enduring-support-for-its-role/), et al), most Americans have been unhappy with the current/projected future of the country for over 20 years. Additionally, the United States has been rated a flawed democracy [since 2017](https://www.washingtonpost.com/news/monkey-cage/wp/2017/02/23/yes-our-flawed-democracy-just-got-downgraded-heres-why/). Talk of secession by some states has become more popular, especially in [Texas](https://www.texasmonthly.com/news-politics/texas-secession-movement-abbott-border-security/) and [California](https://www.chicoer.com/2024/03/20/calexit-sentiment-might-be-on-the-upswing-california-focus/), but [across the US](https://today.yougov.com/politics/articles/48669-state-support-secession-alaska-texas-california-poll) as well. 

This data alone is concerning, but even more problematic is the absence of any signal that a reversal of these polls is possible. According to [one poll](https://www.monmouth.edu/polling-institute/documents/monmouthpoll_us_062023.pdf/), *68% of Republicans, the current party controlling the House of Representatives, think Biden won in 2020 because of voter fraud*. *[30%](https://www.cbsnews.com/news/jan-6-opinion-poll-republican-disapproval-wanes-2024-01-06/) of Republicans now approve of the rioters who forced their way into the Capitol*. Those numbers are going up, not down. *[25%](https://www.washingtonpost.com/dc-md-va/2024/01/04/fbi-conspiracy-jan-6-attack-misinformation/) now think the FBI orchestrated the riot.* 

For a few days after Jan 6, 2020, it seemed like the country might be able to turn a corner and unify. But hindsight being 20/20, it’s obvious now that the deep divide in America was not going to be fixed that easily. *[20%](https://time.com/4236640/donald-trump-racist-supporters/) of Trump supporters think freeing the slaves was a bad idea.* Slavery ended over 150 years ago. If that poll is accurate, it represents a significant philosophical and cultural divide between many Americans that is *never* going away.

Nearly everything is political now, even policies rooted in scientific evidence. This makes it impossible to get anything to get done. The result is that Republicans are now resigning from Congress en masse. And as far as I’m aware, there have been no proposals to fix the trajectory of the country. And if we’re all being honest, the trajectory is not looking good.

Therefore, I propose that we need to tweak how the United States is governed to ensure that we can continue to manage this large area of land as one entity, before things get even more bloody.

Fortunately, as an engineer working in software development for over 10 years, there’s an operational model that we’ve seen work in engineering that can be applied to the US Government.

In software development, there’s a practice called “[DevOps](https://en.wikipedia.org/wiki/DevOps)”. This methodology was used most famously by Amazon (before spreading across the industry) with their [two-pizza teams](https://martinfowler.com/bliki/TwoPizzaTeam.html). They were so called because they were small teams that were supposed to be fully accountable for their applications from end-to-end including: product management, marketing, and operations. The mantra for those teams is: “You build it, you run it”. DevOps is part of this strategy. It dictates that product software **Dev**elopers are fully responsible for the **Op**erations of their applications.

So what does this have to do with the US Government? One of the benefits of this strategy is it creates more decentralized teams and reduces the possibility of monolithic applications and teams. Reading between the lines, you might be screaming: *“So basically just states rights vs a large central government? This isn’t a new argument”*. Yes and no. 

The traditional “states rights” argument is generally just people arguing where to draw the line between state governments and the federal government: “Where should abortion laws be set?”, “Who should set education curriculum?”, “What about health care?”, etc, etc.

DevOps says that a central team should own *none* of the infrastructure of the development teams. But that doesn’t mean there’s no central teams (read: Federal government) at all. On the contrary, it just changes their responsibilities. Now instead of controlling everything, they have two main responsibilities:
1. Set security and other operational guardrails to ensure that development teams are meeting the standards of the business
2. Building tooling, blueprint, and common services to help reduce the overhead on development teams from having to duplicate the same non-business related operations

So what does this look like in the context of a government?

Let’s start with the base position: States would be free to set whatever laws they want and implement anything they want. For the most part, there’d be few federal laws dictating what they have to do. Instead, the federal laws that would be in place would be to set *base standards* that all states would be expected to meet, as agreed upon by Congress. Some examples:
- **Standard: Abortion rates must be below a certain level.**
	- Some states would choose to implement this as banning abortions
	- Some states would choose to meet this as more access to birth control or other health services
	- Some states might take a middle ground approach
- **Standard: Unemployment must be below a certain level**
	- Some states might choose to meet this by providing more unemployment services 
	- Some states might make a fine for those earning under a certain amount on their tax returns
- **Standard: High school graduation rates above required threshold**
	- Some states might choose to build more free public schools
	- Some states might want to provide more financing to charter schools
	- Some states might choose to provide no public schools and give people back the tax dollars to spend on their own schools

I think you get the idea. These same concepts could be applied to violent crime rates, health care, etc. The point is that the implementation is left to the states, but that all states are required to meet the agreed upon standards for the country.

Beyond setting standards, the central government would also need to provide *optional* “common services”. Health care is a good example here. The Affordable Care Act (i.e. Obamacare), is an optional health care marketplace. States can opt-in if they choose. However, its value as a marketplace might seem obscure to most Americans. What if instead of having a centrally managed marketplace, we had an optional centrally managed health care service. How would that get created and how would that get consumed?

Let’s first look at how that would work in a standard enterprise company. First, a central IT team might get requests from numerous business units for a specific capability, let’s say video conferencing. The IT team would then go and handle the research, procurement/building, and operations of such a system, with input from the business unit stakeholders. Then, once flipped on, the IT team could then “charge” the business units for their use of that system. Other business units who have their own video conferencing system would be unaffected and could continue using it if they desired. (Ok, maybe multiple video conferencing solutions in a company is a bad example, but you get the point).

In government, something similar could happen. A number of states could get together and decide they would like a team in the Federal government to manage a health care system for them. The Federal government would then either build such a system, or find an “approved vendor” to run such a system, managed by the Federal government. The team inside the Federal government running this system would be responsible for the profit and loss of this system just like any commercial entity would. Therefore, they’d have to make sure to have customer agreements “i.e. states” before turning such a system on. States could then join or leave this system just as any other health care system. States that don’t participate, would not be on the hook for any part of the cost of this health care system. States that do participate could then choose to turn around and tax their constituents as needed.

## Conclusion
There’s obviously a lot that would have to be worked out here including determining how standards are defined, and ensuring metrics aren’t being manipulated. However, these are all problems that have been solved over and over in enterprises across America and can be solved for America itself as well.

This will be a large undertaking and not require a lot of collaboration. But at the end of it, it should require *less* of the need for 100% agreement between the states as are expected of them today (or the 60% votes in congress). 

Given the growing fragility of the country, and lack of alternate proposals for change other than empty campaign speeches, doesn’t it seem worth trying?

