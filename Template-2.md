---
layout: default
title: Guidance Document Template
permalink: /template/
---

This page serves as a template to help you create a new guide to add to the FICAM Guides. 

This template tells you: 

  1. How to create a new file.
  2. How to use this template. 
  3. A basic outline for a guide.
  4. A Markdown style sheet and how to use it. 
  5. Some resources on writing (plain language, etc.) and style.  
  
# Create a New File

To create a new file to start your guide, do this:  

  1. Look at the **_Branch_** button at the top left-hand corner of your GitHub Repo's main page. The name showing on the **_Branch_** button is where your new file will be stored.  You can also create a new Branch name, if you prefer. 
  2. To create a new Branch, click on the **_Branch_** button and add a new Branch name.  
  
  > The **_Branch_** button will display the new Branch name and your new file will reside there.  **Note:**  Be sure to remember the Branch name where you are working on your file.
  
  3. Click on the **_Create New File_** button at the top right of the Branch directory window. 
  > At the top **left-hand-side** of the screen, the Branch directory name appears with a **"/"** after it and a text box. (You can also select **_Cancel_**, if you want to start over.) 
  4. In the text box, enter your new file name and add the extension, **.md** for **Markdown** (for example, **Mynewfile.md**). 
  5. Copy the content from this document, **_Template.md_**, and paste it into your new file. 
  6. At the top-left-hand side of the pasted text in your new file, change **Guidance Document Template** to your new file's title and **permalink** at the top, left-hand-side of the file (between the dashed lines [**---**]).
  
  > Change the **permalink** to a short version of the new file name (for example, **template** for **Guidance Document Template**). The **title** should be what you want to appear at the top of the **website page** where your guide will eventually be posted.
  
  > The **permalink** text should be in the format: **/mypage/**, instead of mypage.md.

# Basic Outline 

The outline gives you a starting point for creating your guide. 

## Overview

This text should give a brief overview of what content is contained within the guidance document. It may include information on the intended audience, the intended outcome of the guide, and any other information that would help the user to understand the guide.

## Assumptions _/Prerequisites/Required Hardware and Software_

  This text in this section will be a bullet list explaining a precondition or assumption before the user begins to follow the steps outlined in this document

## Before you get started

This section will tell the user what he/she needs to do to prepare before starting a set of procedures. For example, the user would need to know what specific hardware and software are required for the procedures.

## Title of Procedure 1

This paragraph should introduce the procedure and give user-friendly background information.

  1. Step 1 of procedure 1.
  2. Step 2 of procedure 1.
  
## Title of Procedure 2

This paragraph should introduce the procedure and give user-friendly background information.

  1. Step 1 of the procedure 2.
  2. Step 2 of the procedure 2.
  
  > Repeat Procedure sections, as needed.

# Markdown Style Sheet (Syntax)

Pages use markdown formatting for content.  You can review markdown formatting and a quick three-minute guide by browsing to the Mastering Markdown guide from Github: https://guides.github.com/features/mastering-markdown/

This template is for submitting NEW pages to the site.   

For guidance, pages should be brief to reduce scrolling by users, be written in Plain Language, and use bullets, lists and images.  Paragraphs should be short.

Samples are provided below for the formats used on this site.

# This is a top level header
## This is a second level header
### This is a third level header
#### This is a fourth level header

Start your page with a top level header.

# Type your header here

Include a brief description of the purpose of the page.

As you add sub-sections, you can create links from the top by creating a linked list like this:

- [Sub Section1](#sub-section1)
- [Sub Section2](#sub-section2)

## Sub Section1

Italics use underscores.  This is _italics_.
Bold uses asterisks.  This is **bold**.

Use two spaces, an asterisk, plus one space to start a bullet list.   use the dash, followed by two spaces.

  * The asterisk symbol denotes a bulleted item, 
    * This is a second-level bullet - An indented asterisk denotes a second level bullet

-  Bullet 1
-  Bullet 2

Numbered lists can use numbers, and the lists will automatically increment for you.

  1. Numbered List 1
  1. Numbered List 2
    1. Numbered sublist 1
    2. Numbered sublist 2


## Sub Section2

To reference an image, you will need to upload the image file to the /img/ folder on the github repository.  Here is a sample for referencing an image:

![This is what I want a screen reader to say for 508 compliance]({{site.baseurl}}/img/thisisthesampleimagefile.png)

To link to another page that already exists, 

[This is what I want my link to say]({{site.baseurl}}/insertlink/) 




**WHERE WAS HERE BEFORE**


reference information that may be needed to complete the steps outlined in the guide.

  * This text gives a link to a reference document [with the hyperlink text within brackets](and the actual URL within parentheses)

  * If you want to insert an image onto a page use the format below. The **align** instruction at the end of the link can either be **"left"**, **"center"**, or **"right"**.

![Alt text for an image goes here]({{site.baseurl}}/folder that image is in/imagename.png){:align="right"}

### 1. Title of Procedure 1

  1. Step 1 of the procedure.
  2. Step 2 of the procedure.
  


In Markdown, the **#** symbol is used to denote and format headers (for example, **#** denotes a **Heading 1**, **##** denotes a **Heading 2**, and so on).  (Please see the _Markdown Style Sheet_ given below for more details on Markdown formatting.)

<!--- For example, this code denotes a comment, and information written inside of it will not appear on the website but can be used as a reference for others viewing the file. -->
> This text will appear as a 'warning flag' on the website, which is a yellow banner. (The ">" symbol and the line directly underneath this body of text create the formatting for this flag.) Warning flags can be used for notifications such as notifying a user that they should skip a certain procedure.
{:class="warning"}

> This text will appear as a red banner, for an 'alert' message. Alert flags can be used for notifications such as common problems that may occur.
{:class="alert"}

> This text will appear as a green banner, for an 'informational' message. These flags can be used for notifications such as useful links or helpful tips.
{:class="info"}

This is the main body text that explains the purpose of the procedure and any context that you might need before diving into the individual steps. The text within each step should walk the user directly through exactly what they need to do to complete the procedure.

**Text within double asterisks will appear as bolded.**

*Text within single asterisks will appear as italicized.*

```Text within three backticks style code or command line samples```



1.	Step 1 of the procedure...
2.	Step 2 of the procedure...


#### References

Any referential links should be added to this section. Links appear in the following format [hyperlink text]({{ site.baseurl }}{{ page.url }})

For more information on formatting in markdown, go [here.](https://help.github.com/articles/basic-writing-and-formatting-syntax/)


**WHAT WAS HERE BEFORE**
