# h2 Infraa koodina

x)Lue ja tiivistä.

1)Hello Salt Infra as code, https://terokarvinen.com/2024/hello-salt-infra-as-code/

-Salt luo yksinkertainen Infrastructure as Code (IaC) -tila, joka varmistaa tietyn tiedoston olemassaolon.

-Salt moduulin luonti ja  asetukset kirjoitetaa init.sls tiedostoihin.

-Idempotenssi, Salt luo puuttuvan tiedoston ensimmäisessä koodin ajamisessa, ja seuraavat ajot eivät tee enää muutoksia.

2)Salt contributors, https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml

Rules of YAML

-YAML on helppolukuinen tiedostomuoto, jota Salt käyttää.

-Rakenne perustuu avain–arvo-pareihin avain=arvo. 

-Parit merkitään kaksoispisteillä ja välilyönnillä

-Kommentit alkavat #-merkillä.

-välilyönnit, ei tabulaattoreit

YAML simple structure

-Skalaarit ovat yksinkertaiset "avain: arvo" -parit, joissa arvo voi olla luku, merkkijono tai totuusarvo

-Avain, lista arvoja, joista jokainen alkaa kahdella välilyönnillä ja yhdysviivalla ( -) omalla rivillään

-Sanakirjat, kokoelma avain-arvo-pareja ja listoja.

-Avaimia ja arvoja, listat alkavat - merkillä.

Lists and dictionaries - YAML block structures

-Sisennyksillä kaksi välilyöntiä on yleinen standardi

-Dictionary = avain ja arvo , List = useita arvoja

-Listat tai sanakirjat luodaan lohkorakenteina yhdysmerkin (- ) avulla.

3)Salt contributors: The top file, https://docs.saltproject.io/en/latest/ref/states/top.html, kohdat

Introduction

-Top File on Saltin keskeinen tiedosto, joka määrittää, mitkä määritykset kohdistetaan millekin palvelinryhmälle

-Tiedoston oletusnimi on top.sls, ja se sijoitetaan tilapuun (state tree) hakemistohierarkian "huipulle

-Tiedoston oletusnimi on top.sls, ja se sijoitetaan tilapuun hakemistohierarkian huipulle

A basic example

-Top File koostuu kolmesta pääkomponentista: Environment, tilatiedostot sisältävä hakemisto
  Ympäristöt sisältävät Kohderyhmiä.

  Target, Koneiden ryhmä , johon tietyt tilat on tarkoitus kohdistaa. 
  Kohderyhmät sisältävät Tilapisteitä.

  State files, lista varsinaisista määritystiedostoista, jotka suoritetaan kohderyhmän koneissa.


a) Hei infrakoodi!

Kokeile paikallisesti (esim 'sudo salt-call --local') infraa koodina. Kirjota sls-tiedosto, joka tekee esimerkkitiedoston /tmp/ -kansioon.

Päivitetään järjestelmä ja salt minion asennus

<img width="717" height="236" alt="image" src="https://github.com/user-attachments/assets/4e0e2f2d-b1c1-4a49-9594-1a2895cb6cb2" />

Loin uusi moduuli nimellä "hello". Moduulit asentavat, konfiguroivat ja käynnistävät jonkin ohjelman. 

Tässä /srv/salt/ on kansio, joka jaetaan kaikkien orjatietokoneiden kanssa.
Siirrytään kansiolle. 

<img width="587" height="36" alt="image" src="https://github.com/user-attachments/assets/c6375562-8b53-4d19-88a9-34e9d4f4e5ad" />

Pääsin muokkamaan tekstieditoriin komennolla $sudo salt-call --local state.apply hellotero ja sinne kirjoitin 

<img width="525" height="158" alt="image" src="https://github.com/user-attachments/assets/3a9386bc-602d-4332-9d96-eef0a9479d21" />

Testasin sen komennolla $ sudo salt-call --local state.apply hello

<img width="692" height="415" alt="image" src="https://github.com/user-attachments/assets/f02d239d-b304-4422-a837-f1ed162b3654" />

Katsoin että Salt on tehnyt työnsä oikein.

<img width="517" height="72" alt="image" src="https://github.com/user-attachments/assets/468cde10-3dce-41ac-9f16-d9ecbaa322b6" />


b) Toppping. 
Tee top-file, niin että kaikki omat tilasi ajetaan kerralla komennolla 'sudo salt-call --local state.apply'.

Komennolla $sudoedit /srv/salt/top.sls pääsen avamaan ja muokkamaan top.sls tiedostoa.
Tekstieditoriin kirjoitin base:
  '*':
    - hello
    
