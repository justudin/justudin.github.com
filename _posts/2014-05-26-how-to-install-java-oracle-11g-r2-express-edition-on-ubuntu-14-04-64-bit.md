---
id: 238
title: How to Install Java, Oracle 11g R2 Express Edition on Ubuntu 14.04 64-bit
date: 2014-05-26T11:18:17+00:00
author: justudin
layout: post
guid: http://justudin.wordpress.com/?p=238
permalink: /how-to-install-java-oracle-11g-r2-express-edition-on-ubuntu-14-04-64-bit/
categories:
  - Tutorial
tags:
  - java
  - oracle 11g
  - oracle express
  - ubuntu 14.04
  - ubuntu server
---
A while ago I tried to install Oracle 11g R2 Express Edition on a 64-bit Ubuntu Server. This prove to be not as easy as you would expect. There are many blogs and articles about this subject and I tried a number of them. Unfortunately neither of the instructions seemed to work completely on my server. With the combined information from the authors, I finally got it to work and I&#8217;ll gladly share my recipe in this blog. The installation was performed on a Ubuntu Server 14.04 64-bit with the following software:

  * Oracle Java 1.7.0_51
  * Oracle XE 11.2.0 (<a href="http://www.oracle.com/technetwork/database/database-technologies/express-edition/downloads/index.html" target="_blank">here</a>)

<!--more-->

**Installing Java**

We start with installing Java on the machine. My personal preference is to use Oracle Java JDK. Installing this JDK could be done easily by performing the following statements.

<pre class="brush: bash; title: ; notranslate" title="">$ sudo add-apt-repository ppa:webupd8team/java
$ sudo apt-get update
$ sudo apt-get install oracle-java7-installer
</pre>

The screen in figure 1 will appear in the terminal, hit enter to proceed. After this, the screen in figure 2 will be shown. Navigate to <Yes> using the left arrow on your keyboard and hit enter. Oracle JDK 7 will be installed.<figure id="attachment_239" style="width: 665px" class="wp-caption aligncenter">

<img class="wp-image-239 size-full" src="files/uploads/2014/05/oracle-java.png" alt="Figure 1: Binary Code license" width="665" height="395" srcset="files/uploads/2014/05/oracle-java-768x457.png 768w, files/uploads/2014/05/oracle-java.png 810w" sizes="(max-width: 665px) 100vw, 665px" /><figcaption class="wp-caption-text">Figure 1: Binary Code license</figcaption></figure> <figure id="attachment_240" style="width: 665px" class="wp-caption aligncenter"><img class="size-full wp-image-240" src="files/uploads/2014/05/jdk-agreement.png" alt="Figure 2: JDK License Agreement" width="665" height="398" srcset="files/uploads/2014/05/jdk-agreement-300x180.png 300w, files/uploads/2014/05/jdk-agreement-768x460.png 768w, files/uploads/2014/05/jdk-agreement.png 810w" sizes="(max-width: 665px) 100vw, 665px" /><figcaption class="wp-caption-text">Figure 2: JDK License Agreement</figcaption></figure> 

The next next step is to set the JAVA_HOME environment variable. To do this, open the /etc/bash.bashrc file by executing the following statement.

<pre class="brush: bash; title: ; notranslate" title="">$ sudo gedit /etc/bash.bashrc
</pre>

Scroll to the bottom of the file and add the following lines.

<pre class="brush: bash; title: ; notranslate" title="">export JAVA_HOME=/usr/lib/jvm/java-7-oracle
export PATH=$JAVA_HOME/bin:$PATH
</pre>

Save the file and close the editor. To load the changes, execute the following statement.

<pre class="brush: bash; title: ; notranslate" title="">$ source /etc/bash.bashrc
</pre>

To validate the changes you can execute the following statement.

<pre class="brush: bash; title: ; notranslate" title="">$ echo $JAVA_HOME
</pre>

The result of this statement should be the following.

<pre class="brush: bash; title: ; notranslate" title="">/usr/lib/jvm/java-7-oracle
</pre>

**Installing Oracle 11g R2 Express Edition**

For the installation of Oracle 11g R2 Express Edition (XE), a couple of additional Linux packages are required. These packages can be installed by executing the following statement.

