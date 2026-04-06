x) 
Ensimmäinen artikkeli "Sudo without password" on ohje salasanattoman sudon käyttämiseen, joka siis mahdollistaa ansiblen automaation koska salasanoja ei tarvitse enää kirjoittaa. Tehtävä suoritettu ohjeiden mukaan, 
eli tein ryhmän **sudoless** ja lisäsin uuden käyttäjän "antero" siihen ja muokkasin sudoers.d-hakemistoa niin että sudoless ryhmällä on oikeus käyttää sudoa ilman salasanaa. Hyödyllinen ja elintärkeä toiminto Ansiblen
toiminnalle. Tässä huomiona että on tärkeä pitää toista terminaalia auki siltä varalta jos rikkoo jotain alkuperäisellä terminaalilla. Näin et lukitse itseäsi ulos omasta systeemistäsi.

Toisen linkin sarjakuva oli ihan hauska.

Kolmas artikkeli "Passwordless Sudo with Ansible" on ohjeet samaan prosessiin kuin ensimmäisessä artikkelissa, mutta tällä kertaa automatisoituna Ansiblella. Tein sen ohjeiden mukaan ja lopussa näkyy kuvassa että kaikki toimii.

ansible-doc -komennot ovat kuin ansiblen omat linuxista tutut **man**-sivut. Käytetään esimerkiksi **ansible-doc copy**. **copy** komento on tiedostojen kopiointia varten. **copy**-komennolla on optioita kuten **content** ja **dest**. nämä määrittävät sisällön ja kohteen.

**ansible-doc apt** hallinnoi paketteja ja on ikäänkuin linuxista tuttu **sudo apt**. Optio **name** viittaa paketin nimeen ja **state** sen tilaan.

**ansible-doc file** käsittelee tiedostoja ja hakemistoja. Optiot **path** ja **state** määrittää polun ja kohteen tyypin, eli esim hakemisto/linkki.

**ansible-doc user** on käyttäjien hallinnointia varten. Optiot **name** ja **group** määrittävät käyttäjän tunnuksen ja ryhmän.

**ansible-doc authorized_key** on SSH-avaimia varten. Optio **user** tarkoittaa käyttäjää jolle avain lisätään, ja **key** tarkoittaa lisättävää avainta.


a & b)
Ekana loin manuaalisesti uuden käyttäjän ja ryhmän joka oli sudoless, b. tehtävässä automatisoin sen ansiblella.

<img width="512" height="164" alt="sudoless_antero" src="https://github.com/user-attachments/assets/56add814-88a9-49b0-b727-c03747334eca" />


c)
Asensin paketit **htop** ja **git**. Toimivuus testattu terminaalissa ja todettu onnistuneeksi.

<img width="158" height="84" alt="paketit" src="https://github.com/user-attachments/assets/3d14fc29-d098-49b4-8e28-e4bbffb6c200" />


d)
Ansiblen avulla loin moni-rivisen tiedoston tiukoilla oikeuksilla. oikeudet "**600**" tarkoittaa, että vain tiedoston omistajalla on oikeus lukea ja kirjoittaa. Loput 2 nollaa tarkoittavat ryhmää ja muita käyttäjiä, heillä ei ole lainkaan oikeuksia. Oikeudet 600 on kirjaimina -rw-------.

<img width="299" height="79" alt="file_tehtävä" src="https://github.com/user-attachments/assets/084b889f-c628-427e-96f3-67f14fea66f4" />

e)
Löysin uuden moduulin jota ei ole vielä käytetty kurssilla, **timezone**. Se on vastuussa palvelimen kellonajasta.

<img width="146" height="37" alt="jotainmuuta" src="https://github.com/user-attachments/assets/02a1fb56-727c-4130-a81b-d66d3553c3a3" />



Testaus)

Ajoin playbookin komennolla **ansible-playbook site.-yml -K** ja tuloksena oli seuraava:

<img width="586" height="392" alt="h2_kuva5" src="https://github.com/user-attachments/assets/7ff00922-8fca-44c1-a34c-f7266017c2ba" />














<img width="586" height="392" alt="h2_kuva5" src="https://github.com/user-attachments/assets/e3d553df-2c9d-4217-8214-a61edeccbfc4" />

