# terrainGenUsingPerlinNoise
Terrain generation using perlin noise made in Unity. It might be totally inefficient but I had fun 😌😌😌


Readme (in Serbian):

=======================================================================================================================================================================

Dobrodošli u program za generisanje naizgled prirodnog terena :)

=======================================================================================================================================================================

=== NAPOMENA! ===
Program je veoma procesorski i grafički zahtevan i potrebno je dosta RAM memorije.
Nemojte generisati mape veće od 300*300 i bazene veće od 500000 ukoliko imate 8 GB RAM memorije.

Program koristi ugrađenu funkciju Perlinovog šuma i ako je broj oktava veći od 1, tada preklapa više funkcija i generiše prirodniji teren(sa određenim parametrima).
Perlinov šum se takođe koristi za efekat talasanja vode, naravno definisan drugačijim parametrima.

Radi optimizacije programa, svi blokovi se generišu i postavljaju u bazene. 
Kompjuteru je mnogo lakše da prvo stvori blokove koji će se koristiti pa onda da ih pozicionira tamo gde treba, nego da ih kreira iznova i iznova, svaki put kad se klikne dugme.

Pored funkcije Perlinovog šuma, koristi se i algoritam koji popunjava rupe u terenu koje se prave kada je razlika izmedju visina blokova veća od 1. Algoritam je ubačen kako bi teren izgledao lepše.

Ukoliko pri sporom generisanju terena želite da se generiše jos brže, usmerite kameru od terena, kako kompjuter ne bi morao da vam prikaže pojedinačno iscrtavanje blokova.

=======================================================================================================================================================================

1. Skala - Predstavlja maksimalnu visinu generisanog terena.

2. Pomeraj - Predstavlja nagib odnosno razliku između visina. Što je veći to je teren haotičniji. Što je manji, to je teren ravniji.

3. Dimenzija - Predstavlja broj blokova u jednom redu, a kvadrat ove promenljive čini površinu terena.
(16GB rama sa skalom 150, pomerajem 0.02 i 1 oktavom bez vode može da generiše 750x750 sa otprilike 2,000,000 blokova u prvom bazenu).

4. Seed - Predstavlja pomeraj po x odnosno z osi matrice i naizgled pomaže u generisanju slučajnog terena. (U Unity okruženju, Y osa predstavnja visinu, tako da se koriste X i Z ose)
Isti seed pravi isti teren, dokle god su svi ostali parametri isti. Seed možete uneti manuelno.

5. Nivo - Predstavlja dodatan pomeraj visine. (opcionalno)

6. Oktave - Predstavljaju broj preklapanja funkcije koja se koristi. Koristi 2 parametra ispod navedena kako bi detaljnije(na mikro nivou) generisala teren.

7. Okt Pomeraj - Predstavlja pomeraj na mikro nivou, gde za svaku narednu preklopljenu funkciju množi Pomeraj(2.).

8. Okt Skala - Predstavlja skalu na mikro nivou, gde za svaku narednu preklopljenu funkciju množi Skalu(1.).

9. Nadmorski Nivo - Predstavlja trenutni nivo vode. Manuelno je postavljena vrednost 50, što je visina na kojoj teren prelazi iz braon u zelenu boju (trave).

10. Crtaj Vodu - Predstavlja toggle koji kontroliše crtanje vode. Ukoliko se odštiklira dok je voda prisutna, voda biva zamrznuta. 
Ukoliko se štiklira dok voda nije prisutna, ona se postavlja na nadmorski nivo, ali se bočna voda ne generiše.
Ukoliko treba, bočnu vodu mozete dodati pomoću ponovnog generisanja terena. 
Ukoliko želite da teren ostane isti, pre generisanja odštiklirajte Slučajan Teren (13.).

11. Brzo Iscrtavanje - Predstavlja toggle koji kontroliše da li će se teren brzo(štikliran) ili sporo(odštikliran) generisati. 
Pri sporom generisanju, u donjem delu ekrana se pojavljuje ProgressBar(19.) koji se puni kako se blokovi postavljaju.
Iznad ProgressBar-a se nalazi brojač blokova, koliko ih je nacrtano (bez vode, ali sa bočnom vodom) i koliko treba da bude nacrtano.

12. Vremenski Pomeraj - Predstavlja brzinu iscrtavanja blokova pri opciji sporog iscrtavanja (Kada se Brzo Iscrtavanje (11.) odštiklira). 
Sto je Slider vise levo, to je generisanje brže. Sto je Slider vise desno, to je sporije (maks 1).

13. Slucajan Teren - Predstavlja toggle koji kontroliše da li će se pri generisanju koristiti Seed(4.). 
Odštiklirati ukoliko želite da teren koristi trenutni Seed. 

14. Generiši Teren - Glavno dugme za generisanje terena. Ukoliko imate problem sa trenutnim terenom, možda bi pomoglo da kliknete na ovo dugme. 
Ukoliko želite da teren ostane isti, pre generisanja odštiklirajte Slucajan Teren (13.).

15. Bazen za blokove terena (prva šarena kocka) - Bazen za sve blokove koji čine teren (bez bočne vode). 
Dimenzije terena ne daju dobar broj blokova koji će se iskoristiti zbog algoritma za popunjavanja rupa. 
Radi dobrog terena, staviti makar 5-10 puta veći broj blokova nego sto je kvadrat dimenzije. (5*dimenzija*dimenzija) 
Za veće terene (preko 300*300) eksperimentalno doći do broja blokova potrebnih za bazen. 
Takođe, što je skala veća, to će biti potrebno više blokova.

