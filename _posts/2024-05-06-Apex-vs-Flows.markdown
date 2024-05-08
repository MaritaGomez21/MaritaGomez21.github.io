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
 overlay_image: "/assets/images/HammerScrewBanner.jpg"
 teaser: "/assets/images/hammerscrew.jpg"
 
description: This is a brief example of Apex vs Flows and using the right tool for the job.
---
>"If all you have is a hammer, everything looks like a nail."
—Abraham Kaplan, Abraham Maslow

# ARTICLE UNDER CONSTRUCTION
With anything Salesforce there are multiple ways to provide a solution, the key is to provide a solution that is best for the user, business, and within generally accepted best practices. The solution is not always Apex nor always Flows or even automation.

## The Situation
In a hypothetical case the a sales manager would like a task assigned to the lead owner to follow up with the lead based on selected product interest. If the product interest is changed for an existing lead then assign a task to the lead owner. 

## The Approach
In Salesforce, the following are only two of many ways to automate the creation of a task 
* A record trigger flow
* Apex
To understand these 2 solutions of going either route (programmatic vs flows) I set up both utilizing separate developer orgs.

### The LeadTrigger, LeadTriggerHandler, UtilityClass, and LeadTriggerHandler Test
To keep in line with best practices, I set up a Lead Trigger to redirect records to their destined path of automation, Lead Trigger Handler to hold all the business logic, a Utility class to avoid having repetitive code ("DRY" aka don't repeat yourself!), and a Lead Trigger Handler Test class to not only meet Salesforce's minimum code coverage for deployments but to also make sure the code is working properly.

Follow this link to the sample code. [Link soon to come!]

### The Record Trigger Flow:
* A simple formula to set up the entry criteria for the flow when a Lead Record is Created or Updated.

```css

ISNEW() || ISCHANGED({!$Record.ProductInterest__c})

```
* A decision element to determine if the Product Interest was changed (a simple way to segregate new records
vs updated lead records).
* If the lead record is new, [ustomize the verbage]
* If the lead record was updated and the product interest was changed, then [use this verbage]


## The Results
In this specific scenario...

## Next Steps
[add details here]