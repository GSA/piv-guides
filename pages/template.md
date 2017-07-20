---
layout: default
title: Contributor's Template for Writing a FICAM Guide
permalink: /template/
---

Thank you for your interest in writing a FICAM Guide! We welcome your contributions. 

This **Contributor's Template for Writing a FICAM Guide** gives guidance and a template to help you get started with your new guide.

{% include alert-info.html heading = "Before starting a new FICAM guide, please review the Contributing page!" content="The Contributing page provides terms and conditions and other instructions." %}


* [Select a Topic for Your Guide](#select-a-topic-for-your-guide)
* [Use GitHub](#use-github)
* [Template and Markdown Text Editor](#template-and-markdown-text-editor)

  
## Select a Topic for Your Guide
Propose a topic by [opening an Issue]({{site.baseurl}}/contribute/#open-an-issue){:target="blank"} 

If you don't have a topic, a good place to start is the open **Issues** lists. 

* [PIV Guides Issues](https://github.com/GSA/piv-guides/issues){:target="blank"} 
* [Federal PKI Guides Issues](https://github.com/GSA/fpki-guides/issues){:target="blank"} 
* [FICAM Architecture Issues](https://github.com/GSA/ficam-arch/issues){:target="blank"} 

## Use GitHub

Using GitHub as a first time user can be overwhelming.  An introduction video is available from DigitalGov on YouTube: [Introduction to GitHub](https://www.youtube.com/watch?v=uNa9GOtM6NE&t=1737s){:target="blank"}.  

* [Create a GitHub Account](#create-a-github-account) 
* [Fork the Repository](#fork-the-repository)
* [Create a Branch](#create-a-branch)
* [Create a Page](#create-a-page)

### Create a GitHub Account

You can create a GitHub account by browsing to: [Join GitHub](https://github.com/join). For more help, contact GSA GitHub Support at: gsa-github.support@gsa.gov. 

* GitHub allows you to remain pseudonymous. You can select the options that suit you on the _Profile_ and _Emails_ pages of your _Personal Settings_ in your GitHub account.  
* We also highly encourage you to turn on **two-factor authentication** in the _Security_ page (also part of _Personal Settings_).

### Fork the Repository

Once you have a GitHub account, you can create a personal copy (called a "_fork_") to work on in your GitHub profile.  It's simple: 

*  In the upper right-hand corner, click on the **Fork** button.

A version controlled _copy_ will now be in your GitHub profile.

For more help with forking a repo, go to [Fork a Repo](https://help.github.com/articles/fork-a-repo/){:target="blank"}

### Create a Branch

To create a new branch to store your guide:

1. In the top right-hand corner of the repository window, click on the down-arrow next to your profile icon/picture. Select **_Your profile_**.  
2. Click on the repository that you forked. 
3. Above the listing of folders and files in the repository, look for the **Branch** button. Click on the down-arrow and select the **_Staging_** branch. 
4. Click on the **_Branch_** button again and enter a new **branch name** into the _text field_ (e.g., **_[Guide Name] Branch_**).
5. Click on the blue button that now displays your new branch name. (The gray Branch button now also displays your branch name.)

{% include alert-warning.html heading = "The **_Staging_** branch is the master for each FICAM guides repository. It is important that you always start with the **_Staging_** branch in your forked repository when you create a new branch. Starting at **_Staging_** helps keep your files sychronized with GSA's repository." %}  

### Create a Page

To create a new **Page** where you can write your guide:  

1. Check the gray **_Branch_** button to ensure that the new branch name is displayed. If it isn't, select it from the Branch drop-down list.
2. Click on the **_Create New File_** button located above the top right-hand area of your repository's window (above the folders and files listing).  
  
> At the top left-hand area of the Page window, the branch name now appears with a **"/"** after it and a text box.

3. In the text box, enter your new Page's name with the extension, **.md**, for **Markdown** (e.g., Mynewfile.md).
4. Go to the bottom of your Page. Below the **Commit new file** comment box, click on the green **Commit new file** button to save your new Page.

## Template and Markdown Text Editor
Markdown is a simple way of writing and formatting.  The formats can be used across many different platforms including for websites and documents.  We created a sample template to help you with your page.  The basic markdown syntax is embedded in the template. 

If you want to learn more about markdown formatting: [**Mastering Markdown**](https://guides.github.com/features/mastering-markdown/){:target="blank"}.

Use these steps to copy and paste the Template below into your GitHub markdown file to start your guide: 

1. Go to the section below called **Template with Markdown Syntax**. Copy the entire Template (headings, text, and samples) up to **Template Ends Here**. 
2. Now, go to your new GitHub Page and click on the **pencil** symbol (top right-hand side of window). The **pencil** opens Markdown's writing and editing mode.
3. Next, click on Line **1** of your Page (top left-hand corner) and paste in the copied Template. 
4. Scroll down to the bottom of your Page window. Click on the green **Commit changes** button to save the Template to your Page.


## Writing and Style Resources

Here are some general writing and formatting tips for writing your guide:

  * All pages should be brief.
  * Use titles to help the user identify jumping off points for information.
  * Paragraphs should be short. 
  * All text should be written in plain language and in a user-friendly active voice as much as possible. 
  * Use numbered steps, bullet lists, and graphics.
  
The following sources can provide additional help with plain language, writing, and style:

  * [18F Content Guide](https://content-guide.18f.gov/){:target="_blank"}
  * [Federal Plain Language Guidelines](http://www.plainlanguage.gov/){:target="_blank"}


# Template with Markdown Syntax
---
layout: default 
title: Title of the Page
permalink: /template/
---
The navigation block is used for website navigation when your guide is posted.  Update the _Title of the Page_ and the _/template/_ 

To begin your guide, briefly state its purpose in one to two sentences.  You may include information on the intended audience, the intended outcome of the guide, and any other information that would help the user to understand the guide.

Add a table of contents link for each section. For example:

* [Section 1 Title](#words-in-section1-title-separated-by-dashes)
* [Section 2 Title](#words-in-section2-title-separated-by-dashes)
* [Section 3 Title](#words-in-section3-title-separated-by-dashes)

We propose these sections for most guides:

### Before You get Started
This section should tell the user what to prepare before starting a set of procedures. Explain any assumptions as bulleted lists. Clearly state the hardware and software requirements. 

### Procedure 1
This section should tell the user how to achieve the goal. Explain all steps simply and don't try to recreate other resources that are easily found.  Focus on the government and what can be unique when implementing or executing.

### Procedure 2
This section should tell the user how to achieve the goal. Explain all steps simply and don't try to recreate other resources that are easily found.  Focus on the government and what can be unique when implementing or executing. 


## Overview (Heading 2)

# This Is a First-Level Heading
## This Is a Second-Level Heading
### This is a third-level heading
#### This is a fourth-level heading
##### This is a fifth-level heading

### Number List Items

1. Step 1 of procedure. (Indent 2 spaces, enter a number, and add 1 space.) 
2. Step 2 of procedure.

### Bullet List Items

* Bullet 1 (Indent 2 spaces, enter an asterisk, and add 1 space.)
* Bullet 2

### Bold and Italics

* Use double asterisks to bold a word:  **bold**.
* Use underscores to create italics:  _italics_.

### Code Blocks

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

### Code Comments

Code comments will be invisible in a webpage view, but others will be able to see the comment in GitHub Markdown. <!--For example, this code denotes a comment. It will not appear on a webpage but can be used as a reference for others viewing the file.-->

### Images

To insert an image into your Page, upload the image file to the **/img/** folder in the GitHub repository.  Then at the image insertion point in your page, add these formats to link to the image.

![This is what I want a screen reader to say for 508 compliance]({{site.baseurl}}/img/imagename.png)

![Text for an image aligned right goes here]({{site.baseurl}}/img/imagename.png){:align="right"}

![Text for another image aligned left goes here]({{site.baseurl}}/img/anotherimagename.png){:style="float:left;width:25%;"}


### Links to Other Documents

To link to useful references, information, or another page within GSA's IDManagement.gov website, use: 

[This is what I want my link to say]({{site.baseurl}}/insertlink/)

Link to an document so that it opens a new window:

[This is what I want my link to say](https://www.governmentagency.gov){:target="blank"}

## TEMPLATE ENDS HERE
___



