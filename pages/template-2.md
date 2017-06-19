---
layout: default
title: Contributor's Template for Writing a FICAM Guide
permalink: /template/
---

**Add LaChelle's other changes**

**FIX ALERTS AND LINKS**

Thank you for your interest in creating a FICAM Guide! We welcome your contribution to solving a PIV, FPKI, or FICAM-Arch technical issue. 

{% include alert-info.html heading = "Before starting a new FICAM guide, please review the _Contributing_ page!" content="The _Contributing_ page provides terms and conditions and other important instructions." %}

The purpose of this **Contributor's Template** is to help you get you started on your new FICAM guide.

After reading the _Contributing_ page, it is recommended that you read this entire _Contributor's Template_. If you want to go to a specific section, click on one of the links below:  

  * [**Selecting a Topic for Your Guide**](#selecting-a-topic-for-your-guide)
  * [**Using GitHub**](#Using-Github)
  * [**Structuring Your Guide and Using Markdown**](#structuring-your-guide-and-using-markdown)
  * [**Resources for Writing and Style**](#resources-for-writing-and-style)  
  
# Selecting a Topic for Your Guide

## If You Don't Have a Topic
  
**If you would like to write a guide but don't yet have a topic** &mdash; A good place to start is to look at the open **Issues** lists in the GSA GitHub repositories. The open **Issues** lists discuss many technical issues in search of contributors.

To review the open **Issues** lists, select a repository:

  * **PIV-Guides:**  [PIV-Guides](https://github.com/GSA/piv-guides){:target="blank"} 
  * **FPKI-Guides:**  [FPKI-Guides](https://github.com/GSA/fpki-guides){:target="blank"} 
  * **FICAM-Arch:**  [FICAM-Arch](https://github.com/GSA/ficam-arch){:target="blank"} 

**Once you select a topic** &mdash; The next step is to create a GitHub account, if you don't have one. See [**Create a GitHub Account**](#create-a-github-account). If you already have an account, see the steps below to [**Create a Repository**](#create-a-repository) to "fork" the GSA repos related to your topic.

## If You Already Have a Topic

**If you already have a topic for your new guide** &mdash; The first step is to create a GitHub account, if you don't have one. (See the next section, **_Create a GitHub Account_**.

# Working with GitHub

This sections explains how to:

  * [Create a GitHub Account](#create-a-github-account) 
  * [Create a Repository](#create-a-repository)
  * [Create a Branch](#create-a-branch)
  * [Create a Page](#create-a-page)
  * [Create an Issue](#create-an-issue)

## Create a GitHub Account

For help with creating a GitHub account, go to: [Signing up for a New GitHub Account](https://help.github.com/articles/signing-up-for-a-new-github-account/). For more help, you can contact GSA GitHub Support at: gsa-github.support@gsa.gov. 

## Create a Repository

Once you have a GitHub account, you will need to create a copy of the GSA repository related to your topic. (A personal copy of a GitHub repository is called a "fork." When you have a forked repository, you can create a new file and work on it without affecting GSA's original repository.)

1. To locate the GSA repository that you want to fork, go to: [GSA Respositories at GitHub.com](https://github.com/GSA){:target="blank"}.
2. Select the repository. 
3. In the upper right-hand corner of the GSA repository screen, click on the gray **Fork** button.

> The forked GSA repo will now be in your GitHub profile.

For more help with forking a repo, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/){:target="blank"}

Now that you have a forked repo, you need to create a new branch to store your guide. See the next section, **_Create a Branch_**.

## Create a Branch

To create a new branch to store your guide:

1. Make sure you are in your profile area. In the top right-hand corner of the respository screen, click on the down-arrow next to your profile icon/picture. Select **_Your profile_**.  
2. Click on the personal repository where you want to store your guide.
3. Just above the listing of folders and files in the repository, go to the gray **_Branch_** button. Click on the down-arrow in the **_Branch_** button and select the **_Staging_** branch. 

{% include alert-info.html heading = "The GSA repository's **_Staging_** branch is the master branch for each GSA repository. It is important that you always start with the **_Staging_** branch in your forked repository when you create a new branch. Starting at **_Staging_** helps keep your repository's files sychronized with GSA's repository (e.g., PIV-Guides)." %}
  
2. Click on the **_Branch_** button and enter your new **branch name** into the _text field_ (e.g., **_[Guide Name] Branch_**).
3. Select the blue button that now displays your new branch name.
  
> The gray **_Branch_** button now also displays your new branch name. 

Now that you have a new branch to store your guide, you need to create a new **"Page"**, where you can write your guide. See the next section, **_Create a Page_**.
    
## Create a Page

To create a new **Page** where you can write your guide:  

1. Check the **_Branch_** button to ensure that the branch name you created is displayed. If it isn't, click on the down-arrow and select the new branch name from the drop-down list.
2. Click on the gray **_Create New File_** button located at the top right-hand area of your repository's window (above the folders and files listing).  
  
> At the top left-hand area of this window, the branch name now appears with a **"/"** after it and a text box. (If you want to start over, select **_Cancel_**.)

4. In the text box, enter your new Page's name with the extension, **.md**, for **Markdown** (e.g., **Mynewfile.md**).

> **Note:**  In GitHub, all text files must be written using the **Markdown** text editor.

5. Scroll down to the bottom of your screen. At the left side of your screen, below the **Commit new file** comment box, click on the green button that says **Commit new file**.

> This creates and saves your new Page in your new branch.
  
## Create an Issue

Once you have a topic for your guide, a forked repository, a branch, and a page, the next step is to create an **Issue** in GitHub. A new **Issue** gives you a forum to discuss and collaborate with other community members about your topic. Collaboration with community members may help bring to light other related issues, insights, and new solutions and these may help you to write your guide.

To create a new Issue in GitHub:

1. Go to your forked repository and click on the **Issues** tab in the upper-right area of your window just below the repository's name.
2. Click on the green **New Issue** button to create a new Issue.
3. A helpful template to use for writing your Issue summary can be found in the PIV-Guides, FPKI-Guides, and FICAM-Arch repositories at the main directory level in the **ISSUES_TEMPLATE.md** file. 

For more help with **Issues**, go to:  [Mastering Issues](https://guides.github.com/features/issues/){:target="blank"}.

# Structuring Your Guide and Using Markdown

The template below will help you to structure your guide and use Markdown syntax, which is GitHub's required text editor. 

1. See the following header, **Template with Markdown Syntax**. Copy the text up to **Template Ends Here**. 
2. Paste the text into your new GitHub Page. 
3. At the top right-hand area of your new **Page's** window, click on the **pencil** (content writing and editing mode).
4. Once you have made these changes, scroll down to the bottom of your screen. At the left side of the screen, click on the green button that says **Commit changes.** (This saves all changes to your Page.)
  
> For more on Markdown, go to:  [**Mastering Markdown**](https://guides.github.com/features/mastering-markdown/){:target="blank"}.
___

# Template with Markdown Syntax

## Navigation Block and Title of Guide

Once you have copied and pasted this **Template** into your Page, follow the steps below to make a few changes to the navigation block, which will be used when your guide is posted on the website for navigation purposes. The **navigation block** looks like this:

---
layout: default _("Default" is the standard layout. Do not change.)_
title: Guidance Document Template _(Change the **title**, "Guidance Document Template," to your guide's title._) 
permalink: /template/ _(Change **/template/** to a short name for your guide using the "/name/" format._)
--- 

(_Main Body Paragraph_) Begin your guide with a brief statement about its purpose.

(_Table of Contents_) After the first main body paragraph, add a TOC link to each Heading 1 section. For example:

  * [Section 1 Title](#words-in-section3-title-separated-by-dashes)
  * [Section 2 Title](#words-in-section2-title-separated-by-dashes)
  * [Section 3 Title](#words-in-section3-title-separated-by-dashes)

# Overview (Heading 1)

(_Main body paragraph_) This introductory text should be a brief overview of your guide's topic. In addition to the overview, you may include information on the intended audience, the intended outcome of the guide, and any other information that would help the user to understand the guide.

# Assumptions (Heading 1)

(_Main body paragraph_) This section should be a bullet list that explains any assumptions that must be understood before the user can begin the procedures in the guide. This section may also include conditions that must be met before the user can begin the procedures. Alternate titles may be: **Preconditions** (i.e., list any conditions that must be met) or **Hardware and Software_Requirements** (i.e, list any hardware or software that must be obtained and/or configured).

# Before You Get Started (Heading 1)

This section should tell the user what he/she needs to do to prepare before starting a set of procedures. 

# Title of Procedure 1 (Heading 1) (_Repeat Procedural Sections as Needed_)

(_Main body paragraph_) This introductory text should give any user-friendly background information; explain the purpose of the procedure; and give any context that the user might need before diving into the steps. The text within each step should directly walk the user through exactly what they need to do to complete the procedure.

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

**Bullet List Items:**

* Bullet 1 (Indent 2 spaces, enter an asterisk, and add 1 space.)
* Bullet 2

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

**Code Comments**

<!--For example, this code denotes a comment. The comment will not appear on the website but can be used as a reference for others viewing the file.-->

**Images**

To insert an image (graphic) into your Page, first upload the image file to the **/img/** folder in the appropriate GitHub repository.  Next, at the image insertion point in your Page, add this format to link to the image:

![This is what I want a screen reader to say for 508 compliance]({{site.baseurl}}/img/thisisthesampleimagefile.png)

> To align an image in your Page, use the **align** instruction at the end of an image link (i.e., **"left"**, **"center"**, or **"right"**) using this format:

![Alt text for an image goes here]({{site.baseurl}}/folder that image is in/imagename.png){:align="right"}

**Alerts, Warnings, and Information Blocks**

Use the Alert, Warning, or Information Block formatting to highlight specific information in your Page.

{% include alert-info.html heading = "Before starting a new Guide, please review the _Contributing.md_ page!" content="The _Contributing.md_ page provides terms and conditions and other important instructions." %}

**FIND FORMAT FOR WARNING, ALERT, AND SUCCESS - CHANGE ALL BELOW TO SAME FORMAT**

* **Warning Blocks**

This text will appear as a **warning flag**, which is a yellow banner on the website. (The ">" symbol and the coded line directly underneath the text will create the formatting for this flag.) Warning flags can be used for notifications, such as when a user should skip a certain procedure.
{:class="warning"}

* **Alerts for Notifications or Problems**

This text will appear as an **alert flag**, which is a red banner on the website. Alert flags may be used for notifications, such as common problems that may occur.
{:class="alert"}

* **Information Alerts**

This text will appear as **informational flag**, which is a green banner on the website. Information flags can be used for notifications such as useful links or helpful tips.
{:class="info"}

* **Success Alerts** **BLUE BANNER??**

This text will appear as **success flag**, which is a **blue?** banner on the website. These flags are used to let the user know they succeeded when carrying out a step or action. 

**Links to Other Documents**

To link to useful references, information, or another page within GSA's IDManagement.gov website, use: 

[This is what I want my link to say]({{site.baseurl}}/insertlink/)<!--Is that correct for this type of link?-->

Link to an document outside the GSA IDManagment.gov website (opens a new window):

[This is what I want my link to say](https://www.governmentagency.gov){:target="blank"}

### TEMPLATE ENDS HERE
___

# Resources for Writing and Style

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
