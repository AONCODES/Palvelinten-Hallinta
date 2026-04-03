# H2
## Artikkelit
### <span style="color:red">Sudo without password</span>
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

### Passwordless Sudo with Ansible




## Sudoless
## Ansibaatu
## Package
## File

## Lähteet
Karvinen, 2026. Palvelinten Hallinta. Luettavissa: https://terokarvinen.com/palvelinten-hallinta/#laksyt. Luettu: 

Karvinen, 2026. Sudo without password. Luettavissa: https://terokarvinen.com/passwordless-sudo/. Luettu: 

Munroe, 2006. xkcd. Luettavissa: https://xkcd.com/149/. Luettu: 

Karvinen, 2026. Passwordless sudo with ansible. Luettavissa: https://terokarvinen.com/passwordless-sudo-with-ansible/. Luettu: 
