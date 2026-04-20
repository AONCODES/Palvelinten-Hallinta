# H4

## Configuration Management of Distributed Systems over Unreliable and Hostile Networks
Tarkastelussa Teron tutkielman kohdat 4.12.1, 4.12.2 & 4.12.3.1. (Karvinen 2023, 112-117)

### 4.12.1
- Ensimmäisessä kohdassa Tero käy läpi konfiguraationhallintatyökaluja Salt ja Puppet sekä niiden DSL:ät (kieli joka tarkoitettu yhteen tarkoitukseen). Ansible kuuluu myös konfiguraationhallintaan.
- Saltilla on 510 toimintaa ja pohjana on jinja2 josta saadaan Ansiblen tapaan YAML-koodi josta edelleen muunnetaan tieto python-rakenteeksi.
- Puppetilla 113 toimintoa. Puppet ei hyödynnä yleisimpiä koodauskieliä (kuten python) vaan käyttää omia toimintojaan, määrittelee uudet resurssit ja niiden väliset yhteydet.

### 4.12.2
- Tässä kohdassa on analysoity kahta eri julkista puppet konfiguraatiota.
- Toistuvia komentoja molemmissa on esim file, package ja service. Määrällisesti näitä on käytetty todella paljon, vaikka muitakin toimintoja olisi.
- file package ja service on Ansiblestakin tuttuja, ohjelmia ladataan, tiedostoja muokkaillaan ja hallitaan sekä servicellä hallitaan esim. ohjelman käynnistymistä tai pysäytystä.

### 4.12.3.1
- Monella toiminnolla on riippåuvuksiaa kuten package, file ja service. Esim. service ei toimi ilman packagea (asenna Ansible).
- Kohdassa puhutaan myös idempotenssista joka on myös tullut tutuksi. Tällä tarkoiteaan sitä, että ohjelma voidaan ajaa niin monta kertaa kun halutaan, ja muutokset tulee vain kun niitä on tehty.


## mariadb asennus manuaalisesti
Tehtävänä oli asentaa jokin uusi demoni, valitsin tähän listalta mariadb tietokannan. Aluksi kun avasin virtuaalilinuxin päivitin niin, että kaikki syteemit ovat ajan tasalla. Tämän lisäksi asensin mariadb:n
```
sudo apt-get update
sudo apt-get install mariadb-server
```
Asennuksen jälkeen testasin tilanteen, joka näytti että ohjelma on active ja running, eli ei tarvinut tehdä `sudo systemctl start mariadb`, joka muuten olisi käynnistänyt ohjelman.

<img width="897" height="449" alt="Näyttökuva 2026-04-20 kello 16 34 01" src="https://github.com/user-attachments/assets/b4bdc5e8-386c-45de-8cda-ed3fc624ec07" />

Hieman hämmennyin, kun tuo mariadb.service teksti tulostui uudelleen ja uudelleen noin 20 kertaa. Ajoin status komennon uudelleen ja tällä kertaa ilmestyi vain kerran (?).



## Asennuksen automatisointi Ansiblella

## Asetus

## Idempotentti

## Lähteet

Karvinen, T. 2023. Configuration Management of Distributed Systems over
Unreliable and Hostile Networks. PhD Thesis. University of Westminster. Luettavissa: https://westminsterresearch.westminster.ac.uk/download/4cc417566aa9af60fe3826d690719e390abdb7a3c8672f3d51b1eb4ca75e7624/1427236/karvinen-2023-configuration-management-of-distributed-systems.pdf. Luettu 20.4.2026

https://terokarvinen.com/palvelinten-hallinta/#alustava-aikataulu

https://mariadb.com/docs/server/mariadb-quickstart-guides/installing-mariadb-server-guide



