---
layout: default
title: Template Title of This Page
permalink: /template/
---

Markdown is a simple way of writing and formatting.  The formats can be used across many different platforms including for websites and documents.  We created a sample template to help you with your page. 

To review information on how to contribute and how to Add a New Page: https://piv.idmanagement.gov/contribute 
If you want to learn more about markdown formatting: https://guides.github.com/features/mastering-markdown/

You can copy and paste this template into a new page, and use the sample markdown. 

You probably noticed this block at the top of the page.  

layout: default 
title: Title of the Page
permalink: /template/

This block at the top of the page is used for website navigation when your guide is posted.  Update the _Title of the Page_ and the _/template/_ 

## Overview

To begin your guide, briefly state its purpose in one to two sentences for an Overview.  You may include information on the intended audience, the intended outcome of the guide, and any other information that would help the user to understand the guide.

Then add a table of contents link for each section. For example:

* [Section 1 Title](#words-in-section1-title-separated-by-dashes)
* [Section 2 Title](#words-in-section2-title-separated-by-dashes)
* [Section 3 Title](#words-in-section3-title-separated-by-dashes)

We propose these sections for most guides:

## Before You get Started
This section should tell the user what to prepare before starting a set of procedures. Explain any assumptions as bulleted lists. Clearly state the hardware and software requirements. 

## Procedure 1
This section should tell the user how to achieve the goal. Explain all steps simply and don't try to recreate other resources that are easily found.  Focus on the government and what can be unique when implementing or executing.

## Procedure 2
This section should tell the user how to achieve the goal. Explain all steps simply and don't try to recreate other resources that are easily found.  Focus on the government and what can be unique when implementing or executing. 

Here are sample markdown formats for you:

Headings use the hash sign with a space. 

## This Is a Second-Level Heading
### This is a third-level heading
#### This is a fourth-level heading


### Number List Items

1. Step 1 of procedure. (Indent 2 spaces, enter a number, and add 1 space.) 
2. Step 2 of procedure.

### Bullet List Items

* Bullet 1 (Indent 2 spaces, enter an asterisk, and add 1 space.)
* Bullet 2

### Bold and Italics

* Use double asterisks to bold a word:  **bold**.
* Use underscores to create italics:  _italics_.

### Code Blocks

To create a code block, use spaces, backticks (```), and Returns in this order: 

* 4 spaces plus 3 backticks (```) to start the code block 
* A Return
* Type or paste in the code that the user needs to enter for a specific step
* Another Return
* 4 spaces plus 3 backticks to end the code block
* Another Return

For example:

   ```
   Text within three backticks for code or command line samples
   ```

### Code Comments

Code comments will be invisible in a webpage view, but others will be able to see the comment in GitHub Markdown. <!--For example, this code denotes a comment. It will not appear on a webpage but can be used as a reference for others viewing the file.-->

### Images

To insert an image into your Page, upload the image file to the **/img/** folder in the GitHub repository.  Then at the image insertion point in your page, add these formats to link to the image.

![This is what I want a screen reader to say for 508 compliance]({{site.baseurl}}/img/imagename.png)

![Text for an image aligned right goes here]({{site.baseurl}}/img/imagename.png){:align="right"}

![Text for another image aligned left goes here]({{site.baseurl}}/img/anotherimagename.png){:style="float:left;width:25%;"}


### Links to Other Documents

To link to useful references, information:

[This is what I want my link to say]({{site.baseurl}}/insertlink/)

To link to a document, or to another website, you need to always open the link in a new window: 

[This is what I want my link to say](https://www.governmentagency.gov){:target="blank"}



