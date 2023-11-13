---
title: Log your played iTunes tracks
author: Alex
type: posts
date: 2016-07-24T07:21:38+00:00
url: /log-your-played-itunes-tracks/
categories:
  - Tutorial
tags:
  - Applescript
  - iTunes
  - logging

---
A few days ago I was looking for a way to log all tracks that I listen to in iTunes. Something like <a href="http://www.last.fm" target="_blank">Last.fm</a> but that works local and for macOS. I did a quick search and couldn&#8217;t find anything (maybe there is something already). So I decided to built something simple on my own using AppleScript, which allows me to easily access the iTunes information I need.

Doing some research I found an article at <a href="http://dougscripts.com/itunes/itinfo/idle00.php" target="_blank">Doug&#8217;s AppleScripts</a> that described the problem I wanted to solve. Copy the code below in the Script Editor (or <a href="https://github.com/alexrockt/itunes-log" target="_blank">get from GitHub</a>), change the path to the text file and save as an application and don&#8217;t forget to check the &#8220;Stay open after run handler&#8221;.

<a href="assets/images/2016/07/ScriptEditor_saveDialog.jpg" rel="lightbox[89]"><img loading="lazy" decoding="async" src="assets/images/2016/07/ScriptEditor_saveDialog.jpg" alt="Save Dialog of Script Editor" width="385" height="139" class="aligncenter size-full wp-image-100" srcset="assets/images/2016/07/ScriptEditor_saveDialog.jpg 385w, assets/images/2016/07/ScriptEditor_saveDialog-300x108.jpg 300w" sizes="(max-width: 385px) 100vw, 385px" /></a>

Run the app and voilà! I haven&#8217;t looked into possibilities to hide the dock icon or anything else. And I guess you can run the code with some modifications as a shell script in the background. Maybe I&#8217;ll look into it later.

<pre class="brush: as3; title: ; notranslate" title=""># based on http://dougscripts.com/itunes/itinfo/idle00.php

global latest_song

on run
	tell application "System Events"
		if not (exists process "iTunes") then return
	end tell
	
	set latest_song to ""
end run

on idle
	tell application "iTunes"
		try
			copy name of current track to current_tracks_name
			if current_tracks_name is not latest_song then
				copy current_tracks_name to latest_song
				copy artist of current track to current_track_artist
				set output to current_track_artist & " - " & latest_song
				set dateString to do shell script "date +'%Y-%m-%d %H:%M'"
				
				do shell script "echo " & dateString & " - " & output & " &gt;&gt; ~/Desktop/test.txt"
			end if
		on error
			return 20
		end try
		return 10
	end tell
end idle
</pre>