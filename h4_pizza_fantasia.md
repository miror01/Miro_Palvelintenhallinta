## x)

Ensiksi luin sivut 112-117, eli siis kappaleet 4.12.1, 4.12.2, 4.12.3.1. Koin tekstin melko vaikealukuiseksi ja tiheäksi, mutta tekstissä puhutaan DSL:stä, eli Domain Specific Languageista,
tarkoittaen siis konfiguraatiotyökalujen omia kieliä, kuten Salt ja Puppet joista puhuttiin artikkelissa paljon. Artikkelissa käsiteltiin sitä, miten nämä kielet voivat olla erittäin tiheitä, laajoja, sekä monimutkaisia.

Saltissa itsessään on jo 510 eri toimintoa, ja sen dokumentaatio on yli 20000 riviä pitkä, yli 75000 sanaa. Puppetissa taas vähemmän, 113 toimintoa. Mielestäni tämän kaltainen määrä kaikkea teknistä on erittäin uuvuttavaa, 
mutta onneksi näistä ei tarvitse kuin erittäin pientä osaa. Artikkelissakin käsitellään tätä, jos kaikkia toimintoja tarvittaisiin, käyttäjän pitäisi opetella järkyttävä määrä uusia komentoja ja syntaksia. Näin ei onneksi
kuitenkaan ole. Hyvin pientä osaa näistä toiminnoista käytetään arkisesti, esimerkiksi komentoja kuten **file**, **package**, **service**, jne. Yleisiä tehtäviä konfugroinnissa ja hallinnassa tehdään yleensä samoilla perus
toimintamalleilla. Kurssilta erittäin tuttu palvelun (demonin) asennus on yksinkertainen package, file, service- paketti, jota on jo toteutettu ja josta on jo puhuttu paljon kurssilla. Onneksi kaikkea ei tarvitse osata, vaan perustoiminnoilla pärjää. Itsellä ainakin pysyy paremmin pakka kasassa.

Idempotentista puhutaan. Järjestelmän tulisi olla idempotentti, eli turhia muutoksia ei tehdä. Voidaan ajaa playbookki uudestaan ja kun muutoksia ei tapahdu tilana on idempotentti.


## a) Räpylä.

Valitsin demoniksi Caddyn. Pääsin alkuun komennolla **sudo apt install caddy** ja tarkistin Caddyn toiminnan komennoilla **sudo systemctl status caddy**, joka näytti että jotakin epäonnistui, sitten tajusin että aiemmin asentamani
Apache2-palvelin käyttää jo samaa porttin, 80, ja poistin Apache2:n tilapäisesti käytöstä, **sudo systemctl stop apache2**, ja käynnistin Caddyn komennola **sudo systemctl start caddy**, ja tarkistin statuksen aiemmalla komennolla
uudestaan, sekä toiminnan komennolla **curl localhost**.

<img width="431" height="359" alt="h4_kuva1" src="https://github.com/user-attachments/assets/0ae761c7-6e76-43f4-8632-aee69573c9fc" />

## b) Automaatio.

Ensiksi automaatiota varten loin tuttuun tapaan uuden roolin Caddylle. Komentona toimi **mkdir -p roles/caddy/{tasks,handlers,files}**. Tässä kohtaa olin siis jo ansible-hakemistossa, muuten ei toimi.

<img width="190" height="151" alt="h4_2" src="https://github.com/user-attachments/assets/23874a1d-53d6-4a57-ae46-95b7bebd644f" />


Seuraavaksi konfiguroin Caddyn näyttämään valitsemani tekstin web-palvelimessani, tein ekana filesiin "Caddyfilen". Komentona "**nano roles/caddy/files/Caddyfile**.

<img width="410" height="75" alt="h4_3" src="https://github.com/user-attachments/assets/5558e58c-f380-4b83-bf25-b8c9ffe53855" />

Sitten määrittelin asennuksen ja tilan varmistuksen tasks- hakemiston main.yml- tiedostossa. Se antaa tehtävän playbookille.

<img width="404" height="191" alt="h4_4" src="https://github.com/user-attachments/assets/550ee9e0-d9ef-4732-953a-69a8090dfb10" />