<img width="521" height="86" alt="image" src="https://github.com/user-attachments/assets/d41c608c-25f9-4f36-865d-e06cdd23f32f" />

Ajetaan nyt kaikki tilat komennolla $sudo salt-call --local state.apply

<img width="547" height="325" alt="image" src="https://github.com/user-attachments/assets/e5feabea-6864-4009-a7d6-9eebf5e753f1" />

c) Viisikko tiedostossa.
Tee erilliset esimerkit kustakin viidestä tärkeimmästä tilafunktiosta pkg, file, service, user, cmd. Kirjoita esimerkit omiksi tiloikseen /srv/salt/ alle, esim /srv/salt/hellopkg/init.sls.

Tein jokaiselle funktiolle oma kansio ja init.sls tiedosto.

1.pkg pakettien asennus, pkg.installed
Loin tiedosto hellopkg komennolla $sudo mkdir -p /srv/salt/hellopkg
Pääsin muokkamaan tiedostoa komennolla $sudo nano /srv/salt/hellopkg/init.sls
<img width="537" height="61" alt="image" src="https://github.com/user-attachments/assets/adb78b60-66cf-4c80-bd0c-daa36c94895d" />

Sen sisällä kirjoitin
<img width="527" height="72" alt="image" src="https://github.com/user-attachments/assets/9cf32ed3-ff23-4c7b-a645-0978fbacd67f" />

2.file, tiedosto olemassa, file.managed
loin tiedosto ja muokkasin sen komennolla 
<img width="581" height="37" alt="image" src="https://github.com/user-attachments/assets/8012ea01-2257-4f33-9471-b8f06715582a" />

Sisällöksi kirjoitin 
<img width="542" height="150" alt="image" src="https://github.com/user-attachments/assets/9188e4e4-8106-451e-9b88-fe71369502a1" />

3.Service, plavelu käynnissä, service.running
Loin tiedoston ja muokkasin sen komennoilla $sudo mkdir -p /srv/salt/helloservice ja $sudo nano /srv/salt/helloservice/init.sls

Valitsin apache2 koska sen piti olla asennettuna järjestelmään
<img width="550" height="96" alt="image" src="https://github.com/user-attachments/assets/600f4e89-942b-4cbc-b864-3f003abdddc5" />

4.user, käyttäjän hallinta, user.present
Ajoin komennot luodaaksen tiedoston ja muokkamaan sen $sudo mkdir -p /srv/salt/hellouser ja $sudo nano /srv/salt/hellouser/init.sls

Sen sisään kirjoitin
Tässä päätin luoda uuden käyttäjän kaveri, en halunnut varmistaa minun oman käyttäjän robabe2 olemassaolon.

<img width="542" height="82" alt="image" src="https://github.com/user-attachments/assets/247e66c6-f9cb-476c-8295-71f3a2a5d447" />


5.cdm, komentojen suoritus, cmd.run
Ajoin ensin $sudo mkdir -p /srv/salt/hellocmd ja sitten $sudo nano /srv/salt/hellocmd/init.sls
Tiedoston sisälle kirjoitin
<img width="558" height="77" alt="image" src="https://github.com/user-attachments/assets/21c02974-1c5e-430f-a08b-0ab3138b1233" />

Päivitin top.sls tiedoston sisältö ja kirjotin kaikki tilat komennolla $sudo nano /srv/salt/top.sls
Kun avasin tiedoston siinä oli 
<img width="131" height="57" alt="image" src="https://github.com/user-attachments/assets/cf6801d0-43db-49be-964c-459fa699e22a" />
ja lisäsin 
<img width="486" height="161" alt="image" src="https://github.com/user-attachments/assets/dbd50ed5-1ca1-418d-a49a-a23a92dfceff" />

Testasin kaikki tilat komennolla $sudo salt-call --local state.apply
<img width="678" height="532" alt="image" src="https://github.com/user-attachments/assets/5ac8593b-b2e1-4cbe-958e-fc6a70aa6d4a" />
<img width="480" height="522" alt="image" src="https://github.com/user-attachments/assets/e7a7e9ce-6f1e-4539-a2c6-1c4a23f7fc84" />
<img width="677" height="655" alt="image" src="https://github.com/user-attachments/assets/90254b7a-59f5-476e-b832-315cc6864456" />
<img width="242" height="125" alt="image" src="https://github.com/user-attachments/assets/78778958-9f70-4fc2-b1f5-43c191f6452d" />
Kaikki on kunnossa. 
Ajoin ja testasin yksittäisen tilan hellopkg
<img width="596" height="330" alt="image" src="https://github.com/user-attachments/assets/6e55f9f7-f358-44d8-92a0-e6f4ea9b88a0" />






















