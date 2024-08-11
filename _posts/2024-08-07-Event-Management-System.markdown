---
layout: posts
title:  "Event Management System"
date:   2024-08-07 15:48:21 +0000
tagline: "Salesforce Apex and Flows"
tags: [Salesforce, Apex, Flows]
author_profile: true
author: Marita Gomez
categories: [work]
highlight_home: true
header:
 overlay_image: "/assets/images/product-school-unsplash.jpg"
 teaser: "/assets/images/product-school-unsplash.jpg"
 caption: "Photo Credit: [Unsplash: Product School](https://unsplash.com/@productschool)"
description: This is a sample use case provided by CampApex.org
---
>CampApex.org is a great free resource for those learning Apex. Highly recommend for hands on experience.

**Currently in progress**

# Background
This Scenario, Data Model, User Stories belong to CampApex.org. The following is a brief summary of solutions that I put together (1 solution in code the other declaratively).

Primary goal was to practice writing Apex triggers and Apex classes. 
This exercise can then be extended by providing a 2nd solution (declarative version) with same result, write my version of Apex tests, and add import sample data to create appropriate reports and dashboards.

# 01 - Initializing Event Status upon Creation

**User Story**

"As an event coordinator, I need the system to automatically place a newly created event record into a planning status, so that we can start the event organization process with a clear, initial state that indicates the event is in the early stages of planning."

**Acceptance Criteria:**

When a new CAMPX__Event__c record is created, the CAMPX__Status__c field should reflect the "Planning" picklist value

**Test Results:**

Scenario 1: Verify that creating a CAMPX__Event__c should set the CAMPX__Status__c to "Planning".

Scenario 2: Verify that creating a CAMPX__Event__c sets the CAMPX__Status__c to "Planning", even when the user sets CAMPX__Status__c to "Active" when creating the record.

Scenario 3: Verify that creating 300+ CAMPX__Event__c records in bulk sets the CAMPX__Status__c to "Planning" for all records.

Scenario 4: Verify that updating a CAMPX__Event__c record's CAMPX__Status__c to "Postponed" does not revert the CAMPX__Status__c back to "Planning".

# US-01 Solution

**With Code:**

CAMPXEventTrigger

![CAMPXEventTrigger](/assets/images/US01-Trigger.png)

CAMPXEventTriggerHandler
![CAMPXEventTriggerHandler](/assets/images/US01-TriggerHandler.png)

**With Flow**

A Before Save Record Trigger Flow
![CAMPX__Event__c RT Before Save Flow US-01-01](/assets/images/US01_Flow01.png)

Only 1 update element is needed
![CAMPX__Event__c RT Before Save Flow US-01-02](/assets/images/US01-Flow02.png)


# 02 - Capturing Event Status Change Timestamp

**User Story**

As an event coordinator, I need the system to automatically capture the current date and time whenever the status of an event changes, so that we can have an accurate and automatic record of when each event's status was last modified, helping in timeline tracking and accountability.

**Acceptance Criteria:**

When the CAMPX__Status__c field of an CAMPX__Event__c record is edited, the CAMPX__StatusChangeDate__c field should capture the current date and time

**Test Results:**

Scenario 1: Scenario: Verify that creating a CAMPX__Event__c record should set CAMPX__StatusChangeDate__c to the current date and time.

Scenario 2: Scenario: Verify that when a CAMPX__Event__c record's CAMPX__Status__c is updated, the CAMPX__StatusChangeDate__c is reset to the current date and time.

Scenario 3: Scenario: Verify that when a CAMPX__Event__c record is updated without changing CAMPX__Status__c, the CAMPX__StatusChangeDate__c does not change.

# US-02 Solution

**With Code:**

CAMPXEventTrigger
![CAMPXEventTrigger](/assets/images/US02-Trigger.png)

CAMPXEventTriggerHandler
![CAMPXEventTriggerHandler](/assets/images/US02-TriggerHandler.png)

# 03 - Defaulting Sponsor Status to Pending on Creation

**User Story**

As a sponsorship coordinator, I need the system to automatically mark a sponsor as "Pending" if the field is blank upon creation, so that we can ensure all sponsors are initially considered for review and categorization, streamlining the sponsorship management process.

**Acceptance Criteria:**

When a CAMPX__Sponsor__c record is created, and the CAMPX__Status__c is blank, it should be set to "Pending”

**Test Results:**

Scenario 1: Verify that creating a CAMPX__Sponsor__c record without a CAMPX__Status__c, defaults the CAMPX__Status__c to "Pending".

Scenario 2: Verify that creating a CAMPX__Sponsor__c record with CAMPX__Status__c set to "Rejected", does not default the CAMPX__Status__c to "Pending".

# US-03 Solution

**With Code:**

US03- CAMPXSponsorTrigger
![CAMPXSponsorTrigger](/assets/images/US03-Trigger.png)

US03- CAMPXSponsorTriggerHandler
![CAMPXSponsorTriggerHandler](/assets/images/US03-TriggerHandler.png)

# 04 - Enforcing Email Requirement for Sponsor Creation

**User Story**

