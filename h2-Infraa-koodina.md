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

Pääsin muokkamaan tekstieditoriin komennolla sudo salt-call --local state.apply hellotero ja sinne kirjoitin 

<img width="525" height="158" alt="image" src="https://github.com/user-attachments/assets/3a9386bc-602d-4332-9d96-eef0a9479d21" />

Testasin sen komennolla $ sudo salt-call --local state.apply hello

<img width="692" height="415" alt="image" src="https://github.com/user-attachments/assets/f02d239d-b304-4422-a837-f1ed162b3654" />

Katsoin että Salt on tehnyt työnsä oikein.

<img width="517" height="72" alt="image" src="https://github.com/user-attachments/assets/468cde10-3dce-41ac-9f16-d9ecbaa322b6" />





















