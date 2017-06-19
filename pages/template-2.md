---
layout: default
title: Contributor's Template for Writing a FICAM Guide
permalink: /template/
---

**Add LaChelle's other changes**

**FIX ALERTS AND LINKS**

{% include alert-info.html heading = "Before starting a new FICAM guide, please review the _Contributing.md_ page!" content="The _Contributing.md_ page provides terms and conditions and other important instructions." %}

Thank you for your interest in creating a FICAM Guide! We welcome your contribution to solving a PIV, FPKI, or FICAM-Arch technical issue! 

This **Contributor's Template** will gives some helpful steps to get you started on your new FICAM guide.

Click on one of these links to go to a specific section:  

  * [**Select a Topic for Your Guide**](#select-a-topic-for-your-guide)
  * [**Create a GitHub Account**](#create-a-github-account)
  * [**Create a GitHub Repository, Branch, and Page**](#create-a-github-repository,-branch-,-and-page)
  * [**Create an Issue in GitHub**](#create-an-issue-in-github)
  * [**Structure Your Guide &mdash; Template with Markdown Syntax**](#structure-your-guide-&mdash;-template-with-markdown-syntax)
  * [**Additonal Help with Markdown Syntax**](#additional-help-with-markdown-syntax)
  * [**Help with Writing and Style**](#help-with-writing-and-style)  
  
# Select a Topic for Your Guide
  
**If you would like to write a guide but don't yet have a topic** &mdash; A good place to start is to look at the open **Issues** lists in the GSA GitHub repositories. The open **Issues** lists offer many technical issues in search of a contributor.

Select a repository ("repo"):

  * **PIV-Guides** [PIV-Guides](https://github.com/GSA/piv-guides){:target="blank"}
  * **FPKI-Guides** [FPKI-Guides](https://github.com/GSA/fpki-guides){:target="blank"}
  * **FICAM-Arch** [FICAM-Arch](https://github.com/GSA/ficam-arch){:target="blank"}
  
**Once you select a topic** &mdash; The next step is to create a GitHub account, if you don't have one. See [**Create a GitHub Account**](#create-a-github-account). If you already have a GitHub account, see the steps below to [**Create a Repository**](#create-a-repository) to "fork" one of the GSA repos (i.e., related to your topic).

**If you already have a topic for your new FICAM Guide** &mdash; The first step is to create a GitHub account. See [**Create a GitHub Account**](#create-a-github-account).

# Create a GitHub Account

For the steps needed to create a GitHub account, go to: [Signing up for a New GitHub Account](https://help.github.com/articles/signing-up-for-a-new-github-account/). For more help, you can contact GSA GitHub Support at: gsa-github.support@gsa.gov. 

## Create a Repository

If you don't have a GSA repo related to your topic (e.g., PIV-Guides), you need to fork the repo. (A fork is your personal copy of a repo. With a forked repo, you can create a new file and work on it without affecting GSA's original repo.)

1. Go to: [GSA Respositories at GitHub.com](https://github.com/GSA){:target="blank"}.
2. Select the repo you want to fork. 
3. In the upper right-hand corner of the GSA repo screen, click on the gray **Fork** button.

> The forked GSA repo will now be in your GitHub profile.

For more help with forking a repo, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/){:target="blank"}

Now that you have a forked repo, you need to create a new branch to store your guide.

## Create a Branch

To create a new branch, do this:

1. Go to the **_Branch_** button. At the pull-down, select the **_Staging_** branch. 

{% include alert-info.html heading = "The GSA repo's **_Staging_** branch is the master branch for the GSA repos. It is important that you always start with the **_Staging_** branch in your forked repo. This keeps your repo's files sychronized with GSA's repo (e.g., PIV-Guides)." %}
  
2. Click on the **_Branch_** button and enter your new **branch name** into the _text field_ (e.g., **_[Guide Name] Branch_**).
3. Select the blue button below the text field with your new branch's name.
  
> The **_Branch_** button now displays your new branch name. 

Now that you have a new branch to store your guide, you need to create a new **Page**, where you will write your guide.
    
## Create a "Page"

To create a new **Page** for writing your guide, do this:  

  1. Check the **_Branch_** button to ensure that the branch name you selected or created is displayed. If it isn't, click on the down-arrow and select the branch name from the drop-down list.
  2. Click on the **_Create New File_** button located at the top right area of your repository's directory window.  
  > At the top left area of this window, the branch name appears with a **"/"** after it and a text box. (If you want to start over, select **_Cancel_**.) 
  4. In the text box, enter your new Page's name with the extension, **.md**, for **Markdown** (e.g., **Mynewfile.md**).
  5. Scroll down to the bottom of your screen. At the left side of your screen, below the **Commit new file** comment box, click on the green button that says **Commit new file**.
  > This creates and saves your new Page in your selected or new branch.
  
# Create an Issue in GitHub

Once you have a guide topic, a forked repo, a branch, and a page, the next step is to discuss your topic on GitHub by creating an **Issue**. By discussing your topic through GitHub, you can collaborate with other community experts. Added insights and new solutions from the community may help you to write your guide.

To create a new Issue in GitHub, do this:

*************************stopped

create a new **Issue** in GitHub to discuss your topic and ask for other community members to collaborate/contribute.  



# Structure Your Guide &mdash; Template with Markdown Syntax

Starting with [**Template Starts Here**](#template-starts-here) below, copy and paste the text to **Template Ends Here**, into your new GitHub Page. THis template will help you to structure and develop your guide. Do this:

  1. At the top right area of your Page's content window, click on the **pencil** symbol.

  > You will use this mode to create and edit content for your guide.
  
  2. **Select all of the Template contents below. Copy and paste the content into your Page.**
  3. Change the **title**, "Guidance Document Template," to your guide's title (for example, _My Technical Guide_).
  4. Change the **permalink** title to a short version of your guide's title (for example, _/myguide/_.
  
  > The **permalink** title should be in the format: **/mypage/**, instead of _mypage.md_ 
  
  6. Once you have made these changes, scroll down to the bottom of your screen. At the left side of the screen, click on the green button that says **Commit changes.**
  
  > This action saves all of your changes to your Page. When you are ready, you can use the Template as the basis for writing your guide. 

  * The Template below is already formatted in Markdown syntax for you to use.  
  * Copy and paste the Template into your Page.
  
  > For more on Markdown, go to:  [**Mastering Markdown**](https://guides.github.com/features/mastering-markdown/){:target="blank"}.

___

### Template Starts Below

# Template with Markdown Syntax

## Navigation Block and Your Guide's Title
---
layout: default
title: Guidance Document Template 
permalink: /template/
---

  1. **layout: default**. This field always stays the same. No changes are necessary.
  2. **title: [document title]**.  On your Page (Markdown), you _won't_ see a main title. The **Title** field automatically adds the title to your guide when it is posted on the IDManagement.gov website.
  3. **permalink: /[name]/**. The **permalink** should be a short name for your document title. Change **/template/** to a short name for your guide.

Add a **Table of Contents (TOC)** after the first main body paragraph. THe TOC should link to each major section. For example:

  * [Section 1 Title](#words-in-section3-title-separated-by-dashes)
  * [Section 2 Title](#words-in-section2-title-separated-by-dashes)
  * [Section 3 Title](#words-in-section3-title-separated-by-dashes)

# Overview (Heading 1)

(Main body paragraph) This introductory text should give a brief overview of the topic covered in your guide. In addition to the topic overview, you may include information on the intended audience, the intended outcome of the guide, and any other information that would help the user to understand the guide.

# Assumptions (Heading 1)

(Main body paragraph) This section should be a bullet list that explains any assumptions that must be understood before the user can begin the procedures in the guide. This section may also include conditions that must be met before the user can begin the procedures. Alternate titles may be: **_Preconditions_** (i.e., list any conditions that must be met) or **_Hardware and Software_Requirements** (i.e, list any hardware or software that must be obtained and/or configured).

# Before You Get Started (Heading 1)

This section will tell the user what he/she needs to do to prepare before starting a set of procedures. 

# Title of Procedure 1 (Heading 1)

This introductory text should give any user-friendly background information; explain the purpose of the procedure; and give any context that the user might need before diving into the steps. The text within each step should walk the user directly through exactly what they need to do to complete the procedure.

**Use additional Headings, as needed:**

## This Is a Second-Level Heading
### This is a third-level heading
#### This is a fourth-level heading
##### This is a fifth-level heading

**Number List Items:**

1. Step 1 of procedure 1. (Numbered List item - Indent 2 spaces, enter a number, and add 1 space.) 
2. Step 2 of procedure 1. (Numbered List item) 

  > **Note:** or call-out needed.
  
**Add one Alert with reference to others in More Markdown Syntax**
  
# Title of Procedure 2 (Heading 1)

**This is the main body paragraph style.** This introductory text should give any user-friendly background information; explain the purpose of the procedure; and give any context that the user might need before diving into the steps. The text within each step should walk the user directly through exactly what they need to do to complete the procedure.

## This Is a Second-Level Heading (Use other Headings as needed)
### This is a third-level heading
#### This is a fourth-level heading
##### This is a fifth-level heading

  1. Step 1 of procedure 1. (Numbered List item)
  2. Step 2 of procedure 1. (Numbered List item)

  > **Note:** or call-out needed. (**Citation??**)
  
  > Repeat procedural sections, as needed.
  
*************************Add a different Alert with reference to others in More Markdown Syntax**

### TEMPLATE ENDS HERE
___

## Additional Help with Markdown Syntax

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

[This is what I want my link to say](https://www.governmentagency.gov){:target="blank"}

**Template Ends Here**

ADD A LINE HERE

# Help with Writing and Style

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

