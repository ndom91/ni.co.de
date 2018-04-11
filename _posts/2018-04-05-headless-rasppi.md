---
layout:  post_content
title:  "headless rasp pi"
date:   2018-04-05 01:16:01 -0600
comments: true
excerpt_separator: <!---excerpt--->
---

### SSH
> Create an empty file named <code>ssh</code> _without an extension_ in the root of the <code>BOOT</code> partition

### WiFi

> Also in the root of the <code>BOOT</code> partition:
> Create a file named <code>**wpa_supplicant.conf**</code> with the following contents:
>  

{% highlight sh linenos %}
country=DE
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
	ssid="Finger_Weg_OBEN"
	scan_ssid=1
	psk="1123581321345589"
	key_mgmt=WPA-PSK
}
{% endhighlight %}
