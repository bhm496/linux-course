h3 Soitto kotiin

x)Lue ja tiivistä. 

1.Karvinen 2021, 
https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/

-Vargant Virtuabox asennus
-Tehdään kaksi virtuaalikonetta Vargantin avulla
-Koneet ovat yhdistettynä verkkoon ja kommunikoivat yhdessä
-Helppo ja nopea poistaa virtuaalikonetta

2.Karvinen 2018, 
https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux

-Salt Master ja Salt Slave asennus
-Master kertoo, mitä tehtäviä minionien pitää tehdä.
-Salt asentamiseen tarvitaan repository package

3.Karvinen 2023, 
https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file

-Infra as Code, Your wishes as a text file
    -Palvelinten asetukset kirjoitetaan tekstitiedostoihin
-top.sls - What Slave Runs What States
    -Tiedostossa määritetään mitä tehtäviä jokainen slave tekee


a)Hello Vagrant! 

Osoita jollain komennolla, että Vagrant on asennettu (esim tulostaa vagrantin versionumeron). 
Jos et ole vielä asentanut niitä, raportoi myös Vagrant ja VirtualBox asennukset. (Jos Vagrant ja VirtualBox on jo asennettu, niiden asennusta ei tarvitse tehdä eikä raportoida uudelleen.)
Kokeilin komennolla $vagrant --version että onko minulla sen asennettua mutta järjestelmä ei löytänyt sitä.
Latasin Vagrant amd64 osoitteesta: https://developer.hashicorp.com/vagrant/install

Sitten ajoin uudestaan komento vagrant --version ja sain 
<img width="401" height="47" alt="image" src="https://github.com/user-attachments/assets/3cb209b0-bf40-4f4c-a169-5c08de38207f" />

Ajoin seuraavat komennot cmd:llä 

mkdir testi-vagrant  , Luo kansion, johon Vagrant-projekti tallennetaan
cd testi-vagrant  , Siirtyy siihen kansioon
vagrant init debian/bookworm64  , Luo tiedoston Vagrantfile, joka kertoo millainen virtuaalikone tehdään
vagrant up  , Käynnistää Vagrantin ohjaaman virtuaalikoneen (VirtualBoxiin ilmestyy Debian)

<img width="787" height="227" alt="image" src="https://github.com/user-attachments/assets/c7862d8a-f74e-41a2-baec-5567f902b9ce" />
<img width="1688" height="927" alt="image" src="https://github.com/user-attachments/assets/a7bda1eb-ceec-4116-809f-9959c968ae53" />
<img width="1145" height="638" alt="image" src="https://github.com/user-attachments/assets/be1f2c50-a3df-4162-b89b-fb7b5dca1b00" />

Pääsin Vagrant sisälle vagrant ssh

Ajoin seuraavat komennot
sudo apt update      , päivittää pakettien tiedot
sudo apt install vim   , asentaa testiksi ohjelman (vim on tekstieditori)
hostname -I    ,  näyttää virtuaalikoneen IP-osoitteen

<img width="1118" height="922" alt="image" src="https://github.com/user-attachments/assets/9cdb4d79-0f42-4c8b-9cd0-1fd2f62f9290" />
<img width="1395" height="911" alt="image" src="https://github.com/user-attachments/assets/dc9f83ae-0228-49af-81e3-7a2841727e9f" />
<img width="1162" height="271" alt="image" src="https://github.com/user-attachments/assets/64df7a41-0267-4995-801f-c7cb42bc7a44" />

Katsoin myös ip osoitteen

<img width="1197" height="371" alt="image" src="https://github.com/user-attachments/assets/1f188d2c-0dce-4529-b0cb-29843e17cd7e" />

Komennolla exit pääsin pois Vargant sisältä.
En ole varma pitääkö poista vagrant vai ei.











