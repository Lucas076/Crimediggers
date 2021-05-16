# Crimediggers
Dit is een uitwerking van de eerste 3 opdrachten van de nieuwe game gemaakt door de politie genaamd Crimediggers. De resterende opdrachten daar ben ik zelf nog mee bezig.

## Opdracht 1 - Camerabeelden
Wanneer je de camerabeelden aandachtig bekijkt zul je erachter komen dat Ulrieke in de volgende camera's op chronologische volgorde verschijnt:
- TRH03
- GNG04
- GNG03
- GNG07
- EXT02

## Opdracht 2 - Kenteken auto
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

## Opdracht 3 - Data telefoon Ulrieke uitlezen
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
10. Het IP-adres van de server is `136.144.181.113`.
