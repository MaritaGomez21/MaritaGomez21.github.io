---
layout: posts
title:  "Event Management System"
date:   2024-08-07 15:48:21 +0000
tagline: "Salesforce Automations"
tags: [Salesforce, Apex, Flows]
author_profile: true
author: Marita Gomez
categories: [work]
highlight_home: false
header:
 overlay_image: "/assets/images/product-school-unsplash.jpg"
 teaser: "/assets/images/product-school-unsplash.jpg"
 caption: "Photo Credit: [Unsplash: Product School](https://unsplash.com/@productschool)"
description: This is a sample use case provided by CampApex.org
---
>CampApex.org is a great free resource for those learning Apex.

# Background
This Scenario, Data Model, User Stories belong to CampApex.org. The following is a brief summary of solutions that I put together (1 solution in code the other declaratively).

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

# User Story 02 - Capturing Event Status Change Timestamp
**User Story:** 

As an event coordinator, I need the system to automatically capture the current date and time whenever the status of an event changes, so that we can have an accurate and automatic record of when each event's status was last modified, helping in timeline tracking and accountability.

**Acceptance Criteria:**

• When the CAMPX__Status__c field of an CAMPX__Event__c record is edited, the CAMPX__StatusChangeDate__c field should capture the current date and time

**Test Results:**

Scenario 1: Scenario: Verify that creating a CAMPX__Event__c record should set CAMPX__StatusChangeDate__c to the current date and time.

Scenario 2: Scenario: Verify that when a CAMPX__Event__c record's CAMPX__Status__c is updated, the CAMPX__StatusChangeDate__c is reset to the current date and time.

Scenario 3: Scenario: Verify that when a CAMPX__Event__c record is updated without changing CAMPX__Status__c, the CAMPX__StatusChangeDate__c does not change.

**Solution**

With Code:
<code>
trigger CAMPXEventTrigger on CAMPX__Event__c (before insert, before update) {
        if (Trigger.isInsert && Trigger.isBefore) {
        
	        CAMPXEventTriggerHandler.handleBeforeInsert (Trigger.new);
        
        } else if (Trigger.isUpdate && Trigger.isBefore) {
           
	         CAMPXEventTriggerHandler.handleBeforeUpdate (Trigger.new, Trigger.oldMap);
        }
}
</code>
<code>
public with sharing class CAMPXEventTriggerHandler {
    public static void handleBeforeInsert(List<CampX__Event__c> newCampXEventList){
        // Loop through each new campX event and update status to "Planning" 
        // and status change date to current date for timeline tracking and accountability.
        for(CampX__Event__c newCampXEvent : newCampXEventList){
            newCampXEvent.CAMPX__Status__c = 'Planning';
            newCampXEvent.CAMPX__StatusChangeDate__c = DateTime.now();
            CampXEventTriggerHandler.updateNetRevenueHelper(newCampXEventList);
        }
    }
    
    public static void handleBeforeUpdate(List<SObject> newSobjs, Map<Id,SObject> oldSobjsMap){

        List<CAMPX__Event__c> newCampXEventList = (List<CAMPX__Event__c>) newSobjs;
        Map<Id, CAMPX__Event__c> oldCampXEventMap = (Map<Id, CAMPX__Event__c>)oldSobjsMap;
        
        // Loop through each updated campX Event record
        for (CAMPX__Event__c newEvent : newCampXEventList) {

            // Use the map method "get" to retrieve the old event record from the map.
            CAMPX__Event__c oldEvent = oldCampXEventMap.get(newEvent.Id);

            // If the status has changed, update the status change date by using the DateTime class method now()
            if (newEvent.CAMPX__Status__c != oldEvent.CAMPX__Status__c) {
                newEvent.CAMPX__StatusChangeDate__c = DateTime.now();
            }
            CampXEventTriggerHandler.updateNetRevenueHelper(newCampXEventList);
        }
    }
    </code>