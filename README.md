# Crimediggers
Dit is een uitwerking van de eerste 4 opdrachten van de nieuwe game gemaakt door de politie genaamd Crimediggers. De resterende opdrachten daar ben ik zelf nog mee bezig.

## Objective 1 - Camerabeelden
Wanneer je de camerabeelden aandachtig bekijkt zul je erachter komen dat Ulrieke in de volgende camera's op chronologische volgorde verschijnt:
- TRH03
- GNG04
- GNG03
- GNG07
- EXT02

## Objective 2 - Kenteken auto
Je krijgt van de parkeergarage een `logs.csv` bestand. Een CSV bestand kan je openen met behulp van Microsoft Excel.
1. Open het bestand `logs.csv` in Excel.
2. Selecteer alles met behulp van de toetsen `Ctrl` + `A`.
3. Ga binnen Excel naar het kopje `Gegevens` en druk op de knop `Tekst naar kolommen`.
4. Kies voor de eerste optie `Gescheiden` en klik op de knop `Volgende >`.
5. Bij `Scheidingstekens` voer je bij `Overige:` een `#` in.
6. Klik op de knop `Volgende >` en daarna op de knop `Voltooien`.

Als het goed is heb je nu een duidelijker overzicht van de tabel.
Er worden bij de data van timein en timeout verschillende formaten gebruikt.
Je bent opzoek naar 20 september 19:07.
1. Voer met behulp van `Ctrl` + `F` de tekst `Sep 20` in.
2. Als snel zul je bij timeout een timestamp vinden van `Sep 20 2020 19:07:00` wat matcht met de tijd dat Ulrieke in de auto is gestapt.
3. De auto is een grijze Tesla maar het kenteken is nogal raar. Dit komt omdat het kenteken is opgeslagen in Base64 formaat. Voor het omzetten naar tekst heb ik gebruik gemaakt van [CyberChef](https://gchq.github.io/CyberChef/).
4. Voer het kenteken `Ry00OTYtUFg=` in bij `Input`.
5. Sleep de optie `From Base64` naar de `Recipe`.
6. Het kenteken van de grijze Tesla is `G-496-PX`.

## Objective 3 - IP-adres C&C server
Deze opdracht heb ik uitgevoerd met behulp van [Kali Linux](https://kali.org).
1. Download het bestand `phone_final.dd`.
2. Maak een folder aan met behulp van het commando `mkdir /media/test`.
3. Mount het bestand `phone_final.dd` in de aangemaakte folder met behulp van het commando `mount -o loop phone_final.dd /media/test`.
4. Wanneer je de folder bekijkt zul je de data van een Android telefoon aantreffen.
5. Na enige tijd zoeken val het je op dat er in de `app` folder een bestand staat met de naam `com.confengine.android_chat_app-rfVVPmV_y311ebcnNPd6rw==`.
6. In deze folder staat een APK bestand genaamd `base.apk`.
7. Decompileer dit bestand met behulp van deze website [APK Decompilers](https://www.apkdecompilers.com/).
8. Navigeer naar de folder `sources` > `com` > `agilefaqs` > `chatapp`.
9. Open het bestand `BackDoor.java` met een tekst editor.
10. Het IP-adres van de C&C server is `136.144.181.113`.

## Objective 4 - Naam van de hacker
In de vorige opdracht is ene IP-adres gevonden. Wanneer we naar dit IP-adres toegaan in een browser wordt ons verteld dat er op dat IP-adres 2 websites worden gehost genaamd `welingelichtebronnen.nl` en `huur-een-hacker.nl`.
1. Gebruik een website directory bruteforce applicatie (bijvoorbeeld [Dirbuster](https://sourceforge.net/projects/dirbuster/)).
2. Kies 1 van de woordenlijsten die met de applicatie geleverd worden en ga opzoek naar hidden directories die beginnen met een `.`.
3. Al snel zul je de hidden directory `.git` vinden.
4. Ga naar `welingelichtebronnen.nl/.git/config` en download het bestand.
5. In bestand staat de naam en het e-mailadres van de hacker namelijk `Sp3xz0R@gmail.com`.
6. Googelen op het e-mailadres heeft weinig zin dus we googelen op de gebruikersnaam `Sp3xz0R`.
7. Je vindt een YouTube account met 2 videos van een hamsterkooi.
8. Wanneer je bij deze [video](https://www.youtube.com/watch?v=LquXRhfIhR0) doorspoelt naar 19:54 zie je een pakket met een postlabel.
9. De naam van de hacker is `Niko van der Spek`.

## Objective 5 - GPS coördinaten uitstappen Ulrieke
Je krijgt een bestand met daarin 2 carimages. De bedoeling is om deze 2 bestanden te mounten en te assemblen omdat het RAID files zijn.
1. Download het bestand `carimage.zip` en unzip het met het commando `unzip carimage.zip`.
2. Maak 2 nieuwe folders aan met het commando `mkdir rawimage1` en `mkdir rawimage2`.
3. Mount elke carimage naar elk zijn aparte aangemaakte folder met de commando's `sudo ewfmount carimage1.E01 rawimage1` en `sudo ewfmount carimage2.E01 rawimage2`.
4. Maak vervolgens loop images met de commando's `sudo losetup /dev/loop1 rawimage1/ewf1` en `sudo losetup /dev/loop2 rawimage2/ewf1`.
5. Nu combineer je de loop images met de commando's `sudo mdadm --assemble --run /dev/md0 /dev/loop1` en `sudo mdadm --assemble --run /dev/md0 /dev/loop2`.
6. Als het gelukt is kun je deze folder nu mounten met het commando `sudo mount /dev/md0 /media/test`.
7. Wanneer je in de gemounte folder kijkt tref je een bestandsysteem aan.
8. Na enige tijd zoeken vind je in de folder `var` > `logs` een bestand genaamd `Car_gps.log`.
9. Importeer dit bestand in de website [GPS Visualiser](https://www.gpsvisualizer.com) en je krijgt een map te zien met GPS punten.
10. Als je de punten bekijkt valt het je op dat er wordt gestopt bij een McDonalds in Breukelen.
11. De coordinaten waar Ulrieke is uitgestapt is `52.171442, 4.989492`.
