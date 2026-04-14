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


Annoin oikeudet eli hakemistoihin x-oikeus ja tiedostoon r-oikeus sekä vaihdoin hakemiston omistajaksi aatu1:

    sudo chmod ugo+x /home/aatu1/
    sudo chmod ugo+x /home/aatu1/nginxtestisivu/
    sudo chmod ugo+r /home/aatu1/nginxtestisivu/index.html
    sudo chown -R aatu1:aatu1 /home/aatu1/nginxtestisivu/

<img width="684" height="325" alt="Näyttökuva 2026-04-14 kello 12 49 02" src="https://github.com/user-attachments/assets/0d91de61-f283-4492-9c4e-3a4ed1636ebf" />

Tämän jälkeen jouduin buuttaamaan UTM:n ja testasin muuten vaan selaimessa localhostia, ja sehän näytti apache2:n sivut. Olikin ilmeisesti ansiblella se automaattinen käynnistys (?), olin laittanut apache2:n stopille mutta en disabloinut. Apache oli käynnissä ja nginx = failed. Sammutin apachen uudelleen ja laitoin vielä disabledin mukaan ja sitten käynnistin nginx:n -> buuttasin ja nyt nginx on edelleen running. (toivottavasti mikään ei hajonnut :D)

<img width="725" height="128" alt="Näyttökuva 2026-04-14 kello 12 53 39" src="https://github.com/user-attachments/assets/3b395bc9-cee9-42b2-8bbf-f0b343584824" />

Seuraavaksi menin `cd /etc/nginx/sites-available` ja avasin default tiedoston -> kopioin sielä perältä valmiin koodi pohjan. Tämän jälkeen:

    micro nginxtestisivu

ja liitin koodipohjan sinne ja muokkasin sitä seuraavanlaisesti:

<img width="390" height="235" alt="Näyttökuva 2026-04-14 kello 13 00 19" src="https://github.com/user-attachments/assets/35ca2630-dbc8-4435-85d5-ef2871d6bc60" />

Tämän jälkeen taas kokeilin localhostia, mutta eihän mitään tapahtunut, koska sivu ei ole ns käynnissä.

nginx aktivointi erosi hieman a2ensitesta:

<img width="695" height="36" alt="Näyttökuva 2026-04-14 kello 13 04 59" src="https://github.com/user-attachments/assets/4c38b5a7-57d8-4b63-9325-cc9f9886403e" />

Tämän jälkeen käynnistin nginx uudelleen ja testatin localhostia: ei toimi.

- Pienen nettiselailun jälkeen löytyi vastaus: minulla oli servernamena nginxtestisivu vaikka olisi pitänyt olla localhost (ongelma 1 korjattu)
- Tämän jälkeen ei vieläkään toiminut, mutta `sudo systemctl realod nginx` korjasi tämän ja localhost toimii selaimessa.
  
- <img width="463" height="133" alt="Näyttökuva 2026-04-14 kello 13 14 16" src="https://github.com/user-attachments/assets/4b045c10-ddc9-471f-94d9-07fc4cc90203" />

Testasin vielä muokata sivua, ja toimi ilman sudoa:

<img width="407" height="157" alt="Näyttökuva 2026-04-14 kello 13 17 47" src="https://github.com/user-attachments/assets/d3a63a83-d08f-42d5-8aa0-7370943f4075" />



   
## Nginx asennuksen automatisointi Ansiblella

Aloitin aluksi tekemällä uuden roolin nginx, sekä sinne tasks hakemiston ja main.yml 
tiedoston.

<img width="536" height="445" alt="Näyttökuva 2026-04-14 kello 13 39 36" src="https://github.com/user-attachments/assets/a4cb19dd-c242-4e89-85b3-5ff1aa77af6d" />

Tämän jälkeen lisäsin site.yml tiedostoon uuden roolin nginx.

Muokkasin main.ymliin 

    - apt:
        name: nginx
        state: present

ja testasin playbookilla:

<img width="694" height="71" alt="Näyttökuva 2026-04-14 kello 13 45 07" src="https://github.com/user-attachments/assets/0a795623-96fd-49d4-b403-b946b39150c9" />

Lisäsin main.yml tiedostoon vielä:

    - service:
        name: nginx
        state: started

Tämän jälkeen hieman perehdyin Teron apache ansible automatisointiin tarkemmin ja lähdin tekemään nginx:lla samoja juttuja.

main.ymliin copy tiedosto:

<img width="671" height="259" alt="Näyttökuva 2026-04-14 kello 14 27 17" src="https://github.com/user-attachments/assets/5912164e-48d5-4218-99cd-5007e13dcf4c" />


ja tuli pitkä error:

<img width="894" height="276" alt="Näyttökuva 2026-04-14 kello 14 26 11" src="https://github.com/user-attachments/assets/1313ee5d-3eef-431d-89de-dc3408ee0eae" />

Korjasin tämän vaihtamalla src: index.html ja sitten playbook meni läpi.

Tämän jälkeen lisäsin file kohdan:

<img width="539" height="123" alt="Näyttökuva 2026-04-14 kello 14 31 35" src="https://github.com/user-attachments/assets/8eab327b-ef72-4f9d-ac5a-f3f580b9f104" />


Puuttuu ainakin tuo files/index.html, lisätään se:

    mkdir /roles/nginx/files
    micro roles/nginx/files/index.html
  

<img width="374" height="210" alt="Näyttökuva 2026-04-14 kello 14 56 29" src="https://github.com/user-attachments/assets/7f825dbe-86bb-4985-b77d-91891c57b600" />


Lopuksi testaan vielä playbookkia ja näyttäisi menevän kaikki OK:

<img width="727" height="75" alt="Näyttökuva 2026-04-14 kello 15 35 33" src="https://github.com/user-attachments/assets/244658d8-86ee-4049-918d-9e5827f95792" />








## Lähteet
https://terokarvinen.com/apache-ansible/

https://terokarvinen.com/palvelinten-hallinta/#laksyt

https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html
