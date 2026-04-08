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


## Sudoless
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

- Tämän jälkeen taas testailen ja näyttäisi toimivan.

  <img width="703" height="256" alt="Näyttökuva 2026-04-06 kello 16 42 21" src="https://github.com/user-attachments/assets/b6d7a333-bf77-4725-9f09-3a2256f3b1e5" />

- Lopuksi vielä poistan salasanan kysymisen ssh-kirjautumiseen:

   ```
   ssh-copy-id ansibaatu@localhost
   ```



  <img width="713" height="236" alt="Näyttökuva 2026-04-06 kello 16 46 19" src="https://github.com/user-attachments/assets/52cd1381-0a04-4ca1-8f2c-bf3129d99dd6" />

## ansibaatu

Tehdään salasanaton, automaattisesti SSH:lla kirjautuvas tunnus Ansiblella. Aikaisemmassa kohdassa automatisoitiin sudo ja ssh ilman salasanaa, lisäksi h1 tehtävässä on asennettu ansible ja tehty tarvittavat konfiguraatiot siihen.

1. Ensiksi loin uudet directoryt /roles/ansibaatu/tasks ja sinne main.yml tiedoston. Loin ansibaatu ja tasksin erikseen komennolla `mkdir ansibaatu` ja siirryin ansibaatuun ja siellä taas `mkdir tasks`.
   
2. main.yml tiedostoon täytin tarvittavia tietoja:
   - Luodaan ryhmä: sudoless (state:present eli luodaan jos ei ole jo olemassa) (vastaa `groupadd sudoless` komentoa)
   - Luodaan käyttäjä: ansibaatu (tässä myös state:present).
   - Lisätään käyttäjä ryhmiin sudoless, sudo ja adm
   - Lisää ssh-avaimen käyttäjälle (**kirjaudu ilman salasanaa**)
   - Copy kohdassa luodaan tiedosto ja määrittää sille sisällön
   - Copy kohdasa annetaan sudo-oikeudet ilman salasanaa tässä tehvässä.
     <br>

   <img width="722" height="320" alt="Näyttökuva 2026-04-06 kello 20 04 39" src="https://github.com/user-attachments/assets/ee0a366d-2bca-4d01-b2af-8e78f4d2732f" />

3. Lisätään site.yml tiedostoon hostin alapuolelle kohda `become: true`, sekä rooli **ansibaatu**. 

   <img width="217" height="116" alt="Näyttökuva 2026-04-06 kello 20 31 41" src="https://github.com/user-attachments/assets/da0f3e2c-bf67-4a4b-8d5f-61d92ef7815d" />


4. Tämän jälkeen `ansible-playbook site.yml` komento oli pitänyt valittaa sudo need a password, mutta minulla ei tullut tätä ongelmaa (?)
  
  
   <img width="985" height="521" alt="Näyttökuva 2026-04-06 kello 20 34 18" src="https://github.com/user-attachments/assets/44a07609-7e91-40eb-8cae-efe683e5c592" />

## Package

Tehtävänä asentaa kaksi pakettia Ansiblella.

1. Luodaan uusi rooli: mkdir paketit ja sinne jälleen tasks

   <img width="483" height="33" alt="Näyttökuva 2026-04-06 kello 20 42 37" src="https://github.com/user-attachments/assets/9a2f643c-2b67-4c78-bb40-d5376ddd6f3c" />

2. Tehdään main.yml tiedosto johon annetaan name: ladattavat ohjelmat ja state: present.
   
   <img width="254" height="66" alt="Näyttökuva 2026-04-06 kello 20 52 08" src="https://github.com/user-attachments/assets/514bc7fc-e398-4ad8-854f-0eac7efa5335" />

3. Lisätään site.yml:iin uusi rooli: paketit

   <img width="188" height="133" alt="Näyttökuva 2026-04-06 kello 20 53 06" src="https://github.com/user-attachments/assets/d120eaec-683d-48e1-ad41-cc14a06abe3e" />

4. Ajetaan ansible-playbook site.yml
   - Tulee virhe site.yml tiedostossa -> typo korjataan.
     
   <img width="529" height="168" alt="Näyttökuva 2026-04-06 kello 20 56 48" src="https://github.com/user-attachments/assets/6a146d3e-156e-495d-b175-1ec968e5440a" />

   - Ajetaan ansible-playbook site.yml uudestaan ja tulee taas uusi virhe -> korjataan lisäämällä välilyönti.

   <img width="567" height="152" alt="Näyttökuva 2026-04-06 kello 20 57 42" src="https://github.com/user-attachments/assets/53ed59db-8d70-4d93-b36a-fbdb195abd89" />

   - Virheet korjattu ja toimii ja ohjelmat ladattu.
     
    <img width="917" height="566" alt="Näyttökuva 2026-04-06 kello 20 59 38" src="https://github.com/user-attachments/assets/37c3fcae-3fe4-4e04-a9e0-706096f7cb49" />

## File

Tämä oli hieman epäselvä kohta ja jouduinkin googlettamaan -> googlesta tekoälymode antoi aika suoria ehdotuksia ja lähdinkin kokeilemaan niitä hieman soveltaen.

1. Loin uuden tiedoston ansibaatun alaisuuteen files kansion alle (foo.txt)
2. Muokkasin main.yml tiedostoa:

   <img width="356" height="111" alt="Näyttökuva 2026-04-06 kello 21 18 18" src="https://github.com/user-attachments/assets/4c02839c-3e06-4bf6-adf1-48f5f78bf0a5" />

   - src =  tiedosto haetaan automaattisesti
   - dest = mihin se kopioidaan
   - owner ja group = tiedoston omistaja ja ryhmä
   - mode = "0600", tähän hieman taas googlea niin "-rw-------". 
   - tällä oktaalinumerolla vain ansibaatu saa read and write, muilla ei ole oikeuksia.

3. Ajoin playbookin ja tuli jotain (läpi meni), mutta en ole yhtään varma menikö kaikki niin kuin pitää:

   <img width="934" height="565" alt="Näyttökuva 2026-04-06 kello 21 23 37" src="https://github.com/user-attachments/assets/615d16dc-e557-492d-81d8-938a9da838fc" />

 
4. Testasin katsoa foo.txt tiedostoa aatu1 käyttäjälle ja *permission denied*
5. SSH yhteys ansibaatuun ja tällä käyttäjällä oli oikeudet ja foo.txt sisältö tuli näkyviin.
 
   <img width="729" height="291" alt="Näyttökuva 2026-04-06 kello 21 39 46" src="https://github.com/user-attachments/assets/6e5a7541-3a68-4429-acc0-a35023d8e6ae" />


## Lähteet
Karvinen, 2026. Palvelinten Hallinta. Luettavissa: https://terokarvinen.com/palvelinten-hallinta/#laksyt. Luettu: 

Karvinen, 2026. Sudo without password. Luettavissa: https://terokarvinen.com/passwordless-sudo/. Luettu: 

Munroe, 2006. xkcd. Luettavissa: https://xkcd.com/149/. Luettu: 

Karvinen, 2026. Passwordless sudo with ansible. Luettavissa: https://terokarvinen.com/passwordless-sudo-with-ansible/. Luettu: 
