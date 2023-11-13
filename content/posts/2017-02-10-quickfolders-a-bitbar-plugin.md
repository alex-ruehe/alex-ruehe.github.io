---
title: QuickFolders – a BitBar plugin
author: Alex
type: posts
date: 2017-02-10T13:23:47+00:00
url: /quickfolders-a-bitbar-plugin/
categories:
  - Article
tags:
  - BitBar
  - plugin
  - script

---
I&#8217;m a big fan of <a href="https://getbitbar.com" target="_blank">BitBar</a>, an application that allows you to &#8220;Put anything in your Mac OS X menu bar&#8221; (macOS nowadays). People have already created more than 250 plugins which allow you to show plenty of information in the menubar. Basically any script that can be executed on the terminal and has some kind of output can be used to display this output.

This is how my BitBar output looks at the moment:


![](/images/2017/02/Screen-Shot-2017-02-10-at-13.36.20.png)


It shows me (from left to right):

  * GitHub notifications
  * Bitcoin price at bitcoin.de
  * QuickFolders &#8211; the plugin this blog post is about
  * Online status of two remote servers I manage (plugin not published)
  * Battery status of Macbook, keyboard and trackpad

You can click on every item and depending on the plugin get to see more information.

**QuickFolders** is a plugin that might help if you often need files that are sorted in a certain kind of folder structure.

You specify a directory and using various kinds of bash commands the script outputs all subfolders below this directory that have files inside (empty subdirectories are omitted). You can also specify which kind of suffix you want to be considered (e.g. only pdf) and which files you want to ignore (e.g. everything starting with a dot). The plugin then only shows directories that match these criteria.

You could use it the following way (just an fictitious example):

Have a folder for each semester and inside this folder another one for every course you&#8217;re going to visit. Put all the course materials into the corresponding folders and add the path to the script


![](/images/2017/02/Screen-Shot-2017-02-10-at-14.06.19.png)


The actual folder structure looks like this:

![](/images/2017/02/Screen-Shot-2017-02-10-at-14.13.03.png)


The "Homework" folder doesn't show up, because it contains only DOC files and I changed the plugin to only show folders with PDF files.

If you click on any of those subdirectories in the BitBar menu it will open the corresponding folder in the finder.