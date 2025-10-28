H1 Viisikko

x)

Install Salt on Debian 13 Trixie
-Ohje miten asennetaan Salt Debian 13 käyttöjärjestelmään
-kahden tiedoston asennus suoraan salt sivulta 
-PGP julkinen avain

Run Salt Command Locally
-Salt Slave asennus
-Salt-call --local komennon käyttö
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

a) Asenna Debian 13-Trixie virtuaalikoneeseen. 

b) Asenna Salt
Ensin yritin tekoälyn avulla aktivoida kopiointi ominaisuuden Debiaaniin, vaikka olen yrittänyt monesti mutta ei onnistunut.Uskoisin että johtuisi Guest Addition  
CD image:sta, kun yritän kometoa  "sudo sh /media/cdrom/VBoxLinuxAdditions.run"  , se sanoo että ei voi avata koska tiedostoa ei löyty.

Salt asennus sujui alussa hyvin mutta kun halusin testata "salt --version" se sanoi "-bash:salt:command not found".enkä päässyt eteenpäin ajamaan kometoja.

c) Viisi tärkeintä Saltin tilafunktiota Linuxissa pkg, file, service, user, cmd.


d) Esimerkki idempotenssista. Aja 'salt-call --local' komentoja
Idempotentti on metodi, jossa sen vaikutukset ovat samat riippumatta siitä, suoritetaanko se vain yhden vai useamman kerran eli uusi ajokerta ei tee mitään muutoksia. 


Tarkistuslista:
x) Tehty
a) Tehty vaikka piti asentaa kahta kerta debian 13
b) Kesken, ei onnistunut täysin, salt --version komennon jälkeen en päässyt eteenpäin
c) Kesken, en pääse ajamaan tilafunktion komentoja kun en saanut salt-call --local toimimaan
d) Kesken, täydennän kun saan salt toimimaan. 






















