---
title: 'LaMetric & local push'
author: Alex
type: posts
date: 2016-03-03T18:55:08+00:00
url: /posts/lametric-local-push/
categories:
  - Tutorial
tags:
  - LaMetric
  - PHP
  - Tutorial
draft: false
---
UPDATE: This doesn&#8217;t work with firmware 1.6.0 &#8211; see updated article here: [LaMetric Firmware 1.6.0 and local push][1]

With the latest firmware upgrade (1.50) the <a href="https://lametric.com" target="_blank">LaMetric</a> finally got support for local push &#8211; allowing you to sent messages to the LaMetric without needing an internet connection. Because some people in the support forums asked how to use local push I decided to write a tutorial (I do this on OS X).

<!--more-->

### Creating the app

First step is to create the app for the LaMetric which later will show the information. If you don&#8217;t have a <a href="https://developer.lametric.com" target="_blank">developer account, create one and log in</a>.

<a href="assets/images/2016/03/App-Overview.png"  rel="lightbox[12] attachment wp-att-29"><img loading="lazy" decoding="async" class="aligncenter wp-image-29 size-large" src="assets/images/2016/03/App-Overview-1024x576.png" alt="List of all apps" width="792" height="446" srcset="assets/images/2016/03/App-Overview-1024x576.png 1024w, assets/images/2016/03/App-Overview-300x169.png 300w, assets/images/2016/03/App-Overview-768x432.png 768w, assets/images/2016/03/App-Overview.png 1280w" sizes="(max-width: 767px) 89vw, (max-width: 1000px) 54vw, (max-width: 1071px) 543px, 580px" /></a>

You will see a list of all the apps you have created so far. **Click on &#8220;Create New App&#8221;.**

<a href="assets/images/2016/03/Create-Indicator-App.png"  rel="lightbox[12] attachment wp-att-30"><img loading="lazy" decoding="async" class="aligncenter size-large wp-image-30" src="assets/images/2016/03/Create-Indicator-App-1024x576.png" alt="Create Indicator App" width="792" height="446" srcset="assets/images/2016/03/Create-Indicator-App-1024x576.png 1024w, assets/images/2016/03/Create-Indicator-App-300x169.png 300w, assets/images/2016/03/Create-Indicator-App-768x432.png 768w, assets/images/2016/03/Create-Indicator-App.png 1280w" sizes="(max-width: 767px) 89vw, (max-width: 1000px) 54vw, (max-width: 1071px) 543px, 580px" /></a>

In this case we want to create an indicator app, so **choose &#8220;Create&#8221; on the left side**. We&#8217;re now in the editor and can add and edit frames. A frame can be compared to a page in a book and every app can have multiple frames. In this tutorial we will create two frames. The first one shows an icon and a text string and the second frame shows a chart.

At the moment there are four types of frames &#8211; &#8220;Name&#8221;, &#8220;Metric&#8221;, &#8220;Goal&#8221; and &#8220;Sparkline&#8221;. Each type can display different kind of information and you can choose what you want for your needs. In this tutorial we will stick with &#8220;Name&#8221; and &#8220;Sparkline&#8221;.

Every frame has a number assigned to it. This number (or **index**) is used to address the frame and it starts at 0 not 1.

<div id='gallery-1' class='gallery galleryid-12 gallery-columns-2 gallery-size-medium'>
  <figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='assets/images/2016/03/Create-Indicator-App-Frame-0.png' rel="lightbox[12]"><img loading="lazy" decoding="async" width="300" height="169" src="assets/images/2016/03/Create-Indicator-App-Frame-0-300x169.png" class="attachment-medium size-medium" alt="" aria-describedby="gallery-1-31" srcset="assets/images/2016/03/Create-Indicator-App-Frame-0-300x169.png 300w, assets/images/2016/03/Create-Indicator-App-Frame-0-768x432.png 768w, assets/images/2016/03/Create-Indicator-App-Frame-0-1024x576.png 1024w, assets/images/2016/03/Create-Indicator-App-Frame-0.png 1280w" sizes="100vw" /></a>
  </div><figcaption class='wp-caption-text gallery-caption' id='gallery-1-31'> Frame 0 </figcaption></figure><figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='assets/images/2016/03/Create-Indicator-App-Frame-1.png' rel="lightbox[12]"><img loading="lazy" decoding="async" width="300" height="169" src="assets/images/2016/03/Create-Indicator-App-Frame-1-300x169.png" class="attachment-medium size-medium" alt="" aria-describedby="gallery-1-32" srcset="assets/images/2016/03/Create-Indicator-App-Frame-1-300x169.png 300w, assets/images/2016/03/Create-Indicator-App-Frame-1-768x432.png 768w, assets/images/2016/03/Create-Indicator-App-Frame-1-1024x576.png 1024w, assets/images/2016/03/Create-Indicator-App-Frame-1.png 1280w" sizes="100vw" /></a>
  </div><figcaption class='wp-caption-text gallery-caption' id='gallery-1-32'> Frame 1 </figcaption></figure>