16. Bazen za blokove vode (naredna svetlo plava kocka) - Bazen za vodu (koja se pomera) koja se generiše na nadmorskoj visini, ukoliko je štikliran Crtaj Vodu (10.), iznad blokova, ali ne ispod drugih blokova. 
Nepotrebno je staviti veci broj od kvadrata dimenzije.

17. Bazen za blokove bočne vode (naredna tamno plava kocka) - Bazen za bočnu vodu, koja se stvara samo ukoliko je čtikliran Crtaj Vodu (10.). 
Staviti broj koji je okvirno 2 puta veći od kvadrata dimenzije.

Dimenzije bazena se menjaju nakon sto se završi upis u polje pored bazena. Menjanje dimenzije bazena sa mnogo blokova moze da potraje. 
Ukoliko ne želite da promenite dimenzije bazena, nemojte kliktati na njegovo polje za unos jer će sam klik
da natera bazen da promeni dimenzije, i ako nije uneta druga vrednost.

18. 2D Prikaz trenutno generisanog terena - Predstavlja top-down pogled na teren. Boja piksela predstavlja visinu: Bela boja za viši teren, crna za niži. 
Što je dimenzija terena veća, to ima vise piksela. Što je pomeraj veći, to ima više 
promena u bojama.

19. ProgressBar - Pri sporom generisanju, u donjem delu ekrana se pojavljuje ProgressBar(19.) koji se puni kako se blokovi postavljaju. 
Iznad ProgressBar-a sa leve strane ekrana se nalazi brojač blokova, koliko ih je nacrtano (bez vode, ali sa bočnom vodom) i koliko treba da bude nacrtano.
Ukoliko treba eksperimentalno doći do ukupnog broja blokova za neku dimenziju, savetuje se da pre brzog iscrtavanja terena, prvo stavite sporo iscrtavanje kako bi se izračunao broj blokova.
Tada ćete moći lakše znati koju vrednost treba staviti u polje za unos bazena. (Ukoliko iscrtavate teren sa vodom, ovo vam neće previše pomoći jer u UkupnoBlokova staju blokovi koji pripadaju bazenu bočne vode (3. bazen)).


=======================================================================================================================================================================

Kontrole na tastaturi:

Enter: Ulazak u mod pokreta kamere (Izlazak iz UI)

WSAD: Pokretanje kamere kroz prostor (Intuitivan raspored)

Escape (ESC): Izlazak iz moda pokreta kamere (Ulazak u UI)

"1": Promena pozicije kamere na X:0, Z:0, Y:skala + 50

"2": Promena pozicije kamere na X:0, Z:dimenzija, Y:skala + 50

"3": Promena pozicije kamere na X:dimenzija, Z:dimenzija, Y:skala + 50

"4": Promena pozicije kamere na X:dimenzija, Z:0, Y:skala + 50

"5": Promena pozicije kamere na X:dimenzija/2, Z:dimenzija/2, Y:skala + 50 (Centar terena)

Iako se kamera pomera, moraćete da usmerite ugao kamere pomerajem miša kako biste videli teren.

"-": Umanjenje od 50 u daljini iscrtavanja terena (od kamere) tzv Clipping Plane Far opcija kamere u Unity okruženju. 
Ukoliko kamera previše secka pri svom pomeranju, probajte da smanjite daljinu iscrtavanja ovako. 
PAZNJA: Kliknite veoma brzo jer nije implementiran metod kojim se umanjuje samo jedanput kad se pritisne bez obzira koliko dugo držite. 
Nemojte drzati dugo jer bi program mogao da se zamrzne.

"+" i "="(Zbog nemogućnosti na nekim tastaturama da se klikne +): Uvećanje od 50 u daljini iscrtavanja terena (od kamere). 
PAZNJA: Kliknite veoma brzo jer nije implementiran metod kojim se umanjuje samo jedanput kad se pritisne bez obzira koliko dugo drzite.
 
Pomeranje misa utiče direktno na ugao gde gleda kamera. Nije moguće okrenuti kameru više od 720 stepeni.

=======================================================================================================================================================================

Preporuke:

Ukoliko se previše odaljite od terena kamerom i kako god da pomerite ugao kamere ga ne možete videti, preporučuje se da kliknete "5" kako biste se vratili iznad centra terena, usmerite kameru na dole i pritisnite + (=) par puta dok teren
ne postane vidljiv opet. 
Ukoliko teren još uvek nije vidljiv, verovatno je da u bazenu nema dovoljno blokova (ako ste štiklirali crtaj vodu, odštiklirajte i probajte ponovo).
Ukoliko još uvek imate problema, izađite iz programa i ponovo pokrenite program. (Izlaženje je najlakše moguće kombinacijom tastera alt+f4).

Ukoliko vam se zamrzne program iz bilo kog razloga, ukoliko ne želite da sačekate da izvrši radnju, uvek možete bez ikakvog problema zatvoriti program nasilno i ponovo pokrenuti program.

Preporučuje se cooler ukoliko se program pokreće na laptopu.

Pri svojim osnovnim vrednostima, program zauzima 1GB RAM memorije kada se pokrene.

=======================================================================================================================================================================

Autori:
Andrija Stojković
Milanče Andrejić
Milica Štrbac

Vreme kreiranja projekta: okvirno 100 sati kroz 2 nedelje;

Zahvalnica:

Sebastian Lague		https://www.youtube.com/channel/UCmtyQOKKmrMVaKuRXz02jbQ
Brackeys		https://www.youtube.com/user/Brackeys
Unity docs:		https://docs.unity3d.com/
Stack Overflow		https://stackoverflow.com/
The Coding Train	https://www.youtube.com/user/shiffman

Hvala na pažnji :)

=======================================================================================================================================================================
