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
- service ei asenna mitään (apt) eikä luo ryhmiä tai käyttäjiä (group / user) vaan se hallitsee demoneja.
- apt:illa voidaan ladata esim nginx tai apache2, ja servicellä se voidaan käynnistää tai vaikka lopettaa.

## Apache2 asennus

## Nginx asennus

## Nginx asennuksen automatisointi Ansiblella

## Lähteet
https://terokarvinen.com/apache-ansible/

https://terokarvinen.com/palvelinten-hallinta/#laksyt

https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html
