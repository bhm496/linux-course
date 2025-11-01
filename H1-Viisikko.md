H1 Viisikko

#x) Lue ja tiivistä

Install Salt on Debian 13 Trixie
-Ohje miten asennetaan Salt Debian 13 käyttöjärjestelmään
-kahden tiedoston asennus suoraan salt sivulta 
-PGP julkinen avain
-salt-minion ja salt-master asennus apt install -komennolla

Run Salt Command Locally
-Salt Slave asennus
-Salt-call --local komennon käyttö ilman master 
-Saltin tilafunktiota pkg, file, service, user and cmd

Salt Quickstart
-Salt Master ja Slave 
-Salt Master antaa käskyjä ja hallinnoi konfiguraatioita ja Salt Slave suorittaa ne
Montako slave Salt master voi hallita? 

Raportin kirjoittaminen
-Raportin tulee olla tarkka, perusteltuna hyvin ja helppolukuinen
-Viittaa lähteisin
-Vaiheiden perustelu eli mitä teit ja mitä tapahtui
-Miten liitän kuvakaappauksia raporttiin? 

#a) Asenna Debian 13-Trixie virtuaalikoneeseen. 
Asennus onnistui.

<img width="512" height="246" alt="image" src="https://github.com/user-attachments/assets/8f272934-571b-4017-92b7-3115432d8516" />


#b) Asenna Salt

Ensin päivitin järjestelmän ja  loin Saltrepo tiedostoa.

<img width="841" height="346" alt="image" src="https://github.com/user-attachments/assets/9e3d0ab2-4e33-4a0e-93bc-50d6e556a2eb" />


Latasin kahta tiedostoa osoitteesta  https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/linux-deb.html

<img width="903" height="356" alt="image" src="https://github.com/user-attachments/assets/c070073d-43a5-4ab3-ad90-4d9f8676d1c5" />


<img width="1185" height="638" alt="image" src="https://github.com/user-attachments/assets/9d3c05c7-44a8-4dae-ac9d-4479216d106e" />


Tutkitaan tiedostoa.  

<img width="740" height="534" alt="image" src="https://github.com/user-attachments/assets/4002bdcc-1562-42df-a21e-82c8c0610582" />



Tämä on PGP-julkinen avain. Se on ASCII-armor-muodossa, base64-muodossa.Helppo luettava. 

<img width="832" height="287" alt="image" src="https://github.com/user-attachments/assets/a23f42c1-1ba4-4b7d-a089-eee4bf897cbd" />


Tässä sanotaan, missä luotettavan PGP-julkissivuston on oltava, "Signed-By".
Se on sormenjälki, joka tunnistaa avaimen.
<img width="742" height="102" alt="image" src="https://github.com/user-attachments/assets/435316c1-e737-4d05-80e2-a0647b28d960" />


Asennetaan repository eli arkistoa. Lisäämällä avaimen luotamme projektin. 

Komennoilla: $ sudo cp public /etc/apt/keyrings/salt-archive-keyring.pgp
$ sudo cp salt.sources /etc/apt/sources.list.d/


<img width="1004" height="258" alt="image" src="https://github.com/user-attachments/assets/60931526-0266-4231-9071-b6ae6a53b62d" />

Päivitetään ja asennetaan Salt-minion ja Salt master komennoilla  $ sudo apt-get update
$ sudo apt-get install salt-minion salt-master

Tässäkin näkyy että Saltin testin komennot 

<img width="533" height="45" alt="image" src="https://github.com/user-attachments/assets/f06e684d-e896-4852-9101-6972403d7a3f" />

Seuraava komento  $sudo salt-call --local state.single file.managed /tmp/hellotero luo  /tmp/hellotero tiedoston olemassaolon ja oikeudet ja raportoi onnistumisesta.


<img width="926" height="376" alt="image" src="https://github.com/user-attachments/assets/c1a48132-d22d-4d54-a590-239db212dd82" />


Testataa vielä


<img width="441" height="42" alt="image" src="https://github.com/user-attachments/assets/514de3c3-f6cf-44ab-a443-8b9bf44fafba" />




#c) Viisi tärkeintä Saltin tilafunktiota Linuxissa pkg, file, service, user, cmd.
 

