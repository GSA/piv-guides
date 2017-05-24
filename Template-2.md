---
layout: default
title: Guidance Document Template
permalink: /template/
---

This **_Template.md_** page serves as a template and guidance document to help you create a new FICAM Guide for the www.IDManagment.gov website. 

To create a new guide (or contribute to one), please read the **_Contributing.md_** page for more information, as well as terms and conditions. (The **_Contributing.md** file is located in the GitHub PIV-Guides, FPKI-Guides, and FICAM-Arch Repos.){:class="info"} 

This **_Template.md_** page provides: 

  1. **_Steps to create a new Page (file)_** for your guide. 
  2. An **_Example Outline_** to copy and paste into your page (i.e., to help structure your guide).
  3. A **_Markdown Template_** to copy and paste into your page (i.e., to help with Markdown formatting). 
  4. Some **_writing and style resources_** (i.e., to help with plain language, writing, and style).  
  
# Create a New Page to Start Your Guide

To create a new **_Page_** to start your guide, do this:  

  1. Before you create a new **Page**, you need to select a **Branch** where your page will be stored. At the top left-hand corner of your GitHub Repo's directory window, you will see a **_Branch_** button. The branch (name) shown on this button is where your new page will be stored. 
  2. You may also create a new branch for your guide, if you prefer. To create a new branch, click on the **_Branch_** button and add a new name.  
  
  > The **_Branch_** button will display the new branch name. When you save your new page, it will be stored in this branch. (**Note:**  It's important to remember the **_branch name where your page is stored** for future updates to your guide.)
  
  3. Click on the **_Create New File_** button located at the top right area of your Repo's directory window.  
  > At the top left-hand-side of the window, the Branch directory name appears with a **"/"** after it and a text box. (You can also select **_Cancel_**, if you want to start over.) 
  4. In the text box, enter your new page's name with the extension, **.md**, for **Markdown** (for example, **Mynewfile.md**). 
  5. Copy the **_Example Outline_** and **_Markdown Template_** from this document, **_Template.md_**, and paste it into your new page. 
  6. At the top-left-hand side of your new page, change **Guidance Document Template** to your new page's title. 
  7. Change the **permalink** title to a short version of your new page's title.
  
  > The **permalink** title should be in the format: **/mypage/**, instead of mypage.md

# Example Outline 

Now that you have created a new page, this **Example Outline** will help you to create your guide.

  1. Copy and paste this **Example Outline** into your new page as a starting point for your guide's document structure.

## Overview

This text should give a brief overview of what content is contained within the guidance document. It may include information on the intended audience, the intended outcome of the guide, and any other information that would help the user to understand the guide.

## Assumptions 

  > This section could also be called **_Preconditions_** or **_Required Hardware and Software_**.
  
  This section will be a bullet list explaining assumption(s) or other needed precondition(s) before the user can begin to follow the steps outlined in the new guide.

## Before You Get Started

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

# Markdown Template

Copy and paste this **Markdown Template** into your new page.  Use Markdown styles to write NEW pages to be submitted to the IDManagement.gov website. 

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

## Code Blocks

For code blocks, enter three backticks (```) before and after the code example:

```Text within three backticks style code or command line samples```

## Code Comments

<!--For example, this code denotes a comment, and information written inside of it will not appear on the website but can be used as a reference for others viewing the file.-->

## Images

To insert an image (graphic) into your page, first upload the image file to the **/img/** folder in the appropriate GitHub repository.  Next, use this format to link to the image:

![This is what I want a screen reader to say for 508 compliance]({{site.baseurl}}/img/thisisthesampleimagefile.png)

  > To align an image on a page, use the **align** instruction at the end of an image link (i.e., **"left"**, **"center"**, or **"right"**) using this format:

![Alt text for an image goes here]({{site.baseurl}}/folder that image is in/imagename.png){:align="right"}

## Alerts, Warnings, and Information Blocks

> This text will appear as a 'warning flag' on the website, which is a yellow banner. (The ">" symbol and the line directly underneath this body of text create the formatting for this flag.) Warning flags can be used for notifications such as notifying a user that they should skip a certain procedure.
{:class="warning"}

> This text will appear as a red banner, for an 'alert' message. Alert flags can be used for notifications such as common problems that may occur.
{:class="alert"}

> This text will appear as a green banner, for an 'informational' message. These flags can be used for notifications such as useful links or helpful tips.
{:class="info"}

This is the main body text that explains the purpose of the procedure and any context that you might need before diving into the individual steps. The text within each step should walk the user directly through exactly what they need to do to complete the procedure.

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
