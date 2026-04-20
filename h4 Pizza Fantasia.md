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


## Asennuksen automatisointi Ansiblella

## Asetus

## Idempotentti

## Lähteet

Karvinen, T. 2023. Configuration Management of Distributed Systems over
Unreliable and Hostile Networks. PhD Thesis. University of Westminster. Luettavissa: https://westminsterresearch.westminster.ac.uk/download/4cc417566aa9af60fe3826d690719e390abdb7a3c8672f3d51b1eb4ca75e7624/1427236/karvinen-2023-configuration-management-of-distributed-systems.pdf. Luettu 20.4.2026

https://terokarvinen.com/palvelinten-hallinta/#alustava-aikataulu

