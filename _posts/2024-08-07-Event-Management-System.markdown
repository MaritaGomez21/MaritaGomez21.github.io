---
layout: posts
title:  "Event Management System"
date:   2024-08-07 15:48:21 +0000
tagline: "Salesforce Automations"
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

# User Story 01 - Initializing Event Status upon Creation
"As an event coordinator, I need the system to automatically place a newly created event record into a planning status, so that we can start the event organization process with a clear, initial state that indicates the event is in the early stages of planning."

## Acceptance Criteria:
When a new CAMPX__Event__c record is created, the CAMPX__Status__c field should reflect the "Planning" picklist value

## Test Results:
Scenario 1: Verify that creating a CAMPX__Event__c should set the CAMPX__Status__c to "Planning".

Scenario 2: Verify that creating a CAMPX__Event__c sets the CAMPX__Status__c to "Planning", even when the user sets CAMPX__Status__c to "Active" when creating the record.

Scenario 3: Verify that creating 300+ CAMPX__Event__c records in bulk sets the CAMPX__Status__c to "Planning" for all records.

Scenario 4: Verify that updating a CAMPX__Event__c record's CAMPX__Status__c to "Postponed" does not revert the CAMPX__Status__c back to "Planning".

## Solutions for US-01

**With Code:**
CAMPXEventTrigger
![CAMPXEventTrigger](/assets/images/US01-Trigger.png)

CAMPXEventTriggerHandler
![CAMPXEventTriggerHandler](/assets/images/US01-TriggerHandler.png)

**With Flow**
A Before Save Record Trigger Flow
![CAMPX__Event__c RT Before Save Flow US-01-01](/assets/images/US01_Flow01.png)

Only 1 update element is needed
![CAMPX__Event__c RT Before Save Flow US-01-02](/assets/images/US01_Flow02.png)


# User Story 02 - Capturing Event Status Change Timestamp
As an event coordinator, I need the system to automatically capture the current date and time whenever the status of an event changes, so that we can have an accurate and automatic record of when each event's status was last modified, helping in timeline tracking and accountability.

## Acceptance Criteria:
When the CAMPX__Status__c field of an CAMPX__Event__c record is edited, the CAMPX__StatusChangeDate__c field should capture the current date and time

## Test Results:
Scenario 1: Scenario: Verify that creating a CAMPX__Event__c record should set CAMPX__StatusChangeDate__c to the current date and time.

Scenario 2: Scenario: Verify that when a CAMPX__Event__c record's CAMPX__Status__c is updated, the CAMPX__StatusChangeDate__c is reset to the current date and time.

Scenario 3: Scenario: Verify that when a CAMPX__Event__c record is updated without changing CAMPX__Status__c, the CAMPX__StatusChangeDate__c does not change.

## Solutions for US-02

**With Code:**
CAMPXEventTrigger
![CAMPXEventTrigger](/assets/images/US02-Trigger.png)

CAMPXEventTriggerHandler
![CAMPXEventTriggerHandler](/assets/images/US02-TriggerHandler.png)



