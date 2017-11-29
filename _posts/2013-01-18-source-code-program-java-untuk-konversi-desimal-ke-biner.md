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

​	Oke, kali ini saya mau share source code program konversi desimal ke biner..kebalikan dari posting saya sebelumnya tentang <a href="http://udin-just4u.blogspot.com/2011/04/share-program-java-untuk-konversi-biner.html">Program Java untuk konversi Biner ke desimal</a> ..<br /> Oke langsung saja silahkan copy source code berikut dan save dengan nama *.java

*Sesuaikan dengan nama Class, disini saya save dengan nama **DesToBin.java**

```java
import java.util.Scanner;

class Konversi{

public void desimalkebiner(int a){

if (a>1) {

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

System.out.print("Masukkan Angka : ");

des = input.nextInt();

System.out.println("Bilangan Desimalnya : "+des);

System.out.print("Konversi Binernya : ");

angka.desimalkebiner(des);

System.out.println();

}

}
```



Lalu compile dengan mengetikkan command berikut *jika anda menggunakan command line


```bash
javac DesToBin.java
```

lalu jalankan / run dengan mengetikkan command berikut :

```bash 
java DesToBin
```

~ScreenShotz

<img alt="" src="https://justudin.com/files/uploads/2013/01/screenshot-1.png?w=300" width="400" height="125" border="0" />



Cukup sekian, semoga bermanfaat dan terimakasih dah mampir blog saya 😀