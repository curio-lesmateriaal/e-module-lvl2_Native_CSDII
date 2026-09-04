---
week: 2
title: Accessibility & static
goal: je kunt de juiste toegankelijkheid (public, private, internal, protected) kiezen voor fields, properties en methoden, en je begrijpt wat static betekent
accent: violet
summary: Toegankelijkheid bepaalt wie er aan je fields, properties en methoden mag zitten. Je leert de vier modifiers kennen plus het bijzondere keyword static.
leeruitkomsten:
  - Ik kan uitleggen wat de toegankelijkheid van een member betekent
  - Ik ken het verschil tussen public, private, internal en protected
  - Ik kan beargumenteren waarom je iets private maakt en er methoden voor schrijft
  - Ik kan uitleggen wat static betekent en wanneer je het gebruikt
---

## 2.1 Inleiding

Misschien heb je van je docent al wel eens de tip gekregen om een field of methode "public" te maken als je een foutmelding kreeg, maar we hebben tot nu toe nog niet precies uitgelegd wat "public" precies betekent, wat het doet en waarom het uitmaakt. Omdat we nu steeds complexere applicaties gaan schrijven, wordt de accessibility van fields en methoden steeds belangrijker.

## 2.2 Public/private

Iedere methode, field en property in C# heeft een bepaalde "toegankelijkheid". De toegankelijkheid vertelt wie er aan die methode/field/property mag zitten. Je geeft de toegankelijkheid op door de *modifier* op te geven bij het declareren van het field, property of methode, bijvoorbeeld:

```csharp
public int myInt;

private void ThisMethod()
{
}
```

Er zijn verschillende niveaus:

- Public
- Private
- Internal
- Protected

## 2.3 Public

Een public field, property of methode is toegankelijk voor alles en iedereen: elk object kan de waarde van een public field lezen of wijzigen, en elke public methode aanroepen. Als we teruggaan naar het voorbeeld van de auto en we maken de snelheid public, dan kan elk ander object in de applicatie de snelheid van de auto direct beïnvloeden, zonder dat er specifieke methoden zoals `Accelerate` of `SetSpeed` nodig zijn. Het is alsof de snelheidsmeter en het gaspedaal van de auto in het openbaar beschikbaar zijn, waardoor iedereen de snelheid kan zien en aanpassen. Bij het gebruik van public moet je voorzichtig zijn om niet onbedoeld wijzigingen van buitenaf toe te staan die de interne toestand van het object op een ongewenste manier kunnen veranderen.

## 2.4 Private

Een private field, property of methode mag enkel door het eigen object worden aangesproken. Concreet betekent dit zoveel dat als de snelheid van een auto private is, niemand de snelheid van de auto mag aanpassen behalve de auto zelf. Als je toch wilt dat bepaalde andere objecten de snelheid kunnen verhogen of verlagen, zul je hiervoor methoden moeten schrijven (bijv. `Accelerate`, `IncreaseSpeed`, `SetSpeed`, o.i.d.). Een private field, property of methode van een base class is niet toegankelijk voor objecten van een sub class van die base class.

```csharp
public class Meme
{
    private Joke joke;

    public void setJoke(Joke newJoke)
    {
        this.joke = newJoke;
    }
}
```

Hierboven is het field `joke` private: alleen `Meme` zelf komt erbij. Andere objecten kunnen de joke alleen instellen via de public methode `setJoke` — en die methode kan er dan bijvoorbeeld nog controles omheen zetten.

![Meme: iemand die veelbetekenend kijkt met het onderschrift "You wouldn't get it"](./assets/meme-you-wouldnt-get-it.png)

## 2.5 Internal

De internal-modifier lijkt erg op public: een internal field, property of methode is toegankelijk voor alles en iedereen *binnen dezelfde assembly*. Assembly is een wat lastig begrip, maar voor nu houden we het erop dat de assembly de app is waarbinnen je werkt.

## 2.6 Protected

Protected betekent vrijwel hetzelfde als private, met het verschil dat protected fields, properties en methoden wél aanspreekbaar zijn door objecten van een sub class.

<x-koppelvraag>
prompt: Koppel elke modifier aan de juiste omschrijving.
pairs:
  - left: public
    right: Toegankelijk voor alles en iedereen
  - left: private
    right: Alleen toegankelijk voor het eigen object
  - left: internal
    right: Toegankelijk binnen dezelfde assembly (app)
  - left: protected
    right: Als private, maar ook voor sub classes
</x-koppelvraag>

## 2.7 Static

Buiten de accessmodifiers die we hierboven hebben besproken is er nog een belangrijk begrip dat je al een aantal keer bent tegengekomen: de "static". Static is een beetje bijzonder, omdat je static opgeeft, óf niet. Het opgeven van het keyword `static` betekent dat je methode, field of property "static" wordt. En wat betekent dat nu precies? We hebben het bij objectgeoriënteerd programmeren (week 1) gehad over het feit dat een class een blauwdruk is, een sjabloon, bijvoorbeeld van een auto. En van een auto willen we bijvoorbeeld de kleur vastleggen. Maar wat is de kleur van de klasse auto? Tot nu toe hebben we steeds gezegd: die vraag slaat nergens op. Het sjabloon van een auto vertelt ons dat een auto een kleur heeft, maar de vraag welke kleur het sjabloon heeft is… raar…

Totdat… totdat je je beseft dat verreweg de meeste auto's vier wielen hebben. Misschien zou het wel een standaard van de class `Car` moeten zijn dat een standaardauto vier wielen heeft. En misschien willen we wel opgeven dat een Nederlandse auto altijd een nummerbord met zes of zeven tekens moet hebben. Misschien willen we wel een keuze-optie "brandstof" maken, waar je enkel kunt kiezen uit "Benzine", "Diesel" of "Elektrisch"… Al deze zaken zijn eigenschappen *van de class, niet van (een van) de objecten*.

<x-callout type="note">

**Samenvatting.** Een static field of methode is een eigenschap of mogelijkheid *van de class*.

</x-callout>

```csharp
public class Auto
{
    public static int StandaardAantalWielen = 4;

    public string Kleur;
}

// Aanroepen via de class, niet via een object:
Console.WriteLine(Auto.StandaardAantalWielen);
```

<x-keuzevraag>
question: De snelheid van een auto is `private`. Een ander object wil de snelheid verhogen. Wat is de nette oplossing?
options:
  - De snelheid public maken
  - Een public methode zoals Accelerate() schrijven die de snelheid ophoogt
  - De snelheid internal maken
  - Het andere object een sub class maken
correct: 1
explanation: "Zo houd je controle: de class bepaalt zelf hoe en wanneer de snelheid mag veranderen (bijv. nooit boven het maximum)."
</x-keuzevraag>

<x-nav label="Klaar met de theorie?">
[Oefeningen](/pages/week2-oefeningen.html)
[Quiz](/pages/week2-meetmoment.html)
[Inleveropdracht](/pages/week2-inleveropdracht.html)
[Week 3](/pages/week3-theorie.html)
</x-nav>
