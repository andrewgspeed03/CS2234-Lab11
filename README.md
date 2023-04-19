# Lab 11

The goal of this lab is to build and host static web-pages on a virtual machine (VM) instance in the cloud. The web-pages will be automatically generated using a Java program that you'll modify in this lab. 

Before you start, make sure you redeem your GCP credits and verify your account as explained in the canvas announcement.

In order to build static web-pages, we need to use HTML (for the layout) and CSS (for styling). In order to host web-pages, we need to install a web server. There are many available options for webservers such as: Apache, Microsoft IIS, and Nginx. In this lab, we will install and configure Nginx on the virtual machine so that our web pages are accessible on the internet through HTTP.

In order to achieve our goal for this lab, we will go through the following steps:
1. [Get familiar with basic HTML syntax](basicHtmlPage.md)
2. [Creation of HTML pages using Java](src/html/MakePage.java)
3. [Creating and starting a virtual machine on GCP](gcp-console.md)
4. [Installing the software necessary to run a web server on the VM](ssh.md)
5.  Customizing your web-pages: after finishing the previous steps, and generating web-pages using the Java application, you will need to customize these pages by modifying the Java code. The modifications that you need to do are:

	1. In the `myPage` method, replace the string `"Hello"` with a hyperlink. The text of the hyperlink should be "your name". Upon clicking on the hyperlink, it should try to send a message to your email address with the subject being "Message from Your Server" (Hint: look up `HTML mailto links`). The styling and formatting of the link is up to you. 

	2. Use the method `System.nanoTime()` to calculate the time from the start of the `myPage` method to the line that appends the string `"<p> You could provide your text here. </p>\n"`. Replace `"You could provide your text here."` with the time, using the format `"Time: nano-seconds"`.

## Submission
You will submit the link of your colors directory of your web server on Canvas.


### [Additional References](references.md)
