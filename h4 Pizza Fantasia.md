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


## mariadb asennus
Tehtävänä oli asentaa jokin uusi demoni, valitsin tähän listalta mariadb tietokantajärjestelmän. Aluksi kun avasin virtuaalilinuxin päivitin niin, että kaikki syteemit ovat ajan tasalla. Tämän lisäksi asensin mariadb:n
```
sudo apt-get update
sudo apt-get install mariadb-server
```
Asennuksen jälkeen testasin tilanteen, joka näytti että ohjelma on active ja running, eli ei tarvinnut tehdä `sudo systemctl start mariadb`, joka muuten olisi käynnistänyt ohjelman.

<img width="897" height="449" alt="Näyttökuva 2026-04-20 kello 16 34 01" src="https://github.com/user-attachments/assets/b4bdc5e8-386c-45de-8cda-ed3fc624ec07" />
<br></br>
Hieman hämmennyin, kun tuo mariadb.service teksti tulostui uudelleen ja uudelleen noin 20 kertaa. Ajoin status komennon toistamiseen ja tällä kertaa tiedot tulostui vain kerran (?).



## Asennuksen automatisointi Ansiblella

Aluksi ansibles "puu" näytti tältä:

<img width="351" height="427" alt="Näyttökuva 2026-04-20 kello 16 50 03" src="https://github.com/user-attachments/assets/3ebef84f-e297-4325-a8b4-2fb6256f15b6" /><br></br>

Uuteen main.yml tiedostoon lisäsin asennukseen tarvittavat tiedot. apt = lataa, name = mariadb-server, state = present (eli ladataan jos ei ole jo ladattu).

<img width="544" height="58" alt="Näyttökuva 2026-04-20 kello 16 50 33" src="https://github.com/user-attachments/assets/7763da63-6165-4d4d-937e-f68f31506d69" /> 

<img width="517" height="75" alt="Näyttökuva 2026-04-20 kello 16 58 25" src="https://github.com/user-attachments/assets/9f461e90-45cb-4725-acab-c7d5d1ce3217" /> <br></br>

Tämän jälkeen lisäsin uuden roolin site.yml:iin ja ajoin playbookin:

<img width="938" height="355" alt="Näyttökuva 2026-04-20 kello 17 01 41" src="https://github.com/user-attachments/assets/e0d85f89-b981-4939-b337-5063a31893cb" /> <br></br>

Virheilmoitus koski nginx:n starttausta. Tarkistin apachen ja nginx:n statukset.

<img width="931" height="305" alt="Näyttökuva 2026-04-20 kello 17 03 21" src="https://github.com/user-attachments/assets/15273f62-90d3-4a87-ac3c-b88ef254bef9" /> <br></br>

Tein ehkä helpon ratkaisun ja poistin site.ymlista nginx:n roolin. Oliko ongelma se että apache on käynnissä? Tämän jälkeen playbook meni läpi.

<img width="941" height="73" alt="Näyttökuva 2026-04-20 kello 17 06 01" src="https://github.com/user-attachments/assets/9f6874e9-e194-4e91-80b0-b003b131d5b7" /> <br></br>

PÄIVITYS:
Lisäsin vielä update_cachen päivittämään sekä servicen käynnistämään tietokannan myös buutatessa.

<img width="300" height="187" alt="Näyttökuva 2026-04-20 kello 17 50 25" src="https://github.com/user-attachments/assets/0629ee8d-5675-438e-a8cd-becfeedfe24b" /> <br></br>

Ajoin playbookin.

<img width="985" height="257" alt="Näyttökuva 2026-04-20 kello 17 51 08" src="https://github.com/user-attachments/assets/c47c6bf9-09de-493b-8924-efa84e11d3a1" /> <br></br>

Erroria hmm.. Kysäisin googlelta ja vastaukseni tuli heti, että nimi on mariadb, tuo maridb-service on vain apt:issa. Testailin uudestaan ja nyt toimi.

<img width="986" height="174" alt="Näyttökuva 2026-04-20 kello 17 54 24" src="https://github.com/user-attachments/assets/1f96093d-d9d9-4de3-9ae6-2be2b15decfd" />


## Asetus
## Idempotentti

## Lähteet

Karvinen, T. 2023. Configuration Management of Distributed Systems over
Unreliable and Hostile Networks. PhD Thesis. University of Westminster. Luettavissa: https://westminsterresearch.westminster.ac.uk/download/4cc417566aa9af60fe3826d690719e390abdb7a3c8672f3d51b1eb4ca75e7624/1427236/karvinen-2023-configuration-management-of-distributed-systems.pdf. Luettu 20.4.2026

https://terokarvinen.com/palvelinten-hallinta/#alustava-aikataulu

https://mariadb.com/docs/server/mariadb-quickstart-guides/installing-mariadb-server-guide



