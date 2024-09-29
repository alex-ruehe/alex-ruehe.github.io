---
title: Show Download and Upload speed on your LaMetric Time
author: Alex
type: posts
date: 2017-02-06T13:13:57+00:00
url: /posts/show-download-and-upload-speed-on-your-lametric-time/
categories:
  - Tutorial
tags:
  - LaMetric
  - Python
  - Tutorial

---
Following a request at the LaMetric forum I wrote a small Python script for displaying your current download and upload speed on a LaMetric Time. The script can run on your own laptop or server (preferred).

Basically you need to do two things:

  * Create an app for the LaMetric Time
  * run the script that performs the speed test and push the results to the device

#### 1. Create an indicator app

This is quite an easy thing to do. You need an account for the <a href="https://developer.lametric.com" target="_blank">LaMetric developer area</a> (it&#8217;s free, so don&#8217;t worry). In the developer area you can create a new app &#8211; in this case select indicator application.

![](/images/2017/02/Screen-Shot-2017-02-06-at-09.38.34.png)

On the new page, you can create the layout of the app. You need two text frames, one for the download speed and one for the upload speed. Also choose an icon for each frame, I decided to use a green down and green up arrow. It&#8217;s important that you select &#8220;Push&#8221; so that you can send your information to the LaMetric Time.


![](/images/2017/02/Screen-Shot-2017-02-06-at-09.39.00.png)

My design looks like this, but I later decided to drop the &#8220;Mbit/s&#8221;. It made the text too long, which is ok, the text will scroll on the display, but it means you have to wait for the scrolling to end, before the next frame is displayed. Plus I know that it&#8217;s Mbit/s. I&#8217;m also thinking about dropping the &#8220;UL&#8221; and &#8220;DL&#8221; prefix, since the arrows give me enough information.


![](/images/2017/02/Screen-Shot-2017-02-06-at-09.40.54.png)

Next you need to enter some information about the app, that is displayed in the store. You nee an App name and a short description, also make sure to check the &#8220;Private app&#8221; field.

![](/images/2017/02/Screen-Shot-2017-02-06-at-09.41.48.png)

Click &#8220;Save&#8221; and the app is ready to be published. On the next page you will see the URLs and the access token that is needed to send data to the app. Copy the &#8220;Local Push URL&#8221; and &#8220;Access token&#8221;. You could also use the &#8220;Push URL&#8221; instead of the local one, but I prefer it that way. I find it unnecessary  to send the data from my server at home to the LaMetric servers from where it comes back to my LaMetric Time which stands 5m away from my server.

![](/images/2017/02/Screen-Shot-2017-02-06-at-09.42.22.png)

Hit &#8220;Publish&#8221; and after a few minutes you should get a mail telling you that your app is ready.

Now you can install the app on your LaMetric Time. The following four screenshots describe how to do this:

![](/images/2017/02/IMG_0234.png)
![](/images/2017/02/IMG_0235.png)
![](/images/2017/02/IMG_0236.png)
![](/images/2017/02/IMG_0237.png)
<a href="assets/images/2017/02/IMG_0234.png" rel="lightbox[176]"><img loading="lazy" decoding="async" class="aligncenter size-large wp-image-189" src="assets/images/2017/02/IMG_0234-576x1024.png" alt="" width="525" height="933" srcset="assets/images/2017/02/IMG_0234-576x1024.png 576w, assets/images/2017/02/IMG_0234-169x300.png 169w, assets/images/2017/02/IMG_0234.png 750w" sizes="(max-width: 525px) 100vw, 525px" /></a> <a href="assets/images/2017/02/IMG_0235.png" rel="lightbox[176]"><img loading="lazy" decoding="async" class="aligncenter size-large wp-image-190" src="assets/images/2017/02/IMG_0235-576x1024.png" alt="" width="525" height="933" srcset="assets/images/2017/02/IMG_0235-576x1024.png 576w, assets/images/2017/02/IMG_0235-169x300.png 169w, assets/images/2017/02/IMG_0235.png 750w" sizes="(max-width: 525px) 100vw, 525px" /></a> <a href="assets/images/2017/02/IMG_0236.png" rel="lightbox[176]"><img loading="lazy" decoding="async" class="aligncenter size-large wp-image-191" src="assets/images/2017/02/IMG_0236-576x1024.png" alt="" width="525" height="933" srcset="assets/images/2017/02/IMG_0236-576x1024.png 576w, assets/images/2017/02/IMG_0236-169x300.png 169w, assets/images/2017/02/IMG_0236.png 750w" sizes="(max-width: 525px) 100vw, 525px" /></a> <a href="assets/images/2017/02/IMG_0237.png" rel="lightbox[176]"><img loading="lazy" decoding="async" class="aligncenter size-large wp-image-192" src="assets/images/2017/02/IMG_0237-576x1024.png" alt="" width="525" height="933" srcset="assets/images/2017/02/IMG_0237-576x1024.png 576w, assets/images/2017/02/IMG_0237-169x300.png 169w, assets/images/2017/02/IMG_0237.png 750w" sizes="(max-width: 525px) 100vw, 525px" /></a>

Now your LaMetric Time is ready to receive data.

#### 2. Run the script periodically on your server to update the values

The script can be found on GitHub: <a href="https://github.com/alexrockt/lm_connection_speed" target="_blank">lm_connection_speed</a> &#8211; if you don&#8217;t know how to clone a repository, you can also directly download the files: <a href="https://github.com/alexrockt/lm_connection_speed/archive/master.zip" target="_blank">Download</a>

I recommend Python 3, but it should work (no guarantee) with Python 2. It has three dependencies (requests, json and speedtest-cli). Please make sure install those before running the script.

Open the <code class="EnlighterJSRAW" data-enlighter-language="python">connection_speed.py</code> in an text editor and look for lines 21/22 and insert the access token and push url from above. Save the file and you are good to go.

If you remember I said that I don&#8217;t want to see the &#8220;Mbit/s&#8221; &#8211; if you want to see it, you need to change two more lines in the file:

<pre class="EnlighterJSRAW" data-enlighter-language="python">dl_rate = "DL {:.2f}".format(DL / 1000 / 1000)
dl_icon = "i402"
ul_rate = "UL {:.2f}".format(UL / 1000 / 1000)
ul_icon = "i120"</pre>

needs to be:

<pre class="EnlighterJSRAW" data-enlighter-language="python">dl_rate = "DL {:.2f} Mbit/s".format(DL / 1000 / 1000)
dl_icon = "i402"
ul_rate = "UL {:.2f} Mbit/s".format(UL / 1000 / 1000)
ul_icon = "i120"</pre>

Now you can run the script

<code class="EnlighterJSRAW" data-enlighter-language="python">python3 connection_speed.py</code>

Have a look the remarks in the README and for running the script periodically please consult your preferred search engine.