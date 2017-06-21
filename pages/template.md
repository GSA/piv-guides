---
layout: default
title: Contributor's Template for Writing a FICAM Guide
permalink: /template/
---

Thank you for your interest in writing a FICAM Guide! We welcome your contributions to solving a PIV, FPKI, or FICAM-Arch technical issue. 

This **Contributor's Template** will help you get started with writing your new FICAM guide.

{% include alert-info.html heading = "Before starting a new FICAM guide, please review the _Contributing_ page!" content="The _Contributing_ page provides terms and conditions and other important instructions." %}

After reviewing the **Contributing** page, please read through this entire **Contributor's Template** before beginning. Click on a link below to go to a specific section:  

* [**Selecting a Topic for Your Guide**](#selecting-a-topic-for-your-guide)
* [**Using GitHub**](#Using-Github)
* [**Structuring Your Guide and Using Markdown Text Editor**](#structuring-your-guide-and-using-markdown-text-editor)
* [**Writing Guidelines**](#writing-guidelines)
* [**Submitting Your Draft Guide**](#submitting-your-draft-guide)
  
# Selecting a Topic for Your Guide

## If You Don't Have a Topic
  
If you would like to write a FICAM Guide but don't yet have a topic, a good place to start is to review the open **Issues** lists in the GSA's GitHub repositories. To review the open Issues, select a repository and then click on the **Issues** tab at the top of the repository window. The FICAM-related repositories can be found at:

* **PIV-Guides:**  [PIV-Guides](https://github.com/GSA/piv-guides){:target="blank"} 
* **FPKI-Guides:**  [FPKI-Guides](https://github.com/GSA/fpki-guides){:target="blank"} 
* **FICAM-Arch:**  [FICAM-Arch](https://github.com/GSA/ficam-arch){:target="blank"} 

If you find an Issue of interest and want to write a new guide to address it, you will first need to create a GitHub account. To create a GitHub account, see [**Create a GitHub Account**](#create-a-github-account). If you already have an account, the next step is to "_fork_" a copy of the GSA repository related to your topic. For help with forking a repository, see the section called [**Create a Repository**](#create-a-repository).

## If You Already Have a Topic

If you already have a topic in mind for your new guide, you will need to create a GitHub account to start the guide process. For help creating an account, go to [**Create a GitHub Account**](#create-a-github-account).

If you already have a GitHub account; a forked GSA repository related to your topic; a Branch; and a Page, see the section called [Create an Issue](#create-an-issue) for the next step in the guide process.

# Using GitHub

GitHub is the collaboration platform used by GSA for developing the FICAM Guides. This section explains how to use GitHub. Click on a link below to go to a specific section:

* [Create a GitHub Account](#create-a-github-account) 
* [Create a Repository](#create-a-repository)
* [Create a Branch](#create-a-branch)
* [Create a Page](#create-a-page)
* [Create an Issue](#create-an-issue)

## Create a GitHub Account

You can create a GitHub account by browsing to: [Join GitHub](https://github.com/join). For more help, contact GSA GitHub Support at: gsa-github.support@gsa.gov. 

* GitHub allows you to remain pseudonymous. You can select the options that suit you on the _Profile_ and _Emails_ pages of your _Personal Settings_ in your GitHub account.  
* We also highly encourage you to turn on **two-factor authentication** in the _Security_ page (also part of _Personal Settings_).

## Create a Repository

Once you have a GitHub account, you will need to create a personal copy (called a "_fork_") of the GSA repository related to your topic: 

1. To locate the GSA repository that you want to _fork_, go to [GSA Respositories at GitHub.com](https://github.com/GSA){:target="blank"}.
2. Select a GSA repository. 
3. In the upper right-hand corner of the selected GSA repository screen, click on the gray **Fork** button.

> The forked GSA repo will now be in your GitHub profile.

For more help with forking a repo, go to [Fork a Repo](https://help.github.com/articles/fork-a-repo/){:target="blank"}

For the next steps, see the following section, **_Create a Branch_**.

## Create a Branch

To create a new branch to store your guide:

1. In the top right-hand corner of the respository window, click on the down-arrow next to your profile icon/picture. Select **_Your profile_**.  
2. Click on the repository that you forked. 
3. Above the listing of folders and files in the repository, look for the gray **Branch** button. Click on the down-arrow and select the **_Staging_** branch. 

{% include alert-warning.html heading = "The GSA repository's **_Staging_** branch is the master branch for each GSA repository. It is important that you always start with the **_Staging_** branch in your forked repository when you create a new branch. Starting at **_Staging_** helps keep your files sychronized with GSA's repository (e.g., PIV-Guides)." %}
  
4. Click on the **_Branch_** button again and enter a new **branch name** into the _text field_ (e.g., **_[Guide Name] Branch_**).
5. Click on the blue button that now displays your new branch name. (The gray Branch button now also displays your branch name.)

For the next steps, see the following section, **_Create a Page_**.
    
## Create a Page

To create a new **Page** where you can write your guide:  

1. Check the gray **_Branch_** button to ensure that the new branch name is displayed. If it isn't, select it from the Branch drop-down list.
2. Click on the gray **_Create New File_** button located above the top right-hand area of your repository's window (above the folders and files listing).  
  
> At the top left-hand area of the Page window, the branch name now appears with a **"/"** after it and a text box.

3. In the text box, enter your new Page's name with the extension, **.md**, for **Markdown** (e.g., Mynewfile.md).
4. Go to the bottom of your Page. Below the **Commit new file** comment box, click on the green **Commit new file** button to save your new Page.

The next steps, see the following section, **Create an Issue**.
  
## Create an Issue

If you already have a chosen topic that was **not** on the open Issues list and have forked a repository, as well as created a branch and a page, the next step is to create an **Issue** in GitHub, where you can discuss and collaborate with others about your topic. 

To create a new Issue in GitHub:

1. Go to your forked repository and click on the **Issues** tab in the upper right-hand area of your window just below the repository name.
2. Click on the green **New Issue** button to create a new Issue.

> An **ISSUES_TEMPLATE.md** can be found in the PIV-Guides, FPKI-Guides, and FICAM-Arch repositories to help create the Issue. For more help with **Issues**, go to: [Mastering Issues](https://guides.github.com/features/issues/){:target="blank"}.

# Structuring Your Guide and Using Markdown Text Editor

This section provides a Template to help you: 

* Structure your guide by using a suggested outline as a starting point. 
* Use the Markdown Text Editor (i.e., syntax instructions) to write your guide.  

To begin your guide, copy and paste the Template below into your GitHub Page: 

1. Go to the section below called **Template with Markdown Syntax**. Copy the entire Template (headings, text, and samples) up to **Template Ends Here**. 
2. Now, go to your new GitHub Page and click on the **pencil** symbol (top right-hand side of window). The **pencil** opens Markdown's writing and editing mode.
3. Next, click on Line **1** of your Page (top left-hand corner) and paste in the copied Template. 
4. Scroll down to the bottom of your Page window. Click on the green **Commit changes** button to save the Template to your Page.

Basic Markdown syntax is embedded in the Template. If you want to learn more about syntax options, go to: [**Mastering Markdown**](https://guides.github.com/features/mastering-markdown/){:target="blank"}.

___

# Template with Markdown Syntax

**Navigation Block and Title of Guide**

Once you have copied and pasted this **Template** into your Page, go to the **navigation block** in the upper left-hand corner of your Page (Lines 1-5). (The navigation block is used for website navigation when your guide is posted.) Make the following changes to the navigation block:

* **layout:** default _("Default" is the standard layout. Do not change.)_
* **title:** Guidance Document Template _(Change the **title**, "Guidance Document Template," to your guide's title._) 
* **permalink:** /template/ _(Change **/template/** to a short name for your guide using the "/name/" format._)
 
**Template Styles and Syntax**

(_Main Body Paragraph_) To begin your guide, briefly state its purpose (one to two sentences).

(_Table of Contents_) After the first main body paragraph, add a TOC link for each Heading 1 section. For example:

* [Section 1 Title](#words-in-section1-title-separated-by-dashes)
* [Section 2 Title](#words-in-section2-title-separated-by-dashes)
* [Section 3 Title](#words-in-section3-title-separated-by-dashes)

# Overview (Heading 1)

(_Main body paragraph_) This introductory text should be a brief overview of your guide's topic. In addition to the overview, you may include information on the intended audience, the intended outcome of the guide, and any other information that would help the user to understand the guide.

# Assumptions (Heading 1)

(_Main body paragraph_) This section should be a bullet list that explains any assumptions that must be understood before the user can begin the procedures in the guide. This section may also include conditions that must be met before the user can begin the procedures. Alternate titles may be: **Preconditions** (i.e., list any conditions that must be met) or **Hardware and Software_Requirements** (i.e, list any hardware or software that must be obtained and/or configured).

# Before You Get Started (Heading 1)

This section should tell the user what he/she needs to do to prepare before starting a set of procedures. 

**Use additional Headings, as needed:**

## This Is a Second-Level Heading
### This is a third-level heading
#### This is a fourth-level heading
##### This is a fifth-level heading

# Title of Procedure 1 (Heading 1) 

(_Main body paragraph_) This introductory text should give any user-friendly background information; explain the purpose of the procedure; and give any context that the user might need before diving into the steps. The text within each step should directly walk the user through exactly what they need to do to complete the procedure.

(_Main body paragraph_) Add introductory text for Procedure 1, as needed.

_Add as many Procedural sections as needed._

## Title of Procedure 1, Sub-Procedure 1 (Heading 2)

(_Main body paragraph_) Add introductory text for Sub-Procedure 1, as needed. 

_Add as many Sub-Procedures as needed._

## Title of Procedure 1, Sub-Procedure 2 (Heading 2)

(_Main body paragraph_) Add introductory text for Sub-Procedure 2, as needed. 

**Number List Items:**

1. Step 1 of procedure 1. (Numbered List item - Indent 2 spaces, enter a number, and add 1 space.) 
2. Step 2 of procedure 1. (Numbered List item)

**Bullet List Items**

* Bullet 1 (Indent 2 spaces, enter an asterisk, and add 1 space.)
* Bullet 2

**Bold and Italics:**

* Use double asterisks to bold a word:  **bold**.
* Use underscores to create italics:  _italics_.

> **Note:** or call-out indented block.

**Code Blocks**

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

**Code Comments**

<!--For example, this code denotes a comment. The comment will not appear on the website but can be used as a reference for others viewing the file.-->

# Title of Procedure 2 (Heading 1)

(_Main body paragraph_) Add introductory text for Procedure 2, as needed. 

## Title of Procedure 2, Sub-Procedure 1 (Heading 2)

(_Main body paragraph_) Add introductory text for Sub-Procedure 1, as needed. 

## Title of Procedure 2, Sub-Procedure 2 (Heading 2)

(_Main body paragraph_) Add introductory text for Sub-Procedure 2, as needed. 

## Additional Markdown Syntax

**Images**

To insert an image (graphic) into your Page, first upload the image file to the **/img/** folder in the appropriate GitHub repository.  Next, at the image insertion point in your Page, add this format to link to the image:

![This is what I want a screen reader to say for 508 compliance]({{site.baseurl}}/img/imagename.png)

Use these formats to align an image in your Page, use the **align** instruction at the end of an image link (i.e., **"left"**, **"center"**, or **"right"**) and/or to add a sizing instruction, such as **width:15%**.

![Text for an image goes here]({{site.baseurl}}/img/imagename.png){:align="right"}

![Text for another image goes here]({{site.baseurl}}/img/anotherimagename.png){:style="float:left;width:15%;"}&nbsp;

**Alert Blocks:  Information, Warning, Success, and Error**

Use the Alert block formatting for Information, Warning, Success, and Error Alerts to highlight specific information in your guide.

* **Information Alerts**

{% include alert-info.html heading = "Important Information Title!" content="Information information text." %}

This text will appear as an **information flag**, which is a blue banner on the website. These flags are used for "informational" messages or notifications, such as useful links or helpful tips.

* **Warning Alerts**

{% include alert-warning.html heading = "Important Warning Title!" content="Important warning text." %}

This text will appear as a **warning flag**, which is a yellow banner on the website. Warning flags are used for notifications, such as when a user should skip a certain procedure.

* **Error Alerts (Notifications or Problems)**

{% include alert-error.html heading = "Important Alert Notification or Problem Title!" content="Important notification or problem text." %}

This text will appear as an **error flag**, which is a red banner on the website. Error flags are used for notifications, such as common problems that may occur.

* **Success Alerts** 

{% include alert-success.html heading = "Important Success Title!" content="Important success text." %}

This text will appear as a **success flag**, which is a greeb banner on the website. Success flags are used to let the user know they succeeded when carrying out a step or action. 

**Links to Other Documents**

To link to useful references, information, or another page within GSA's IDManagement.gov website, use: 

[This is what I want my link to say]({{site.baseurl}}/insertlink/)

Link to an document so that it opens a new window:

[This is what I want my link to say](https://www.governmentagency.gov){:target="blank"}

## TEMPLATE ENDS HERE
___

# Writing Guidelines

When creating a FICAM Guide, some general writing guidelines are:

  * All pages should be brief.
  * Use titles to help the user identify "jumping off points" for information.
  * Paragraphs should be short. 
  * All text should be written in plain language and a user-friendly tone as much as possible. 
  * Use numbered steps, bullet lists, and graphics whenever possible.
  
## Writing and Style Resources

The following sources provide additional information about plain language, writing, and style:

Link to an outside document (opens a new window):
[open source](https://github.com/gsa/fpki-guides){:target="_blank"}

  * [18F Content Guide](https://content-guide.18f.gov/){:target="_blank"}
  * [Federal Plain Language Guidelines](http://www.plainlanguage.gov/howto/guidelines/FederalPLGuidelines/TOC.cfm/){:target="_blank"}
  * [U.S. Government Printing Office (GPO) Style Manual](https://www.govinfo.gov/app/details/GPO-STYLEMANUAL-2016/){:target="_blank"}
  * [Oxford Dictionary Online](https://en.oxforddictionaries.com/){:target="_blank"}
  * [Merriam Webster Dictionary Online](https://www.merriam-webster.com/){:target="_blank"}
  
# Submitting Your Draft Guide
<!--This information is pertinent to this contributor's template, but I wasn't sure it was up-to-date. Alternately, I could bring the updated text into this template. What are your thoughts?-->
Please visit the **contribute_addpage.md** in your topic's related GSA repository for the steps needed to submit your draft guide.

If you have a question during the contribution process, do not hesitate to open an Issue requesting clarification. You can also email us at icam@gsa.gov. <!--Is this address still good?-->

