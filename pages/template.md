---
layout: default
title: Guidance Document Template
permalink: /template/
---

This page serves as the template for creating your own guidance document to add to one of the FICAM Guides.

To create your own page using the github website, copy the content from this file, paste it into a new file (new files can be created through the 'new file' link at the top of the pages folder), give the new file a name (at the top of the page there will be a box that says 'name your file'), and change the title and permalink at the very top section of the file (the permalink should match the new file name). The title should be what you want to appear at the top of the page on the site, and the permalink text should match the name of the file, but in the format /mypage/ instead of mypage.md.

In this template, you will see text that explains how to use this template and comments explaining the formats.

<!--- For example, this code denotes a comment, and information written inside of it will not appear on the website but can be used as a reference for others viewing the file. -->


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

### 1. Title of Procedure 1

> This text will appear as a 'warning flag' on the website, which is a yellow banner. (The ">" symbol and the line directly underneath this body of text create the formatting for this flag.) Warning flags can be used for notifications such as notifying a user that they should skip a certain procedure.
{:class="warning"}

> This text will appear as a red banner, for an 'alert' message. Alert flags can be used for notifications such as common problems that may occur.
{:class="alert"}

> This text will appear as a green banner, for an 'informational' message. These flags can be used for notifications such as useful links or helpful tips.
{:class="info"}

This is the main body text that explains the purpose of the procedure and any context that you might need before diving into the individual steps. The text within each step should walk the user directly through exactly what they need to do to complete the procedure.

**Text within double asterisks will appear as bolded.**

*Text within single asterisks will appear as italicized.*

```Text within three backticks style code or command line samples```

For more information on formatting in markdown, go [here.](https://help.github.com/articles/basic-writing-and-formatting-syntax/)

1.	Step 1 of the procedure...
2.	Step 2 of the procedure...


#### References

Any referential links should be added to this section. Links appear in the following format [hyperlink text]({{ site.baseurl }}{{ page.url }})
