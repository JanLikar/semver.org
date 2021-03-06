---
layout: slovenian
title: Semantične verzije 2.0.0
---

Semantične verzije 2.0.0
========================

Povzetek
--------

Številke MAJOR.MINOR.PATCH povečajte:

1. MAJOR, ko naredite s trenutno verzijo nezdružljive spremembe API-ja,
1. MINOR, ko dodate funkcionalnost na način, ki je združljiv s trenutno verzijo,
1. PATCH, ko naredite popravke hroščev, ki ne vplivajo na združljivost.

Dodatno oznako predizdaje in metapodatke lahko dodate kot pripono nizu MAJOR.MINOR.PATCH.

Uvod
----

V svetu programske opreme obstaja grozen prostor imenovan
"pekel odvisnosti". Večji kot sistem zraste in več je paketov,
ki jih integrirate v vašo programsko opremo, bolj možno se boste našli nekega
dne v tem obupu.

V sistemih z veliko odvisnostmi lahko izdaja nove verzije paketa hitro
postane nočna mora. Če so specifikacije odvisnosti preveč ozke, ste v
nevarnosti zaklenjenih verzij (nezmožnost nadgradnje paketa brez, da
izdajate nove verzije za vsak odvisni paket). Če so odvisnosti
določene preveč ohlapno, boste neizogibno ugriznjeni s strani promiskuitete verzije
(ob predpostavki, da je združljivost z večimi prihodnjimi verzijami razumna).
Pekel odvisnosti je, kjer ste vi, ko je verzija zaklenjena in/ali vam promiskuiteta verzije
preprečuje, da enostavno in varno prestavite vaš projekt naprej.

Kot rešitev tega problema, predlagam enostaven skupek pravil in
zahtev, ki diktirajo, kako naj bodo številke verzij določene in povečane.
Ta pravila so osnovana na in ne nujno omejena na pred obstoječe
široko skupne prakse v uporabi tako v programski opremi zaprte kode kot odprte kode.
Da ta sistem deluje, morate najprej določiti javni API. To lahko sestoji
iz dokumentacije ali je izvršeno s strani same kode. Ne glede na to,
pomembno je, da je ta API jasen in točen. Ko enkrat identificirate vaš javni
API, lahko komunicirate spremembe na njem z določenimi povečanji na vaši številki
verzije. Smatrajte obliko verzije X.Y.Z (Glavna.Manjša.Popravek). Popravki hroščev ne
vplivajo na API a povečujejo številko popravka, nazaj združljivi API
dodatki/spremembe povečujejo manjšo verzijo in nazaj nezdružljive API
spremembe povečujejo glavno verzijo.

Ta sistem se imenuje "Semantične verzije." Pod to shemo, številke verzij
in način, kako spreminjajo poslani pomen o podležeči kodi in kaj je bilo
spremenjeno iz ene verzije v naslednji.


Specifikacija semantičnih verzij (SemVer)
-----------------------------------------

