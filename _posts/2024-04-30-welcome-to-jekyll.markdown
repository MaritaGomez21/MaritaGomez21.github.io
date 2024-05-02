---
layout: posts
title:  "Standing up a Help Desk for Admins"
date:   2024-05-01 15:48:21 +0000
tagline: "Effective Communication"
tags: [Salesforce, Communication]
author_profile: true
author: Marita Gomez
categories: [work]
highlight_home: true
header:
 overlay_image: "/assets/images/unspashflowers.jpg"
 teaser: "/assets/images/unspashflowers.jpg"
 caption: "Photo Credit: [Unsplash: Christina Deravedisian](https://unsplash.com/@christinadera)"
description: This is an example of how to setup a help desk for Salesforce Administrators
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

### The Screen Flow included the following features:
* Simple screen requesting only 3 user inputs
* A picklist field: Case Type (for example Question/Training, Bug, Data Upload, or Permission Related)
* An option to upload a file (limited to .csv, .xlsx, .jpeg, .jpg, or .png)
* A description field to provide the user ample space to provide specific details of their request
* The user information and user inputs provided the necessary information to create a case
* The case would be assigned to the admin queue
* Case information within the screen flow would then be used to send a confirmation email to the user and notification email to the administrators.

## The Results
Improved User Experience. 
* Quickly and efficiently request for help or communicate with their administrators.
* Increase User Adoption by having transparency with the system (users can track the progress of their case).

Improved Administrator Efficiency and Communication.
* Receive a notification when a case is created via Email to Case or via Screen Flow
* Transparency within the team as to who is already working the case.

## Next Steps
Solution for administrators to handle custom exceptions.