As a sponsorship coordinator, I need the system to prevent the creation of a sponsor without an email, so that we can ensure all sponsor records have valid contact information, facilitate communication, and maintain the integrity of our sponsor database.

**Acceptance Criteria:**
When a CAMPX__Sponsor__c record is created without a value in CAMPX__Email__c, the user should see an error stating "A sponsor can not be created without an email address"

**Test Results:**

Scenario 1: Verify that creating a CAMPX__Sponsor__c record without a CAMPX__Email__c, causes an exception.

Scenario 2: Verify that creating a CAMPX__Sponsor__c record with a CAMPX__Email__c, does not cause an exception.

# US-04 Solution

**With Code:**

CAMPXSponsorTrigger
No change from US-03

US04- CAMPXSponsorTriggerHandler
![CAMPXSponsorTriggerHandler](/assets/images/US04-TriggerHandler.png)

# 05 - Updating Sponsor Tier Based on Contribution Amount

**User Story**

As a event coordinator, I need the system to automatically set a sponsor's tier based on their contribution amount, so that we can ensure sponsors are recognized appropriately for their contribution level and streamline the sponsorship management process.

**Acceptance Criteria:**

The CAMPX__Tier__c should be set based on the following mapping:
* CAMPX__ContributionAmount__c is blank or <= 0 then CAMPX__Tier__c is NULL
* 0 < CAMPX__ContributionAmount__c < 1000 then Bronze
* 1000 <= CAMPX__ContributionAmount__c < 5000 then Silver
* CAMPX__ContributionAmount__c >= 5000 then Gold

**Test Results:**

Scenario 1: Verify that creating a CAMPX__Sponsor__c record with a blank CAMPX__ContributionAmount__c keeps CAMPX__Tier__c blank.

Scenario 2: Verify that creating a CAMPX__Sponsor__c record with a "0" as the CAMPX__ContributionAmount__c keeps CAMPX__Tier__c blank.

Scenario 3: Verify that creating a CAMPX__Sponsor__c record with "$500" as the CAMPX__ContributionAmount__c sets the CAMPX__Tier__c to "Bronze".

Scenario 4: Verify that creating a CAMPX__Sponsor__c record with "$1000" as the CAMPX__ContributionAmount__c sets the CAMPX__Tier__c to "Silver".

# US-05 Solution

**With Code:**

US05- CAMPXSponsorTrigger
![CAMPXSponsorTrigger](/assets/images/US05-Trigger.png)

US05- CAMPXSponsorTriggerHandler
![CAMPXSponsorTriggerHandler](/assets/images/US05-TriggerHandler.png)

# 06 - Conditional Sponsor Status Update Based on Event Association

**User Story**

As a sponsorship coordinator, I need the system to prevent the status of a sponsor record from being updated to "Accepted" unless it is associated with an event, so that we can maintain accurate and meaningful sponsor-event relationships and ensure accepted sponsors are properly linked to specific events.

**Acceptance Criteria:**

The CAMPX__Status__c field of a CAMPX__Sponsor__c record can not be updated to "Accepted" until the CAMPX__Event__c field is populated

The user should see this error when attempting to accept a sponsor without an event: "A Sponsor must be associated with an event before being Accepted."

**Test Results:**

Scenario 1: Verify that creating a CAMPX__Sponsor__c record with an "Accepted" CAMPX__Status__c and a CAMPX__Event__c, does not throw an error.

Scenario 2: Verify that creating a CAMPX__Sponsor__c record with an "Accepted" CAMPX__Status__c and without a CAMPX__Event__c, does throw an error.

Scenario 3: Verify that updating a CAMPX__Sponsor__c record to have an "Accepted" CAMPX__Status__c and a CAMPX__Event__c, does not throw an error.

Scenario 4: Verify that updating a CAMPX__Sponsor__c record to an "Accepted" CAMPX__Status__c without a CAMPX__Event__c, throws an error.

Scenario 5: Verify that updating a CAMPX__Sponsor__c record to "Pending" or "Rejected" CAMPX__Status__c does not require a CAMPX__Event__c.

Message: Attempted to update a CAMPX__Sponsor__c from Pending to an Accepted CAMPX__Status__c without associating a CAMPX__Event__c. Expected an error, but did not find one.

# US-06 Solution

**With Code:**

CAMPXSponsorTrigger, no change from US-05 trigger

CAMPXSponsorTriggerHandler

added a helper method
![CAMPXSponsorTriggerHandler - Method](/assets/images/US06-HelperMethod.png)

this helper method is then called by the handlerBeforeInsert and handlerBeforeUpdate methods.
![CAMPXSponsorTriggerHandler - Method](/assets/images/US06-HelperMethodReferenced.png)

# 07 - Automatic Update of Net Revenue on Financial Changes

**User Story**

As a financial manager, I need the system to automatically update the net revenue of an event record whenever there are changes to its gross revenue or total expenses, so that we can ensure real-time accuracy of our financial reporting and provide stakeholders with up-to-date information on the financial status of our events.

**Acceptance Criteria:**

The CAMPX__NetRevenue__c of an CAMPX__Event__c record should always reflect the formula: `CAMPX__GrossRevenue__c - CAMPX__TotalExpenses__c`

