---
layout: default
title: Guidance Document Template
permalink: /template/
---

This page serves as the template for creating your own guidance document to add to one of the FICAM Guides. This template tells you: 

  1. How to create a new file.
  2. _how to use this template_ 
  2. A basic outline for a guide.
  3. A few tips on style and writing. 
  4. How to use Markdown. (All GitHub pages use the Markdown tool to create and format text.)  

To create your own page using the GitHub website, do this:  

  1. Click on the [Check this--]**_create new file_** button at the top right-hand-side of the Branch directory **Check this.  Use screen capture?**. 
  > At the top **left-hand-side** [**check this**] of the Branch directory there will be a box that says **_name your file_**.
  2. Give the new file a name and add the extension, **.md**. (This means that the file type will be "Markdown").
  3. Copy the content from this Template.md file and paste it into your new file. 
  4. Change the **title** and **permalink** at the top, left-hand-side of the file (between the dashed lines [**---**]).  
  > The **permalink** should be a short version of the new file name (for example, **template** for **Guidance Document Template**). The **title** should be what you want to appear at the top of the website page, and the **permalink** text should be in the format: **/mypage/**, instead of mypage.md.

# Basic Outline 

The following is an outline you can use as a starting point. In Markdown, the **#** symbol is used to denote and format headers (for example, **#** denotes a **Heading 1**, **##** denotes a **Heading 2**, and so on).  (Please see the _Markdown Style Sheet_ given below for more details on Markdown formatting.)

<!--- For example, this code denotes a comment, and information written inside of it will not appear on the website but can be used as a reference for others viewing the file. -->

## Overview

This text should give a brief overview of what content is contained within the guidance document. It may include information on the intended audience, the intended outcome of the guide, and any other information that would help the user to understand the guide.

## Assumptions

  * This text will be a bullet explaining a precondition or assumption before the user begins to follow the steps outlined in this document
  * The asterisk symbol denotes a bulleted item, and an indented asterisk denotes a second level bullet
    * This is a second-level bullet

## Before you get started

This text will provide any steps or information that a user will need to take before starting a set of procedures. For example, you can use this section to provide prerequisite information the user needs to know, such as required hardware and software versions and configuration information.

reference information that may be needed to complete the steps outlined in the guide.

  * This text gives a link to a reference document [with the hyperlink text within brackets](and the actual URL within parentheses)

  * If you want to insert an image onto a page use the format below. The **align** instruction at the end of the link can either be **"left"**, **"center"**, or **"right"**.

![Alt text for an image goes here]({{site.baseurl}}/folder that image is in/imagename.png){:align="right"}

### 1. Title of Procedure 1

  1. Step 1 of the procedure.
  2. Step 2 of the procedure.
  


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

