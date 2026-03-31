# H1 Hei Ansiblen maailma

x. Julkisella SSH-avaimella pääsee kirjautumaan toisiin palvelimiin etänä. Ekan kerran jälkeen salasanaa ei enää tarvita, todella kätevää. Avain luodaan komennolla **ssh-keygen** ja kopioidaan eli lähetetään muille koneille      komennolla **ssh-copy-id**. Edistää turvallisuutta kun salasanoja ei enää tarvita.

x. Ansible on konfigurointi-työkalu ohjelma joka toimii SSH:n yli. Paljon uutta opeteltavaa mutta ohjelma vaikuttaa mielenkiintoiselta.

a. SSH asennettu ja testattu komennoilla **sudo apt install ssh** ja **ssh localhost**. Laitettu käynnistymään aina palvelimen käynnistyksen yhteydessä komennolla **sudo apt enable ssh**

b. SSH-kirjautuminen automatisoitu. Komennolla **ssh-keygen -t ed25519 -C miron_avain** loin oman avaimeni ja lisäsin sen omalle palvelimelleni komennolla **ssh-copy-id localhost**. Nyt SSH-kirjautuminen on automatisoitu ja kirjautuessani localhostiin SSH:lla salasanaa ei enää tarvita.

c. "Hei maailma" tehty ja kokeiltu playbookeilla. tein "https://terokarvinen.com/hello-ansible/" -ohjeen mukaan ekan playbookin ja lisäksi itse toisen yksinkertaisemman "hei-ansible.yml" playbookin josta tulostuu viesti "Hei ansible". Tehtävä ei ollut liian monimutkainen mutta paljon opeteltavaa vielä havainnoinnin kanssa, eli miksi tehtiin mitä tehtiin ja mikä oli joka vaiheen tarkoitus.
