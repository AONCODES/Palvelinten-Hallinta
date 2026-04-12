# H3

## Artikkelit
### Apache installed with Ansible - quick notes
- 

### Handlers: running operations on change
- Ansiblen handlerssit ovat operaatioita/tehtäviä jotka suoritetaan vain silloin kun muutoksia tehdään.
- Notify vaaditaan johonkin suoritettavaan tehtävään jotta se toimii.
- Kun playbook ajetaan handlerssin tekevät tehtäviään jos muutos tapahtuu ja notify on ilmoitettu -> Jos ei tapahdu muutoksia tai notify puuttuu, handlerssit eivät tee mitään.

### ansible-doc service

## Apache2 asennus

## Nginx asennus

## Nginx asennuksen automatisointi Ansiblella

## Lähteet
https://terokarvinen.com/apache-ansible/

https://terokarvinen.com/palvelinten-hallinta/#laksyt

https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html
