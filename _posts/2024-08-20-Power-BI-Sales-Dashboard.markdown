---
layout: posts
title:  "Power BI Sales Dashboard"
date:   2024-08-20 15:48:21 +0000
tagline: "An Adventure Works project"
tags: [Power BI, Sales Operations]
author_profile: true
author: Marita Gomez
categories: [article]
highlight_home: true
header:
 overlay_image: "/assets/images/fermin-rodriguez-penelas-treesBike-unsplash.jpg"
 teaser: "/assets/images/fermin-rodriguez-penelas-treesBike-unsplash.jpg"
 caption: "Photo Credit: [Unsplash: Fermin Rodriguez Penelas](https://unsplash.com/@ferminrp)"
description: This is brief summary on the Power BI Sales Dashboard using Microsoft's well known AdventureWorks dataset used for personal projects and training.
---
>"Form and function are a unity, two sides of one coin.
In order to enhance function,
the appropriate form must exist or be created."
—Dr. Ida P. Rolf

# Background
This Sales Dashboard was built with requirements given by Davidson College’s “Analyzing and Visualizing data with Power BI” Course on EdX.

The main goal is build an interactive Sales Dashboard for the VP of Sales at Adventure Works to see all sales employee's performance over time.

Questions that should be addressed by the dashboard:

- Which sales people produce the most sales?
- Which sales people had the highest sales growth from the previous year?
- What is each sales person’s year to date sales total for this year, and how does that compare to this same period last year?
- For each sales person, what were their top-selling products?
- For each sales person, what are their top-producing sales regions and resellers?

Other key requests:

- Sales reps should only see their data, Sales Managers should see only their data and their team’s data, and finally VP of Sales should see all data.
- Data does not need to be real time.

# Approach
Data Source for this project is a backup file of the AdventureWorks database ( .bak file) and restored locally using SQL Server Management Studio (SSMS). Power Bi was then connected directly to SQL Server using import mode.

## Data Cleaning

It is important to remove any information that is NOT needed, removing uneeded columns, removing duplicate data, formatting to facilitate data analysis and reporting. Formatting may include renaming columns, concatenating names, and ensuring data is filtered to what is needed. For example in this project the date table began in 2005 vs sales data began in 2010. Years before 2010 were removed by filtering by a custom year list created from the sales order table.

## Data Modeling

To use [Time Intelligence Functions](https://learn.microsoft.com/en-us/dax/time-intelligence-functions-dax) in Power BI, one of the tables containing a date column needs to be marked as a Date Table. 

The date table from the AdventureWorks database had 3 relationships with the fact table. To facilitate reporting and have the dimensional tables achieve that desirable one active relationship with the fact table, the date table was referenced ("duplicated") three times in power query. These 3 dimension tables (Order, Ship, and Due) are called [role playing dimension tables](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema). Performing this step does duplicate data but only requires “slightly” more storage. 

Finally these tables were each marked as a data table. The final model looks like this:

![AdventureWorksSalesSchema](/assets/images/AdventureWorksSalesSchema.png)

# Results
The final result provides the VP of Sales with an interactive Dashboard and drill through page to view individual employee key sales information.

The Main Page

![AdventureWorks Power BI SalesDashboard First Page](/assets/images/PowerBISalesDashboard01.png)

A Hidden Menu: Using a button, slicers, and bookmark features

![AdventureWorks Power BI SalesDashboard Menu](/assets/images/PowerBISalesDashboard02.png)

A button that will take the report viewer to the drill through page once the sales person is selected.

![AdventureWorks Power BI SalesDashboard Interactive button](/assets/images/PowerBISalesDashboard03.png)

Key information for the specific employee with dynamic titles

![AdventureWorks Power BI Sales Dashboard Employee Detail Page](/assets/images/PowerBISalesDashboard04.png)

## Row-Level Security in Power BI Desktop
To address the the key requirements on data visibility RLS can be leveraged. To ensure Sales Reps can only see their data, we can use the USERPRINCIPLENAME() function which returns the email of the user.

The following is for the Sales Rep:

![AdventureWorks Power BI Sales Dashboard RLS for Sales Rep](/assets/images/PowerBI_RLS_SalesRep.png)

The following is for the Sales Mgr:

![AdventureWorks Power BI Sales Dashboard RLS for Sales Mgr](/assets/images/PowerBI_RLS_SalesMgr.png)



# Next Steps
The back up database that I have may not be the latest revision for AdventureWorks and this database has information for other departments as well. The opportunity to expand this project is infinite really. 

Sample business questions:

- What are the top 3 Countries in terms of Sales?
- Which are the top 10 resellers?
- What are the top 3 product categories, subcategories each yr?