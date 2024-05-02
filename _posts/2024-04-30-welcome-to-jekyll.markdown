---
layout: posts
title:  "Standing up a Helpdesk for the Salesforce Administrators"
date:   2024-05-01 15:48:21 +0000
tagline: "User Experience"
tags: [Salesforce]
author_profile: true
author: Marita Gomez
categories: [article]
highlight_home: true
header:
 overlay_image: "/assets/images/unspashflowers.jpg"
 teaser: "/assets/images/unspashflowers.jpg"
 caption: "Photo Credit: [Unsplash: Christina Deravedisian](https://unsplash.com/@christinadera)"
description: this is an article about Salesforce
---
>"The single biggest problem in communication is the illusion that it has taken place."
-George Bernard Shaw,
Nobel Prize-winning playwright

# The Situation
Business implemented a new CRM system and a new team was onboarded. Go-Live was in progress and the new CRM users needed issues and requests resolved quickly, so requests were being made directly to all team members or multiple combinations of team members via multiple channels (email, teams, and even phone calls). Users were experiencing multiple reply backs and communication was not transparent to the users nor to the team.

## The Approach
Utilized OOB Salesforce Service Cloud standard objects and features to stand up a help desk with:

* Email to Case - Requested a team email from IT, so that emails sent to this email address would automatically create a case in Salesforce and assigned to the team’s queue. With an assignment rule and a email template, the team was notified immediately when a case was created via email to case. No other automations were needed.
* Submit a Question/Feedback Form - A simple screen flow in the Sales Console’s Utility Bar so that Salesforce Users were able reach out for help without leaving their workspace.
  Feature 1: Only 3 available inputs from the user 
  -Select a Case Type from a picklist
  -Option to upload a filed (limited to .csv, .xlsx, .jpeg, .jpg, or .png)
  -Provide a description of the request
  Feature 2: The user inputs provided the necessary information to create a case and send emails to the administrators and the user of the screen flow.

## The Results
Improved User Experience. 
1. Quickly and efficiently request for help or communicate with their administrators.
2. Increase User Adoption by having transparency with the system (users can track the progress of their case).

Improved Administrator Efficiency and Communication.
1. Receive a notification when a case is created via Email to Case or via Screen Flow
2. Transparency within the team as to who is already working the case.

## Next Steps
Create a case for administrators to handle custom exceptions.