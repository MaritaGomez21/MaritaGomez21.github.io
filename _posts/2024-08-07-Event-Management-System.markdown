---
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

# Background
CampApex.org is a great free resource for those learning Apex. This Scenario, Data Model,  User Stories belong to CampApex.org. 

The following is a brief summary of solutions that I put together (first code then an alternate declarative solution - flows).

Primary goal was to practice writing Apex triggers and Apex classes. 
This exercise can then be extended by providing a 2nd solution (declarative version) with same result, write my version of Apex tests, and add import sample data to create appropriate reports and dashboards.

# User Story 01 - Initializing Event Status upon Creation
"As an event coordinator, I need the system to automatically place a newly created event record into a planning status, so that we can start the event organization process with a clear, initial state that indicates the event is in the early stages of planning."

## Solutions for US-01
With Code:
<code>
trigger CAMPXEventTrigger on CAMPX__Event__c (before insert) {
        if (Trigger.isInsert && Trigger.isBefore) {
        
         CAMPXEventTriggerHandler.handleBeforeInsert (Trigger.new);
        
	      }
}
</code>