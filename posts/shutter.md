## [Greenshot Replacement for Linux](<!this_page!>) {post}
###### 07/19/14 {date}




So today I made a pretty cool script. If you use Windows, Greenshot is a must have screenshot program. But I’ve been seriously considering switching to Linux for my desktop, and one problem I thought of was how Greenshot was not available for Linux (they should really reconsider making a Linux port, they would really be at home being opensource and all.)

So I started looking up alternatives, and I found a great little program called [Shutter](https://shutter-project.org/). Unfortunately Shutter is Linux only, so sorry Windows users, you should stick to Greenshot. One of the great things about Greenshot, though, is the ‘External command’ thing. It allows you to make your own program or batch script and make Greenshot send the image to it. I was using this to send the image to a batch file which would use WinSCP’s scripting features to upload it to my sever, and then paste the link into my clipboard. I would release that, but it’s really bad.

Unfortunately, Shutter has no External command feature. But it doesn’t need to! Linux makes up for it. Shutter does have a –output (-o) argument, which allows you to pick where it saves. So I took that, and made this!

```bash
#!/bin/bash

## Credits to LordOfGears2 - wyattmarks.com

## This script was meant to replicate what I had on my Windows machine with Greenshot. This uses shutter, a program similar to greenshot.
## It requires: shutter and xsel (for pasting the link into your clipboard on finish)
## Problems: 
##	It may require you to type your password, but you should set up RSA keys

ROOT=/home/user/scripts/
REMOTE_DIR=/var/www/images/
URL=http://mycoolsite.com/images/
REMOTE_USER=username
REMOTE_HOST=mycoolsite.com

cd ${ROOT}
OUTPUT=$(date +%Y_%m_%d_%H:%M:%S.png)

shutter -e -n -s -o ${ROOT}${OUTPUT}

scp ./${OUTPUT} ${REMOTE_USER}@${REMOTE_HOST}:${REMOTE_DIR}

echo ${URL}${OUTPUT} | xsel -i -b

rm ${OUTPUT}
```

ROOT is where you are running the script.
REMOTE_DIR is where you are uploading the screenshot.
URL is where the pic gets uploaded in URL format.
REMOTE_HOST is the server you are logging in on.
REMOTE_USER is who you are logging in as on the REMOTE_HOST.

This takes the pic, uploads it, and then puts it in your clipboard. Pretty sweet, huh? Does exactly what Greenshot used to do for me.

This requires xsel too, for putting the link in your clipboard. `sudo apt-get install xsel`

Now to make this automatically run when you press print screen like Greenshot, you need to follow [these](https://shutter-project.org/faq-help/set-shutter-as-the-default-screenshot-tool) instructions, but instead of making the action 'shutter -blah -blah -blah' you need to make the action point to this script. For me, it was /home/lord/scripts/screenshot.sh.

It just depends what/where you save it.
Thanks for reading!