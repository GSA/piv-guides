---
layout: default
title: Template for Contributors to GSA FICAM Guides
permalink: /template/
---

**Add LaChelle's other changes**

**FIX ALERTS AND LINKS**

{% include alert-info.html heading = "Before starting a new FICAM guide, please review the _Contributing.md_ page!" content="The _Contributing.md_ page provides terms and conditions and other important instructions." %}

This guide will help you to create a new FICAM guide. 

  * [**Starting Your Guide**](#starting-your-guide)
  * [**GSA Employees or Contractors&mdash;Using GitHub**](#gsa-employees-or-contractors-using-github)
  * [**Non-GSA Contributors&mdash;Using GitHub**](#non-gsa-contributors-using-github)
  * [**Template**](#template)
  * [**Writing and Style Resources**](#writing-and-style-resources)  
  
## Starting Your Guide

  * If you have topic in mind...**go to <<<<** 
  * If you don't yet a topic in mind...**go to <<<**
  
  Once you have a topic or found a topic you want to write about from the GitHub **Issues** list and don't already have a **GitHub account**, follow the steps for **GSA Employees or Contractor Contributors** or **Non-GSA Contributors** to create an account. 
  * If you don't already have a topic in mind, review the open Issues for a topic you would be interested in writing about in GSA's GitHub **Issues** list for the PIV-Guides, FPKI-Guides, or FICAM-Arch. 

When you have a topic in mind, you'll need to take these steps:

  * Create a GitHub **Account**.
  * Create a **Repository** and **Branch** for storing your guide. 
  * Create a new **Page** to start your guide.
  * Create a basic outline using the **template** below. 
  > **Note:**  The template is preformatted using GitHub **Markdown** syntax. (See [**How To Use Markdown**](#how-to-use-markdown) below for additional help.) 
  * Create a new **Issue** to discuss your topic and collaborate with others about it.
  * Guidelines for collaborating with colleagues and contributors. 

## GSA Employees or Contractor Contributors&mdash;Using GitHub

### Create a new GitHub account

To create your new FICAM guide, you'll need a GitHub account.  If you don't have one, you'll need to create one. GitHub offers free accounts: <!--Is there a GitHub address for just GSA employees/contractors - new accounts?-->

> For help, please see:  [Signing up for a New GitHub Account](https://help.github.com/articles/signing-up-for-a-new-github-account/). 

### Create a repository by "forking" PIV-Guides, FPKI-Guides, or FICAM-Arch

If you don't have a repository that you "forked" from GSA's FICAM guide repositories (**PIV-Guides**, **FPKI-Guides**, or **FICAM-Arch**), do this:  

1. Go to: [GSA Respositories at GitHub.com](https://github.com/GSA){:target="blank"}.
2. Select the repository you want.
3. In the upper right-hand corner of the GSA respository screen, click on the gray **Fork** button.

> This automatically places a copy of the GSA repository in your GitHub profile.

For the next steps, click on [**Create a Branch for Your Guide**](#create-a-branch-for-your-guide).

## Non-GSA Contributors&mdash;Using GitHub

### Create a new GitHub account and repository

If you are not a GSA employee or contractor, you'll also need to set up a repository. For help, go to: [Create a Repo](https://help.github.com/articles/create-a-repo/).

### Create a branch for your guide

Now that you have a GitHub account and repository, you'll need to create a **Branch** where your new guide (called a **Page**) will be stored. 

To create a new branch, do this:
  
  1. Click on the **_Branch_** button and enter a new branch name into the text field. 
  
  > The **_Branch_** button will display the new branch name. 

  2. Select the green-highlighted Branch name.  **CHECK THIS**
  
  > This Branch is where your new Page will be stored.

Once you have created a new Branch, go to [**Create a New Page for Your Guide**](#create-a-new-page-for-your-guide).
    
### Create a New Page for your guide

To create a new **_GitHub Page_** to start your guide, do this:  

  1. Check the **_Branch_** button to ensure that the branch name you selected or created is displayed. If it isn't, click on the down-arrow and select the branch name from the drop-down list.
  2. Click on the **_Create New File_** button located at the top right area of your repository's directory window.  
  > At the top left area of this window, the branch name appears with a **"/"** after it and a text box. (If you want to start over, select **_Cancel_**.) 
  4. In the text box, enter your new Page's name with the extension, **.md**, for **Markdown** (e.g., **Mynewfile.md**).
  5. Scroll down to the bottom of your screen. At the left side of your screen, below the **Commit new file** comment box, click on the green button that says **Commit new file**.
  > This creates and saves your new Page in your selected or new branch.

### Copy and Paste the Template below into your new Page

  1. At the top right area of your Page's content window, click on the **pencil** symbol.

  > You will use this mode to create and edit content for your guide.
  
  2. **Select all of the Template content below. Copy and paste the content into your Page.**
  3. Change the **title**, "Guidance Document Template," to your guide's title (for example, _My Technical Guide_).
  4. Change the **permalink** title to a short version of your guide's title (for example, _/myguide/_.
  
  > The **permalink** title should be in the format: **/mypage/**, instead of _mypage.md_ 
  
  6. Once you have made these changes, scroll down to the bottom of your screen. At the left side of the screen, click on the green button that says **Commit changes.**
  
  > This action saves all of your changes to your Page. When you are ready, you can use the Template as the basis for writing your guide. 

# Markdown Syntax

  * The Template below is already formatted in Markdown syntax for you to use.  
  * Copy and paste the Template into your Page.
  
  > For more on Markdown, go to:  [**Mastering Markdown**](https://guides.github.com/features/mastering-markdown/){:target="blank"}.

Now that you have created a new Page to start your guide, this **Template** will help you to structure and develop content for your guide.

  1. If you have not already done so, copy and paste the **Template** below into your new Page.
  
# Template


# A Word about the Navigation Block (above) and Title of Your FICAM Guide
---
layout: default
title: Guidance Document Template 
permalink: /template/
---

  1. **layout: default**. This field always stays the same. No changes are necessary.
  2. **title: [document title]**.  On your Page (Markdown), you _won't_ see a main title. The **Title** field automatically adds the title to your guide when it is posted on the IDManagement.gov website.
  3. **permalink: /[name]/**. The **permalink** should be a short name for your document title. Change **/template/** to a short name for your guide.

Add a **Table of Contents (TOC)** (links) after the main body's first paragraph. Create a linked list like this:

  * [Section 1 Title](#words-in-section3-title-separated-by-dashes)
  * [Section 2 Title](#words-in-section2-title-separated-by-dashes)
  * [Section 3 Title](#words-in-section3-title-separated-by-dashes)

# Overview (Heading 1)

(Main body paragraph) This introductory text should give a brief overview of the subject matter covered in your guide. In addition to the subject-matter overview, it may include information on the intended audience, the intended outcome of the guide, and any other information that would help the user to understand the guide.

# Assumptions (Heading 1)

(Main body paragraph) This section should be a bullet list that explains any assumptions that must be understood before the user can begin the procedures in the guide. This section may also include conditions that must be met before the user can begin the procedures. Alternate titles may be: **_Preconditions_** (i.e., list any conditions that must be met) or **_Hardware and Software_Requirements** (i.e, list any hardware or software that must be obtained and/or configured).

# Before You Get Started (Heading 1)

This section will tell the user what he/she needs to do to prepare before starting a set of procedures. 

# Title of Procedure 1 (Heading 1)

This introductory text should give any user-friendly background information; explain the purpose of the procedure; and give any context that the user might need before diving into the steps. The text within each step should walk the user directly through exactly what they need to do to complete the procedure.

## This Is a Second-Level Heading (Use other Headings as needed)
### This is a third-level heading
#### This is a fourth-level heading
##### This is a fifth-level heading

  1. Step 1 of procedure 1. (Numbered List item)
  2. Step 2 of procedure 1. (Numbered List item)

  > **Note:** or call-out needed. (**Citation??**)
  
# Title of Procedure 2 (Heading 1)

This introductory text should give any user-friendly background information; explain the purpose of the procedure; and give any context that the user might need before diving into the steps. The text within each step should walk the user directly through exactly what they need to do to complete the procedure.

## This Is a Second-Level Heading (Use other Headings as needed)
### This is a third-level heading
#### This is a fourth-level heading
##### This is a fifth-level heading

  1. Step 1 of procedure 1. (Numbered List item)
  2. Step 2 of procedure 1. (Numbered List item)

  > **Note:** or call-out needed. (**Citation??**)
  
  > Repeat procedural sections, as needed.

++++++++++++++++++++

## Headings

> In Markdown syntax, the **#** symbol is used to format headings.

# This Is a Top-Level Heading 
## This Is a Second-Level Heading
### This is a third-level heading
#### This is a fourth-level heading
##### This is a fifth-level heading


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

  > **Note:** Markdown for the GSA FICAM Guides supports only **one** numbered list level (no second-level items).

## Code Blocks

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

## Code Comments

<!--For example, this code denotes a comment, and information written inside of it will not appear on the website but can be used as a reference for others viewing the file.-->

## Images

To insert an image (graphic) into your Page, first upload the image file to the **/img/** folder in the appropriate GitHub repository.  Next, at the image insertion point in your Page, add this format to link to the image:

![This is what I want a screen reader to say for 508 compliance]({{site.baseurl}}/img/thisisthesampleimagefile.png)

  > To align an image in your Page, use the **align** instruction at the end of an image link (i.e., **"left"**, **"center"**, or **"right"**) using this format:

![Alt text for an image goes here]({{site.baseurl}}/folder that image is in/imagename.png){:align="right"}

## Alerts, Warnings, and Information Blocks

Use the Alert, Warning, or Information Block formatting to highlight specific information in your Page.

{% include alert-info.html heading = "Before starting a new Guide, please review the _Contributing.md_ page!" content="The _Contributing.md_ page provides terms and conditions and other important instructions." %}

**FIND FORMAT FOR WARNING, ALERT, AND SUCCESS - CHANGE ALL BELOW TO SAME FORMAT**

### Warning blocks

This text will appear as a **warning flag**, which is a yellow banner on the website. (The ">" symbol and the coded line directly underneath the text will create the formatting for this flag.) Warning flags can be used for notifications, such as when a user should skip a certain procedure.
{:class="warning"}

### Alerts for Notifications or Problems

This text will appear as an **alert flag**, which is a red banner on the website. Alert flags may be used for notifications, such as common problems that may occur.
{:class="alert"}

### Information Alerts

This text will appear as **informational flag**, which is a green banner on the website. Information flags can be used for notifications such as useful links or helpful tips.
{:class="info"}

### Success Alerts **BLUE BANNER??**

This text will appear as **success flag**, which is a **blue?** banner on the website. These flags are used to let the user know they succeeded when carrying out a step or action. 

## Links to Other Documents

To link to useful references, information, or another page within GSA's IDManagement.gov website, use: 

[This is what I want my link to say]({{site.baseurl}}/insertlink/)<!--Is that correct for this type of link?-->

Link to an document outside the GSA IDManagment.gov website (opens a new window):

[This is what I want my link to say](https://www.governmentagency.gov){:target="_blank"}

# Writing and Style Resources

For the FICAM Guides, general writing guidelines include:

  * All pages should be brief.
  * Use titles to help the user identify "jumping off points" for information.
  * Paragraphs should be short. 
  * All text should be written in plain language as much as possible. 
  * Use numbered steps, bullet lists, and graphics whenever possible. 

The following references provide additional information about plain language, writing, and style:

Link to an outside document (opens a new window):
[open source](https://github.com/gsa/fpki-guides){:target="_blank"}

  * [18F Content Guide](https://content-guide.18f.gov/){:target="_blank"}
  * [Federal Plain Language Guidelines](http://www.plainlanguage.gov/howto/guidelines/FederalPLGuidelines/TOC.cfm/){:target="_blank"}
  * [U.S. Government Printing Office (GPO) Style Manual](https://www.govinfo.gov/app/details/GPO-STYLEMANUAL-2016/){:target="_blank"}
  * [Oxford Dictionary Online](https://en.oxforddictionaries.com/){:target="_blank"}
  * [Merriam Webster Dictionary Online](https://www.merriam-webster.com/){:target="_blank"}

