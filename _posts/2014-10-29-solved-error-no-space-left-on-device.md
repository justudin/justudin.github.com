---
id: 311
title: '[Solved] Error: No space left on device'
date: 2014-10-29T05:44:59+00:00
author: justudin
layout: post
guid: http://justudin.wordpress.com/?p=311
permalink: /solved-error-no-space-left-on-device/
categories:
  - Linux
tags:
  - erorr
  - linux
  - No space left on device
  - ubuntu
---
Hi guys, I would like to share my experience when I got an error &#8220;No space left on device&#8221; after updating my Ubuntu. If you also found the same problem with me. Maybe you can try using my steps to solve this kind of problem. So what should we do are:<!--more-->

1. Check our /boot directory, is it full or not?

<pre class="brush: bash; title: ; notranslate" title="">df -h </pre>

The result in my case is like  in the picture below:

<img class="wp-image-315 size-full" src="files/uploads/2014/10/full.png" alt="full" width="587" height="234" srcset="files/uploads/2014/10/full-300x120.png 300w, files/uploads/2014/10/full.png 587w" sizes="(max-width: 587px) 100vw, 587px" />

2. It means my &#8220;**/boot**&#8221; is full (100% used), so we should remove our old kernel, but before doing it we also should check our old kernels in the **&#8220;/boot&#8221;** directory. Using this command:

<pre class="brush: bash; title: ; notranslate" title="">ls -la /boot </pre>

<img class="wp-image-316 size-full" src="files/uploads/2014/10/old-kernel.png" alt="Result from command &quot;ls -la /boot&quot;" width="755" height="838" srcset="files/uploads/2014/10/old-kernel-270x300.png 270w, files/uploads/2014/10/old-kernel.png 755w" sizes="(max-width: 755px) 100vw, 755px" />

3. Remove old kernel using this command:

<pre class="brush: bash; title: ; notranslate" title="">sudo rm /boot/initrd.img-X.XX.X-XX-generic </pre>

but you should change X.XX.X-XX with your own kernel version. You can look into my case below:

<img class="aligncenter wp-image-320 size-full" src="files/uploads/2014/10/rm-kernel.png" alt="rm kernel" width="594" height="21" srcset="files/uploads/2014/10/rm-kernel-300x11.png 300w, files/uploads/2014/10/rm-kernel.png 594w" sizes="(max-width: 594px) 100vw, 594px" />

After that try this command

<pre class="brush: bash; title: ; notranslate" title=""> sudo apt-get -f install </pre>

again, then purge the package using this command:

&nbsp;

<pre class="brush: bash; title: ; notranslate" title="">sudo apt-get -y purge linux-image-X.XX.X-XX-generic </pre>

4. If you get another `<strong>No space left on device</strong>, `then you should remove one or more initrd.img  (**refer to step 2-3**) and try again.

Good luck!