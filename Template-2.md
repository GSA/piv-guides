---
layout: default
title: Guidance Document Template
permalink: /template/
---

This page serves as a template to help you create a new FICAM Guide for the IDManagment.gov website. 

This template provides: 

  1. The **_steps to create a new Page (file)_** for your guide. (**Note:**  **_files_** in GitHub are called **_Pages_**.)
  2. An **_example outline_**.
  3. A **_Markdown template_** and how to use Markdown **_Styles_**. 
  4. Some **_writing and style resources_** for additional information (plain language, etc.).  
  
# Create a New Page to Start Your Guide

To contribute a new guide, please see the **Contributing.md** file for more information.

To create a new page to start your guide, do this:  

  1. Look at the **_Branch_** button at the top left-hand corner of your GitHub Repo's main page. The name showing on the **_Branch_** button is where your new page will be stored.  You can also create a new Branch name, if you prefer. 
  2. To create a new Branch, click on the **_Branch_** button and add a new Branch name.  
  
  > The **_Branch_** button will display the new Branch name and your new page will reside there.  
  
  > **Note:**  Be sure to remember the Branch name where your file resides.
  
  3. Click on the **_Create New File_** button at the top right of the Branch directory window. 
  > At the top **left-hand-side** of the screen, the Branch directory name appears with a **"/"** after it and a text box. (You can also select **_Cancel_**, if you want to start over.) 
  4. In the text box, enter your new page name with the extension, **.md**, for **Markdown** (for example, **Mynewfile.md**). 
  5. Copy the **_Example Outline_** and **_Markdown Template_** from this document, **_Template.md_**, and paste it into your new page. 
  6. At the top-left-hand side of your new page, change **Guidance Document Template** to your new file's title and **permalink** at the top, left-hand-side of the file (between the dashed lines [**---**]).
  
  > Change the **permalink** to a short version of the new file name (for example, **template** for **Guidance Document Template**). The **title** should be what you want to appear at the top of the **website page** where your guide will eventually be posted.
  
  > The **permalink** text should be in the format: **/mypage/**, instead of mypage.md.
  
# Copy Example Outline and Markdown Template from Here

# Example Outline 

This example outline gives you a starting point for creating your guide. 

  > When you create a new file (page), copy and paste both the Example Outline (if you choose to use it) and the Markdown Template (given below) into your new file.

## Overview

This text should give a brief overview of what content is contained within the guidance document. It may include information on the intended audience, the intended outcome of the guide, and any other information that would help the user to understand the guide.

## Assumptions 

  > This section could also be called **_Preconditions_** or **_Required Hardware and Software_**.
  
  This section will be a bullet list explaining assumption(s) or other needed precondition(s) before the user can begin to follow the steps outlined in the new guide.

## Before you get started

This section will tell the user what he/she needs to do to prepare before starting a set of procedures. 

## Title of Procedure 1

This paragraph should give user-friendly background information and introduce the procedure.

  1. Step 1 of procedure 1.
  2. Step 2 of procedure 1.
  
## Title of Procedure 2

This paragraph should give user-friendly background information and introduce the procedure.

  1. Step 1 of the procedure 2.
  2. Step 2 of the procedure 2.
  
  > Repeat Procedural sections, as needed.

# Markdown Template (Style Sheet)

Copy and paste the styles from this Markdown Template into the new file (page) you created.  Use Markdown styles to write NEW pages to be submitted to the IDManagement.gov website. 

Markdown formatting is used for Pages (file) content.  You can learn more about Markdown formatting by browsing to the "Mastering Markdown" guide from Github: https://guides.github.com/features/mastering-markdown/

## Headings

In Markdown, the **#** symbol is used to denote and format headers.

# This is a top-level heading
## This is a second-level heading
### This is a third-level heading
#### This is a fourth-level heading
##### This is a fifth-level heading

  > Start your page with a top-level heading.

## Table of Contents (TOC)

As you add sections, you can create a Table of Contents (TOC) at the top of your page by creating a linked list like this:

- [Subsection1](#subsection1)
- [Subsection2](#subsection2)

## Bold and Italics

  * Use underscores to create italics:  _italics_.
  * Use double asterisks to bold a word:  **bold**.

## Bulleted and Numbered Lists

Use two spaces, an asterisk, plus one space to start a bullet list.   use the dash, followed by two spaces.

  * The asterisk symbol denotes a bulleted item, 
    * This is a second-level bullet - An indented asterisk denotes a second level bullet

-  Bullet 1
-  Bullet 2

Use two spaces and type "**_1._**," etc., to create a numbered item. You must type each number. The numbers will automatically increment for you when rendered. The first numbered list will render as "1, 2, 3," etc.  Even though you must type 1, 2, etc., for the numbered sub-item list, the sub-items will render as "i, ii, iii," etc.

  > **Note:** Markdown supports only **two** indention levels for numbered lists.

  1. Numbered item 1
  2. Numbered item 2
      1. Numbered sub-item 1
      2. Numbered sub-item 2

## Images

To insert an image (graphic) into your page, first upload the image file to the **/img/** folder in the appropriate GitHub repository.  Next, use this format to link to the image:

![This is what I want a screen reader to say for 508 compliance]({{site.baseurl}}/img/thisisthesampleimagefile.png)

  > To align an image on a page, use the **align** instruction at the end of an image link (i.e., **"left"**, **"center"**, or **"right"**) using this format:

![Alt text for an image goes here]({{site.baseurl}}/folder that image is in/imagename.png){:align="right"}


## Links to References or Other Information

To link to useful references, information, or another page (especially that may be needed to complete the procedures), use this link format: 

[This is what I want my link to say]({{site.baseurl}}/insertlink/) 



# End Copying Markdown Template Here


# Writing and Style Resources

For the FICAM Guides, all pages should be brief, and paragraphs should be short. All text should be written in plain language. Use numbered steps, bullet lists, and graphics whenever possible. 

The following references provide guidance and additional information about plain language, writing, and style:

  * [18F Content Guide]({{site.baseurl}}/https://content-guide.18f.gov/)
  * [Federal Plain Language Guidelines]({{site.baseurl}}/http://www.plainlanguage.gov/howto/guidelines/FederalPLGuidelines/TOC.cfm/)
  * [U.S. Government Printing Office (GPO) Style Manual]({{site.baseurl}}/https://www.govinfo.gov/app/details/GPO-STYLEMANUAL-2016/)
  * The Chicago Manual of Style
  * The Associated Press (AP) Style Guide
  * Oxford Dictionary
  * Merriam Webster Dictionary
  








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

**What was here before ENDS**





**what was here before STARTS again**

**Text within double asterisks will appear as bolded.**

*Text within single asterisks will appear as italicized.*

```Text within three backticks style code or command line samples```



1.	Step 1 of the procedure...
2.	Step 2 of the procedure...


#### References

Any referential links should be added to this section. Links appear in the following format [hyperlink text]({{ site.baseurl }}{{ page.url }})

For more information on formatting in markdown, go [here.](https://help.github.com/articles/basic-writing-and-formatting-syntax/)


**WHAT WAS HERE BEFORE**