Alla kuitenkin esimerkit tärkeimmistä tilafunktioista ja niiden tarkoituksesta. 

Käytetty lähde: https://terokarvinen.com/2021/salt-run-command-locally/


1.pkg
   
pkg.installed` varmistaa, että tietty ohjelma on asennettu järjestelmään.

Asensin tree paketin komennolla
$ sudo salt-call --local -l info state.single pkg.installed tree

<img width="748" height="452" alt="image" src="https://github.com/user-attachments/assets/a92cb7f3-63b5-49fe-9797-34534ffe993b" />

Kuvan mukaisesti komento asensi tree koneelle Saltin kautta, ilman masteria, ja näytä tarkat tiedot siitä, mitä on tehty. 


2.file

file.managed luo tai ylläpitää tiedoston tietyllä sisällöllä.

Luon tiedosto nimellä /tmp/helloworld, jonka sisältö on “Hello World!

Komennolla: $ sudo salt-call --local -l info state.single file.managed /tmp/helloworld contents='Hello World!

<img width="975" height="563" alt="image" src="https://github.com/user-attachments/assets/9bf20ac8-3a00-498b-82d8-1e293754759e" />

Komennolla cat /tmp/helloworld sain nähdä sen sisällön. 


3.service

service.running varmistaa, että palvelu on käynnissä ja käynnistyy automaattisesti onnistuneesti kun asetukset on vaihdettu.

Asensin ensin Apache2

<img width="820" height="576" alt="image" src="https://github.com/user-attachments/assets/3997b228-c6c6-49bc-af07-b81bb9f39bee" />


Komennolla: $ sudo salt-call --local -l info state.single service.running apache2 enable=True

Komento käynnistää Apache2-palvelun ja asettaa sen käynnistymään automaattisesti. 

<img width="922" height="506" alt="image" src="https://github.com/user-attachments/assets/65ef6ce4-6b2a-47c3-8273-2b2dbbdae86b" />


4.user

user.present varmistaa että tietty käyttäjää on olemassa.

Komennolla: $ sudo salt-call --local -l info state.single user.present name=robabe2

<img width="725" height="468" alt="image" src="https://github.com/user-attachments/assets/61f28135-4a4c-496b-aca2-ddef034edee8" />

Käyttäjä robabe2 on jo Debian järjestelmässä.


5.cmd

cmd.run ajaa komentorivikomennon. 

Komennolla: $ sudo salt-call --local -l info state.single cmd.run 'touch /tmp/foo' creates="/tmp/foo"

Komento luo tiedoston /tmp/foo.

creates-parametri tekee tästä idempotentin elitiedostoa ei luoda uudestaan.

<img width="795" height="597" alt="image" src="https://github.com/user-attachments/assets/b52e94b8-d074-4a3a-a0c4-8d3e0a937851" />




#d) Esimerkki idempotenssista. Aja 'salt-call --local' komentoja

Idempotentti tarkoittaa että komennon lopputulokset ovat samat riippumatta siitä, ajetaanko se vain yhden vai useamman kerran eli uusi ajokerta ei tee mitään muutoksia.

Komento: $ sudo salt-call --local state.single pkg.installed name=tree

Ensimmäinen ajo: ohjelman asennus

Toinen ajo: komennon toisto heti perään

<img width="750" height="647" alt="image" src="https://github.com/user-attachments/assets/f5ae80fd-c2c2-43be-8411-8c3fc04d6337" />


Idempotenssin tarkoitus on se että tila pysyy samana, vaikka komento toistetaan.



Tarkistuslista:

x) Tehty

a) Tehty vaikka piti asentaa kahta kertaa debian 13

b) Kesken, ei onnistunut täysin, en saanut asentaa salt

c) Tehty.

d) Tehty.


Lähteet:

Salt asennus: https://terokarvinen.com/install-salt-on-debian-13-trixie/

Salt-call --local: https://terokarvinen.com/2021/salt-run-command-locally/

Salt Master ja Salt Slave: https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/

Raportin kirjoittamisen ohjeet: https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/

Debian 13 asennus virtuaalikoneelle: https://terokarvinen.com/2021/install-debian-on-virtualbox/

ChatGPT






















