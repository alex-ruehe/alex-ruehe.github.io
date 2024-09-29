---
title: LaMetric Firmware 1.6.0 and local push
author: Alex
type: posts
date: 2016-07-17T20:25:28+00:00
url: /posts/lametric-firmware-1-6-0-and-local-push/
categories:
  - Tutorial
tags:
  - LaMetric
  - PHP
  - Tutorial

---
**UPDATE (08.08.2016): Apparently you can get your api key at <a href="https://developer.lametric.com/user/devices" target="_blank">https://developer.lametric.com/user/devices</a> now.** 

With the <a href="http://help.lametric.com/support/discussions/topics/6000038843" target="_blank">LaMetric Time Firmware update 1.6.0</a> the API for local push notifications changed and <a href="https://blog.aruehe.io/lametric-local-push/" target="_blank">my tutorial for the 1.5.0 firmware</a> does&#8217;t work anymore. The new firmware offers the possibility to show notifications without installing an extra app.

<!--more-->

For this to work you have to create an &#8220;notifications app&#8221; in the developer backend. This is similar to creating the old apps, but you don&#8217;t have to add it to your LaMetric Time. Go to the developer backend and create a new notifications app. Choose a name, enter a short description and set the redirect url to a dummy domain &#8211; e.g. http://dfgdgddfdfg.de (in this case, it doesn&#8217;t really matter, because we use this only for ourself). Then click &#8220;Save&#8221; and your app is ready. Get the &#8220;Client ID&#8221; from the info page of the app.

<div id='gallery-5' class='gallery galleryid-64 gallery-columns-4 gallery-size-medium'>
  <figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='assets/images/2016/07/1-e1468784209769.jpeg' rel="lightbox[64]"><img loading="lazy" decoding="async" width="300" height="169" src="assets/images/2016/07/1-300x169.jpeg" class="attachment-medium size-medium" alt="" srcset="assets/images/2016/07/1-300x169.jpeg 300w, assets/images/2016/07/1-768x434.jpeg 768w, assets/images/2016/07/1-1024x578.jpeg 1024w, assets/images/2016/07/1-e1468784209769.jpeg 1280w" sizes="100vw" /></a>
  </div></figure><figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='assets/images/2016/07/2-e1468784226915.jpeg' rel="lightbox[64]"><img loading="lazy" decoding="async" width="300" height="169" src="assets/images/2016/07/2-300x169.jpeg" class="attachment-medium size-medium" alt="" srcset="assets/images/2016/07/2-300x169.jpeg 300w, assets/images/2016/07/2-768x434.jpeg 768w, assets/images/2016/07/2-1024x578.jpeg 1024w, assets/images/2016/07/2-e1468784226915.jpeg 1280w" sizes="100vw" /></a>
  </div></figure><figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='assets/images/2016/07/3-e1468784234332.jpeg' rel="lightbox[64]"><img loading="lazy" decoding="async" width="300" height="170" src="assets/images/2016/07/3-300x170.jpeg" class="attachment-medium size-medium" alt="" srcset="assets/images/2016/07/3-300x170.jpeg 300w, assets/images/2016/07/3-768x435.jpeg 768w, assets/images/2016/07/3-1024x580.jpeg 1024w, assets/images/2016/07/3-e1468784234332.jpeg 1280w" sizes="100vw" /></a>
  </div></figure><figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='assets/images/2016/07/4-e1468784241851.jpeg' rel="lightbox[64]"><img loading="lazy" decoding="async" width="300" height="169" src="assets/images/2016/07/4-300x169.jpeg" class="attachment-medium size-medium" alt="" srcset="assets/images/2016/07/4-300x169.jpeg 300w, assets/images/2016/07/4-768x434.jpeg 768w, assets/images/2016/07/4-1024x578.jpeg 1024w, assets/images/2016/07/4-e1468784241851.jpeg 1280w" sizes="100vw" /></a>
  </div></figure>
</div>

To communicate with the LaMetric Time in a local network we need the api key. With the 1.6.0 firmware this has to be obtained by getting an access token via OAuth2. With your client id at hand open the following URL in a browser after replacing the CLIENT-ID with your client id.

<pre class="brush: plain; title: ; notranslate" title="">https://developer.lametric.com/api/v2/oauth2/authorize/?client_id=CLIENT-ID&response_type=token&scope=basic+devices_read+devices_write&state=STATE</pre>

This should open a website, asking you if you want to authorize your new app to access your LaMetric account. Click &#8220;ALLOW&#8221; and you should be redirected to the redirect url you entered before. If you used facebook.com, you probably see an error messsage, 404 site not found, but that&#8217;s ok. We&#8217;re only interested in the current URL &#8211; this should look like

<pre class="brush: plain; title: ; notranslate" title="">https://developer.lametric.com/api/v2/oauth2/authorize/www.facebook.com#access_token=xyz&expires_in=7200&token_type=Bearer&scope=basic+devices_read+devices_write&state=STATE</pre>

Copy the access token part from the url &#8211; in the example above it&#8217;s &#8220;xyz&#8221;. Using this access token we can get the api key from our LaMetric Time with the following php script &#8211; again, replace the CLIENT-ID with your <del datetime="2016-11-07T13:57:45+00:00">client-id</del>**access token** from before. Make sure you run this script shortly after getting the access token, since it expires after few minutes.

