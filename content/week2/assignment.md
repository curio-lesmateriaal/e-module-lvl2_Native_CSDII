---
week: 2
title: De Sleutel — een veilig objectmodel
subtitle: Inleveropdracht Week 2
client: Autoverhuur De Sleutel
maxPoints: 12
deliverables:
  - Je week 1-project, uitgebreid met doordachte access modifiers
  - Een korte toelichting per class waarin je je keuzes uitlegt
criteria:
  - id: w2h1
    text: Fields die niet van buitenaf gewijzigd mogen worden zijn private (of private set)
    points: 3
  - id: w2h2
    text: Er zijn public methoden waarmee andere objecten gecontroleerd wijzigingen doorvoeren
    points: 3
  - id: w2h3
    text: Minstens één zinvolle static member (bijv. een standaardwaarde of een teller)
    points: 2
  - id: w2h4
    text: De toelichting legt per class uit waarom iets public of private is
    points: 2
  - id: w2h5
    text: Het project compileert en de demo in Program.cs werkt nog steeds
    points: 2
tips:
  - Begin private, maak alleen public wat echt van buitenaf nodig is.
  - Een static teller voor het aantal aangemaakte verhuringen is een mooi voorbeeld.
  - Gebruik `{ get; private set; }` voor een property die je van buiten wel wilt lezen maar niet wijzigen.
---

De eigenaar van De Sleutel schrok toen een stagiair per ongeluk in de code alle dagprijzen op 0 zette. "Kan de code niet gewoon voorkomen dat dat kan?" Dat kan — met de juiste toegankelijkheid.

Neem je objectmodel van week 1 en maak het "veilig". Zet fields die alleen de class zelf hoort te wijzigen op `private` en bied waar nodig public methoden aan om ze gecontroleerd te veranderen (bijvoorbeeld: de dagprijs mag alleen verhoogd of verlaagd worden via een methode die niet onder de 0 komt). Voeg minstens één zinvolle `static` member toe, bijvoorbeeld een standaard-dagprijs voor nieuwe voertuigen of een static teller die bijhoudt hoeveel verhuringen er in totaal zijn gemaakt. Schrijf per class een paar zinnen toelichting waarin je uitlegt waarom je iets public of private hebt gemaakt.

## Inleveren

Lever je bijgewerkte project (als `.zip`) met de toelichting in via **Itslearning**, onder de map "Module: Native (C#)".