</div>

When you create a new app it already has one frame of type &#8220;Name&#8221;. Change the text to what you want and choose an icon. Next add a new frame by clicking the small +-sign next to the list of frames. Change the type of this frame to &#8220;Sparkline&#8221; and enter some arbitrary numbers.

At the top of the page there is a simulator that shows you how every frame looks, just hit the play button.

Scroll down and change the communication type from &#8220;Poll&#8221; to **&#8220;Push&#8221;**.

<a href="assets/images/2016/03/Select-Push-App.png"  rel="lightbox[12] attachment wp-att-33"><img loading="lazy" decoding="async" class="aligncenter size-large wp-image-33" src="assets/images/2016/03/Select-Push-App-1024x576.png" alt="Select Push App" width="792" height="446" srcset="assets/images/2016/03/Select-Push-App-1024x576.png 1024w, assets/images/2016/03/Select-Push-App-300x169.png 300w, assets/images/2016/03/Select-Push-App-768x432.png 768w, assets/images/2016/03/Select-Push-App.png 1280w" sizes="(max-width: 767px) 89vw, (max-width: 1000px) 54vw, (max-width: 1071px) 543px, 580px" /></a>

Scroll to the bottom and click **&#8220;Next&#8221;**. You see the store information. Choose a name and a description and activate &#8220;Private app&#8221;. This way only you will be able to install the app.

<a href="assets/images/2016/03/App-Name.png"  rel="lightbox[12] attachment wp-att-34"><img loading="lazy" decoding="async" class="aligncenter size-large wp-image-34" src="assets/images/2016/03/App-Name-1024x576.png" alt="App Name" width="792" height="446" srcset="assets/images/2016/03/App-Name-1024x576.png 1024w, assets/images/2016/03/App-Name-300x169.png 300w, assets/images/2016/03/App-Name-768x432.png 768w, assets/images/2016/03/App-Name.png 1280w" sizes="(max-width: 767px) 89vw, (max-width: 1000px) 54vw, (max-width: 1071px) 543px, 580px" /></a>

**Click &#8220;Save&#8221;** and your app is ready. For now it&#8217;s in draft mode and before you can use it you have to publish it. On this page you also see the URLs that you can use for local and remote push to your LaMetric. For now we&#8217;re ready, so **click on &#8220;Publish&#8221;** and keep the tab open since we need the information on this page later. After a few minutes you will get an email telling you that your app was published.

<a href="assets/images/2016/03/Local-Address-and-Publish.png"  rel="lightbox[12] attachment wp-att-37"><img loading="lazy" decoding="async" class="aligncenter size-large wp-image-37" src="assets/images/2016/03/Local-Address-and-Publish-1024x576.png" alt="Local Address and Publish" width="792" height="446" srcset="assets/images/2016/03/Local-Address-and-Publish-1024x576.png 1024w, assets/images/2016/03/Local-Address-and-Publish-300x169.png 300w, assets/images/2016/03/Local-Address-and-Publish-768x432.png 768w, assets/images/2016/03/Local-Address-and-Publish.png 1280w" sizes="(max-width: 767px) 89vw, (max-width: 1000px) 54vw, (max-width: 1071px) 543px, 580px" /></a>

### Install the app

Head to your LaMetric app on your smartphone and add your app the LaMetric. Change the filter to only show private apps and add your new app.

