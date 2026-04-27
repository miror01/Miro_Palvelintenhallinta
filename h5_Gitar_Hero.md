## x)

Git on versionhallintajärjestelmä, joka erottuu muista versionhallintajärjestelmistä siinä mielessä että se käsittelee dataa eri tavalla. Se näkee datan muokkaukset ns "tilannekuvina" eikä varsinaisina muutoksina tiedostoihin. Komento **commit** tulee tehtäviä tehdessä varsin tutuksi. Se tallentaa koko prokkiksen tilan tiettynä hetkenä, ns ottaa siitä "tilannekuvan" eikä vain muutoksia. Se ei tallenna mitään uusiksi jos muutoksia ei tapahdu. Gitissä hyvä ominaisuus on se, että se toimii isolta osin paikallisesti, tarkoittaen, että verkkoyhteyttä ei tarvita, muutakun **push**-vaiheessa, jolloin virtualboxissa tehdyt muutokset lisätään webbiliittymään, siihen tietenkin tarvitsee verkkoa että se voi päivittyä nettiin. Gitin keskeisiä komentoja on **git add --all && git commit**, sekä **git pull && git push**. (Git Cheat Sheet). Näiden tarkoitus selittyy hyvin raportissa, mutta perusperiaate on, että **git add --all** lisää tiedostot varastoon, **git commit** tekee päivitykset ja tämän komennon yhteydessä annetaan kuvaus muutoksista. **git pull & git push**, liittyy esim. virtualboxissa tehtyjen muutoksien työntämiseen verkkoon GitHub:in webbiliittymään. **pull** vetää muutokset webbiliittymästä ja **push** lisää virtualboxissa tehdyt muutokset webbiliittymään.



## a)

Tein uuden varaston GitHubiin ohjeiden mukaisesti. On tärkeää lisätä README.md, tai vastaava tiedosto luomisen yhteydessä jotta varasto toimii. Lisäsin myös ohjeiden mukaisesti GPL 3 Lisenssin.

<img width="1247" height="633" alt="image" src="https://github.com/user-attachments/assets/e8a09842-37f7-4df9-98ed-adbbfb06ded1" />


## b)

Sitten onkin aika lisätä varasto virtualboxille, eli toisinsanoen kloonata se. Alla olevassa kuvassa näkyy kaikki vaiheeni, kloonasin varaston virtualboxiin, sitten siirryin varastoon ja loin sinne ekan tiedoston nanolla
nimeltä **ekatiedosto.md**. Seuraavaksi terminaaliin kirjotetaan komento **git add --all**, joka valmistaa uudet tiedostot ja muutokset committia varten. Täten päästääkiin seuraavaan komentoon **git commit**, jonka avulla
päivitetään muutokset ja kirjataan ne ylös. Tässä vaiheessa kirjoitetaan esimerkiksi että mitä on muutettu. Vikana komentona **git push** toimii päivittäjänä, se siis työntää (päivittää) virtualboxilla tehdyt muutokset 
GitHub:in webbiliittymään.

<img width="494" height="305" alt="h5_2" src="https://github.com/user-attachments/assets/18488150-892d-4999-bdd3-12c43eb9e659" />

**ekatiedosto.md** päivittyi onnistuneesti webbiliittymään.

<img width="954" height="320" alt="image" src="https://github.com/user-attachments/assets/72dfa96b-fd0b-4a60-8d5d-dbbd87a283ee" />


## c)

C kohdan tarkoitus on perehtyä uuteen komentoon **git reset --hard**. Se tuhoaa viimeiset muutokset ja näkyy konkreettisesti kuvasta. Ekana kuvassa näkyy komento **nano ekatiedosto.md**, jossa kävin lisäämässä c. kohdan
muutoksen, komento **cat ekatiedosto.md** näyttää tämän. Sitten kokeillaan ekaa kertaa komentoa **git reset --hard**, ja nähdään taas cat:lla, että aiemmat tallentamattomat muutokset ovat poistuneet. Kyseinen reset- komento
siis palauttaa tilan viimeisimpään committiin. Kätevä komento ja tulee varmasti joskus hyödylliseksi.