Seuraavaksi tein myös handlerin, joka estää turhat uudelleenkäynnistykset jos muutoksia ei tapahdu, ja tällä kertaa se toimiikin, kun tasks- hakemiston main.yml tiedostossa on käsky **notify**, jota en viimeksi tehnyt.

<img width="416" height="59" alt="h4_5" src="https://github.com/user-attachments/assets/df3826a1-04ae-4833-bfe2-a8932922d56f" />

Lisäsin kurssin alussa tehtyyn "site.yml" playbookkiin rooliksi caddy, ja siirsin muut roolit kommentiksi playbookin ajon nopeuttamista varten.

<img width="362" height="98" alt="h4_6" src="https://github.com/user-attachments/assets/4064e2c7-6f6b-411f-ad05-5f2353622de1" />

Ajoin playbookin komennolla **ansible-playbook -K site.yml**. Tuli virheilmoitus:

<img width="632" height="129" alt="h4_8" src="https://github.com/user-attachments/assets/cc12a71d-8966-43a8-8354-43ef4bba1829" />

Minulla oli pari perusjuttua tasks/main.yml tiedostossa väärin, joka näkyy ylempänä main.yml kuvassa. "state: enabled" ja "enabled: yes" oli väärin, muutin state "started" ja kaikki toimi.

<img width="121" height="59" alt="h4_7" src="https://github.com/user-attachments/assets/f78c417a-f035-4b2a-a520-a99cbc21393f" />

Koska Caddy oli jo manuaalisesti asennettu, ei muutoksia pahemmin tapahtunut, vain configin kopiointi oikeaan paikkaan, koska sitä en itse ollut tehnyt., suoritin välissä pari kertaa uudestaan kun tarkistelin asioita ja nyt näkyy,
että site.yml playbookki on idempotentissa tilassa.

<img width="581" height="209" alt="h4_9" src="https://github.com/user-attachments/assets/b3023e74-08a8-4244-92b6-4e650dc795cd" />

## c) Muokkaus

Seuraavaksi kokeilin muuttaa asetuksia ja katsoa, toimiiko playbookkini kuten pitää. Muutin Caddyfile- oletussivua vähän:

<img width="404" height="77" alt="h4_10" src="https://github.com/user-attachments/assets/d6d9df08-73bc-4c01-942a-0674e992bd4d" />

ja ajoin site.yml- playbookin uudestaan. Muutokset näkyvät, ja kuvassa todistuu myös uuden sivun toiminta komennolla **curl localhost**. Kuvassa ylimpänä näkyy myös, että sivu oli juuri aiemmin ollut **curl localhost**:lla eri,
ja playbookin ajon ansiosta tuloste muuttui.

<img width="464" height="283" alt="h4_11" src="https://github.com/user-attachments/assets/540c0f80-2f38-4936-bc6a-3de72b7e6a46" />

## d) Remontti

Nyt rikotaan caddy, käytän komentoa **sudo apt-get purge caddy**, ja katson komennolla **sudo systemctl status caddy**, että purge oikeasti toimi.

<img width="407" height="192" alt="h4_12" src="https://github.com/user-attachments/assets/b38d0b58-5127-4ff0-9723-c18714d062e7" />


Ajan seuraavaksi site.yml- playbookin uudestaan, ja katsotaan mitä käy. Katsotaan samalla, että **curl localhost** näyttää haluamani sivun.

<img width="481" height="275" alt="h4_13" src="https://github.com/user-attachments/assets/b07c67e4-be65-408c-a7af-2c8093142173" />

Mainiota! oli ilahduttavaa nähdä, että kaikki toimii niinkuin pitääkin, sitten tarkistetaankin vain idempotentti ja homma on paketissa :)

## e) Idempotentti

Kaikki skulaa, ja sisäistin tämän tehtävän avulla paljon uutta, jota oli ehkä tehty aiemmin, mutta nyt ymmärrän paremmin konkreettisesti, mitä tehtiin ja miksi. 

<img width="571" height="298" alt="h4_14" src="https://github.com/user-attachments/assets/8462cc59-c640-45a8-9672-ebfa064716c7" />













