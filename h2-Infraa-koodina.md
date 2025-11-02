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


























