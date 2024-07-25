---
layout: posts
title:  "LWC Carousel Image Component"
date:   2024-07-24 15:48:21 +0000
tagline: "Lightning Web Components"
tags: [JavaScript, CSS, HTML, Salesforce]
author_profile: true
author: Marita Gomez
categories: [work]
highlight_home: true
header:
 overlay_image: "/assets/images/spices.jpg"
 teaser: "/assets/images/spices.jpg"
 caption: "Photo Credit: [Unsplash: Calum Lewis](https://unsplash.com/@calumlewis)"
description: This is an example of how to create a LWC Carousel Image Component
---
>"This is my advice to people: Learn how to cook, try new recipes, learn from your mistakes, be fearless, and above all have fun."
-Julia Child

## Caution post Under Construction!

# Summary

Using the Carousel image component recipe from the Salesforce developer guide
{ % https://developer.salesforce.com/docs/component-library/bundle/lightning-carousel-image/documentation % }

and referencing lightning design system
{ % https://www.lightningdesignsystem.com/components/carousel/ % }

# Key steps

To display an image from the org’s static resources

    1. One image file (vegetables)

![Static Resources Vegetables](/assets/images/StaticResourcesVegetables.png)

    2. an image file within multiple files in a zip file (uploaded as a static resource)
    
![Static Resources Ingredients](/assets/images/StaticResourcesIngredients.png)

    3. Expose the static resource URL for use; keyword: resourceURL

![recipeCarousel js file](/assets/images/recipeCarousel-js.png)

## QUICK TIP: LWC Test file kept erroring out; to address the issue the following was changed: import {createElement } from ‘lwc’; to import { createElement } from "@lwc/engine-dom";

    4. To display the images use src={spicesUrl} as shown below

![recipeCarousel html file](/assets/images/recipeCarousel-html.png)

## QUICK TIP: To center the component within the section of the lightning record page use “slds-align_absolute-center”

    5. Finally add the css

![recipeCarousel css file](/assets/images/recipeCarousel-css.png)

    6. If possible, extend this project by aligning the auto-replay button.

## Results (Version 1)

Screenshot of the result on a lightning record page:

![Screenshot Carousel Demo](/assets/images/ScreenshotCarouselDemo.png)

Screen Recording:
The recording shows the lwc automatically playing to display the 3 images.

{ % https://youtu.be/Wn_HY4Un30M % }