<pre class="brush: php; title: ; notranslate" title="">&lt;?php
$url = "https://developer.lametric.com/api/v2/users/me/devices";

$curl = curl_init();

$headers = array(
    "Accept: application/json",
    "Authorization: Bearer ACCESS TOKEN", 
    "Cache-Control: no-cache", 
);

curl_setopt($curl, CURLOPT_HTTPHEADER, $headers);
curl_setopt($curl, CURLOPT_URL, $url); 
curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1); 
curl_setopt($curl, CURLOPT_HTTPHEADER, $headers); 

$response = curl_exec($curl);

echo $response;
curl_close($curl);

?&gt;
</pre>

The result should look like

<pre class="brush: jscript; title: ; notranslate" title="">[
   {
      "updated_at" : "---",
      "api_key" : "123123123",
      "serial_number" : "---",
      "name" : "LaMetric",
      "id" : ---,
      "created_at" : "---",
      "state" : "configured",
      "mac" : "---",
      "ipv4_internal" : "123.123.123.123",
      "wifi_ssid" : "---"
   }
]
</pre>

The two important parts are the api\_key and the ipv4\_internal. With those two things we can send notifications directly to the LaMetric Time. To use the api key, it has to be prefixed by &#8220;dev:&#8221; and the whole string needs to be base64 encoded &#8211; if you don&#8217;t know what this means, don&#8217;t worry, it&#8217;s easy to do:

1. api key from above: 123123123  
2. new api key with prefix: dev:123123123  
3. Copy the whole string and paste it on <a href="https://www.base64encode.org" target="_blank">https://www.base64encode.org</a> and click &#8220;ENCODE&#8221;: ZGV2OjEyMzEyMzEyMw==

This is your api key you need to use whenever you interact with the LaMetric Time. Using the following script you can see all available api endpoints on your device &#8211; meaning all the things you can interact with.

<pre class="brush: php; title: ; notranslate" title="">&lt;?php
$url = "https://123.123.123.123:4343/api/v2";

$curl = curl_init();

$headers = array(
    "Accept: application/json",
    "Authorization: Basic ZGV2OjEyMzEyMzEyMw==", 
    "Cache-Control: no-cache", 
);

curl_setopt($curl, CURLOPT_HTTPHEADER, $headers);
curl_setopt($curl, CURLOPT_URL, $url); 
curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1); 
curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($curl, CURLOPT_HTTPHEADER, $headers); 


$response = curl_exec($curl);

echo $response;
curl_close($curl);

?&gt;
</pre>

The output of this script looks like

<pre class="brush: jscript; title: ; notranslate" title="">{
   "endpoints" : {
      "audio_url" : "https://123.123.123.123:4343/api/v2/device/audio",
      "concrete_notification_url" : "https://123.123.123.123:4343/api/v2/device/notifications{/:id}",
      "device_url" : "https://123.123.123.123:4343/api/v2/device",
      "widget_update_url" : "https://123.123.123.123:4343/api/v2/widget/update{/:id}",
      "notifications_url" : "https://123.123.123.123:4343/api/v2/device/notifications",
      "current_notification_url" : "https://123.123.123.123:4343/api/v2/device/notifications/current",
      "bluetooth_url" : "https://123.123.123.123:4343/api/v2/device/bluetooth",
      "wifi_url" : "https://123.123.123.123:4343/api/v2/device/wifi",
      "display_url" : "https://123.123.123.123:4343/api/v2/device/display"
   },
   "api_version" : "2.0.0"
}
</pre>

To sent a notification use the following script as an example:

<pre class="brush: php; title: ; notranslate" title="">&lt;?php
$url = "https://123.123.123.123:4343/api/v2/device/notifications";

$frames = array(
    "priority" =&gt; "info",
    'icon_type' =&gt; 'none',
    "model" =&gt; array(
        "cycles" =&gt; 0,
    	"frames" =&gt; array(
    		array(
                "icon" =&gt; "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAICAYAAADED76LAAAAUklEQVQYlWNUVFBgYGBgYBC98uE/AxJ4rSPAyMDAwMCETRJZjAnGgOlAZote+fCfCV0nOmA0+yKAYTwygJuAzQoGBgYGRkUFBQZ0dyDzGQl5EwCTESNpFb6zEwAAAABJRU5ErkJggg==",
    			"text" =&gt; "Hello"
    		)	
    	)
    )
);

$curl = curl_init();

$headers = array(
    "Accept: application/json",
    "Content-Type: application/json",
    "Authorization: Basic ZGV2OjEyMzEyMzEyMw==", 
    "Cache-Control: no-cache", 
);

echo json_encode($frames);

echo "\n";

curl_setopt($curl, CURLOPT_HTTPHEADER, $headers);
curl_setopt($curl, CURLOPT_URL, $url); 
curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1); 
curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($curl, CURLOPT_HTTPHEADER, $headers); 
curl_setopt($curl, CURLOPT_POST, 1); 
curl_setopt($curl, CURLOPT_POSTFIELDS, json_encode($frames)); 


$response = curl_exec($curl);

echo $response;

curl_close($curl);

?&gt;
</pre>

When you run this script, you should see a &#8220;Hello&#8221; notification that stays until you hit the Action button. To get more information about notifications (e.g. setting sound) have a look at the new <a href="http://lametric-documentation.readthedocs.io/en/latest/reference-docs/device-notifications.html" target="_blank">documentation for firmware 1.6.0</a>.