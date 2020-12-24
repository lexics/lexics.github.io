---
layout: post
author: Ashutosh Kumar
title: Installing Microsoft Fonts on Linux(Comprehensive Guide)
---

After installing Linux, one of the most important thing to do is installing essential Microsoft Fonts that you will need while working with Microsoft Office Documents, Microsoft Teams, or on the web. It is important to do so as many times you won't be able to process the documents correctly when you try to open it with diffrent font sets.

In this article we will cover how to install all the essential Microsoft Fonts.

## Installing Microsoft Core TrueType Fonts on Ubuntu-based Linux distributions

---

Microsoft Fonts doesn't come pre-installed in Linux. The reason behind it is that these fonts are not Open Source and are owned by Microsoft and many linux distributions don’t provide proprietary software by default to avoid licensing issue. But Microsoft has released its Core TrueType Fonts for free of charge.

Since this is not an Open Source software, you need to first enable the **multiverse repository**. To do so execute the following command:

> sudo add-apt-repository multiverse

Now to install Microsoft Core TrueType Fonts, execute the following command:

> sudo apt update && sudo apt install ttf-mscorefonts-installer

After that press **OK**(using ENTER button) when Microsoft’s End user agreement appears(use **TAB** for moving the cursor to **OK** button).Then press **Yes** to accept the Microsoft’s agreement.

In case that you accidentally reject the license agreement, you can reinstall the installer with the following command:

> sudo apt install –reinstall ttf-mscorefonts-installer

This package installs the following fonts:

- Andale Mono
- Arial Black
- Arial (Bold, Italic, Bold Italic)
- Comic Sans MS (Bold)
- Courier New (Bold, Italic, Bold Italic)
- Georgia (Bold, Italic, Bold Italic)
- Impact
- Times New Roman (Bold, Italic, Bold Italic)
- Trebuchet (Bold, Italic, Bold Italic)
- Verdana (Bold, Italic, Bold Italic)
- Webdings

## Installing Microsoft ClearType Fonts

---

Microsoft ClearType Fonts was first introduced in Windows Vista and in Office 2007 and since then it has been a part of Windows and thus is very essential when working with Microsoft Documents. The ClearType Fonts Collection includes:

- Calibri
- Cambria
- Candara
- Consolas
- Constantia
- Corbel

To install ClearType Fonts, execute the following command:

<pre style="color:#86bb48">
wget -q -O - https://gist.githubusercontent.com/Blastoise/72e10b8af5ca359772ee64b6dba33c91/raw/2d7ab3caa27faa61beca9fbf7d3aca6ce9a25916/clearType.sh | bash
</pre>

## Installing Tahoma and Segoe-UI Fonts

---

Tahoma is a part of TrueType Fonts by Microsoft but is not available in **ttf-mscorefonts-installer** package and thus need to be installed manually.

To install Tahoma Fonts, execute the following command:

<pre style="color:#86bb48">
wget -q -O - https://gist.githubusercontent.com/Blastoise/b74e06f739610c4a867cf94b27637a56/raw/96926e732a38d3da860624114990121d71c08ea1/tahoma.sh | bash
</pre>

Segoe UI font is probably one of the most important font that we will install in this blog. This font is now used by Microsoft in every project and thus can be regarded as the font that will become a standard very soon.

To install Segoe-UI Fonts, execute the following command:

<pre style="color:#86bb48">
wget -q -O - https://gist.githubusercontent.com/Blastoise/64ba4acc55047a53b680c1b3072dd985/raw/6bdf69384da4783cc6dafcb51d281cb3ddcb7ca0/segoeUI.sh | bash
</pre>

## Installing Other Essential Fonts

---

This section deals with installing essential fonts that you will require when opening documents containing Maths symbols and thus is used for correct processing of these characters.
We will install the following fonts in this section:

- mtextra.ttf
- symbol.ttf
- webdings.ttf
- wingding.ttf
- wingdng2.ttf
- wingdng3.ttf

To install these fonts, execute the following command:

<pre style="color:#86bb48">
wget -q -O - https://gist.githubusercontent.com/Blastoise/d959d3196fb3937b36969013d96740e0/raw/429d8882b7c34e5dbd7b9cbc9d0079de5bd9e3aa/otherFonts.sh | bash
</pre>

#### References:

[It's FOSS](https://itsfoss.com/install-microsoft-fonts-ubuntu/)

<h4 style="color:orange">Fun Fact:</h4>

After installing Segoe-UI fonts this page will look different on many systems as it uses Segoe-UI font.

We come to an end of this comprehensive guide of installing Microsoft Fonts. I hope this article helped you in doing so.

Questions, suggestions, a word of thanks is always encouraged.
