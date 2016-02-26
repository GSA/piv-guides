---
layout: page
title: Guidance Document Template
permalink: /template/
---
This page serves as the template for creating your own guidance document to add to one of the FICAM Playbooks. For an example of a completed guidance document, visit the 'How do I PIV enable my network logon?' page [here]({{ site.baseurl }}/devconfig/15_network/). To create your own page using the github website, copy the content from this file, paste it into a new file (new files can be created through the 'new file' link at the top of the pages folder), give the new file a name (at the top of the page there will be a box that says 'name your file'), and change the title and permalink at the very top section of the file (the permalink should match the new file name). The title should be what you want to appear at the top of the page on the site, and the permalink text should match the name of the file, but in the format /mypage/ instead of mypage.md. Throughout this file, you will see text that explains how to correctly use this template and comments explaining the nature of the code that you will encounter.

<!--- For example, this code denotes a comment, and information written inside of it will not appear on the website but can be used as a reference for others viewing the file. -->

<!--- The code below allows for the use of an 'accordion' on the page, which collapses or shows text when you click on a section of it. This code should not be removed from the file. -->
<script>
$(function() {
  $( "#accordion" ).accordion({
    heightStyle: "content",
    collapsible: "true",
    active: "false"
  });
});
</script>

<!--- The code below creates a difficulty identifier on the page, which can either be Beginner, Moderate, or Advanced depending on the technical knowledge required to complete the procedure. The example below includes text that mark the document as 'Advanced', this string can be changed as needed.-->
<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Difficulty: Advanced</em>
</div>
</div>

<!--- The '#' symbol is used to denote headers, with different amounts aligning with different header styles. -->

#### Overview
This text should be populated with a brief overview of what content is contained within the guidance document, and may include information on the intended audience, the outcome of the guide, and any other information that would help the user to understand the guide.

##### Assumptions
*  This text will be a bullet explaining a precondition or assumption before the user begins to follow the steps outlined in this document
*  The asterisk symbol denotes a bulleted item, and an indented asterisk denotes a second level bullet
    *  This is a second level bullet

#### Before you get started
This text will provide any reference information that may be needed to complete the steps outlined in the guide.

*  This text names a link to a reference document [with the hyperlink text within brackets](and the actual URL within parentheses)

<!-- If you want to insert an image onto the page use the format below. The align feature at the end can either be "left", "center", or "right". -->

![Alt text for an image goes here]({{site.baseurl}}/folder that image is in/imagename.png){:align="right"}

#### Complete the following tasks:

<!--- The code below triggers the start of the accordion dropdown for the main steps of the guidance document. -->
<div id="accordion" markdown="1">


### 1. Title of Procedure 1
<div markdown="1">

> This text will appear as a 'warning flag' on the website, which is a yellow banner. (The ">" symbol and the line directly underneath this body of text create the formatting for this flag.) Warning flags can be used for notifications such as notifying a user that they should skip a certain procedure.
{:class="warning"}

> This text will appear as a red banner, for an 'alert' message. Alert flags can be used for notifications such as common problems that may occur.
{:class="alert"}

> This text will appear as a green banner, for an 'informational' message. These flags can be used for notifications such as useful links or helpful tips.
{:class="info"}

This is the main body text that explains the purpose of the procedure and any context that you might need before diving into the individual steps. The text within each step should walk the user directly through exactly what they need to do to complete the procedure. **Text within double asterisks will appear as bolded.** *Text within single asterisks will appear as italicized.* For more information on formatting in markdown, go [here.](https://help.github.com/articles/basic-writing-and-formatting-syntax/)

1.	Step 1 of the procedure...
2.	Step 2 of the procedure...

This text is for separating a procedure into separate  processes, if needed.

1.	Step 1
2.	Step 2
3.	Step 3

</div>

### 2. Title of Procedure 2
<div markdown="1">

Introductory text for the procedure with numbered steps.

1.	Step 1
2.	Step 2

</div>

### 3. Title of Procedure 3
<div markdown="1">

Introductory text for the procedure. The text below is tabbed twice, which is used for creating a code block to show commands that the user will need to execute a process.

        code goes here


</div>
</div>

#### References

Any referential links should be added to this section. Links appear in the following format [hyperlink text]({{ site.baseurl }}{{ page.url }})