<img width="274" height="96" alt="h5_3" src="https://github.com/user-attachments/assets/5b439885-8488-4d50-969d-5984c4111885" />

## d)

Seuraavaksi tarkistellaan lokia. Tämänkaltaisessa versionhallinta-toiminnassa lokien ylläpitö on erittäin tärkeää ja avuliasta. Jokainen muutos kuvaillaan ja selitetään ja se tekee kaikesta helpompaa. Varsinkin, jos 
käyttäjiä on monia yhdessä varastossa, tai varastossa on satoja/tuhansia tiedostoja, lokien ylläpitämisestä tulee elintärkeää. Alla olevassa kuvassa näkyy 2 committia ja lokipäivitystä. Alempi lokipäivitys on siitä, kun
ihan ekan kerran loin varaston GitHubin webbiliittymässä. "Initial commit" tulee itsestään README.md, tiedoston yhteydessä. Ylempi loki on minun tekemä päivitys virtualboxissa, jonka kuvailin tekstillä "Eka update". 
Sähköposti ylemmässä lokipäivityksessä ei ole aito.

<img width="462" height="124" alt="h5_4" src="https://github.com/user-attachments/assets/9df55d9f-d736-430e-83a1-9c94d3f04781" />

Tärkeä lisäys loki-komentoihin on **--patch**. Komento **git log --patch** näyttää tarkemman selityksen siitä, mitä muutoksia tiedostoissa on tarkalleen tehty. Aiemmassa **git log**- komennossa näkyy vain kirjaajan
kirjoittama kuvaus. Komennolla **git log --patch**, näemme, että tiedostoon on lisätty teksti "moro :D", sekä varastoa luodessa lisätty GPL Lisenssi, tämä näkyy vihreällä tekstillä.

<img width="493" height="345" alt="h5_5" src="https://github.com/user-attachments/assets/f2329c13-a5d0-4162-adae-7b1519668318" />

## e)

Seuraavaksi laitetaan Ansible-kansio versionhallintaan. Tarkistin ekana onko Git jo käytössä ansible-hakemistossa, komentona toimii **git status** joka näyttää kuvassa "not a git repository". Seuraavaksi lisätään Git.
Komentona toimii **git init**. Se luo kansioon Git-varaston ja alkaa seurata muutoksia. Lisäsin kansion kaikki tiedostot varastoon komennolla **git add --all**, ja komennolla **git commit** kuvailin ensimmäisen muutoksen.
Kuvaus on vähän hutera, tajusin jälkeenpäin vasta että parempi kuvaus olisi ollu "Add ansible files" eli lisää kaikki ansible-tiedostot varastoon, sillä se tuossa juuri tehtiin.

<img width="423" height="293" alt="h5_6" src="https://github.com/user-attachments/assets/7f17c6e1-5853-40c9-8fd6-57c65a404a3b" />


Tehdään tiedostoihin joku muutos. Valitsin muutokseksi että lisään **site.yml**- playbookkiinihi aiemman tehtävän vapaavlintaisen demonin, Caddyn, laittamisen kommentiksi. Kun rooli siirretään kommentiksi, sitä ei enää
ajeta playbookin suorittamisen kohdalla ja näin voi vaikkapa säästää aikaa, kun playbook ajetaan.

Caddy-rooli on nyt muutettu kommentiksi. Seuraavaksi ajetaan playbook, **ansible-playbook -K site.yml** ja katsotaan komennolla **git status**, jossa lukee "modified: site.yml". Lisään tiedostot komennolla **git add --all**
ja seuraavaksi komennolla **git commit** kuvailen muutoksen. Kuvassa näkyy kirjoittamani kuvaus commit-komennolla, sekä muutetut rivit. "- caddy" rivin eteen on tullut #-merkki kommentin osoittamiseksi.

<img width="340" height="318" alt="h5_9" src="https://github.com/user-attachments/assets/0bd9d370-86ca-4839-9153-572a20204755" />

## Lähteet.

Chacon and Straub 2014: Pro Git, 2ed: 1.3 Getting Started - What is Git?. Luettu 27.4.2026

Apuna toteutuksen ideoinnissa on käyetty ChatGPT:n 5.3-mini -kielimallia. Komennot ja itse toteutus on kuitenkin omaa työtä.

















