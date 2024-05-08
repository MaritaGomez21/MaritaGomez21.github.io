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
In Salesforce, the following are two examples of how to solution this business request:
1. An After Save Record Trigger Flow
2. Apex Trigger, Handler, Utility Class, and Test
To understand these 2 solutions of going either route (programmatic vs flows) I set up both utilizing separate developer orgs.

### The Record Trigger Flow:
Simple After Save Record Trigger Flow can be set up as follows:

![LeadFlow](/assets/images/Lead Flow.jpg)

* A simple formula to set up the entry criteria for the flow when a Lead Record is Created or Updated.

![Lead Flow Entry Criteria](/assets/images/LeadFlowEntryCriteria.jpg)

* A decision element to determine if the lead record is new or if the product interest was changed (meaning the lead record was updated).

![Lead Flow Decision Element](/assets/images/LeadFlowDecisionElement.jpg)

* If the lead record was updated and the product interest was changed, then create a task with the subject as indicated in the following Text Template.
![Lead Flow Text Template Prod](/assets/images/LeadFlowTextTemplateProdInterestChanged.png)

![Lead Flow Create Records Prod](/assets/images/LeadFlowCreateRecordsProdInterestChanged.jpg)

* If the lead record was new, then create a task with the subject line as indicated in the following Text Template.
![Lead Flow Text Template New Record](/assets/images/LeadFlowTextTemplateNewRecord.png)

![Lead Flow Create Task for New Record](/assets/images/LeadFlowCreateTaskforNewRecord.jpg)

* You can optionally set the Due Date dynamically (depends on business requirement) for the Task using the following formula resource.
![Lead Flow Formula Due Date](/assets/images/LeadFlowFormulaDueDate.jpg)

* Just in case there is ever an error, add error handling in the flow with a Fault Path and Custom Error. Creates a better user experience instead of seeing an Unhandled fault error.
![Lead Flow Custom Error](/assets/images/LeadFlowCustomError.jpg)


### The Apex Trigger and Classes
To keep in line with best practices, I set up a Lead Trigger to redirect records to their destined path of automation, Lead Trigger Handler to hold all the business logic, a Utility class to avoid having repetitive code ("DRY" aka don't repeat yourself!), and a Lead Trigger Handler Test class to not only meet Salesforce's minimum code coverage for deployments but to also make sure the code is working properly.

Follow this link to the sample code. [Link soon to come!]

## The Results
In this specific scenario...

## Next Steps
[add details here]

[def]: /assets/images/DecisionElement.jpg