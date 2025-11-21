# H5 Toimiva versio


# x) Lue ja tiivistä.

1.Chacon and Straub 2014

https://git-scm.com/book/en/v2 , https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F

  Git on ohjelma, jolla voi tallentaa omatyön eri versiot ja palata niihin myöhemmin.

  Git pitää kirjaa jokaisesta muutoksesta, kuka sen teki ja milloin, kuten loki. 

  Git mahdollistaa yhteistyön muiden kanssa.


---


2.Gitin käyttö on lähinnä 'git add . && git commit; git pull && git push'. Selitä tuon komennon jokainen osa. Käytä apuna itse valitsemiasi lähteitä ja viittaa niihin.

https://earthdatascience.org/workshops/intro-version-control-git/basic-git-commands/

https://www.atlassian.com/git/tutorials/syncing/git-pull#:~:text=The%20git%20pull%20command%20is,Git%2Dbased%20collaboration%20work%20flows.

  git add . : Lisää kaikki muuttuneet tiedostot.

  git commit: Tallentaa muutokset Gitin historiaan.

  git pull: Hakee palvelimelta uusimmat muutokset. Yhdistää ne omaan työhösi.

  git push: Lähettää omat tallennetut muutoksesi palvelimelle (esim. GitHubiin). Muutokset näkyvät sen jälkeen myös muille.


---

3.Varaston terokarvinen/suolax/ historia, eli loki ja muutokset. Kätevimmin komentokehotteesta 'git clone https://github.com/terokarvinen/suolax.git; cd suolax/; git log --patch --color|less -R'.

Wepistäkin saattaa onnistua kliksuttelemalla "Commits".

  Komennolla $git log --patch --color | less -R  nähdään: 

  kaikki tehdyt commitit

  kuka ne teki (nimi + sähköposti)

  milloin commit tehtiin

  mitä tiedostoihin on tarkalleen muutettu (rivit + - ja + merkinnät)

  Samaa voi katsoa GitHubissa kohdasta “Commits”.

---

# a) Online. 

Tee uusi varasto GitHubiin (tai Gitlabiin tai mihin vain vastaavaan palveluun). Varaston nimessä ja lyhyessä kuvauksessa tulee olla sana "snow". Aiemmin tehty varasto ei kelpaa. 
(Muista tehdä varastoon tiedostoja luomisvaiheessa, esim README.md ja GNU General Public License 3)

Loin Githubiin uusi repository nimellä snowflake ja siihen lisäsin README ja GNU License. 

<img width="740" height="714" alt="image" src="https://github.com/user-attachments/assets/ffbaef8e-f3fe-477d-92e4-d22a81ef7138" />


---

# b) Dolly. 

Kloonaa edellisessä kohdassa tehty uusi varasto itsellesi, tee muutoksia omalla koneella, puske ne palvelimelle, ja näytä, että ne ilmestyvät weppiliittymään.

Yritin kloonata ja muokata repo komentorivillä komennolla:

$git clone git@github.com:bhm496/snowflake.git

Siirsin repon hakemistoon komnnolla cd snowflake

Komennolla $nano README.md avasin tiedoston ja muokkasin sen ja tallensin.


Ajoin seuraavat komennot:
$git add . ,
$git commit  ,
$git pull  ,
$git push

Muutokset on tallennettu oikein. 

<img width="546" height="201" alt="image" src="https://github.com/user-attachments/assets/d88ac617-9706-4f64-a1e6-4190edf4dc5d" />

<img width="521" height="250" alt="image" src="https://github.com/user-attachments/assets/27212fa1-6a5a-4a9e-b658-e2ee4222ae1e" />

<img width="715" height="596" alt="image" src="https://github.com/user-attachments/assets/7e531b05-a1d8-491e-8ea9-29cd19a09714" />

---

# c) Doh!

Tee tyhmä muutos gittiin, älä tee commit:tia. Tuhoa huonot muutokset ‘git reset --hard’. Huomaa, että tässä toiminnossa ei ole peruutusnappia.

Avasin README.md tiedoston ja lisäsin sinne rivin. 

<img width="615" height="213" alt="image" src="https://github.com/user-attachments/assets/6e04cbb2-60f5-415e-8441-928d654c6595" />

Tarkistin että git on huomannut muutoksen komennolla $git status

Sitten peruin tehdyt muutokset komennolla $git reset --hard

Ajamalla uudelleen $git status varmistin että muutokset on peruttu. 

<img width="819" height="401" alt="image" src="https://github.com/user-attachments/assets/4e242ffe-7dd2-4daf-9c3a-edbfaf9a515c" />

---

# d) Tukki.

Tarkastele ja selitä varastosi lokia. Tarkista, että nimesi ja sähköpostiosoitteesi näkyy haluamallasi tavalla ja korjaa tarvittaessa.

Tarkistin ensin lyhyt commit loki

$git log --oneline --graph --decorate

Sitten ajoin $git log --patch , koko commit loki jossa näkyy tehdyt muutokset.  

<img width="858" height="829" alt="image" src="https://github.com/user-attachments/assets/606f0352-50ef-4cb0-99bd-2a99c51c34c6" />


Tarkistin myös nimi ja sähköpostini komennolla $git log , ja kaikki näytti oikein.

<img width="866" height="398" alt="image" src="https://github.com/user-attachments/assets/cc88f720-9d60-44fd-8e7a-d5452ea9f703" />

---

# e) Suolattu rakki. 

Aja Salt-tiloja omasta varastostasi. (Salt tiedostot mistä vain hakemistosta "--file-root teronSaltHakemisto". Esimerkiksi 'sudo salt-call --local --file-root srv/salt/ state.apply',
huomaa suhteellinen polku.)

Tein Salt tiedoston omaan repoosi 

Loin hakemiston Salt tilalle: $mkdir -p salt. 

Sitten loin tiedoston $nano salt/init.sls

Tiedostoon lisäsin:

/tmp/snowfile:
  file.managed:
    - contents: "Snow state toimii!"

<img width="445" height="113" alt="image" src="https://github.com/user-attachments/assets/0715659b-5143-4946-9309-283c8fcd0dda" />

Sitten ajoin Salt tila

$sudo salt-call --local --file-root . state.apply salt

Tarkistin myös sen sisällön

$cat /tmp/snowfile

<img width="979" height="581" alt="image" src="https://github.com/user-attachments/assets/b480a74b-f9b9-49d4-b066-a37523745849" />


---

Tarkistuslista:

-Komennot: add, commit, pull, push

-Loki näyttää commitit, tekijä ja muutokset

-Repo “snowflake”, README + GPLv3 luotu

-Kloonaus, tehty muutos ja push toiminta 

-Tyhmä muutos, reset , peruutettu muutos

-Loki, näyttää nimi ja sähköposti

-Salt-tila ajettu, tarkistus


Lähteet:

https://git-scm.com/book/en/v2

https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F

https://earthdatascience.org/workshops/intro-version-control-git/basic-git-commands/

https://www.atlassian.com/git/tutorials/syncing/git-pull#:~:text=The%20git%20pull%20command%20is,Git%2Dbased%20collaboration%20work%20flows.

annetut vinkit



















