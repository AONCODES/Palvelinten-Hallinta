# h1 Hei Ansiblen maailma
Aloitin tehtävän palauttelemalla muistiin linuxin ja virtuaalikoneen käyttöä. Muistin että olin luonut keygenillä avaimet syksyllä, mutta en silti päässyt SSH yhteydellä localhostiin ilman sudo salasanaa. Tämä ongelma ratkesi `ssh-copy-id aatu1@localhost` komennolla. 

Teron artikkeli SSH public key - Login without password (2026) käsittelikin juuri tuota aihetta:
- SSH Yleisin/johtava ja turvallinen kirjautumis ratkaisu palvelimille
- Käytetään monessa tuotteessa, nopeuttaa myös toimintaa kun ei tarvitse salasanalla kirjautua joka kerta

Toinen artikkeli Hello Ansible (2026) käsitteli nimensä mukaisesti ansiblea, ohjeita kuinka se ladataan ja mitä sillä voidaan tehdä. Artikkelin perusteella seuraavassa kappaleessa esittelen konkreettisia esimerkkejä.

## SSH kirjautumisen automatisointi

Automatisoin aluksi SSH kirjautumisen, kuten ylempänäkin mainittu niin en saanut aluksi toimimaan vaikka `ssh-keygen` komennolla olin luonut avainparin. Tämä ongelma poistui kokonaan tuolla `ssh-copy-id localhost` komennolla.

## Ansible

Latasin ansiblen `sudo apt-get install ansible`, hetken aikaa kun Linux lataili niin lataus oli ilmeisesti onnistunut. Tein ohjeiden mukaisesti kansion ansiblesjoka toimii työkansiona tässä tehtävässä (ainakin). Tämän jälkeen loin tiedoston hosts.ini ja lisäsin localhostin sinne, lisäksi ryhmän [web]. Tänne pystyisi lisäämään useampia hosteja mitä haluttaisiin kontrolloida sekä muitakin ryhmiä esim tietokantoja.

<img width="162" height="33" alt="Näyttökuva 2026-03-30 kello 19 47 54" src="https://github.com/user-attachments/assets/f5e1da8e-2e8c-4450-9b8c-f0b9db18f0dc" />


Testasin toimintaa ja näyttäisi toimivan, poislukien jonkinlainen Python [warning]
<img width="733" height="144" alt="Näyttökuva 2026-03-30 kello 19 52 31" src="https://github.com/user-attachments/assets/a015779d-8e2b-4cf1-bd23-c77fddeeb34b" />


hosts.ini tiedostoon lisäsin pohjalle kuvassa näkyvän komennn, jolla sai Python varoituksen poistumaan. 

<img width="438" height="109" alt="Näyttökuva 2026-03-30 kello 19 55 22" src="https://github.com/user-attachments/assets/547d9ef4-9fa8-482f-9f37-84f88f04443e" />








## Lähteet
Karvinen 2026. Palvelinten Hallinta. Luettavissa: https://terokarvinen.com/palvelinten-hallinta/#laksyt. Luettu 26.3.2026.

Karvinen 2026. Hello Ansible. Luettavissa: https://terokarvinen.com/hello-ansible/. Luettu 30.3.2026.

Karvinen 2026. SSH public key - Login without password. Luettavissa: https://terokarvinen.com/ssh-public-key-login-without-password/. Luettu 30.3.2026.

Karvinen 2023. Create a Web Page Using Github. Luettavissa: https://terokarvinen.com/2023/create-a-web-page-using-github/. Luettu 26.3.2026.