Ključne besede "MORA", "NE SME", "ZAHTEVANO", "BO", "NE BO", "BI MORALO",
"NE BI SMELO", "PRIPOROČLJIVO", "LAHKO" in "OPCIJSKO" se v tem dokumentu
interpretira, kot so opisane v [RFC 2119](http://tools.ietf.org/html/rfc2119).

1. Programska oprema, ki uporablja semantične verzije MORA določiti javni API. Ta API
je lahko določen v kodi sami ali pa obstaja striktno v dokumentaciji.
Ko je končan, mora biti točen in celovit.

1. Običajna številka verzije MORA biti oblike X.Y.Z, kjer so X, Y, in Z
pozitivna cena števila in NE SMEJO vsebovati vodilnih ničel. X je
glavna(MAJOR) verzija, Y je manjša(MINOR) verzija in Z je verzija popravka(PATCH).
Vsak element se MORA povečevati numerično. Na primer: 1.9.0 -> 1.10.0 -> 1.11.0.

1. Ko je paket verzije enkrat izdan, se vsebina te verzija
NE SME spremeniti. Kakršnekoli spremembe MORAJO biti izdane kot nova verzija.

1. Glavna verzija nič (0.y.z) je namenjena prvotnemu razvoju - karkoli se lahko spremeni
kadarkoli. Javnega API takega paketa se NE SME smatrati kot stabilnega.

1. Verzija 1.0.0 definira javni API. Kako se številka verzije
povečuje, je odvisno od javnega API-ja in kako se le-ta spreminja.

1. Verzija popravka Z (x.y.Z | x > 0) MORA biti povečana, če so izdani samo
popravki, ki so združljivi s prejšnjo različico. Popravek je definiran kot notranja
sprememba, ki popravi nepravilno obnašanje.

1. Manjša verzija Y (x.Y.z | x > 0) MORA biti povečana, če so javnemu API-ju
dodane funkcionalnosti, tako da so spremembe združljive s prejšnjo različico.
MORA biti povečana, če je katerakoli funkcionalnost javnega API-ja označena kot "opuščena".
LAHKO je povečana, če so znotraj privatne kode vpeljane nove funkcionalnosti ali izboljšave.
LAHKO vključuje spremembe, ki bi navadno terjale povečanje verzije popravka.
Verzija popravka MORA biti ponastavljena na nič, ko je manjša verzija povečana.

1. Glavna verzija X (X.y.z | X > 0) MORA biti povečevana, če je v javen API vpeljana kakršnakoli
nezdružljiva sprememba. LAHKO vključuje spremembe, ki bi navadno terjale povečanje manjše verzije
in verzije popravka. Manjša verzija in popravek MORATA biti ponastavljena na 0, ko je
glavna verzija povečana.

1. Verzija predizdaje je LAHKO označena z dodajanjem vezaja in
serije s pikami ločenih oznak. Oznake MORAJO biti sestavljene samo iz alfanumeričnih znakov
nabora ASCII in vezaja [0-9A-Za-z-]. Identifikatorji NE SMEJO biti prazni.
Numerični identifikatorji NE SMEJO vključevati vodilnih ničel. Verzije predizdaj po urejenosti
manjše od običajnih verzij. Verzija predizdaje označuje, da je verzija nestabilna in mogoče ne zadosti
zahtevam združljivosti, ki jih pripisujemo pripadajočim normalnim verzijam.
Primeri verzij predizdaj: 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7, 1.0.0-x.7.z.92.

1. Metapodatki so LAHKO označeni z dodajanjem znaka plus in serije s pikami
ločenih oznak, ki sledijo verziji popravka ali verziji predizdaje.
Oznake MORAJO biti sestavljene samo iz alfanumeričnih znakov nabora ASCII in vezajev [0-9A-Za-z-].
Oznake NE SMEJO biti prazne. Metapodatki BI MORALI biti ignorirani, ko se določa
vrstni red verzij. Zato sta dve verziji, ki se razlikujeta samo v metapodatkih,
v vrstnem redu na istem mestu. Primeri verzij z dodanimi metapodatki: 1.0.0-alpha+001,
1.0.0+20130313144700, 1.0.0-beta+exp.sha.5114f85.

1. Vrstni red se sklicuje na to, kako so verzije primerjane druga z drugo, ko so urejene.
Vrstni red MORA biti izračunan z ločitvijo verzije v glavno, manjšo, popravek
in identifikator predizdaje v tem vrstnem redu (metapodatki gradnje ne pašejo
v vrstni red). Vrstni red je določen s prvo razliko, ko
primerjate vsako od teh identifikatorjev iz leve proti desni kot sledi: Verzije glavna, manjša
in popravek so vedno primerjane s številkami. Na primer: 1.0.0 < 2.0.0 <
2.1.0 < 2.1.1. Ko so glavna, manjša in popravek enake, ima verzija pred-izdaje
manjši vrstni red kot običajne izdaje. Na primer 1.0.0-alpha < 1.0.0. Vrstni red
za dve verziji pred-izdaje z enako verzijo glavne, manjše in popravka MORATA
biti določeli s primerjanjem vsake pike ločenega identifikatorja iz leve proti desni
dokler ni razlika najdena kot sledi: identifikatorji sestavljeni iz samo številk
so primerjani numerično in identifikatorji s črkami ali vezaji so primerjani
besedno v ASCII vrstnem redu. Numerični identifikatorji imajo vedno manjši vrstni red
kot ne-numerični identifikatorji. Večji skupek polj pred-izdaje imajo večji
vrstni red kot manjši skupek, če vsi prejšnji identifikatorji so enaki.
Na primer: 1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-alpha.beta < 1.0.0-beta <
1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1 < 1.0.0.

Zakaj uporabljati semantične verzije?
-------------------------------------

To ni nova ali revolucionarna ideja. V bistvu delate nekaj podobnega
temu že sedaj. Problem je, da "nekaj podobnega" ni dovolj dobro. Brez
skladnosti z nekakšno uradno specifikacijo, so številke verzij
v bistvu neuporabne za upravljanje odvisnosti. Z dodajanjem imena in jasne
definicije zgornjim idejam, postane enostavno za komunicirati vaše namere
uporabnikom vaše programske opreme. Ko enkrat postanejo te namere jasne, fleksibilne (vendar
ne preveč fleksibilne), se lahko končno naredi specifikacija odvisnosti.

Enostaven primer bo demonstriral, kako semantične verzije lahko naredijo pekel
odvisnosti stvar preteklosti. Premislite o knjižnici imenovani "Firetruck". Zahteva
paket s semantično verzijo in se imenuje "Ladder". Ko je Firetruck
narejen, je Ladder pri verziji 3.1.0, lahko varno določite verzijo odvisnosti Ladder
kot večjo ali enako 3.1.0, vendar manjšo kot 4.0.0. Sedaj ko postane
Ladder verzija 3.1.1 in 3.2.0 postane na voljo, jih lahko izdate v vašem
sistemu paketnega upravljanja in veste, da bodo postale kompatibilne z obstoječo
odvisno programsko opremo.

Kot odgovoren razvijalec boste seveda želeli preveriti, da katerikoli
paket nadgradnje funkcionira, kot je oglaševano. Realni svet je grdo mesto;
ničesar ni, kar bi lahko naredili o tem, razen da smo pazljivi. Kar lahko naredite je
omogočiti semantičnim verzijam, da vam ponudijo pameten način izdaje in nadgradnje
paketov brez, da morate kotaliti nove verzije odvisnih paketov, kar vam prihrani
čas in težave.

Če to vse zveni zaželjeno, je vse kar morate storiti, da začnete uporabljati semantične
verzije, razglasitev, da to tako delate in nato slediti pravilom. Povežite
na to spletno stran iz vaše datoteke README, da ostali vedo pravila in jih lahko
koristijo.


Pogosta vprašanja
-----------------

### Kako ravnam z revizijami v 0.y.z začetni fazi razvoja?

Najenostavneje je prvo izdajo označiti z 0.1.0 in ob
vsaki nadaljnji izdaji povečati število MINOR.

### Kako vem, kdaj izdati 1.0.0?

Če se vašo programska oprema uporablja v produkciji, bi morala verjetno že biti
označena z 1.0.0. Če imate stabilen API od katerega so uporabniki odvisni, bi morali
imeti 1.0.0. Če vas skrbi združljivost, bi morali verjetno že biti na 1.0.0.

### Ali to ne odvrača hitrega razvoja?

Verzija z MAJOR številko enako nič je namenjena hitremu razvoju. Če spreminjate API
vsakodnevno, bi morali biti še vedno na verziji 0.y.z. Če razvijate naslednjo MAJOR
verzijo programske opreme, bi morali delati na ločeni veji projekta.

### Če že najmanjša nezdružljiva sprememba javnega API-ja zahteva povečanje MAJOR verzije, ali ne bom zelo hitro končal pri verziji 42.0.0?

To je vprašanje odgovornega razvoja in previdnega načrtovanja. Nezdružljivih
sprememb se ne sme malomarno vpeljevati v programsko opremo, od katere
je odvisnih veliko uporabnikov. To, da morate povečati MAJOR verzijo za
izdajo nezdružjivih sprememb pomeni, da boste bolj pozorni na vpliv vaših
sprememb.

### Dokumentiranje celotnega javnega API-ja terja preveč dela!

Kot profesionalni razvijalec programske opreme ste odgovorni, da ustrezno dokumentirate
programsko opremo, ki je namenjana, da jo uporabljajo tudi drugi. Upravljanje kompleksnosti
predstavlja zelo pomemben del ohranjanja učinkovitosti projekta. To je težavna naloga,
če nihče ne ve, kako uporabljati vašo programsko opremo in katere metode so varne za klicanje.
Uporaba semantičnih verzij in vztrajanje pri dobro definiranem javnem API-ju, lahko zagotovi,
da bo vaš projekt dolgoročno lahko vzdrževati.

### Kaj narediti, če ponesreči izdam nezdružljivo spremembo?

Kakor hitro se zaveste, da ste prekršili pravila semantičnih verzij, popravite napako in
izdajte različico, ki povrne združljivost, ter ima novo oznako verzije. Tudi v teh
okoliščinah, ni sprejemljivo spreminjati že izdane kode. Če je primerno,
dokumentirajte svojo napako in obvestite uporabnike o napačni izdaji.

### Kaj naj naredim, če posodobim svoje lastne odvisnosti brez spremembe javnega API-ja?

To bi moralo biti smatrano kompatibilno, ker ne vpliva na javni API.
Programska oprema, ki je eksplicitno odvisna od istih odvistnosti, bi vaš paket
moral imeti svoje lastne specifikacije odvisnosti in avtor bo opazil kakršnekoli
konflikte. Določanje ali je sprememba modifikacije nivoja popravka ali manjšega nivoja
zavisi na tem ali posodabljate vaše odvisnosti z namenom popraviti hrošč ali dodati novo
funkcionalnost. Običajno bi pričakoval dodatno kodo
za slednjo instanco, v katerem primeru je očitno povečanje manjšega nivoja.

### Kaj če nehote spremenim javni API na način, ki ni skladen s spremembo številke verzije (t.j. koda nepravilno predstavi glavno zlomljivo spremembo v izdaji popravka)?

Uporabite vašo najboljšo presojo. Če imate veliko občinstvo, ki bo močno
vplivano s spreminjanjem obnašanja nazaj k čemur je bil javni API namenjen, potem
je lahko najboljše opraviti glavno verzijo izdaje, četudi bi popravek
striktno bil smatran za izdajo popravka. Spomnimo se, semantične verzije so samo
transportiranje, kar pomeni za koliko se številka verzije spremeni. Če so te
verzije pomembne za vaše uporabnike, uporabite številko verzije, da jih obvestite.

### Kako ravnam z opuščenimi funkcionalnostmi?

Opuščanje obstoječe funkcionalnosti je običajen del razvoja programske opreme in
je pogosto zahtevano za narediti, da se naredi nadaljnji razvoj. Ko opuščate del vašega
javnega API-ja, bi morali narediti dve stvari: (1) posodobiti vašo dokumentacijo, da
obvestite uporabnike o spremembi, (2) izdati novo manjšo verzijo z opuščenostjo
na mestu. Preden v celoti odstranite funkcionalnost v novi glavni izdaji
bi morala biti vsaj ena manjša izdaja, ki vsebuje opuščenost, da
lahko uporabniki gladko preidejo na nov API.

### Ali ima semver omejitev dolžine niza verzije?

Ne, vendar uporabite presojo. Uporaba oznake verzije, sestavljene iz 255
znakov dolgega niza, je najverjetneje pretiravanje.
Kljub temu, imajo lahko nekateri sistemi omejeno dolžino niza.

O projektu
----------

Avtor specifikacije semantičnih verzij je [Tom
Preston-Werner](http://tom.preston-werner.com), izumitelj Gravatarja in
soustanovitelja GitHub-a.

Slovenski prevod so prispevali:

* [Peter Kokot](https://github.com/peterkokot)
* [Aleš Šarkanj](https://github.com/alsar)
* [Jan Likar](https://github.com/JanLikar)

Če želite pustiti povratne informacije, prosimo, da [odprete vprašanje na
GitHub-u](https://github.com/mojombo/semver/issues).


Licenca
-------

[Creative Commons - CC BY 3.0](http://creativecommons.org/licenses/by/3.0/)
