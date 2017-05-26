---
layout: default
title: Guidance Document Template
permalink: /template/
---
# Contributing to the GSA FICAM Guides

> Before starting a new Guide, please read the **_Contributing.md_** Page, which is located in the **_GSA GitHub repositories for the PIV-Guides, FPKI-Guides, and FICAM-Arch_**. The **_Contributing.md_** Page provides terms and conditions and other important instructions.{:class="info"}

This **_Template.md_** gives instructions and templates to help you with your new Guide for the www.IDManagment.gov website, including:

  1. [**Starting Your Guide**](#Starting-Your-Guide) 
  2. [**Example Outline Template**](#Example-Outline-Template) 
  3. [**Markdown Template**](#Markdown-Template)
  4. [**Writing and Style Resources**](#Writing-and-Style-Resources)  
  
# Starting Your Guide

This section tells you: 

  * How to select or create a new **_Branch_** in your GitHub repository where you want your guide to be stored 
  * How to create a new **_Page_** to start your guide 
  * How to use the **_Example Outline Template_** and **_Markdown Template_** to develop your guide

## Select or Create a Branch for Your Guide

A branch is where your new guide (called a **Page**) will be stored in your repository. Before you create a new Page to start your guide, you need to **_select an existing branch_** or **_create a new branch_**. 

### Select an Existing Branch

To select an existing branch, do this: 
  
  1. At the top left area of your GitHub repository directory window (for example, PIV-Guides repository), you will see the **_Branch_** button. Click on the button's down-arrow to select an existing branch. The branch (name) shown on the button is where your new Page will be stored.
  
  > Once you have selected an existing branch, go to [**Create a New Page for Your Guide**](#Create-a-New-Page-for-Your-Guide).
  
### Create a New Branch

To create a new branch, do this:
  
  1. Click on the **_Branch_** button and enter a new branch name into the text field.  
  
  > The **_Branch_** button will display the new branch name. This is where your new Page will be stored.
  
## Create a New Page to Start Your Guide

To create a new **_Page_** to start your guide, do this:  

  1. Check the **_Branch_** button to ensure that the branch name you selected or created is displayed. If it isn't, click on the down-arrow and select the branch name from the drop-down list.
  2. Click on the **_Create New File_** button located at the top right area of your repository's directory window.  
  > At the top left area of this window, the branch name appears with a **"/"** after it and a text box. (If you want to start over, select **_Cancel_**.) 
  4. In the text box, enter your new Page's name with the extension, **.md**, for **Markdown** (e.g., **Mynewfile.md**).
  5. Scroll down to the bottom of your screen. At the left side of your screen, below the **Commit new file** comment box, click on the green button that says **Commit new file**.
  > This creates and saves your new Page in your selected or new branch.

## Copy and Paste the Content from the **_Template.md_** into your new Page.

  1. At the top right area of your Page's content window, click on the **pencil** symbol.

  > Your Page window is now in editing view (i.e., also Markdown content creation mode). You will use this view to create content for your guide.
  
  2. Select all of the content in this **_Template.md_** page. Copy and paste the content into your Page.
  
  3. When you are ready, delete the **Template.md** _introductory text and steps to select/create a branch and a Page_, but keep the the following:
  
<UL><UL>
<LI> Document <b>navigation block</b> (at the top left corner of your Page window). (See example below.) 
<LI> The <b>Example Outline</b>. (See **Templates** section below.)
<LI> The <b>Markdown Template</b>. (See **Templates** section below.)
</UL></UL>

   ```
       ---
       layout: default
       title: Guidance Document Template 
       permalink: /template/
       ---
   ```
<BR>

  4. Once you have deleted the introductory text and steps, go to the top left corner of your new Page.
  5. Change the **title**, "Guidance Document Template," to your guide's title (for example, _My Technical Guide_).
  6. Change the **permalink** title to a short version of your guide's title (for example, _/myguide/_.<BR>
  > The **permalink** title should be in the format: **/mypage/**, instead of _mypage.md_  
  7. Once you have made these changes, scroll down to the bottom of your screen. At the left side of the screen, click on the green button that says **Commit changes.**<BR>
  > This action saves all of your changes to your Page.

# TEMPLATES

# Example Outline Template

Now that you have created a new Page to start your guide, this **Example Outline** will help you to structure and develop content for your guide.

  1. If you have not already done so, copy and paste this **Example Outline** into your new Page.

## Overview

This text should give a brief overview of the subject matter covered in your guide. In addition to the subject-matter overview, it may include information on the intended audience, the intended outcome of the guide, and any other information that would help the user to understand the guide.

## Assumptions 

This section should be a bullet list that explains any assumptions that must be understood before the user can begin the procedures in the guide. Alternatively, this section may include conditions that must be met before the user can begin the procedures. Alternate titles may be: **_Preconditions_** (i.e., list any conditions that must be met) or **_Hardware and Software_Requirements** (i.e, list any hardware or software that must be obtained and/or configured).

## Before You Get Started

This section will tell the user what he/she needs to do to prepare before starting a set of procedures. 

## Title of Procedure 1

This paragraph should give user-friendly background information, introduce the procedure, and then give the detailed procedures in simple statements.

  1. Step 1 of procedure 1.
  2. Step 2 of procedure 1.
  
## Title of Procedure 2

This paragraph should give user-friendly background information, introduce the procedure, and then give the detailed procedures in simple statements.

  1. Step 1 of the procedure 2.
  2. Step 2 of the procedure 2.
  
  > Repeat procedural sections, as needed.

# Markdown Template

This **Markdown Template** will help you to use Markdown syntax to format the content for your guide. You can learn more about Markdown formatting by browsing to the "Mastering Markdown" guide from Github: https://guides.github.com/features/mastering-markdown/

  1. If you have not already done so, copy and paste this **Markdown Template** into your new Page.  

## Headings

In Markdown, the **#** symbol is used to format headers.

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

  * Use double asterisks to bold a word:  **bold**.
  * Use underscores to create italics:  _italics_.

## Bulleted and Numbered Lists

Use two spaces, an asterisk, plus one space to start a bullet list.   use the dash, followed by two spaces.

  * Bullet 1 (Indent 2 spaces, plus an asterisk and 1 space.)
  * Bullet 2
    * Sub-bullet 1 (Indent 4 spaces, plus an asterisk and 1 space.)
    * Sub-bullet 2

Use two spaces and type "**_1._**," etc., to create a numbered item. You must type each number. The numbers will automatically increment for you when rendered. The first numbered list will render as "1, 2, 3," etc.  Even though you must type 1, 2, etc., for the numbered sub-item list, the sub-items will render as "i, ii, iii," etc.

  > **Note:** Markdown supports only **two** indention levels for numbered lists.

  1. Numbered item 1 (Indent 2 spaces, plus a number and 1 space. First-level numbered items will render as "1, 2, 3," etc.)
  2. Numbered item 2
      1. Numbered sub-item 1 (Second-level numbered items will render as "i, ii, iii," etc.)
      2. Numbered sub-item 2

## Code Blocks

For code blocks, enter three backticks (```) before and after the code example:

```Text within three backticks style code or command line samples```

## Code Comments

<!--For example, this code denotes a comment, and information written inside of it will not appear on the website but can be used as a reference for others viewing the file.-->

## Images

To insert an image (graphic) into your page, first upload the image file to the **/img/** folder in the appropriate GitHub **repository**.  Next, use this format to link to the image:

![This is what I want a screen reader to say for 508 compliance]({{site.baseurl}}/img/thisisthesampleimagefile.png)

  > To align an image on a page, use the **align** instruction at the end of an image link (i.e., **"left"**, **"center"**, or **"right"**) using this format:

  > ![Alt text for an image goes here]({{site.baseurl}}/folder that image is in/imagename.png){:align="right"}

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

  > # End of Markdown Template


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