<div id='gallery-2' class='gallery galleryid-12 gallery-columns-2 gallery-size-large'>
  <figure class='gallery-item'> 
  
  <div class='gallery-icon portrait'>
    <a href='assets/images/2016/03/Select-1.png' rel="lightbox[12]"><img loading="lazy" decoding="async" width="405" height="720" src="assets/images/2016/03/Select-1.png" class="attachment-large size-large" alt="" aria-describedby="gallery-2-38" srcset="assets/images/2016/03/Select-1.png 405w, assets/images/2016/03/Select-1-169x300.png 169w" sizes="100vw" /></a>
  </div><figcaption class='wp-caption-text gallery-caption' id='gallery-2-38'> Public Apps </figcaption></figure><figure class='gallery-item'> 
  
  <div class='gallery-icon portrait'>
    <a href='assets/images/2016/03/Select-2.png' rel="lightbox[12]"><img loading="lazy" decoding="async" width="405" height="720" src="assets/images/2016/03/Select-2.png" class="attachment-large size-large" alt="" aria-describedby="gallery-2-39" srcset="assets/images/2016/03/Select-2.png 405w, assets/images/2016/03/Select-2-169x300.png 169w" sizes="100vw" /></a>
  </div><figcaption class='wp-caption-text gallery-caption' id='gallery-2-39'> Private Apps </figcaption></figure>
</div>

Now your LaMetric is ready and we can write some code to send data directly from your PC to it.

### Pushing data

I&#8217;ll use PHP to write a short piece of code that will send data to the local address of the LaMetric. For this to work you need a PHP interpreter on your system. You also need the local push url and your access token (which can be found on the page we left open &#8211; if not head back to the developer center and select your app and choose the &#8220;Published&#8221; tab). Paste this code into a text file and replace LOCAL\_PUSH\_URL with the url and ACCESS_TOKEN with the access token.

<pre class="brush: php; title: curl.php; notranslate" title="curl.php">&lt;?php

$url = "LOCAL_PUSH_URL";

$frames = array( "frames" =&gt; array(
		array(
			'index' =&gt; 0,
			'text' =&gt; "Hello",
			'icon' =&gt; "i1653"
		),
		array(
			'index' =&gt; 1,
			'chartData' =&gt; [
			                1,
			                2,
			                3,
			                4,
			                8,
			                11,
			                7
			            ]
		)	
	)
);

$curl = curl_init();

$headers = array(
    "Accept: application/json",
    "X-Access-Token: ACCESS_TOKEN", 
    "Cache-Control: no-cache", 
);

curl_setopt($curl, CURLOPT_HTTPHEADER, $headers);
curl_setopt($curl, CURLOPT_URL, $url); 
curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1); 
curl_setopt($curl, CURLOPT_HTTPHEADER, $headers); 
curl_setopt($curl, CURLOPT_POST, 1); 
curl_setopt($curl, CURLOPT_POSTFIELDS, json_encode($frames)); 


$response = curl_exec($curl);
curl_close($curl);
?&gt;
</pre>

Your code should now be similar to this:

<a href="assets/images/2016/03/Code.png"  rel="lightbox[12] attachment wp-att-44"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-44" src="assets/images/2016/03/Code.png" alt="Code" width="654" height="720" srcset="assets/images/2016/03/Code.png 654w, assets/images/2016/03/Code-273x300.png 273w" sizes="(max-width: 654px) 100vw, 654px" /></a>

The part of the code that contains the data that is sent to the LaMetric is the _$frames_ variable. For each frame we created in the editor it has an array. Each of those arrays contains the index &#8211; this way the LaMetric knows which data belongs where. For a simple name frame you can also sent the text and the icon. For the sparkline you just send the y-values of the line. For a goal frame you have other parameters &#8211; those can be found on the developer page after you created an app.

<a href="assets/images/2016/03/Data-Format.png"  rel="lightbox[12] attachment wp-att-51"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-51" src="assets/images/2016/03/Data-Format.png" alt="Example of data format" width="775" height="411" srcset="assets/images/2016/03/Data-Format.png 775w, assets/images/2016/03/Data-Format-300x159.png 300w, assets/images/2016/03/Data-Format-768x407.png 768w" sizes="(max-width: 767px) 89vw, (max-width: 1000px) 54vw, (max-width: 1071px) 543px, 580px" /></a>

