---
id: 208
title: Life is experiences..
date: 2013-10-24T04:32:38+00:00
author: justudin
layout: post
guid: http://justudin.wordpress.com/?p=208
permalink: /life-is-experiences/
publicize_facebook_url:
  - https://facebook.com/100001042857820_680218165356272
  - https://facebook.com/100001042857820_680218165356272
publicize_twitter_user:
  - udinjust4u
  - udinjust4u
publicize_twitter_url:
  - http://t.co/V2jPRivGBz
  - http://t.co/V2jPRivGBz
publicize_linkedin_url:
  - 'http://www.linkedin.com/updates?discuss=&scope=127669681&stype=M&topic=5798999287828316160&type=U&a=E_aA'
  - 'http://www.linkedin.com/updates?discuss=&scope=127669681&stype=M&topic=5798999287828316160&type=U&a=E_aA'
categories:
  - Curhatan
tags:
  - oracle
  - query
  - rollback
  - update
---
Hai pembaca budiman, how are you? I hope God keep you safe! 😀

Kembali saya dalam  posting kali ini akan menuliskan sedikit &#8220;_pengalaman <del>suram</del>_&#8221; yang membuat saya sedikit pusing dan kecewa. #loh?

hehe ya pengalaman adalah guru yang paling berharga, namun saya sarankan setelah membaca postingan ini jangan sampai teman-teman mengalami apa  yang saya alami. Ya kalau pengen ngalamin sendiri juga gak pa pa dink :p. <!--more-->

Jadi gini ceritanya, baru saja saya ingin meng-_update _data yang ada di dalam database _oracle. _Data yang ingin saya ganti adalah data yang sebelumnya saya masukan untuk ujicoba (sample). Namun karena entah kenapa baru ngalamun atau galau eh ngetik sintaknya kurang lengkap udah saya run aja querynya.  Jadi kayak gini deh hasile.

[<img class="size-full wp-image-210 alignleft" alt="update sembrono" src="https://justudin.com/files/uploads/2013/10/update-sembrono.png" width="359" height="51" srcset="https://justudin.com/files/uploads/2013/10/update-sembrono-300x43.png 300w, https://justudin.com/files/uploads/2013/10/update-sembrono.png 359w" sizes="(max-width: 359px) 100vw, 359px" />](https://justudin.com/files/uploads/2013/10/update-sembrono.png)

&nbsp;

&nbsp;

**Bayangkan** ya data **6689 **berubah semua wis_nim nya jadi &#8216;**096500xx**&#8216;. OMG, what the h*ll I&#8217;m doing! This is not fake data, this is for real.

[<img alt="ss hasil update nglantur" src="https://justudin.com/files/uploads/2013/10/ss-hasil-update-nglantur.png" width="509" height="448" />](https://justudin.com/files/uploads/2013/10/ss-hasil-update-nglantur.png)

&nbsp;

Ya, langsung lemes deh, tapi tenang gak sampe pingsan kok :p . Relax! ya kuncinya adalah tenang, slow down. Hirup napas dalam-dalam  dan keluar kan pelan-pelan. Ya seperti di adegan film-film jenius langsung muncul lampu bolam tuing-tuing :D. Langsung deh nyari di mbah _google _buat ngembaliin data ke semula. Soalnya neh data uda dipakai buat pendaftaran wisuda tanggal 1 november. Yah langsung dapat deh di mbah google, ternyata di oracle ada fitur _rollback _apa itu maksudnya? gini singkat cerita fitur ini bisa mengembalikan data yang uda diubah sebelumnya tapi syaratnya datanya belum di-_commit._ Istilah apalagi itu, ya silahkan _search _di internet saja ya. Itung2 tambah pengetahuan :D. Tapi _**unfortunetly,** software _yang saya pakai langsung meng-_commit_ apa saja yang sudah di-_run._ Yah udah seneng data mau balik jadi down lagi deh. Kayak gini _rollback not make data sense_.

&nbsp;

Yah, 1 solusi not solved. Cari lagi sambil mikir-mikir. Akhirnya setelah buka-buka file Alhamdulillah ternyata kemarin saya sudah memback-up data tersebut. Langsung saja deh saya bikin table baru dengan nama berbeda dan saya isikan data-data tersebut. Setelah itu saya gunakan metode update untuk mengganti data di kolom wis\_nim doang, karena yang berubah cuma yang wis\_nim doang seh.

Dan ketemu solusi yang singkat querynya seperti ini :

<pre class="brush: plain; title: ; notranslate" title="">UPDATE WIS_SUDAH s SET s.WIS_NIM=(SELECT e.WIS_NIM FROM WIS_SUDAH_BACKUP e WHERE e.WIS_ID=s.WIS_ID);

</pre>

Jadi query tersebut cuma mengganti wis\_nim dengan wis\_nim yang ada di table back up-an, dengan syarat wis\_id table sebelumnya sama dengan wis\_id table back up-annya. Dan alhamdulillah it&#8217;s work. Seneng deh data kembali lagi, Horee! 😀

Pelajaran yang bisa diambil adalah :

  1. Teliti dan berhati-hatilah dalam melakukan sesuatu
  2. Jika sedang mengerjakan hal penting jangan sambil melamun or disambi dengan kerjaan lain
  3. Jika ada masalah yang terjadi, relax tenang dan pikirkan dengan hati jernih
  4. Cari solusi semaksimal mungkin, jika solusi A tidak bisa cari solusi B-Z
  5. Bersyukur dan Bersabar dalam setiap hal dalam kehidupan.

Cukup sekian semoga bermanfaat buat diri saya sendiri khususnya. Terimakasih sudah membaca coretan ini.