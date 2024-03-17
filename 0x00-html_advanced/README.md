LIGHT THE CODED SIGHT
0x00. Advanced HTML
HTML
Front-end
 By: David Dias, Senior Software Engineer at HomeX
 Weight: 1
 Project will start Mar 14, 2024 6:00 AM, must end by Mar 20, 2024 6:00 AM
 Checker was released at Mar 15, 2024 6:00 PM
 An auto review will be launched at the deadline
Concepts
For this project, we expect you to look at this concept:

HTML - elements of a web page


Welcome!
Welcome to the Web Stack specialization. The 3 first projects will give you all basics of the Web development: HTML, CSS and Developer tools.

In this project, you will learn how to use HTML tags to structure a web page. No CSS, no styling - don’t worry, the final page will be “ugly” it’s normal, it’s not the purpose of this project.

Important note: details are important! lowercase vs uppercase / wrong letter… be careful!

Resources
Read or watch:

HTML 5.2
HTML: HyperText Markup Language | MDN
HTML Reference - A free guide to all HTML elements and attributes
Can I use… Support tables for HTML5, CSS3, etc
HTML Cheat Sheet - WebsiteSetup
Learning Objectives
At the end of this project, you are expected to be able to explain to anyone, without the help of Google:

Which guidelines to follow for HTML
How to create the skeleton of an HTML5 page
How to use semantic HTML tags to structure a web page
Which use cases to use div vs span
The semantic value’s of header, main, footer, article, nav, section, aside
How to use headings (and why it’s important to follow the hierarchical order)
How to make lists in HTML
The differences between medias (SVG, GIF, PNG, JPG)
How to structure data in a table
How to integrate a video in a webpage
How to integrate an audio file in a webpage
How to embed external content
How to correctly structure an HTML page
Requirements
A README.md file at the root of the folder of the project is mandatory
Your code should be W3C compliant and validate with W3C-Validator
Techium will be the name of the company we will use across our webpages.
Sitemap of the project


Wireframe of Techium project


Quiz questions
Great! You've completed the quiz successfully! Keep going! (Show quiz)
Tasks
0. Create your first webpage
mandatory
Create your first HTML file 0-index.html with:

Add the doctype on the first line (without any comment)
After the doctype, open and close a html tag
Add the language tag, specify English for ISO language code and add the direction tag (ltr or rtl) on the html tag.
Open your file in your browser (the page should be blank)
W3C won’t pass - you can ignore it

Repo:

GitHub repository: alx-frontend
Directory: 0x00-html_advanced
File: 0-index.html
  
1. Structure your webpage
mandatory
Copy the content of 0-index.html into 1-index.html

Create the head and body sections

inside the html tag, create the head and body tags (empty) in this order
W3C won’t pass - you can ignore it

Repo:

GitHub repository: alx-frontend
Directory: 0x00-html_advanced
File: 1-index.html
  
2. The head - meta charset, viewport, title, description, favicons
mandatory
Copy the content of 1-index.html into 2-index.html



Meta charset:

add a meta tag inside the head:
add the charset attribute with the value utf-8
Viewport:

add a meta tag inside the head:
add an attribute name on the tag and specify that it is the meta viewport
add the key width with the value device-width
add the key initial-scale with the value 1.0
add the key viewport-fit with the value cover
Title:

add the title tag just after the meta viewport with value: Homepage - Techium
Description:

add a meta tag inside the head section
add an attribute name on the tag and specify that is the meta description
add another attribute called content
add the following description: Techium is a digital agency
Favicons:

download the image above to use as a favicon
Use the tool at https://realfavicongenerator.net/ to generate all the favicon formats
take the favicon.ico and favicon.png and place these at the root of your project directory, so that it is siblings with your [0-9]+-index.html files.
inside the head, create 2 link tags with these 3 attributes: rel, type, and href.
the first link tag:
rel: icon
type: image/x-icon
href: ./favicon.ico
the second link tag:
rel: icon
type: image/png
href: ./favicon.png