Before we can go on there are two small changes necessary, that I&#8217;ve already done in the image: Change the &#8220;https&#8221; to &#8220;http&#8221; and &#8220;4343&#8221; to &#8220;8080&#8221;. This will sent your data without any encryption to your LaMetric device, but for now this is how we will do it. If you know how to trust the certificate you can do this and leave the url. Save the PHP file (mine is name curl.php) and open a terminal window.

### Send the data

After installing and selecting the app your LaMetric shows you the default values that you entered in the editor.

<div id='gallery-3' class='gallery galleryid-12 gallery-columns-2 gallery-size-medium'>
  <figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='assets/images/2016/03/Default-0.png' rel="lightbox[12]"><img loading="lazy" decoding="async" width="300" height="93" src="assets/images/2016/03/Default-0-300x93.png" class="attachment-medium size-medium" alt="" aria-describedby="gallery-3-45" srcset="assets/images/2016/03/Default-0-300x93.png 300w, assets/images/2016/03/Default-0-768x239.png 768w, assets/images/2016/03/Default-0.png 785w" sizes="100vw" /></a>
  </div><figcaption class='wp-caption-text gallery-caption' id='gallery-3-45'> Frame 0 </figcaption></figure><figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='assets/images/2016/03/Default-1.png' rel="lightbox[12]"><img loading="lazy" decoding="async" width="300" height="101" src="assets/images/2016/03/Default-1-300x101.png" class="attachment-medium size-medium" alt="" aria-describedby="gallery-3-46" srcset="assets/images/2016/03/Default-1-300x101.png 300w, assets/images/2016/03/Default-1.png 753w" sizes="100vw" /></a>
  </div><figcaption class='wp-caption-text gallery-caption' id='gallery-3-46'> Frame 1 </figcaption></figure>
</div>

In the code you see the text string &#8220;Hello&#8221; and the numbers used for the Sparkline. Change those and call your run your php script.

<a href="assets/images/2016/03/Terminal.png"  rel="lightbox[12] attachment wp-att-47"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-47" src="assets/images/2016/03/Terminal.png" alt="Terminal" width="993" height="717" srcset="assets/images/2016/03/Terminal.png 993w, assets/images/2016/03/Terminal-300x217.png 300w, assets/images/2016/03/Terminal-768x555.png 768w" sizes="(max-width: 767px) 89vw, (max-width: 1000px) 54vw, (max-width: 1071px) 543px, 580px" /></a>

Your LaMetric should show the new data (it may take 1-2s).

<div id='gallery-4' class='gallery galleryid-12 gallery-columns-2 gallery-size-medium'>
  <figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='assets/images/2016/03/After-0.png' rel="lightbox[12]"><img loading="lazy" decoding="async" width="300" height="103" src="assets/images/2016/03/After-0-300x103.png" class="attachment-medium size-medium" alt="" aria-describedby="gallery-4-48" srcset="assets/images/2016/03/After-0-300x103.png 300w, assets/images/2016/03/After-0.png 699w" sizes="100vw" /></a>
  </div><figcaption class='wp-caption-text gallery-caption' id='gallery-4-48'> updated Frame 0 </figcaption></figure><figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='assets/images/2016/03/After-1.png' rel="lightbox[12]"><img loading="lazy" decoding="async" width="300" height="108" src="assets/images/2016/03/After-1-300x108.png" class="attachment-medium size-medium" alt="" aria-describedby="gallery-4-49" srcset="assets/images/2016/03/After-1-300x108.png 300w, assets/images/2016/03/After-1.png 708w" sizes="100vw" /></a>
  </div><figcaption class='wp-caption-text gallery-caption' id='gallery-4-49'> updated Frame 1 </figcaption></figure>
</div>

Now you&#8217;re done. You can modify this script the way you want. On a linux machine you can use cron to call this script periodically if you have to. On OS X use launchd.

&nbsp;

 [1]: https://blog.aruehe.io/lametric-firmware-1-6-0-and-local-push/