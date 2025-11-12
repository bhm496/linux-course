#h4 Pkg-file-service


# x) Lue ja tiivistä.

Karvinen 2018: Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port

https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh

 -Salt automatisoi daemonien hallinnan kolmen hallintajärjestelmän avulla: Package-file-service

 -Asenna ohjelmisto, korvaa konfiguraatiotiedosto, Salt watcha sitä ja lopuksi käynnistä uudelleen daemon käyttääksesi uutta konfiguraatiota






# a) SSHouto. Lisää uusi portti, jossa SSHd kuuntelee.

-Jos käytät Vagrantia, muista jättää portti 22/tcp auki - se on oma yhteytesi koneeseen.

SSHd:n asetustiedostoon voi tehdä yksinkertaisesti kaksi "Port" riviä, molemmat portit avataan.


Ensin asensin SSH palvelinta komennoilla:

$sudo apt-get update
$sudo apt-get install ssh

<img width="707" height="527" alt="image" src="https://github.com/user-attachments/assets/4a687b27-58ad-43da-bb54-7ece64c09d18" />

Katsoin asetutstiedostoa $sudoedit /etc/ssh/sshd_config

Etsin #Port 22, se on nyt kommentoitu ja poistin # ja aktivoin portin ja lisäsin myös uusi port 1234 .Tällä portilla testataan SSH-yhteyden.

<img width="672" height="615" alt="image" src="https://github.com/user-attachments/assets/4278e20e-2e5e-4d66-9c27-b860efc639d8" />

Käynnistin palvelun uudelleen komennolla

$sudo systemctl restart ssh

ja testasin että SSH toimi

$sudo ss -tlnp | grep ssh. (testasin portti 1234 yhteyden)

Testasin myös $ssh -p 1234 robabe2@localhost

<img width="797" height="162" alt="image" src="https://github.com/user-attachments/assets/a4a20553-6482-4553-b497-01bbc9556a5c" />
<img width="857" height="290" alt="image" src="https://github.com/user-attachments/assets/b168cf6a-0aa2-408a-8631-f7aa37fa16ae" />



Muokkasin sshd_config tiedostoa ja poistin portti 1234

$sudo nano /etc/ssh/sshd_config

Käynnistin uudelleen

$sudo systemctl restart ssh

Tarkistin vielä että portti 1234 ei toimi

$nc -vz localhost 1234

<img width="681" height="432" alt="image" src="https://github.com/user-attachments/assets/3235b2dc-e5c9-4bbe-adf7-bcf22a82c5f7" />

<img width="585" height="91" alt="image" src="https://github.com/user-attachments/assets/9965bbae-6224-4152-8354-37153ebaf07e" />


Sitten automatisoin asetukset

Salt-tila tarkistin komennolla $sudo salt-call --local state.apply ssh

<img width="557" height="287" alt="image" src="https://github.com/user-attachments/assets/cf223d90-1d93-4374-bf57-73f0c8870d55" />

Lisäsin port22 ja port1234 Masterin asetustiedostoihin.

<img width="752" height="75" alt="image" src="https://github.com/user-attachments/assets/5116b2f1-cfbe-40a2-b13d-8765e821da7e" />

Tarkistin init.sls komennolla $sudo cat /srv/salt/ssh/init.sls

<img width="561" height="345" alt="image" src="https://github.com/user-attachments/assets/c8924f1f-1321-4d0e-aa5f-2ba5252df6ba" />

Ajoin Salt-tila 

$sudo salt-call --local state.apply ssh

<img width="843" height="723" alt="image" src="https://github.com/user-attachments/assets/1877ddc7-adae-4181-bd55-ccc3988057d6" />
<img width="702" height="717" alt="image" src="https://github.com/user-attachments/assets/04d66f20-8d8a-4add-b367-49e4c3591e43" />
<img width="733" height="671" alt="image" src="https://github.com/user-attachments/assets/3556ba9b-3b12-451d-96fc-1bdd3abc8eab" />

Tarkistin onnistumisen komennoilla

$sudo salt-call --local state.apply ssh

Tarkistin että portti 1234 nyt toimii

$sudo ss -tlnp | grep ssh

$nc -vz localhost 1234

$ssh -p 1234 robabe2@localhost "echo 'Nyt toimii!'"

<img width="807" height="128" alt="image" src="https://github.com/user-attachments/assets/758e361e-b283-4637-a91b-39975a4107d6" />

<img width="883" height="406" alt="image" src="https://github.com/user-attachments/assets/2e036f2e-1529-4c69-a072-007d3e993c06" />

<img width="805" height="62" alt="image" src="https://github.com/user-attachments/assets/4b0e8d45-4553-4970-921e-38ed9ff8a615" />




Tarkistuslista:

-Pkg-File-Service -malli toimii

-Paketin asennus onnstui

-Asetustiedoston hallinta käsin tehdyllä ja automaattisella

-Palvelun hallinta watch-toiminnolla

-Automaatio korjasi puutteen ilman käsin tekemistä

-Watch-toiminto käynnistää palvelun uudelleen automaattisesti























