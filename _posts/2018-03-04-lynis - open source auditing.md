---
layout:  post_content
title:  "lynis auditing"
date:   2018-03-04 13:16:01 -0600
comments: true
excerpt_separator: <!---excerpt--->
---


So you’ve got your system up and running the way you like it, but your wondering what else can I do to harden my server?

Lynis to the rescue!

Lynis is an open-source auditing tool that will run through a ton a of vulnerability checks and general best practice type checks and give you a thorough summary of your system at the end.
<!---excerpt--->
The best part is, its super easy to run and even automate with a cronjob 1/week or 1/month.

So lets get started!

I like to run it out of /opt, so we’ll cd there.


<div class="codeblok">{% highlight shell linenos %}
cd /opt
{% endhighlight %}</div>


Then we’ll download the tool. Please check the [lynis download page](https://cisofy.com/downloads/lynis/) for the newest version

sudo wget https://cisofy.com/files/lynis-2.6.2.tar.gz

and extract it

<div class="codeblok">{% highlight shell linenos %}
 tar -xvf lynis-2.6.2.tar.gz
 cd lynis
{% endhighlight %}</div>

And that was actually all there is to it!

You can run ./lynis now to run a scan.

Now of course this isn’t the end of your journey. I want to run this as a cronjob and email me the output.

So to run lynis as a cron job we’ll define the lynis command with the following options:

<div class="codeblok">{% highlight shell linenos %}
./lynis audit system --cronjob
{% endhighlight %}</div>

Unfortunately that will only run lynis and dump a report file on our system. In order to have it email us the results we’ll have to write a little script.

I whipped up the following:

<div class="codeblok">{% highlight shell linenos %}
#!/bin/bash

###################
\# VARIABLES
###################

CURDATE=$(date '+%d-%m-%Y %H:%M')
FILEDATE=$(date '+%d%m%Y')
LYNIS_PATH=/opt/lynis

cd $LYNIS_PATH

./lynis audit system --cronjob > $LYNIS_PATH/scan_$FILEDATE.txt

MAILCONTENT=$(cat $LYNIS_PATH/scan_$FILEDATE)

echo "From: [from Name]
To: [to Address]
Subject: Lynis Scan - $CURDATE

$MAILCONTENT" | /usr/sbin/sendmail [to Address]
{% endhighlight %}</div>

This gets saved in, for example, lynis_mail.sh

Don’t forget to mark this as executable:

<div class="codeblok">{% highlight shell linenos %}
sudo chmod +x /path/to/your/script/lynis_mail.sh
{% endhighlight %}</div>

And finally, set your cronjob like this for example to run every Monday morning at 5:30 so you can browse it on your commute to work in the train 😉

<div class="codeblok">{% highlight shell linenos %}
sudo crontab -e

30 5 * * MON /path/to/your/script/lynis_mail.sh
{% endhighlight %}</div>
