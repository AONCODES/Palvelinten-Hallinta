# H3

## Artikkelit
### Apache installed with Ansible - quick notes
- Artikkelissa uutena informaationa notify, joka ilmoittaa handlerssille -> käynnistä apache2 jos muutoksia tehty.
- taskin mainissa asennetaan apache2 (jos ei ole jo) ja kopioidaan example.com.conf apachen hakemistoon oikeuksineen.
- filessa siirretään sites-enabled hakemistoon haluttu tiedosto (a2ensite (?)).

### Handlers: running operations on change
- Ansiblen handlerssit ovat operaatioita/tehtäviä jotka suoritetaan vain silloin kun muutoksia tehdään.
- Notify vaaditaan johonkin suoritettavaan tehtävään jotta se toimii.
- Kun playbook ajetaan handlerssit tekevät tehtäviään jos muutos tapahtuu ja notify on ilmoitettu -> Jos ei tapahdu muutoksia tai notify puuttuu, handlerssit eivät tee mitään.

### ansible-doc service
- service ei asenna mitään (apt) eikä luo ryhmiä tai käyttäjiä (group / user) vaan se hallitsee palveluita (proxyna toisilla service managereille).
- apt:illa voidaan ladata esim nginx tai apache2, ja servicellä se voidaan käynnistää tai vaikka lopettaa.

## Apache2 asennus
Aloitin lataamalla apache2:n. Tämä löytyi jo minulta koneelta, mutta siihen oli tarjolla päivityksiä.
  
<img width="596" height="178" alt="Näyttökuva 2026-04-13 kello 14 53 11" src="https://github.com/user-attachments/assets/76689208-d445-4db9-b688-e042635fffc5" />

Tein uuden hakemiston `mkdir /var/www/uusisivu` ja uuden index.html tiedoston `micro index.html`.

<img width="430" height="183" alt="Näyttökuva 2026-04-13 kello 14 59 17" src="https://github.com/user-attachments/assets/8142800e-2ca5-4e96-9a0b-4218b069c75b" />

Siirryn seuraavaksi `cd /etc/apache2/sites-availble` ja luon sinne uuden tiedoston `micro uusisivu.conf`

<img width="351" height="183" alt="Näyttökuva 2026-04-13 kello 15 05 36" src="https://github.com/user-attachments/assets/45f22f68-411c-4668-abee-e2eaeda08a52" />

Otan sivun käyttöön:

    sudo a2ensite uusisivu.conf

Tällä luodaan linkki sites-enabled hakemistoon eli otetaan sivu käyttöön.

<img width="438" height="38" alt="Näyttökuva 2026-04-13 kello 15 07 34" src="https://github.com/user-attachments/assets/1ec863e4-3833-4017-b504-61238c780fab" />

Annetaan oikeudet ohjeiden mukaisesti sekä ´potkaisin´ demonia:

    sudo chmod -R ugo+rw /var/www/uusisivu
    sudo systemctl restart apache2



Tässä kohtaa sivut näyttivät tältä:

<img width="387" height="209" alt="Näyttökuva 2026-04-13 kello 15 16 31" src="https://github.com/user-attachments/assets/f11c1f8e-cb93-4b6c-9033-05ad533e432b" />

Muokkasin sivuja:

<img width="661" height="254" alt="Näyttökuva 2026-04-13 kello 15 17 59" src="https://github.com/user-attachments/assets/96bbc9bc-e29f-4e39-9aef-1972e1040477" />



## Nginx asennus

Asensin nginx:n

    sudo apt-get install nginx

Suljin tässä kohtaa apache2 ja starttasin nginx

    sudo systemctl stop apache2
    sudo systemctl start nginx

Tarkistin `sudo systemctl status` komennolla nginx ja apachen tilan -> nginx = active (running) ja apache2 = inactive (dead).

Lisäksi katsoin selaimelta localhostin niin tulee:

<img width="544" height="210" alt="Näyttökuva 2026-04-14 kello 12 00 14" src="https://github.com/user-attachments/assets/0596da3f-ccb1-47b9-b376-a118dbf5746d" />

Tässä kohtaa tein uuden hakemiston apachen2n tyylisesti sekä loin uuden tiedoston. (tein nämä omaan kotihakemistoon, apache oli /var/www).

    sudo mkdir /home/aatu1/nginxtestisivu
    sudo micro /home/aatu1/nginxtestisivu/index.html

<img width="493" height="182" alt="Näyttökuva 2026-04-14 kello 12 19 45" src="https://github.com/user-attachments/assets/4cb2b9d6-fafe-49a0-a2e9-9c9678486978" />


Annoin oikeudet eli hakemistoihin x-oikeus ja tiedostoon r-oikeus:

    sudo chmod ugo+x /home/aatu1/
    sudo chmod ugo+x /home/aatu1/nginxtestisivu/
    sudo chmod ugo+r /home/aatu1/nginxtestisivu/index.html


<img width="680" height="323" alt="Näyttökuva 2026-04-14 kello 12 29 29" src="https://github.com/user-attachments/assets/760f22b1-b421-4bdf-8d9f-8263915a4184" />







   
## Nginx asennuksen automatisointi Ansiblella

## Lähteet
https://terokarvinen.com/apache-ansible/

https://terokarvinen.com/palvelinten-hallinta/#laksyt

https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html
