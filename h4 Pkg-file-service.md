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

Käynnistin palvelun uudelleen komennolla $sudo systemctl restart ssh
ja testasin että SSH toimi $sudo ss -tlnp | grep ssh. (testasin portti 1234 yhteyden)

Testasin myös $ssh -p 1234 robabe2@localhost

<img width="797" height="162" alt="image" src="https://github.com/user-attachments/assets/a4a20553-6482-4553-b497-01bbc9556a5c" />
<img width="857" height="290" alt="image" src="https://github.com/user-attachments/assets/b168cf6a-0aa2-408a-8631-f7aa37fa16ae" />

Sitten automatisoidaan asetukset






























