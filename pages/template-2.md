---
layout: default
title: Contributor's Template for Writing a FICAM Guide
permalink: /template/
---

Thank you for your interest in creating a FICAM Guide! We welcome your contributions to solving a PIV, FPKI, or FICAM-Arch technical issue. This **Contributor's Template** will help you get you started on your new FICAM guide.

{% include alert-info.html heading = "Before starting a new FICAM guide, please review the _Contributing_ page!" content="The _Contributing_ page provides terms and conditions and other important instructions." %}

After reviewing the **Contributing** page, please read through the entire **Contributor's Template** before beginning. To go to a specific major section, click a link below:  

  * [**Selecting a Topic for Your Guide**](#selecting-a-topic-for-your-guide)
  * [**Using GitHub**](#Using-Github)
  * [**Structuring Your Guide and Using Markdown**](#structuring-your-guide-and-using-markdown)
  * [**Writing Guidelines**](#writing-guidelines)
  * [**Submitting Your Draft Guide**](#submitting-your-draft-guide)
  
# Selecting a Topic for Your Guide

## If You Don't Have a Topic
  
If you would like to write a FICAM Guide but don't yet have a topic, the open **Issues** lists in the GSA's GitHub repositories is a good place to start. Select a repository and then click on the **Issues** tab at the top of the repository window.

  * **PIV-Guides:**  [PIV-Guides](https://github.com/GSA/piv-guides){:target="blank"} 
  * **FPKI-Guides:**  [FPKI-Guides](https://github.com/GSA/fpki-guides){:target="blank"} 
  * **FICAM-Arch:**  [FICAM-Arch](https://github.com/GSA/ficam-arch){:target="blank"} 

If you find a topic of interest for your new guide, you will need to create a GitHub account to start the guide process. See [**Create a GitHub Account**](#create-a-github-account). If you already have a GitHub account, the next step is to "fork" a copy of the related GSA repository. See [**Create a Repository**](#create-a-repository).

## If You Already Have a Topic

If you already have a topic in mind for your new guide, you will need to create a GitHub account. See [**Create a GitHub Account**](#create-a-github-account).

# Using GitHub

This section explains how to use GitHub for developing your new guide. To go to a specific section, click a link below:

  * [Create a GitHub Account](#create-a-github-account) 
  * [Create a Repository](#create-a-repository)
  * [Create a Branch](#create-a-branch)
  * [Create a Page](#create-a-page)
  * [Create an Issue](#create-an-issue)

## Create a GitHub Account

You can create a GitHub account by browsing to: [Join GitHub](https://github.com/join). For more help, you can also contact GSA GitHub Support at: gsa-github.support@gsa.gov. 

* GitHub allows you to remain pseudonymous. You can select the options that suit you on the _Profile_ and _Emails_ pages of your _Personal Settings_ in your GitHub account.  
* We also highly encourage you to turn on **two-factor authentication** in the _Security_ page, also part of _Personal Settings_.

## Create a Repository

Once you have a GitHub account, you will need to "fork" a copy of your topic's related GSA repository. 

1. To locate the GSA repository that you want to fork, go to: [GSA Respositories at GitHub.com](https://github.com/GSA){:target="blank"}.
2. Select the repository. 
3. In the upper right-hand corner of the GSA repository screen, click on the gray **Fork** button.

> The forked GSA repo will now be in your GitHub profile.

For more help with forking a repo, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/){:target="blank"}

For the next step, see the following section, **_Create a Branch_**.

## Create a Branch

To create a new branch to store your guide:

1. In the top right-hand corner of the respository window, click on the down-arrow next to your profile icon/picture. Select **_Your profile_**.  
2. Click on the repository that you forked. (Your guide will be stored in this repository.)
3. Above the listing of folders and files in the repository, look for the gray **Branch** button. Click on the down-arrow and select the **_Staging_** branch. 

{% include alert-warning.html heading = "The GSA repository's **_Staging_** branch is the master branch for each GSA repository. It is important that you always start with the **_Staging_** branch in your forked repository when you create a new branch. Starting at **_Staging_** helps keep your repository's files sychronized with GSA's repository (e.g., PIV-Guides)." %}
  
2. Click on the **_Branch_** button again and enter your new **branch name** into the _text field_ (e.g., **_[Guide Name] Branch_**).
3. Select the blue button that now displays your new branch name.

Next, see the following section, **_Create a Page_**.
    
## Create a Page

To create a new **Page** where you can write your guide:  

1. Check the **_Branch_** button to ensure that the new branch name you created is displayed. If it isn't, select it from the drop-down list.
2. Click on the gray **_Create New File_** button located at the top right-hand area of your repository's window (above the folders and files listing).  
  
> At the top left-hand area of this window, the branch name now appears with a **"/"** after it and a text box.

4. In the text box, enter your new Page's name with the extension, **.md**, for **Markdown** (e.g., Mynewfile.md).
5. Go to the bottom of your Page. Below the **Commit new file** comment box, click on the green **Commit new file** button to save your new Page.
  
## Create an Issue

If you already have a chosen topic that was **not** on the open Issues list and have forked a repository, as well as created a branch and a page, the next step is to create an **Issue** in GitHub. 

A new **Issue** gives you the opportunity to discuss your topic and collaborate with other community members about it. Community collaboration may help bring to light related issues, insights, and new solutions. These may help you to write your guide.

To create a new Issue in GitHub:

1. Go to your forked repository and click on the **Issues** tab in the upper-right-hand area of your window just below the repository name.
2. Click on the green **New Issue** button to create a new Issue.

> An **ISSUES_TEMPLATE.md** can be found in the PIV-Guides, FPKI-Guides, and FICAM-Arch repositories to help create the Issue. For more help with **Issues**, go to: [Mastering Issues](https://guides.github.com/features/issues/){:target="blank"}.

# Structuring Your Guide and Using Markdown

To help structure your guide and use Markdown syntax, use the template included in this section. 

1. Go to the heading entitled: **Template with Markdown Syntax**. Copy all of the text and and other samples from that point up to **Template Ends Here**. 
2. Go to your new Page and click on the **pencil** symbol (top right-hand side of window). The **pencil** opens up the content writing and editing mode for your Page.
3. Click on Line 1 of your Page and paste in the copied template. 
4. Scroll down to the bottom of your screen. At the left-hand side of the screen, click on the green **Commit changes** button. (This saves the changes to your Page.)
___

# Template with Markdown Syntax

For more help with Markdown syntax, go to: [**Mastering Markdown**](https://guides.github.com/features/mastering-markdown/){:target="blank"}.

**Navigation Block and Title of Guide**

Once you have copied and pasted this **Template** into your Page, go to the **navigation block** in the upper left-hand corner of your Page. (The navigation block will be used for website navigation when your guide is posted.) Make the following changes to the navigation block:

 * **layout:** default _("Default" is the standard layout. Do not change.)_
 * **title:** Guidance Document Template _(Change the **title**, "Guidance Document Template," to your guide's title._) 
 * **permalink:** /template/ _(Change **/template/** to a short name for your guide using the "/name/" format._)


(_Main Body Paragraph_) To begin your guide, briefly state its purpose (one to two sentences).

(_Table of Contents_) After the first main body paragraph, add a TOC link for each Heading 1 section. For example:

  * [Section 1 Title](#words-in-section1-title-separated-by-dashes)
  * [Section 2 Title](#words-in-section2-title-separated-by-dashes)
  * [Section 3 Title](#words-in-section3-title-separated-by-dashes)

# Overview (Heading 1)

(_Main body paragraph_) This introductory text should be a brief overview of your guide's topic. In addition to the overview, you may include information on the intended audience, the intended outcome of the guide, and any other information that would help the user to understand the guide.

# Assumptions (Heading 1)

(_Main body paragraph_) This section should be a bullet list that explains any assumptions that must be understood before the user can begin the procedures in the guide. This section may also include conditions that must be met before the user can begin the procedures. Alternate titles may be: **Preconditions** (i.e., list any conditions that must be met) or **Hardware and Software_Requirements** (i.e, list any hardware or software that must be obtained and/or configured).

**Bullet List Items**

* Bullet 1 (Indent 2 spaces, enter an asterisk, and add 1 space.)
* Bullet 2

# Before You Get Started (Heading 1)

This section should tell the user what he/she needs to do to prepare before starting a set of procedures. 

# Title of Procedure 1 (Heading 1) 

(_Main body paragraph_) This introductory text should give any user-friendly background information; explain the purpose of the procedure; and give any context that the user might need before diving into the steps. The text within each step should directly walk the user through exactly what they need to do to complete the procedure.

> **Note:** Repeat Procedural sections as needed.

**Use additional Headings, as needed:**

## This Is a Second-Level Heading
### This is a third-level heading
#### This is a fourth-level heading
##### This is a fifth-level heading

**Bold and Italics:**

  * Use double asterisks to bold a word:  **bold**.
  * Use underscores to create italics:  _italics_.

**Number List Items:**

1. Step 1 of procedure 1. (Numbered List item - Indent 2 spaces, enter a number, and add 1 space.) 
2. Step 2 of procedure 1. (Numbered List item)

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

**Images**

To insert an image (graphic) into your Page, first upload the image file to the **/img/** folder in the appropriate GitHub repository.  Next, at the image insertion point in your Page, add this format to link to the image:

![This is what I want a screen reader to say for 508 compliance]({{site.baseurl}}/img/imagename.png)

Use these formats to align an image in your Page, use the **align** instruction at the end of an image link (i.e., **"left"**, **"center"**, or **"right"**) and/or to add a sizing instruction, such as **width:15%**.

![Text for an image goes here]({{site.baseurl}}/img/imagename.png){:align="right"}

![Text for another image goes here]({{site.baseurl}}/img/anotherimagename.png){:style="float:left;width:15%;"}

**Alerts, Warnings, and Information Blocks**

Use the Alert, Warning, Success, or Information Block formatting to highlight specific information in your Page.

* **Warning Blocks**

{% include alert-warning.html heading = "Important Warning Title!" content="Important warning text." %}

This text will appear as a **warning flag**, which is a yellow banner on the website. Warning flags can be used for notifications, such as when a user should skip a certain procedure.

* **Alerts for Notifications or Problems**

{% include alert-notification.html heading = "Important Alert Notification or Problem Title!" content="Important notification or problem text." %} <!--Is "alert-notification.html" correct? I couldn't find any template or page with an example to bring in here.-->

This text will appear as an **alert flag**, which is a red banner on the website. Alert flags may be used for notifications, such as common problems that may occur.

* **Information Alerts**

{% include alert-info.html heading = "Important Information Title!" content="Information information text." %}

This text will appear as an **information flab**, which is a green banner, for an "informational" message. Information flags can be used for notifications such as useful links or helpful tips.

* **Success Alerts** 

{% include alert-success.html heading = "Important Success Title!" content="Important success text." %}

This text will appear as a **success flag**, which is a blue banner on the website. These flags are used to let the user know they succeeded when carrying out a step or action. <!--Is this correct? I couldn't find any template or page where this was used as an example to bring in here.-->

**Links to Other Documents**

To link to useful references, information, or another page within GSA's IDManagement.gov website, use: 

[This is what I want my link to say]({{site.baseurl}}/insertlink/)

Link to an document so that it opens a new window:

[This is what I want my link to say](https://www.governmentagency.gov){:target="blank"}

### TEMPLATE ENDS HERE
___

# Writing Guidelines

When creating a FICAM Guide, the general writing guidelines are:

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
