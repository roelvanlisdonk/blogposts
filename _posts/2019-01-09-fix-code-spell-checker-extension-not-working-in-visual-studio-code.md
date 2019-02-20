---
ID: 5320
post_title: >
  Fix Code Spell Checker extension NOT
  working in Visual Studio Code
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2019/01/09/fix-code-spell-checker-extension-not-working-in-visual-studio-code/
published: true
post_date: 2019-01-09 08:11:47
---
I installed the code spell checker extension for Visual Studio Code <a href="https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker">https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker</a>.

But the spell checker was not working, the status bar showed an exclamation mark icon.

<img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2019/01/010919_0711_FixCodeSpel1.png" alt="">

For some reason the spell checker was disabled in the workspace settings:

<img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2019/01/010919_0711_FixCodeSpel2.png" alt="">

After this setting was set to true and the workspace settings json file was saved, the code spell checker started working again.