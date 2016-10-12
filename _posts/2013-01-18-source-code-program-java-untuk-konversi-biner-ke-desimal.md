---
id: 40
title: '[source code] Program Java untuk konversi Biner ke Desimal'
date: 2013-01-18T14:31:10+00:00
author: justudin
layout: post
guid: http://justudin.wordpress.com/?p=40
permalink: /source-code-program-java-untuk-konversi-biner-ke-desimal/
categories:
  - Tutorial
tags:
  - biner
  - java
  - konversi
  - Tutorial
---
Oke, kali ini saya mau share source code program konversi biner ke desimal..
  
silahkan copy source code berikut dan save dengan nama **BinaryToDecimal.java**
  
*****Nama harus sama dengan nama Class..

<!--more-->

<pre class="brush: java; title: ; notranslate" title="">import java.lang.*;
import java.io.*;

public class BinaryToDecimal {
   public static void main ( String [] args ) throws IOException {
     BufferedReader bf= new BufferedReader ( new InputStreamReader ( System.in )) ;
     System.out.print ( &quot;Masukan Bilangan Binernya = &quot; ) ;
     String str = bf.readLine () ;
     long num = Long.parseLong ( str ) ;
     long rem;
     while ( num &gt; 0 ){
       rem = num % 10 ;
       num = num / 10 ;
       if ( rem != 0 &amp;&amp; rem != 1 ){
         System.out.println ( &quot;Ini bukan bilangan biner.&quot; ) ;
         System.out.println ( &quot;Silahkan Coba lagi&quot; ) ;
         System.exit ( 0 ) ;
       }
     }
     int i= Integer.parseInt ( str, 2 ) ;
     System.out.println ( &quot;Desimalnya : &quot; + i ) ;
   }
}

</pre>

dan compile dengan mengetikkan di CMD untuk pengguna windows atau TERMINAL untuk pengguna Linux ubuntu
  
`javac BinaryToDecimal.java`
  
dan jalakan dengan mengetikkan
  
`java BinaryToDecimal`

#ScreenShotznya

<div>
</div>

<div>
  <a href="https://justudin.com/files/uploads/2013/01/screenshot-11.png"><img alt="" src="https://justudin.com/files/uploads/2013/01/screenshot-11.png?w=300" width="400" height="125" border="0" /></a>
</div>

Oke, Sekian..
  
Semoga bermanfaat..