---
week: 4
title: De Sleutel — beheerconsole
subtitle: Inleveropdracht Week 4
client: Autoverhuur De Sleutel
maxPoints: 14
deliverables:
  - Een console-app die met een menu de vier CRUD-bewerkingen op voertuigen uitvoert
  - De gegevens blijven bewaard na afsluiten (ze staan in de database)
  - Screenshot van de database vóór en ná een paar bewerkingen
criteria:
  - id: w4h1
    text: Er is een menu (bijv. met een while-lus en Console.ReadLine) met de opties toevoegen, tonen, wijzigen, verwijderen, stoppen
    points: 2
  - id: w4h2
    text: Toevoegen leest gegevens in, maakt een object, doet Add en SaveChanges
    points: 3
  - id: w4h3
    text: Tonen haalt alle voertuigen op en print ze
    points: 2
  - id: w4h4
    text: Wijzigen haalt één voertuig op (bijv. op kenteken), past het aan en slaat op
    points: 3
  - id: w4h5
    text: Verwijderen haalt één voertuig op, doet Remove en SaveChanges
    points: 2
  - id: w4h6
    text: Elke bewerking gebruikt een context binnen een using-blok; SaveChanges op dezelfde context
    points: 1
  - id: w4h7
    text: Ongeldige invoer (bijv. onbekend kenteken) geeft een nette melding in plaats van een crash
    points: 1
tips:
  - Gebruik `FirstOrDefault` en check op `null` voordat je wijzigt of verwijdert.
  - Zet elke menukeuze in een eigen methode — dat houdt Main klein.
  - 'Test of je gegevens echt bewaard blijven: sluit de app, start opnieuw, kies "tonen".'
---

De balie van De Sleutel wil niet in Visual Studio hoeven werken. Ze willen een simpel programma met een menu waarmee ze voertuigen kunnen toevoegen, bekijken, aanpassen en verwijderen — en dat alles bewaard blijft.

Bouw een console-app bovenop je database van week 3. Maak een menu met de opties: voertuig toevoegen, alle voertuigen tonen, een voertuig wijzigen, een voertuig verwijderen, en stoppen. Elke optie werkt via de `DeSleutelContext`: toevoegen met `Add` + `SaveChanges`, tonen door de `DbSet` te doorlopen, wijzigen door een voertuig op te halen (bijvoorbeeld op kenteken), een property aan te passen en op te slaan, en verwijderen met `Remove` + `SaveChanges`. Zorg dat het programma niet crasht als de gebruiker een kenteken invoert dat niet bestaat.

## Inleveren

Lever je project (als `.zip`, zonder `bin/` en `obj/`) met de screenshots in via **Itslearning**, onder de map "Module: Native (C#)".