If either CAMPX__GrossRevenue__c or CAMPX__TotalExpenses__c are blank, the CAMPX__NetRevenue__c should be blank

**Test Results:**

Scenario 1: Verify that creating a CAMPX__Event__c record with $0 for CAMPX__GrossRevenue__c and $0 for CAMPX__TotalExpenses__c sets $0 value for CAMPX__NetRevenue__c.

Scenario 2: Verify that creating a CAMPX__Event__c record with $3000 for CAMPX__GrossRevenue__c and $1000 for CAMPX__TotalExpenses__c sets $2000 for CAMPX__NetRevenue__c.

Scenario 3: Verify that creating a CAMPX__Event__c record with $1000 for CAMPX__GrossRevenue__c and $2000 for CAMPX__TotalExpenses__c sets $-1000 for CAMPX__NetRevenue__c.

Scenario 4: Creating a CAMPX__Event__c record with empty values for CAMPX__GrossRevenue__c and CAMPX__TotalExpenses__c should set a blank value for CAMPX__NetRevenue__c.

Scenario 5: Updating the CAMPX__GrossRevenue__c should recalculate CAMPX__NetRevenue__c.

Scenario 6: Updating the CAMPX__TotalExpenses__c should recalculate CAMPX__NetRevenue__c.

**With Code:**

CAMPXEventTrigger
![CAMPXEventTrigger](/assets/images/US07-Trigger.png)

CAMPXEventTriggerHandler
![CAMPXEventTriggerHandler](/assets/images/US07-TriggerHandler.png)

# 08 - Automatic Update of Net Revenue on Financial Changes

**User Story**

As a finance manager, I need the system to automatically keep track of an event's gross revenue by taking a sum of all accepted sponsor's contributions, so that we can maintain an accurate and real-time tally of an event's gross revenue and ensure that financial reporting reflects all accepted sponsor contributions.

**Acceptance Criteria:**

When a CAMPX__Sponsor__c record is updated to have an "Accepted" CAMPX__Status__c, the system should account for the sponsor's CAMPX__ContributedAmount__c in the CAMPX__Event__c's CAMPX__GrossRevenue__c field

**Test Results:**

Scenario 1: When an event recieves it's first accepted sponsorship, verify the the event's initial CAMPX__GrossRevenue__c is updated.

Scenario 2: When an event receives its second sponsorship, the event's CAMPX__GrossRevenue__c should be updated.

Scenario 3: When two distinct events receive sponsorship at the same time by creating 2 distinct Accepted CAMPX__Sponsor__c records with a CAMPX__ContributionAmount__c of $250 and $150 respectively, the first event's CAMPX__GrossRevenue__c is updated by $250 and the second by $150.

Scenario 4: When a new event receives its first sponsorship, by updating a CAMPX__Sponsor__c to the Accepted Status, it's CAMPX__ContributionAmount__c should carry over.

**With Flow:**

An After Save Record Trigger Flow, when a Sponsor record is created or updated and CAMPX__Status__c = "Accepted". This is an example of a roll up summary field with flow for a lookup relationship. As the flow loops through each sponsor record of the Sponsor Record Collection related to that specific Event record, the contribution amount is added to a flow variable "varTotalContributionAmountSponsorCollection". The Event Gross Revenue is then updated with the value from this variable.

![Update CAMPX Event Gross Revenue](/assets/images/US08-RTFlow.png)

# 09 - Adjusting Event Gross Revenue for Cancelled Sponsorships Or Event Changes

**User Story**

As a finance manager, I need the system to automatically subtract a sponsor's contribution amount from its associated event's gross revenue when the sponsor is no longer "Accepted" or tied to the event, so that our financial records accurately reflect the current status of sponsor contributions and ensure that the event's gross revenue reports are precise and reliable for making informed decisions.

**Acceptance Criteria:**

When the CAMPX__Status__c of a CAMPX__Sponsor__c changes from "Accepted" to "Cancelled" or "Pending" the associated CAMPX__Event__c's CAMPX__GrossRevenue__c field should no longer reflect the sponsor's CAMPX__ContributedAmount__c

When the CAMPX__Event__c lookup of a CAMPX__Sponsor__c changes, the previously associated CAMPX__Event__c's CAMPX__GrossRevenue__c field should no longer reflect the sponsor's CAMPX__ContributedAmount__c

Scenario 1: An Event had an accepted Sponsor that contributed $500. Verify that changing the sponsor's status to Rejected removes the $500 contribution from the event's gross revenue.

Scenario 2: An Event had an accepted Sponsor that contributed $2500. Verify that changing the sponsor's status to Pending removes the $2500 contribution from the event's gross revenue.

Scenario 3: An Event had an accepted Sponsor that contributed $100. Verify that removing the sponsor's event lookup the $100 contribution is removed from the event's gross revenue.

**With Flow:**

An After Save Record Trigger Flow, when a Sponsor record is updated and CAMPX__Status__c isChanged OR CAMPX__Event__c isChanged. 

![Adjust CAMPX Event Gross Revenue](/assets/images/US09-RTFlow.png)