# H2
## Artikkelit
### Sudo without password
 - Artikkeli lähtee liikenteeseen uuden käyttäjän luonnilla ja uuteen ryhmään lisäämisellä.
    ```
    sudo adduser ansibaatu
    sudo groupadd sudoless
    sudo adduser ansibaatu sudoless
    ```
- Ohjeet ongelmatilannetta varten: sudo rikki, mitä teen? - Avaa uusi cmd ikkuna ja SSH-yhteys kohde palvelimeen ja vaihda root käyttäjäksi `sudo -i` (tällä tavoin voidaan mahdollisesti korjata rikki mennyt sudo).
  
- Sudoers sääntö lisätään **visudo**-tiedostoon, jossa annamme luvan sudoless ryhmän jäsenille luvan käyttää sudoa **ilman** salasanaa.

      sudo visudo /etc/sudoers.d/sudoless
      sudoless ALL = (ALL) NOPASSWD: ALL

- Lopuksi annetaan tärkeä vinkki: **TESTAA**. Vain testaamalla näet onnistuiko muutokset ja pystytkö käyttämään nyt sudoa ilman salasanaa. [Karvinen 2026](https://terokarvinen.com/passwordless-sudo/)

### xkcd 149: Sandwitch
- Mielenkiintoinen webbisivu, jossa koomisia lyhyt sarjakuvia. Mukaan lukien ajankonhtainen sudo vitsi.
- Sivusto on todella yksinkertainen ja aihealueina heidän sanojensa mukaan: romance, sarcasm, math & languange. [xkcd](https://xkcd.com/149/)

### Passwordless Sudo with Ansible
- Ansiblen avulla voidaan automatisoida mm. käyttäjien luonti sekä sudo asetukset, niin jokaisella koneella ei tarvitse erikseen tätä käsin tehdä.
  
- main.yml tiedostoon tulee huomattavasti enemmän tietoa automaatiota varten. Aikaisemmin main.yml tiedostossa oli vain copy osio (h1 teht), tässä ansiblen automaatio versiossa main.yml tiedosto sisältää lisäksi osiot: ryhmät, käyttäjät, avaimet. 
  
- Tällä tyylillä varsinkin typo virheitä tulee todella vähän (0?).
  
- Manuaalisen luonnin/harjoittelun ja **TESTauksen** jälkeen voi asetukset kopioida automaatiota varten.
  
- Kovakoodattuna nimi *Antero*, niin jos halutaan vaikka käyttäjä *Matti*, niin ei varmaan kovakoodata nimiä yml-tiedostoon? Sama koskee muita asetuksia (?). [Karvinen 2026](https://terokarvinen.com/passwordless-sudo-with-ansible/)

### Ansible-doc (sisäinen dokumentaatio)
- Ansiblen sisäistä dokumentaatiota pääsi näkemään suoraan linuxin komentoriviltä erinäisillä komennoilla esim.
  
    ```
    ansible-doc copy
    ansible-doc apt
    ansible-doc user
    ```
- Koodien takaa löytyy 'suht' selkeät ohjeet tai tiedot kustakin *Optionista*. Minulle vähän epäselkeää vielä, tekemällä oppinee nämäkin.
  
- Example osio mielestäni tärkeä, siitä hahmottaa kokonaisuden hieman selkeämmin (mitä kopioidaan, minne kopioidaan, kuka/mikä ryhmä omistaa **filen/directoryn** ja millä oikeuksilla): Esimerkkinä `ansible-doc copy`.
  
   <img width="409" height="148" alt="Näyttökuva 2026-04-06 kello 15 33 31" src="https://github.com/user-attachments/assets/dc87d7d5-a555-414c-b372-5a38597863ef" />


## Sudoless + User: ansibaatu
- Käyttäjän luon komennolla `sudo adduser <nimi>`, tämän jälkeen tulee muutamia kysymyksiä -> nimesin käyttäjän selvyyden vuoksi.

  <img width="480" height="222" alt="Näyttökuva 2026-04-06 kello 16 10 02" src="https://github.com/user-attachments/assets/0817c67a-ec99-4244-837a-be932329c603" />

- Käyttäjän tekemisen jälkeen luodaan sudoless ryhmä ja lisätään käyttäjä sinne.

  <img width="508" height="38" alt="Näyttökuva 2026-04-06 kello 16 10 53" src="https://github.com/user-attachments/assets/5c08f015-e3cf-4b56-b5f2-75a78984a468" />

- Avaan komentoriville uuden ikkunan ja kirjaudun `sudo -i` komennolla root käyttäjäksi ja siirryn takaisin 'normi' ikkunaan. Tällä tavoin voidaan välttää suurempia virheitä sudon rikkoutuessa.

  <img width="742" height="100" alt="Näyttökuva 2026-04-06 kello 16 29 42" src="https://github.com/user-attachments/assets/91d45a4d-e647-4f0b-8870-87b1a8781c1a" />

- Seuraavaksi lisätään uuden 'sudoers rule', tässä kohtaa hieman sekoilin ja lisäsin erinäisiä komentoja useaan paikkaan, koska en saanut aluksi toimimaan. Mitkä näistä voisi poistaa (?) Säännön tarkoitus oli siis poistaa sudon salasanan käyttö.
  
- Avaan visudon ja sudoers.d on ainakin tyhjä. Lisään kuitenkin komennon `%sudoless ALL = (ALL) NOPASSWD: ALL`.

  ```
  sudo visudo /etc/sudoers.d/sudoless
  ```

- Tämän lisäksi avaan pelkästään `sudo visudo` ja täältä löytyy enemmän tekstiä, lisään saman %sudoless komennon tänne sekä myös käyttäjälle erikseen saman komennon (koska ei aluksi toiminut).

  <img width="518" height="137" alt="Näyttökuva 2026-04-06 kello 16 39 46" src="https://github.com/user-attachments/assets/efce15f4-54eb-454a-9697-f918fa2bd704" />



Sudoless. Tee ansiblea varten tunnus, jolla voi käyttää sudoa ilman salasanaa. Sekä ssh-kirjautuminen että sudon käyttö tulee olla ansbilea varten automatisoitu.
b) Antero. Tee salasanaton, automaattisesti ssh:lla kirjautuva tunnus Ansiblella.

## Package
## File

## Lähteet
Karvinen, 2026. Palvelinten Hallinta. Luettavissa: https://terokarvinen.com/palvelinten-hallinta/#laksyt. Luettu: 

Karvinen, 2026. Sudo without password. Luettavissa: https://terokarvinen.com/passwordless-sudo/. Luettu: 

Munroe, 2006. xkcd. Luettavissa: https://xkcd.com/149/. Luettu: 

Karvinen, 2026. Passwordless sudo with ansible. Luettavissa: https://terokarvinen.com/passwordless-sudo-with-ansible/. Luettu: 
