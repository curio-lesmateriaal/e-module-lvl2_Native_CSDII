---
week: 1
title: Autoverhuur De Sleutel — het objectmodel
subtitle: Inleveropdracht Week 1
client: Autoverhuur De Sleutel
maxPoints: 12
deliverables:
  - Een C#-console-project met minimaal de classes Voertuig, Klant en Verhuur
  - Een Program.cs die een paar objecten aanmaakt en een korte demo in de console toont
  - Een kort tekstbestand (of README) waarin je je modelkeuzes uitlegt
criteria:
  - id: w1h1
    text: Er zijn minimaal drie samenhangende classes met logische fields/properties
    points: 3
  - id: w1h2
    text: Elke class heeft een constructor die de verplichte gegevens instelt
    points: 2
  - id: w1h3
    text: Een Verhuur heeft een referentie naar een Voertuig én een Klant
    points: 2
  - id: w1h4
    text: Er is minimaal één methode met gedrag (bijv. Verhuur.BerekenPrijs of Voertuig.MarkeerAlsVerhuurd)
    points: 2
  - id: w1h5
    text: Program.cs maakt objecten aan en roept methoden aan; de output klopt
    points: 2
  - id: w1h6
    text: Namen zijn in het Nederlands of Engels consequent; code is netjes ingesprongen
    points: 1
tips:
  - Begin met opschrijven welke gegevens De Sleutel per voertuig, klant en verhuur wil bijhouden.
  - Laat een Verhuur naar bestaande objecten verwijzen — maak niet in elke Verhuur een nieuwe Klant.
  - Kijk terug naar het RaceCar/RaceDriver-voorbeeld uit de theorie voor het doorgeven van referenties.
---

Autoverhuur De Sleutel verhuurt auto's en bestelbussen aan particulieren en bedrijven. Nu gaat alles nog met een schrift achter de balie: welk voertuig is verhuurd, aan wie, en van wanneer tot wanneer. De eigenaar wil dit gaan automatiseren en vraagt jou om als eerste stap het *objectmodel* te ontwerpen — nog zonder database, gewoon in C#.

Bouw een console-app met een objectmodel voor De Sleutel. Bedenk welke classes er nodig zijn (denk minimaal aan `Voertuig`, `Klant` en `Verhuur`) en welke fields of properties elke class krijgt. Geef elke class een constructor. Zorg dat een `Verhuur` een referentie heeft naar een bestaand `Voertuig` en een bestaande `Klant`. Voeg minstens één methode met echt gedrag toe, bijvoorbeeld een methode die de huurprijs berekent op basis van het aantal dagen, of een methode die een voertuig op "verhuurd" zet. Maak in `Program.cs` een paar voertuigen, klanten en verhuringen aan en laat in de console zien dat je model werkt.

Je hoeft nog geen invoer van de gebruiker te verwerken en nog niets op te slaan — daar gaan de volgende weken over.

## Inleveren

Lever je project (als `.zip`) plus je uitleg in via **Itslearning**, onder de map "Module: Native (C#)". Je docent geeft feedback op je objectmodel.
