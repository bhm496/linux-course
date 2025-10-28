H1 Viisikko

#x)Lue ja tiivistä

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

Ensin yritin tekoälyn avulla aktivoida kopiointi ominaisuuden Debiaaniin, vaikka olen yrittänyt monesti mutta ei onnistunut.Uskoisin että johtuisi Guest Addition  
CD image:sta, kun yritän kometoa  "sudo sh /media/cdrom/VBoxLinuxAdditions.run"  , se sanoo että ei voi avata koska tiedostoa ei löyty. Kuvassakin näkyy että Guest additions päivittämine ei onnistu ja se jää 77% kohdassa. 

<img width="854" height="353" alt="image" src="https://github.com/user-attachments/assets/d3fbf780-8ecb-4ca7-9a65-f06a6dde1755" />



Salt asennus sujui alussa hyvin mutta kun halusin testata "salt --version" se sanoi "-bash:salt:command not found".enkä päässyt eteenpäin ajamaan kometoja.

Ensin loin Saltrepo tiedostoa.
<img width="881" height="540" alt="image" src="https://github.com/user-attachments/assets/c39b1486-de80-4d1a-8616-958c48f58f79" />

Latasin kahta tiedostoa osoitteesta  https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/linux-deb.html
<img width="1004" height="579" alt="image" src="https://github.com/user-attachments/assets/2045d9c8-744c-451e-b89e-5fb9fcfe19f5" />

tutkitaan tiedostoa.  
<img width="648" height="840" alt="image" src="https://github.com/user-attachments/assets/bebb56e7-628f-4733-93c1-0a82718128ec" />

Tämä on PGP-julkinen avain. Se on ASCII-armor-muodossa, base64-muodossa.Helppo luettava. 
<img width="1003" height="304" alt="image" src="https://github.com/user-attachments/assets/7634704f-36a6-4cf6-b7db-cc6a248ad931" />

Tässä sanotaan, missä luotettavan PGP-julkissivuston on oltava, "Signed-By".
Se on sormenjälki, joka tunnistaa avaimen.
<img width="823" height="165" alt="image" src="https://github.com/user-attachments/assets/b53ed82d-13e1-4fa0-b52f-de6e4f29939e" />

Asennetaan repository eli arkistoa. Lisäämällä avaimen luotamme projektin. Yritin komentoa mutta se sanoi että sellaista tiedostoa ei ole olemassa. 

<img width="610" height="82" alt="image" src="https://github.com/user-attachments/assets/4a10e56e-10e2-4f73-bd29-f602037e6d4f" />

Tässä vaiheessa päivitetään ohjelmistot ja asennetaan salt-minion ja salt-master mutta se sanoi ettei se saa paketti paikantamaan. 
<img width="1004" height="258" alt="image" src="https://github.com/user-attachments/assets/60931526-0266-4231-9071-b6ae6a53b62d" />

Tässäkin näkyy että Saltin testin komennot eivät toimi eli seuraavien vaiheiden komennot eivät toimi. Yritin komennot kotihakemistossa ja saltrepossa. 

<img width="903" height="406" alt="image" src="https://github.com/user-attachments/assets/9a3fd42b-ebdf-4862-8879-ba35c0322acc" />

salt --version ei toimi, vaikka tein ohjeiden mukaisesti. Luulisin ongelman johtuen tallennusjärjestelmästä tai Debianista, ehkä olen vahingossa tehnyt virhettä asennusvaiheessa,tai Repo ei asentunut oikein. Jos jollain tavalla voisin Salt asentumaan koneelleni tai ehkä pitää tehdä Debianin asennus alusta uudelleen. 


#c) Viisi tärkeintä Saltin tilafunktiota Linuxissa pkg, file, service, user, cmd.
Saltin asennus ei vielä onnistunut, joten en saanut komentoja ajettua käytännössä.  
Alla kuitenkin esimerkit tärkeimmistä tilafunktioista ja niiden tarkoituksesta. 
Käytetty lähde: https://terokarvinen.com/2021/salt-run-command-locally/

1. pkg
pkg.installed` varmistaa, että tietty ohjelma on asennettu järjestelmään.
Asensin tree paketin komennolla
$ sudo salt-call --local -l info state.single pkg.installed tree


2. file
file.managed luo tai ylläpitää tiedoston tietyllä sisällöllä.
Luon tiedosto nimellä /tmp/helloworld, jonka sisältö on “Hello World!
Komennolla: $ sudo salt-call --local -l info state.single file.managed /tmp/helloworld contents='Hello World!


3.service
service.running varmistaa, että palvelu on käynnissä ja käynnistyy automaattisesti onnistuneesti kun asetukset on vaihdettu.
Komennolla: $ sudo salt-call --local -l info state.single service.running apache2 enable=True
Komento käynnistää Apache2-palvelun ja asettaa sen käynnistymään automaattisesti. 

4.user
user.present varmistaa että tietty käyttäjää on olemassa. 
Komennolla: $ sudo salt-call --local -l info state.single user.present name=robabe1

5.cmd
cmd.run ajaa komentorivikomennon. 
Komennolla: $ sudo salt-call --local -l info state.single cmd.run 'touch /tmp/foo' creates="/tmp/foo"
Komento luo tiedoston /tmp/foo.
creates-parametri tekee tästä idempotentin elitiedostoa ei luoda uudestaan.


#d) Esimerkki idempotenssista. Aja 'salt-call --local' komentoja

Idempotentti tarkoittaa että komennon lopputulokset ovat samat riippumatta siitä, ajetaanko se vain yhden vai useamman kerran eli uusi ajokerta ei tee mitään muutoksia. 
Komento: $ sudo salt-call --local state.single pkg.installed name=tree

Ensimmäinen ajo: ohjelman asennus

Toinen ajo: komennon toisto heti perään

Idempotenssin tarkoitus on se että tila pysyy samana, vaikka komento toistetaan.

En saanut tätä testattua käytännössä, koska Salt ei vielä toiminut koneellani.


Tarkistuslista:

x) Tehty

a) Tehty vaikka piti asentaa kahta kertaa debian 13

b) Kesken, ei onnistunut täysin, en saanut asentaa salt

c) Kesken, en pääse ajamaan tilafunktion komentoja kun en saanut salt-call --local toimimaan.

d) Kesken, täydennän kun saan salt toimimaan. 


Lähteet:

Salt asennus: https://terokarvinen.com/install-salt-on-debian-13-trixie/

Salt-call --local: https://terokarvinen.com/2021/salt-run-command-locally/

Salt Master ja Salt Slave: https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/

Raportin kirjoittamisen ohjeet: https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/

Debian 13 asennus virtuaalikoneelle: https://terokarvinen.com/2021/install-debian-on-virtualbox/

ChatGPT






