<pre class="brush: bash; title: ; notranslate" title="">$ sudo apt-get install alien libaio1 unixodbc
</pre>

The next step is to download the Oracle 11g R2 Express Edition from the Oracle website. Make sure you select the Linux x64 version from Oracle's website. After the download is completed, open the terminal and navigate to the download directory. In my case this can be done by executing the following statement.

The next step step is to unzip the downloaded file. To do this, execute the following command.

<pre class="brush: bash; title: ; notranslate" title="">$ unzip oracle-xe-11.2.0-1.0.x86_64.rpm.zip
</pre>

A new directory (Disk1) is added to the Download directory. Navigate to this directory:

<pre class="brush: bash; title: ; notranslate" title="">$ cd Disk1
</pre>

Now we have to convert the Red Hat package (rpm) to a Debian package. This may be done using the alien command. The -d parameter is used to inform alien that a Debian package should be generated. When the -scripts parameter is toggled, alien will try to convert the scripts that are meant to be run when the package is installed and removed.

<pre class="brush: bash; title: ; notranslate" title="">$ sudo alien --scripts -d oracle-xe-11.2.0-1.0.x86_64.rpm
</pre>

This step may take a while, while this statement is executing we can do the following steps. Open a new terminal window for these steps.

The Red Hat package, relies on the /sbin/chkconfig file, which is not used in Ubuntu. To successfully install Oracle XE we use a simple trick. Start by creating a custom /sbin/chkconfig file by executing the following statement.

<pre class="brush: bash; title: ; notranslate" title="">$ sudo gedit /sbin/chkconfig
</pre>

Copy and paste the following into the editor:

<pre class="brush: bash; title: ; notranslate" title="">#!/bin/bash
# Oracle 11gR2 XE installer chkconfig hack for Ubuntu
file=/etc/init.d/oracle-xe
if [[ ! `tail -n1 $file | grep INIT` ]]; then
echo &amp;gt;&amp;gt; $file
echo '### BEGIN INIT INFO' &amp;gt;&amp;gt; $file
echo '# Provides: OracleXE' &amp;gt;&amp;gt; $file
echo '# Required-Start: $remote_fs $syslog' &amp;gt;&amp;gt; $file
echo '# Required-Stop: $remote_fs $syslog' &amp;gt;&amp;gt; $file
echo '# Default-Start: 2 3 4 5' &amp;gt;&amp;gt; $file
echo '# Default-Stop: 0 1 6' &amp;gt;&amp;gt; $file
echo '# Short-Description: Oracle 11g Express Edition' &amp;gt;&amp;gt; $file
echo '### END INIT INFO' &amp;gt;&amp;gt; $file
fi
update-rc.d oracle-xe defaults 80 01
#EOF
</pre>

Save the file and close the editor. Now we have to provide the file with the appropriate execution privileges.

<pre class="brush: bash; title: ; notranslate" title="">$ sudo chmod 755 /sbin/chkconfig
</pre>

After this, we have to create the file /etc/sysctl.d/60-oracle.conf to set the additional kernel parameters. Open the file by executing the following statement.

<pre class="brush: bash; title: ; notranslate" title="">$ sudo gedit /etc/sysctl.d/60-oracle.conf
</pre>

Copy and paste the following into the file. Kernel.shmmax is the maximum possible value of physical RAM in bytes. 536870912 / 1024 /1024 = 512 MB

<pre class="brush: bash; title: ; notranslate" title=""># Oracle 11g XE kernel parameters
fs.file-max=6815744
net.ipv4.ip_local_port_range=9000 65000
kernel.sem=250 32000 100 128
kernel.shmmax=536870912
</pre>

Save the file. The changes in this file may be verified by executing:

<pre class="brush: bash; title: ; notranslate" title="">$ sudo cat /etc/sysctl.d/60-oracle.conf
</pre>

Load the kernel parameters:

<pre class="brush: bash; title: ; notranslate" title="">$ sudo service procps start
</pre>

The changes may be verified again by executing:

<pre class="brush: bash; title: ; notranslate" title="">$ sudo sysctl -q fs.file-max
</pre>

