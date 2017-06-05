---
layout: default
title: Template for Contributing to GSA FICAM Guides
permalink: /template/
---

- BRING in LACHELLE'S CHANGES

- FIX ALERTS AND LINKS

{% include alert-info.html heading = "Before starting a new Guide, please review the _Contributing.md_ page!" content="The _Contributing.md_ page provides terms and conditions and other important instructions." %}

This **_Template.md_** gives instructions and templates to help you with your new Guide for the www.IDManagment.gov website, including:

  1. [**Starting Your Guide**](#starting-your-guide) 
  2. [**Example Outline Template**](#example-outline-template) 
  3. [**Markdown Template**](#markdown-template)
  4. [**Writing and Style Resources**](#writing-and-style-resources)  
  
# Starting Your Guide

This section tells you how to: 

  * Create a new **Issue** to start your guide. 
  * Add more...?
  * Select or create a new **_Branch_** in your GitHub repository where your guide will be stored 
  * Create a new **_Page_** to start your guide 
  * Use the **_Example Outline Template_** with embedded **_Markdown syntax_** to develop your guide

## Create a New Issue to Start Your Guide

To start a new guide, you first need to create a new Issue in GitHub. (If you don't have a GitHub account, you'll need to create one. A good introduction can be found here: **add link to GitHub instructions**.   ADD MORE INSTRUCTIONS...

## Select or Create a Branch for Your Guide

A branch is where your new guide (called a **Page**) will be stored in your repository. Before you create a new Page to start your guide, you need to **_select an existing branch_** or **_create a new branch_**. 

### Select an existing branch

To select an existing branch, do this: 
  
  1. At the top left area of your GitHub repository directory window (for example, PIV-Guides repository), you will see the **_Branch_** button. Click on the button's down-arrow to select an existing branch. The branch (name) shown on the button indicates where your new Page will be stored.
  
  > Once you have selected an existing branch, go to [**Create a New Page for Your Guide**](#Create-a-New-Page-for-Your-Guide).
  
### Create a new branch

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

This introductory text should give a brief overview of the subject matter covered in your guide. In addition to the subject-matter overview, it may include information on the intended audience, the intended outcome of the guide, and any other information that would help the user to understand the guide.

## Assumptions 

This section should be a bullet list that explains any assumptions that must be understood before the user can begin the procedures in the guide. This section may also include conditions that must be met before the user can begin the procedures. Alternate titles may be: **_Preconditions_** (i.e., list any conditions that must be met) or **_Hardware and Software_Requirements** (i.e, list any hardware or software that must be obtained and/or configured).

## Before You Get Started

This section will tell the user what he/she needs to do to prepare before starting a set of procedures. 

## Title of Procedure 1

This introductory text should give any user-friendly background information; explain the purpose of the procedure; and give any context that the user might need before diving into the steps. The text within each step should walk the user directly through exactly what they need to do to complete the procedure.

  1. Step 1 of procedure 1.
  2. Step 2 of procedure 1.
  
## Title of Procedure 2

This introductory text should give any user-friendly background information; explain the purpose of the procedure; and give any context that the user might need before diving into the steps. The text within each step should walk the user directly through exactly what they need to do to complete the procedure.

  1. Step 1 of the procedure 2.
  2. Step 2 of the procedure 2.
  
  > Repeat procedural sections, as needed.

# Markdown Template

This **Markdown Template** will help you to use Markdown syntax to format the content for your guide. You can learn more about Markdown formatting by browsing to the "Mastering Markdown" guide from Github: https://guides.github.com/features/mastering-markdown/.

  1. If you have not already done so, copy and paste this **Markdown Template** into your new Page.  

## Headings

The required Heading formats for the www.IDManagement.gov website are as follows:

  * Top-Level Heading (**T**itle **C**ase)
  * Second-Level Heading (**T**itle **C**ase)
  * Third-level heading (**S**entence case)
  * All lower-level headings (**S**entence case)

> In Markdown syntax, the **#** symbol is used to format headings.

# This Is a Top-Level Heading 
## This Is a Second-Level Heading
### This is a third-level heading
#### This is a fourth-level heading
##### This is a fifth-level heading

  > Start your page with a top-level heading.

## Table of Contents (TOC)

As you add sections, you can create a Table of Contents (TOC) at the top of your Page by creating a linked list like this:

- [Subsection1](#subsection1)
- [Subsection2](#subsection2)

## Main Body Paragraph

This is the main body paragraph style. 

## Bold and Italics

  * Use double asterisks to bold a word:  **bold**.
  * Use underscores to create italics:  _italics_.

## Bulleted and Numbered Lists

To create bullet lists (i.e., unordered list), use spaces (not tabs) and an asterisk, as follows:

  * Bullet 1 (Indent 2 spaces, enter an asterisk, and add 1 space.)
  * Bullet 2
    * Sub-bullet 1 (Indent 4 spaces, enter an asterisk, and add 1 space.)
    * Sub-bullet 2

  > **Note:** Markdown supports only **two** indention levels for bullet lists.

To create a numbered list (i.e., ordered list), use spaces (not tabs) and numbers. The numbers will automatically increment for you when rendered. The first numbered list will render as "1, 2, 3," etc. Even though you need to type 1, 2, etc., for a numbered sub-item list, the sub-items will render as "i, ii, iii," etc.

  1. Numbered item 1 (Indent 2 spaces, enter a number, and add 1 space. First-level numbered items will render as "1, 2, 3," etc.)
  2. Numbered item 2
     1. Numbered sub-item 1 (Indent 5 spaces, enter a number, and add 1 space. Second-level numbered items will render as "i, ii, iii," etc.)
     2. Numbered sub-item 2

  > **Note:** Markdown supports only **two** indention levels for numbered lists.

## Code Blocks

For code blocks, enter a Return, three backticks (```) before and after the code block, plus another Return:

```Text within three backticks style code or command line samples```

## Code Comments

<!--For example, this code denotes a comment, and information written inside of it will not appear on the website but can be used as a reference for others viewing the file.-->

## Images

To insert an image (graphic) into your Page, first upload the image file to the **/img/** folder in the appropriate GitHub repository.  Next, at the image insertion point in your Page, add this format to link to the image:

![This is what I want a screen reader to say for 508 compliance]({{site.baseurl}}/img/thisisthesampleimagefile.png)

  > To align an image in your Page, use the **align** instruction at the end of an image link (i.e., **"left"**, **"center"**, or **"right"**) using this format:

![Alt text for an image goes here]({{site.baseurl}}/folder that image is in/imagename.png){:align="right"}

## Alerts, Warnings, and Information Blocks

Use the Alert, Warning, or Information Block formatting to highlight specific information in your Page.


**CHANGE FOR BELOW--NEW FORMAT FOR ALERTS:**  {% include alert-info.html heading = "Before starting a new Guide, please review the _Contributing.md_ page!" content="The _Contributing.md_ page provides terms and conditions and other important instructions." %}
**FIND FORMAT FOR WARNING, ALERT, AND SUCCESS**

### Warning blocks

> This text will appear as a **warning flag**, which is a yellow banner on the website. (The ">" symbol and the coded line directly underneath the text will create the formatting for this flag.) Warning flags can be used for notifications, such as when a user should skip a certain procedure.
{:class="warning"}

### Alert blocks

> This text will appear as an **alert flag**, which is a red banner on the website. Alert flags may be used for notifications, such as common problems that may occur.
{:class="alert"}

### Information blocks

> This text will appear as **informational flag**, which is a green banner on the website. Information flags can be used for notifications such as useful links or helpful tips.
{:class="info"}

## Links to References or Other Information

To link to useful references, information, or another page (especially that may be needed to complete the procedures), use this link format: 

[This is what I want my link to say]({{site.baseurl}}/insertlink/) 

  > **Note:**  This is the **end of the Markdown Template**.

# Writing and Style Resources

For the FICAM Guides, general writing guidelines include:

  * All pages should be brief.
  * Use titles to help the user identify "jumping off points" for information.
  * Paragraphs should be short. 
  * All text should be written in plain language as much as possible. 
  * Use numbered steps, bullet lists, and graphics whenever possible. 

The following references provide additional information about plain language, writing, and style:

  * [18F Content Guide]({{site.baseurl}}/https://content-guide.18f.gov/)
  * [Federal Plain Language Guidelines]({{site.baseurl}}/http://www.plainlanguage.gov/howto/guidelines/FederalPLGuidelines/TOC.cfm/)
  * [U.S. Government Printing Office (GPO) Style Manual]({{site.baseurl}}/https://www.govinfo.gov/app/details/GPO-STYLEMANUAL-2016/)
  * [Oxford Dictionary Online]({{site.baseurl}}/https://en.oxforddictionaries.com/)
  * [Merriam Webster Dictionary Online]({{site.baseurl}}/https://www.merriam-webster.com/)

