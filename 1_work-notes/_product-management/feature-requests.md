---
title: "Feature Requests"
intro: ""
description: ""
tags: "product management, business analysis, business modelling, backlog, feature request, project request"
date: "2022-11-20"
---

### Feature Requests

Product Managers and Product Owners are often overloaded with feedback and off-the-cuff requests for new features from stakeholders and users. This can become distracting, and worse, can lead to stakeholders and users feeling unheard if they never hear follow-up on something they requested. 

#### Feature Request Document

A good way to solve feature request overload from users is to use a standardized feature request document/form, preferably a form that can be filled out and submitted online. 

If a feature request is made during a user or stakeholder interview, you should complete the form on their behalf, making sure to include them as the reporter so they receive any follow-up updates or questions. 

Ensure the user/stakeholder facing part of your feature request document is simple and easily filled-out, you want them to complete and submit it, not add barriers to idea generation. In my experience, things like market-fit, revenue potential, OKR/KPI, project vs. feature, and vetting demand are better answered by the product team (yes, you will need to do work on every feature request).

Rules I live by:

- **Do not** use a feature request document to "gatekeep" submissions
  - Keep them short and easy to fill out
  - Don't load it with Product specific jargon (eg. stay away from OKR's, KPI's, Lean Canvas)
- **Do** take a submitted feature requests and do analysis
  - Consider the feature request a hypothesis, you need to vet it
- **Do** let the stakeholder know the status
  - Is the feature being put into the backlog or roadmap? Tell them, and give them an indication as to its priority.
  - Is the feature not being pursued? Give them insight into why, you need to build trust and understanding.


##### Template

Keeping this simple, you'll want to collect

|Field | Description|
|-|-|
|Submitter Name: | Name of person submitting the request|
|Submitter Email: | Email of person submitting the request so you can reach them for follow-up |
|Product: | Preferably a drop-down of all the products |
|Title:| A title field |
|Description: | A longer description, give them enough room to lay out as much detail as they can | 
|Attachments: | Let them attach screenshots or supporting documents |


#### Vetting

Since we often get overloaded with feature requests, and since not every feature request should be built, we need a way to vet and prioritize them quickly. You can, and probably should, have a page where users can see and vote on existing feature requests, this helps you see what features engaged users care about.

On a regular cycle you need to review feature requests and determine which need to be added to your backlog or roadmap. Start with making some common-sense decisions, some questions you might ask yourself is if the request is:

- Already in the roadmap or backlog?
  - If yes, add any missing/relevant details to your existing item and close out the new request as a duplicate
- Big enough (effort wise) to be a project?
  - If yes, move it to a Project Request Form and close out the feature request, letting the requester know it's being considered as a project
- Addressing an accessibility issue?
  - I suggest anything that addresses accessibility should automatically be added to the backlog and bumped-up in priority, typically solving accessibility issues improves UX for all users which is always a win
- Antithetical to the product vision?
  - Tag these and use them to influence questions on your next survey, don't actively try to build them
- Small enough to absorb?
  - Sometimes the request is so small and self-contained that you can just add it to your backlog
    - You need to be careful with this, don't die by a thousand tiny cuts

That should leave you with the more difficult decisions, the feature requests you will need to investigate. When analyzing features, you want to look at:

- Complexity
  - Some feature requests are simple on the surface but would require massive investment to build, that is to say that there is no simple way to build and test them. These should be moved to a project request.
- Cost of maintenance (additional tests, logging, monitoring, etc)
  - The requested feature might sound great, but is it still great if it causes you maintenance costs to balloon without bringing in new users?
- Does it match any OKR's?
- Would it move the needle on any KPI's?

Once a feature request has made it this far, you could consider it a hypothesis and apply lean-startup to it:

1. Identify the problem that needs solving (done for you)
2. Create a hypothesis (mostly done for you)
3. Develop MVP
4. Get feedback from users
5. Iterate