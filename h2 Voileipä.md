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
    sudo visudo /etc/sudoers.d/sudoless

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
