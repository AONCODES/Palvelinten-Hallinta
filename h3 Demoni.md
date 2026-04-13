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

Tein uuden sivu `mkdir /var/www/uusisivu` ja tänne loin index.html tiedoston `micro index.html`.

<img width="430" height="183" alt="Näyttökuva 2026-04-13 kello 14 59 17" src="https://github.com/user-attachments/assets/8142800e-2ca5-4e96-9a0b-4218b069c75b" />



## Nginx asennus

## Nginx asennuksen automatisointi Ansiblella

## Lähteet
https://terokarvinen.com/apache-ansible/

https://terokarvinen.com/palvelinten-hallinta/#laksyt

https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html
