---
title: '[Source Code] Program Java untuk konversi Desimal ke Biner'
author: justudin
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

​	Oke, kali ini saya mau share source code program konversi desimal ke biner..kebalikan dari posting saya sebelumnya tentang <a href="https://justudin.com/blog/source-code-program-java-untuk-konversi-biner-ke-desimal/">Program Java untuk konversi Biner ke desimal</a> ..<br /> Oke langsung saja silahkan copy source code berikut dan save dengan nama *.java

*Sesuaikan dengan nama Class, disini saya save dengan nama **DesToBin.java**

```java
import java.util.Scanner;

public class DesToBin {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int des, a;

		Konversi angka = new Konversi();

		Scanner input = new Scanner(System.in);

		System.out.print("Masukkan Angka : ");

		des = input.nextInt();

		System.out.println("Bilangan Desimalnya : " + des);

		System.out.print("Konversi Binernya : ");

		angka.desimalkebiner(des);

		System.out.println();

	}

}

class Konversi {

	public void desimalkebiner(int a) {

		if (a > 1) {

			desimalkebiner(a / 2);

		}

		System.out.print(a % 2);

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

Cukup sekian, semoga bermanfaat dan terimakasih dah mampir di blog saya 😀