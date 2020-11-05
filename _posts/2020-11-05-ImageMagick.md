---
layout: post
author: Ashutosh Kumar
title: How To Merge Multiple PDF/Images to PDF In Ubuntu Linux(ImageMagick)
---

It's not very uncommon that we might need to merge different PDF's or images into one PDF in our daily task. So in this article we learn about a very powerful command line tool called ImageMagick and learn how to use it.

<br>

## Installing ImageMagick through **apt**

---

ImageMagick comes preinstalled in Ubuntu 20.04 as there are many package that use this tool as a dependency.

Installing ImageMagick through apt (Advanced Package Tool) is pretty straightforward. The package is already available in standard Ubuntu repository

Open the terminal and execute the following:

- First refresh your local package index by executing:

  > `sudo apt update`

- Next execute the following command to install ImageMagick:
  > `sudo apt install imagemagick`

<br>

## Using ImageMagick to merge multiple images into one PDF

---

We will use the **_convert_** command line tool of ImageMagick to merge multiple images into PDF.

To convert use the following command:

> `convert image1.jpg image2.png image3.bmp output.pdf`

The order of images in the command determines the order in which images are merged in the **output.pdf**.

If you get the following error while converting to PDF:

> `convert: attempt to perform an operation not allowed by the security policy 'PDF' @ error/constitute.c/IsCoderAuthorized/408`

Jump to [Solving the Security Policy Error](#solving-the-security-policy-error) section where we have discussed how to solve this issue.

<br>

## Using ImageMagick to merge multiple PDF into one PDF

---

We will use similar command that we used before but with some extra options so that quality of the output.pdf is good.

To convert use the following command:

> `convert -density 300 file1.pdf file2.pdf file3.pdf output.pdf`

`-density` sets the dpi that the PDF is rendered at. Setting this to 300/600 will give a fairly good output.

You can also use image and pdf interchangeably in this command which makes it even more powerful.
That is :

> `convert file1.pdf image1.jpg output.pdf`

If you get the following error while converting to PDF:

> `convert: attempt to perform an operation not allowed by the security policy 'PDF' @ error/constitute.c/IsCoderAuthorized/408`

Jump into the [next-section](#solving-the-security-policy-error) of this article to solve this error.

<br>

## Solving the Security Policy Error

---

ImageMagick has some security policies disabling some rights for security reasons.
You will have to edit a config file to re-enble the action you need.

Open `/etc/ImageMagick-6/policy.xml` with your favorite text editor, find the line `<policy domain="coder" rights="none" pattern="PDF" />` and replace `"none"` by `"read|write"`

Step By Step Process to achieve the things mentioned above

Open the file in terminal and execute:

> `sudo nano /etc/ImageMagick-6/policy.xml`

Find and edit the line:

> `<policy domain="coder" rights="none" pattern="PDF" />`

to :

> `<policy domain="coder" rights="read|write" pattern="PDF" />`

References:
[AskUbuntu](https://askubuntu.com/a/1127265)

After performing the task I would recommend to change the policy.xml back to what it was before. There are many other useful tasks that can be performed using `ImageMagick` such as resizing images, converting between image formats and many more but that we would cover in some other article.

I hope this article helped you to merge multiple PDF/images into one PDF in Ubuntu Linux.
Questions, suggestions, a word of thanks is always encouraged.
