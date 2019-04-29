---
title: '[Solved] Error: No space left on device'
author: justudin
categories:
  - Linux
tags:
  - erorr
  - linux
  - No space left on device
  - ubuntu
---
Hi guys, I would like to share my experience when I got an error “No space left on device” after updating my Ubuntu. If you also found the same problem with me. Maybe you can try using my steps to solve this kind of problem. So what should we do are:

1. Check our /boot directory, is it full or not?

   <pre class="brush: bash; title: ; notranslate" title="">df -h </pre>

   The result in my case is like  in the picture below:

   <img class="wp-image-315 size-full" src="/files/uploads/2014/10/full.png" alt="full" width="587" height="234" srcset="/files/uploads/2014/10/full-300x120.png 300w, /files/uploads/2014/10/full.png 587w" sizes="(max-width: 587px) 100vw, 587px" />

2. It means my “**/boot**” is full (100% used), so we should remove our old kernel, but before doing it we also should check our old kernels in the **“/boot”** directory. Using this command:

   ```bash
   ls -la /boot
   ```

   ![](/files/uploads/2014/10/old-kernel.png)

   ​


3. Remove old kernel using this command:

   ```bash
   sudo rm /boot/initrd.img-X.XX.X-XX-generic
   ```

   but you should change X.XX.X-XX with your own kernel version. 

   You can look into my case below:

   ![](/files/uploads/2014/10/rm-kernel.png)

   After that try this command:

   ```bash
   sudo apt-get -f install
   ```

   again, then purge the package using this command: 

   ```bash
   sudo apt-get -y purge linux-image-X.XX.X-XX-generic
   ```

   ​


4. If you get another `No space left on device, `then you should remove one or more **initrd.img**  (**refer to step 2-3**) and try again.

Good luck!