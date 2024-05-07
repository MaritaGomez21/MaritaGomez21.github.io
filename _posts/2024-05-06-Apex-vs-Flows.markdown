---
layout: posts
title:  "Apex vs. Flows"
date:   2024-05-06 15:48:21 +0000
tagline: "Resourceful"
tags: [Salesforce, Perspective Taking]
author_profile: true
author: Marita Gomez
categories: [article]
highlight_home: true
header:
 overlay_image: "/assets/images/hammerscrew.jpg"
 teaser: "/assets/images/hammerscrew.jpg"
 
description: This is a brief example of Apex vs Flows and using the right tool for the job.
---
>"If all you have is a hammer, everything looks like a nail."
—Abraham Kaplan, Abraham Maslow

#ARTICLE UNDER CONSTRUCTION

# The Situation
A real use case for automations is to automatically create a task for the lead owner to follow up with the new lead based on the product interest or when the lead was updated based on a product change. This business request can be solved with either a record trigger flow or Apex. To understand the approach of using Apex vs Flows I did both but in 2 seperate developer orgs.

## The Approach
[add details here]

### The LeadTrigger, LeadTriggerHandler, UtilityClass, and LeadTriggerHandler Test
[add details here]

### The Record Trigger Flow included the following features:
* A simple formula to set up the entry criteria for the flow when a Lead Record is Created or Updated.
* A decision element to determine if the Product Interest was changed (a simple way to segregate new records
vs updated lead records).
* If the lead record is new, [ustomize the verbage]
* If the lead record was updated and the product interest was changed, then [use this verbage]


## The Results
In this specific scenario...

## Next Steps
[add details here]