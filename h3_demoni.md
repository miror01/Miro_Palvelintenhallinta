## x)

Artikkeleissa kerrotaan Apache2:n asennuksen ja konfiguraation automatisoinnista Ansiblella. Ne konfiguroidaan package-file-service -kuviolla. Ensin asennetaan daemoni, sitten konffataan ja käynnistetään.

Handlerit on ns. "tehtäviä" jotka ajetaan vain, jos tapahtuu muutoksia, yleensä tämä toteutetaan **notify**-komennolla, eli jos toinen tehtävä playbookissa ilmoittaa muutoksesta. Handlerit ovat hyvä ja tehokas tapa välttää turhaa uudelleenkäynnistämistä, on hyvin järkevää toteuttaa konfiguraatio, joka käynnistää palvelun uusiksi vasta kun siellä on oikeasti tapahtunut muutoksia.

**ansible-doc service** on ansible-doc:in työkalu hallitsemaan palvelun tilaa, vaihtoehtoja ovat muun muassa **started** , **stopped**, ja **restarted**. **enabled: true** taas määrittää sen käynnistymään automaattisesti.

## a)

Asensin Apache2:n komennolla **sudo apt install apache2**. Tein oman hakemiston sitä varten komennolla **mkdir /home/miror/julkinensivu** ja tein sinne index.html tiedoston johon lisäsin kuvassa olevan tekstin.

Polun ja oikeudet muutin itse konffaustiedostossa nimeltä **/etc/apache2/sites-available/000-default.conf**. Sivu näkyi siis osoitteessa **http://localhost**

<img width="272" height="132" alt="h3_kuva1" src="https://github.com/user-attachments/assets/2cae899b-5fc5-4a28-8c21-cf28f3525a58" />


## b)

Ensiksi sammutin Apache2:n. Ne toimivat samalla tavalla samasta portista joten Nginx:n toiminnan kannalta on oleellista että Apache2 on pois päältä.
Asensin Nginx:in komennolla **sudo apt install nginx**. Konffasin oletussivun omaksi sivukseni ja kokeilin **http://localhost** onnistuneesti Nginx:in kautta.

<img width="427" height="260" alt="h3_kuva2_nettisivutoimii_nginxkautta" src="https://github.com/user-attachments/assets/441a47ff-e7b3-469d-bf1a-a4a4867e51b9" />


## c)

Automatisointi alkoi sillä että loin uudet roolit ja kansiot. Komentona toimi **mkdir -p roles/nginx/{tasks,handlers,files}**. Lisäsin site.yml:ään nginx:in

<img width="397" height="183" alt="h3_kuva4" src="https://github.com/user-attachments/assets/bd9807b1-9059-49fd-ae84-c0b264a2768c" />


Tein tasks-hakemistoon main.yml, johon määrittelin mitä haluan YAML-tiedoston tekevän, eli asennus ja tilan varmistaminen.

<img width="447" height="225" alt="h3_kuva3_nginxtasks" src="https://github.com/user-attachments/assets/8df5568f-f11c-4a12-9866-31e56917f2fa" />

Sitten tein Handler-tiedoston.

<img width="395" height="101" alt="handler" src="https://github.com/user-attachments/assets/eb6b301a-6165-4b65-b17c-39d614c80f9d" />

Sitten ajoin playbookin suorittamaan kyseiset tehtävät. Eli **ansible-playbook -K site.yml**, joka asensi ja käynnisti nginx:in.

<img width="595" height="174" alt="h3_kuva5" src="https://github.com/user-attachments/assets/08363306-a09d-4493-b9c5-0de020e28fc0" />

Ja viimeiseksi tarkistin että localhost sivu toimii edelleen, ja kyllä toimi.

