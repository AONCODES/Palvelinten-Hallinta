# H6

## What is Git?
- Git eroaa muista versionhallintajärjestelmistä toimintatavallaan.
  - Useat muut tallentaa vain tiedostomuutokset.
  - Git tallentaa koko ns. tilannekuvan (snapshot) projektista.
- Git toimii paikallisella koneella ilman nettiyhteyttä.
- Yhteistyön helpottaminen (rinnakkainen työskentely, jokaisella oma kopio)
[Pro Git 2026](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F)

## Gitin käyttö

Gitin peruskäyttöön lukeutuu komennot
```
git add --all - siirretään kaikki muutokset työhakemistossa "staging" tilaan odottamaan committia
git commit  - ottaaa snapshotin ja tallentaa sen projektin historiaan
git pull  - ladataan haara  ´remote´ repositoriosta ja yhdistetään se nykyiseen/paikalliseen haaraan
git push  - pullin vastakohta, siirretään paikallinen haaara toiseen repositorioon
```
[Atlassian 2026](https://www.atlassian.com/git/glossary#commands)

## Online
Tehdään uusi repositorio GitHubiin ja lisätään READMe.md sekä Lisenssi.


<img width="265" height="317" alt="Näyttökuva 2026-04-27 kello 15 11 04" src="https://github.com/user-attachments/assets/e13d03bf-ab72-439f-b0ec-41237ef9fffd" /> <br>


Tässä kohtaa valitaan repositoriolle nimi, kuvaus sekä konfiguroinnit. Valitsin Public, jotta se on kaikille näkyvä, lisäsin README:n sekä valitsin GNU General Public License v3.0, jotta estetään minun työn omiminen. Tämän jälkeen "Create repository" ja homma on valmis.


<img width="795" height="674" alt="Näyttökuva 2026-04-27 kello 15 13 16" src="https://github.com/user-attachments/assets/5bfb6e6f-0434-426a-966b-b36803551f19" />


## Dolly
Kopioin virtuaalilinuxiin kyseisen repositorion. Käytin SSH-osoitetta. Aikaisemmin olin jo kopsannut VM:sta julkisen avaimen ja tallentanut sen GitHubiin (Settings -> SSH and GPG keys -> New SSH key). 

<img width="635" height="183" alt="Näyttökuva 2026-04-27 kello 17 16 35" src="https://github.com/user-attachments/assets/d7c27b69-f5ff-4a18-abee-51d3a3b05da1" />
<br>

Nyt kun repositorio oi kopioitu paikalliselle koneelle menin kyseiseen hakemistoon ja toin tiedot komennolla `git pull` -> Already up to date, eli kun kopoin sen niin ei ollut sen jälkeen muutoksia tullut.


Kun olin lisännyt uuden tiedoston paikallisella koneella -> lisäsin muutokset staging tilaan, ja tallensin ne (commmit). Tämän jälkeen vielä pull komennolla hain jos repositorioon olisi tullut muiden muutoksia, lopuksi git push -> Siirsin muutokset remote repositorioon.

<img width="575" height="489" alt="Näyttökuva 2026-04-27 kello 17 28 42" src="https://github.com/user-attachments/assets/56947398-09ca-45e9-b72e-75c814a31ec4" />
<br>
Tarkistin vielä selaimesta oliko muutokset menneet GitHubiin.

<img width="408" height="188" alt="Näyttökuva 2026-04-27 kello 17 32 06" src="https://github.com/user-attachments/assets/cde4d89c-c56b-4b9d-8eb3-6a6d8b5da092" />


## Doh!
```
git reset --hard
```
Komennolla poistaa kaikki muutokset staging tilasta ja myös muutokset joita ei vielä oltu lisätty `git add --all`. Eli kyseinen komento ns palauttaa kaiken siihen tilaan mikä se oli viimeisimmässä commitissa. [git](https://git-scm.com/docs/git-reset)


Muutin config tiedoston sisältöä ja yritin resetoida, mutta ei onnistunut. Vaihdoin tekemäni muutokset takaisin, miten olisin edennyt jos en olisi muistanut enää mitä muutoksia tein?

<img width="447" height="109" alt="Näyttökuva 2026-04-27 kello 17 48 38" src="https://github.com/user-attachments/assets/2dec7493-6a97-4003-a761-03cafc34a4e4" />
<br>


<img width="723" height="469" alt="Näyttökuva 2026-04-27 kello 17 51 11" src="https://github.com/user-attachments/assets/2e3543b4-ad97-4997-bde3-cb17cfa9b2bd" /><br>

Hieman ongelmiako? 
<img width="491" height="150" alt="Näyttökuva 2026-04-27 kello 17 54 26" src="https://github.com/user-attachments/assets/7146f268-1e7f-4ed7-9b7f-f392da90922f" />
<br>
Löydin HEAD tiedostosta ylimääräistä tekstiä ja pääsin takaisin main haaraan. Ajoin uudelleen git reset --hard komennon.<br>
<img width="474" height="37" alt="Näyttökuva 2026-04-27 kello 18 00 29" src="https://github.com/user-attachments/assets/775560c0-5bdd-40be-ab48-e99fb6399788" />

<br>
Testasin uudelleen kevyemmällä muokkauksella ja nyt näyttäisi juurikin niin, että palautui tuolle f79794e commitille.
<img width="518" height="253" alt="Näyttökuva 2026-04-27 kello 18 08 34" src="https://github.com/user-attachments/assets/7a14f675-a8ad-4360-afa7-c791a3577f11" />



## Tukki

## Gitanbile

## Lähteet

https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F

https://terokarvinen.com/palvelinten-hallinta/#laksyt

https://www.atlassian.com/git/glossary#commands
