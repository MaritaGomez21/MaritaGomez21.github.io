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

# Goal

Create a lightning web component for a lightning record page to display images. Used VSCode, Salesforce CLI, and a dev org to set this up.

# Key steps

To display an image via lwc, image(s) can be referenced from a static resource file, 2 ways:
1. an image can be uploaded individually as a static resource file or 
2. an image can be referenced from a zip file (with a collection of images) uploaded as a static resource.

* In this scenario, one image file (vegetables) was uploaded individually as a static resource.

![Static Resources Vegetables](/assets/images/StaticResourcesVegetables.png)

* In the second scenario, a zip file with multiple files was uploaded as a static resource.
    
![Static Resources Ingredients](/assets/images/StaticResourcesIngredients.png)

 * To expose the static resource URL for use in the HTML; use keyword: resourceURL in the JavaScript file first to pull it in from the org dynamically.

![recipeCarousel js file](/assets/images/recipeCarousel-js.png)

## QUICK TIP: LWC Test file kept erroring out; to address the issue the following was changed: import {createElement } from ‘lwc’; to import { createElement } from "@lwc/engine-dom";

* Then to display the images on the page use src={spicesUrl} as shown below in the html file.

![recipeCarousel html file](/assets/images/recipeCarousel-html.png)

## QUICK TIP: To center the component within the section of the lightning record page use “slds-align_absolute-center”

* Finally add the optional css file to the lwc.

![recipeCarousel css file](/assets/images/recipeCarousel-css.png)

* If possible, extend this project by aligning the auto-replay button.

## Results (Version 1)

Screenshot of the result on a lightning record page:

![Screenshot Carousel Demo](/assets/images/ScreenshotCarouselDemo.png)

Screen Recording:
The recording shows the lwc automatically playing to display the 3 images.

(https://youtu.be/Wn_HY4Un30M%)

## Resources:

[Carousel image component recipe from the Salesforce developer guide](https://developer.salesforce.com/docs/component-library/bundle/lightning-carousel-image/documentation%)

[Carousel Lightning Design System](https://www.lightningdesignsystem.com/components/carousel/)

## Images Credit:

[Calum Lewis. URL: https://unsplash.com/photos/five-gray-spoons-filled-with-assorted-color-powders-near-chilli-vA1L1jRTM70](https://unsplash.com/photos/five-gray-spoons-filled-with-assorted-color-powders-near-chilli-vA1L1jRTM70)

[Anna Jakutajc-Wojtalik. URL:https://unsplash.com/photos/a-pile-of-vegetables-and-eggs-on-a-table-Gxr5vwk1V3k](https://unsplash.com/photos/a-pile-of-vegetables-and-eggs-on-a-table-Gxr5vwk1V3k)

[Margaret Jaszowska. URL: https://unsplash.com/photos/orange-fruits-in-green-round-plastic-container-eJHd6OQx-XA](https://unsplash.com/photos/orange-fruits-in-green-round-plastic-container-eJHd6OQx-XA)