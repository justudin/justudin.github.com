---
id: 31
title: '[Source Code] Program Java untuk konversi Desimal ke Biner'
date: 2013-01-18T14:24:35+00:00
author: justudin
layout: post
guid: http://justudin.wordpress.com/?p=31
permalink: /source-code-program-java-untuk-konversi-desimal-ke-biner/
categories:
  - Tutorial
tags:
  - biner
  - biner desimal
  - desimal
  - desimal biner
  - java
  - konversi
  - source code
  - Tutorial
---
<div id="post-body-3636261864662233949">
  Oke, kali ini saya mau share source code program konversi desimal ke biner..kebalikan dari posting saya sebelumnya tentang <a href="http://udin-just4u.blogspot.com/2011/04/share-program-java-untuk-konversi-biner.html">Program Java untuk konversi Biner ke desimal</a> ..<br /> Oke langsung saja silahkan copy source code berikut dan save dengan nama *.java<br /> *Sesuaikan dengan nama Class, disini saya save dengan nama <b>DesToBin.java</b>
</div>

<div>
  <!--more-->
</div>

<div>
</div>

<div>
  <pre class="brush: java; title: ; notranslate" title="">
import java.util.Scanner;
class Konversi{
public void desimalkebiner(int a){
if (a&gt;1) {
desimalkebiner(a/2);
}
System.out.print(a%2);
}
}
class DesToBin {
public static void main (String args[]){
int des, a;
Konversi angka = new Konversi();
Scanner input = new Scanner(System.in);
System.out.print(&quot;Masukkan Angka : &quot;);
des = input.nextInt();
System.out.println(&quot;Bilangan Desimalnya : &quot;+des);
System.out.print(&quot;Konversi Binernya : &quot;);
angka.desimalkebiner(des);
System.out.println();
}
}
</pre>
  
  <p>
    Lalu compile dengan mengetikkan command berikut *jika anda menggunakan command line
  </p>
  
  <p>
    <code>javac </code><code>DesToBin.java</code><br /> lalu jalankan / run dengan mengetikkan command berikut :<br /> <code>java </code>DesToBin<br /> <b>~ScreenShotz</b>
  </p>
  
  <div>
    <a href="https://justudin.com/files/uploads/2013/01/screenshot-1.png"><img alt="" src="https://justudin.com/files/uploads/2013/01/screenshot-1.png?w=300" width="400" height="125" border="0" /></a>
  </div>
  
  <p>
    <b><br /> </b><br /> Cukup sekian, semoga bermanfaat dan terimakasih dah mampir blog saya 😀
  </p>
</div>