This method should return the following:

<pre class="brush: bash; title: ; notranslate" title="">fs.file-max = 6815744
</pre>

After this, execute the following statements to make some more required changes:

<pre class="brush: bash; title: ; notranslate" title="">$ sudo ln -s /usr/bin/awk /bin/awk
$ mkdir /var/lock/subsys
$ touch /var/lock/subsys/listener
</pre>

Close the second terminal window and return to the first terminal window. The rpm package should be converted and a new file called oracle-xe-11.2.0-2_amd64.deb have been generated. To run this file, execute the following command:

<pre class="brush: bash; title: ; notranslate" title="">$ sudo dpkg --install oracle-xe_11.2.0-2_amd64.deb
</pre>

Execute the following to avoid getting a ORA-00845: MEMORY_TARGET error. **Note:** replace “size=4096m” with the size of your (virtual) machine’s RAM in MBs.

<pre class="brush: bash; title: ; notranslate" title="">$ sudo rm -rf /dev/shm
$ sudo mkdir /dev/shm
$ sudo mount -t tmpfs shmfs -o size=4096m /dev/shm
</pre>

Create the file /etc/rc2.d/S01shm_load.

<pre class="brush: bash; title: ; notranslate" title="">$ sudo gedit /etc/rc2.d/S01shm_load
</pre>

Copy and paste the following in the file. **Note:** replace “size=4096m” with the size of your machine’s RAM in MBs.

<pre class="brush: bash; title: ; notranslate" title="">#!/bin/sh
case &amp;quot;$1&amp;quot; in
start) mkdir /var/lock/subsys 2&amp;gt;/dev/null
touch /var/lock/subsys/listener
rm /dev/shm 2&amp;gt;/dev/null
mkdir /dev/shm 2&amp;gt;/dev/null
mount -t tmpfs shmfs -o size=4096m /dev/shm ;;
*) echo error
exit 1 ;;
esac
</pre>

Save the file, close the editor and provide the appropriate execution privileges.

<pre class="brush: bash; title: ; notranslate" title="">$ sudo chmod 755 /etc/rc2.d/S01shm_load
</pre>

**Configuring Oracle 11g R2 Express Edition**

If you have successfully installed to Oracle 11g R2 Express Edition server, it’s time to configure the server. To start the configuration of the server, execute the following command and follow the “wizard” in the terminal. Default values are shown between brackets for each question.

<pre class="brush: bash; title: ; notranslate" title="">$ sudo /etc/init.d/oracle-xe configure
</pre>

Now it is time to set-up some environmental variables. Open the /etc/bash.bashrc file by executing the following statement:

<pre class="brush: bash; title: ; notranslate" title="">$ sudo gedit /etc/bash.bashrc
</pre>

Scroll to the bottom of the file and add the following lines.

<pre class="brush: bash; title: ; notranslate" title="">export ORACLE_HOME=/u01/app/oracle/product/11.2.0/xe
export ORACLE_SID=XE
export NLS_LANG=`$ORACLE_HOME/bin/nls_lang.sh`
export ORACLE_BASE=/u01/app/oracle
export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$LD_LIBRARY_PATH
export PATH=$ORACLE_HOME/bin:$PATH
</pre>

Save the file and close the editor. To load the changes, execute the following statement:

<pre class="brush: bash; title: ; notranslate" title="">$ source /etc/bash.bashrc
</pre>

To validate the changes you can execute the following statement.

<pre class="brush: bash; title: ; notranslate" title="">$ echo $ORACLE_HOME
</pre>

This statement should result in the following output.

<pre class="brush: bash; title: ; notranslate" title="">/u01/app/oracle/product/11.2.0/xe
</pre>

After this step it is recommended to reboot the machine. After the reboot is completed, you should be able to start the Oracle server using the following command:

<pre class="brush: bash; title: ; notranslate" title="">$ sudo service oracle-xe start
</pre>

Configure your instalation such as a password, port, etc.

After that open your oracle through browser http://YOUR-IP-ADDRESS:PORT/apex/

That&#8217;s all! Thank you for reading my note. If you found any trouble please don&#8217;t hesitate to contact me or leave me a comment!