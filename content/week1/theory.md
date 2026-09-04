---
week: 1
title: OOP in C#
goal: je begrijpt hoe classes, objecten, referenties en value- vs reference-types werken en kunt een programma opbouwen uit samenwerkende objecten
accent: indigo
summary: Herhaling en verdieping van objectgeoriënteerd programmeren — classes als sjabloon, objecten als exemplaar, referenties tussen objecten en het verschil tussen value- en reference-types.
leeruitkomsten:
  - Ik kan uitleggen wat een class, een object en een constructor is
  - Ik kan een probleem uit de echte wereld vertalen naar een class met fields en methoden
  - Ik kan objecten aanmaken met new en hun methoden en fields aanspreken
  - Ik kan met een referentie het ene object het andere object laten aansturen
  - Ik ken het verschil tussen value-types en reference-types en kan voorspellen wat een methode met een parameter doet
---

## Over deze module

In deze module leer je werken met **Objectgeoriënteerd Programmeren (OOP)**, **WinUI**, **Entity Framework Core (EF Core)** en **API's** binnen C#. We herhalen ook enkele basisprincipes uit eerdere modules.

- **OOP:** je leert hoe je klassen en objecten gebruikt, en hoe je je code schoon en overzichtelijk houdt.
- **WinUI:** hiermee bouw je moderne desktopinterfaces voor Windows-toepassingen. WinUI oefen je in de lessen en praktijkopdrachten; deze e-module richt zich op de C#-kant.
- **EF Core:** een ORM waarmee je eenvoudig met databases werkt via C#-code, zonder handmatig SQL te schrijven.
- **API's:** je leert hoe je REST API's maakt en gebruikt om gegevens uit te wisselen tussen applicaties.

Deze module is de ondersteuning bij de praktijkopdrachten van dit blok. Als voorkennis is CSD-I vereist; je hebt een basis van C# nodig.

<x-callout type="info">

**Meetmomenten.** Bij deze module horen een aantal meetmomenten. Je dient voor deze meetmomenten samen een gemiddelde boven de 5,5 te hebben. Je gemiddelde en je cijfers zijn te vinden op SmartPoints. Deze cijfers worden gegeven voor een toets of een CGI.

</x-callout>

### Studiewijzer

| Week (e-module) | Onderwerpen | Studiewijzer |
|---|---|---|
| 1 — OOP in C# | Models, classes, objects, references | Week 1 |
| 2 — Accessibility & static | public, private, internal, protected, static | Week 2 |
| 3 — EF Core: opzet & model | Packages, migrations, models, DbContext | Week 3 |
| 4 — EF Core: CRUD in een console-app | Console-app, gegevens invoeren/wijzigen/verwijderen | Week 4–6 |
| 5 — API: concept & consumeren | API-concept, API uitlezen met HttpClient, JSON | Week 7–8, 10 |
| 6 — API: zelf bouwen | API bouwen met HttpListener, routing | Week 9 |
| 7 — API + EF Core | API-data aanleveren vanuit EF Core, validatie | Week 11–12 |

De weken 13 t/m 16 uit de studiewijzer zijn buffer- en toetsweken: je maakt en levert je eindopdracht op.

## 1.1 Inleiding

OOP staat voor 'Object Oriented Programming' en het betekent zoveel als "we focussen ons op objecten". In OOP is alles een object en een object heeft eigenschappen en mogelijkheden. In C# heb je al eerder met objecten gewerkt. In de komende weken ga je echter veel meer focussen op deze objecten en je gaat programma's maken die helemaal uit objecten bestaan.

## 1.2 De wereld als model

Als je in de echte wereld om je heen kijkt, zie je constant allerlei "objecten": een pen, een tafel en stoel, je laptop, bomen, vogels, voorbij rijdende auto's, verzin het maar. Al deze objecten hebben eigenschappen: een pen heeft een kleur en een hoeveelheid resterende inkt, een tafel heeft afmetingen en een bepaalde hoeveelheid kauwgom, en auto's hebben een merk, type en nummerbord. Daarnaast zijn er objecten die bepaalde mogelijkheden hebben: een pen kan schrijven, een vogel kan vliegen, en een auto kan accelereren.

Wanneer je objectgeoriënteerd programmeert, betekent dat dat je in je app objecten maakt met eigenschappen en mogelijkheden. Vaak begint dat met het vastleggen van je wensen of eisen. Wanneer je bijvoorbeeld een race-spelletje aan het maken bent, is accelereren waarschijnlijk een belangrijke mogelijkheid van de auto, maar misschien is het voor jouw spel helemaal niet belangrijk dat je auto een nummerplaat heeft. Vergelijk dat met een administratieve app die verkeersboetes moet afhandelen: in dat geval is het helemaal niet relevant of een auto kan accelereren, ik ben alleen geïnteresseerd in de snelheid en het nummerbord van de auto die geflitst is. Wat "een auto" is (of: wat de eigenschappen en mogelijkheden van een auto zijn) hangt dus af van de app die je maakt en de wensen en eisen die jíj hebt.

## 1.3 Classes

Een class is een 'sjabloon' van een object. Het bevat alle eigenschappen en mogelijkheden van je object, maar "nog niet ingevuld". Stel, je wilt een app maken met daarin een auto; je auto heeft een merk, type, kleur en maximumsnelheid en kan accelereren, remmen, toeteren, richting aangeven (naar links en naar rechts) en schakelen (naar versnelling 1 t/m 5 of -1 voor achteruit). Je class `Car` zou er dan zo uitzien:

```csharp
public class Car
{
    // Velden (fields) van een auto
    public string Make;
    public string Model;
    public string Color;
    public int MaxSpeed;
    private int currentSpeed; // Een priveveld voor de huidige snelheid

    // Constructor om een nieuwe auto te maken
    public Car(string make, string model, string color, int maxSpeed)
    {
        this.Make = make;
        this.Model = model;
        this.Color = color;
        this.MaxSpeed = maxSpeed;
        this.currentSpeed = 0;
    }

    // Methode om te accelereren
    public void Accelerate()
    {
        if (currentSpeed < MaxSpeed)
        {
            currentSpeed += 10; // Verhoog de snelheid met 10 eenheden
            Console.WriteLine("De auto accelereert naar " + currentSpeed + " km/u.");
        }
        else
        {
            Console.WriteLine("De auto heeft zijn maximale snelheid bereikt!");
        }
    }

    // Methode om te remmen
    public void Brake()
    {
        if (currentSpeed > 0)
        {
            currentSpeed -= 10; // Verminder de snelheid met 10 eenheden
            Console.WriteLine("De auto remt af naar " + currentSpeed + " km/u.");
        }
        else
        {
            Console.WriteLine("De auto staat al stil!");
        }
    }

    // Methode om te toeteren
    public void Honk()
    {
        Console.WriteLine("De auto toetert!");
    }

    // Methode om richting aan te geven
    public void Signal(string direction)
    {
        Console.WriteLine("De auto geeft richting aan naar " + direction + ".");
    }

    // Methode om van versnelling te wisselen
    public void ShiftGear(int gear)
    {
        Console.WriteLine("De auto schakelt naar versnelling " + gear + ".");
    }
}
```

Zoals gezegd is een class een sjabloon, net zoals deze prijskaart van een autodealer: voor iedere auto die te koop staat, kun je invullen wat de prijs is, wat voor model auto het om gaat en uit welk jaar de auto komt. Nu heeft iedere autodealer waarschijnlijk een hele stapel lege prijskaarten liggen, die pas worden ingevuld als ze een auto hebben die verkocht moet worden. Want, hoewel deze prijskaart geschikt is voor iedere auto, heeft het alleen zin om het over "de prijs" te hebben als we het over een specifieke auto hebben.

![Een lege 'FOR SALE'-prijskaart met invulvelden voor Price, Model en Year](./assets/for-sale-kaart.jpg)

<x-callout type="note">

Een class is een sjabloon van eigenschappen (**fields**) en mogelijkheden (**methoden**).

</x-callout>

## 1.4 Objects

Zoals gezegd heeft iedere auto een kleur, maar heeft het alleen zin om het over de kleur van één specifieke auto te hebben. Om een nieuwe auto te maken, volgens het sjabloon `Car` dat we hierboven hebben gemaakt, gebruiken we de volgende regel code:

```csharp
Car myNewCar = new Car("BMW", "M4", "Black", 300);
```

Misschien dat je hier een klein beetje herkent van het aanmaken van een nieuw field (`int thisInt = 12;`) en eigenlijk is dat ook precies wat we doen:

We vertellen C# hier dat we een stuk geheugen willen reserveren, waar we een object van de class `Car` in kunnen stoppen (dat is de eerste `Car`). We willen dat stukje geheugen aan kunnen spreken met de naam `myNewCar` (dat is de tweede). Net als bij een field kunnen we het geheugen (voor nu) nog leeglaten, maar we kunnen er ook direct een `Car` in stoppen. Daarvoor moeten we wel eerst een object maken van de class `Car` (`new Car`). Tussen haakjes geven we vervolgens de parameters voor de constructor op.

We kunnen het field `myNewCar` nu aanspreken om de eigenschappen en mogelijkheden van die auto aan te spreken. Zo kunnen we bijvoorbeeld de auto laten accelereren of laten remmen met de code:

```csharp
myNewCar.Accelerate();
myNewCar.Brake();
```

**Belangrijk:** als we `myNewCar.Accelerate()` aanroepen, roepen we de `Accelerate`-methode van een specifieke auto aan. Wanneer we twee auto's in onze app hebben, zal er met de tweede dus niets gebeuren:

```csharp
Car myNewCar = new Car("BMW", "M4", "Black", 300);
Car myNewCar2 = new Car("Audi", "RS6", "Blue", 290);

myNewCar.Accelerate();
myNewCar.Accelerate();
myNewCar.Accelerate();
```

Na deze code heeft de BMW een snelheid van 30, maar staat de Audi nog steeds stil. Om de Audi ook te laten rijden, moeten we deze code uitvoeren:

```csharp
myNewCar2.Accelerate();
```

<x-keuzevraag>
question: Je hebt `Car auto1 = new Car(...)` en `Car auto2 = new Car(...)`. Je roept `auto1.Accelerate()` drie keer aan. Wat is waar?
options:
  - Beide auto's rijden nu even hard
  - Alleen auto1 heeft snelheid; auto2 staat stil
  - Er ontstaat een foutmelding omdat er twee auto's zijn
  - De class Car heeft nu snelheid 30
correct: 1
explanation: Een methode werkt op het specifieke object waarop je hem aanroept. auto2 is een ander object en blijft onaangeroerd.
</x-keuzevraag>

## 1.5 Referenties

Een belangrijke eigenschap van objectgeoriënteerd programmeren is het feit dat objecten invloed op elkaar kunnen uitoefenen: in een racespel waar je een class `RaceDriver` en `RaceCar` hebt, zal de `RaceDriver` waarschijnlijk de `Accelerate`-methode van de `RaceCar` aanroepen. Maar daarvoor moet de `RaceDriver` wel weten welke auto er moet accelereren. Hiervoor gebruiken we vaak **referenties**.

In onderstaand voorbeeld zie je deze twee classes en een voorbeeld voor hoe de `RaceDriver` ("John") de auto laat accelereren. In de `Main` zie je dat we een nieuwe `RaceCar` aanmaken en deze in een field genaamd `car` plaatsen. Op de regel eronder zie je dat we een nieuwe `RaceDriver` aanmaken en aan deze driver de `car` meegeven. In de constructor van de driver zie je hoe deze `RaceCar` wordt opgeslagen in de `RaceDriver`. Hierdoor heeft de `RaceDriver` een referentie naar de gemaakte `RaceCar` en kan hij op verschillende plaatsen in de `RaceDriver`-code de methoden en fields van `car` aanspreken (zolang deze toegankelijk zijn, zie week 2).

```csharp
public class RaceCar
{
    public string Model { get; set; }

    public RaceCar(string model)
    {
        Model = model;
    }

    public void Accelerate()
    {
        Console.WriteLine($"{Model} accelereert nu!");
    }
}
```

```csharp
public class RaceDriver
{
    public string Name;
    public RaceCar Car;

    public RaceDriver(string name, RaceCar car)
    {
        Name = name;
        Car = car;
    }

    public void Drive()
    {
        Console.WriteLine($"{Name} begint nu met racen.");
        Car.Accelerate();
    }
}
```

```csharp
public class RaceGame
{
    public static void Main(string[] args)
    {
        RaceCar car = new RaceCar("Speedster");
        RaceDriver driver = new RaceDriver("John", car);

        driver.Drive();
    }
}
```

## Reference- vs value-types

Een belangrijke eigenschap van fields waar we het tot nu toe nog niet over hebben gehad, is of het een *reference type* of *value type* field is. In C# zijn de volgende datatypes een value type:

- `int`
- `float`
- `double`
- `char`
- `bool`
- `struct`
- Enums

De meeste andere datatypes en classes zijn reference types. Leuk, maar wat bedoelen we ermee? Bekijk de code hieronder:

```csharp
int number = 5;
void modifyNumber(int num) {
    num = 10; // We passen hier de parameter num aan. Niet de globale variabele number
}

modifyNumber(number);
```

Je ziet hier dat we een field `number` maken en daar het getal 5 in stoppen. Vervolgens roepen we de methode `modifyNumber` aan, met `number` als parameter. In de methode zie je dat we het lokale field `num` aanpassen: eerst zat hier een 5 in en in deze methode maken we daar een 10 van. Ondanks dat we `num` hebben ingesteld op 10, zit er in `number` nog steeds 5. Dit komt omdat we, bij het aanroepen van de methode, niet `number` hebben meegegeven, maar *de waarde die in `number` zat*. Vanaf het moment dat we de methode aanroepen, is er dus geen "verbinding" meer tussen `number` en de parameter of de meegestuurde waarde.

Bekijk nu de code hieronder, waar we hetzelfde doen, maar dan met een reference type field (een object).

```csharp
class SimpleClass
{
    public int Value;

    public SimpleClass(int initialValue)
    {
        Value = initialValue;
    }
}
```

```csharp
void modifyObject(SimpleClass obj, int newValue)
{
    obj.Value = newValue;
}

SimpleClass myObject = new SimpleClass(5);
modifyObject(myObject, 10);
Console.WriteLine(myObject.Value); // Output: 10
```

We maken een nieuw object `myObject` aan, en we geven het nieuwe object de waarde 5 mee. Deze wordt in het object opgeslagen in `Value`. Vervolgens roepen we een vergelijkbare methode `modifyObject` aan, alleen deze krijgt, buiten de waarde 10, ook een referentie naar het gemaakte object mee. Van dit object stelt de methode de `Value` in op de nieuw meegestuurde waarde. Als we nu (buiten de `modifyObject`-methode) de waarde van `Value` bekijken, zien we dat deze wél is aangepast. Dat komt omdat we in dit geval niet een nieuw object ofzo meegeven aan `modifyObject`, maar alleen een *referentie* naar het reeds bestaande object. Hierdoor passen we daadwerkelijk de waarde van `Value` in dat object aan, in plaats van alleen maar de waarde van de lokale parameter.

<x-vind-de-fout>
code: |-
  void ResetAuto(RaceCar auto)
  {
      auto = new RaceCar("Reset");
      auto.Model = "Reset";
  }
errorLine: 3
hint: Denk aan het verschil tussen de parameter aanpassen en het object aanpassen.
explanation: Op regel 3 vervang je de lokale parameter door een nieuw object. De aanroeper houdt zijn eigen auto, dus die ziet niets van deze wijziging. Regel 4 werkt wél op het meegegeven object.
</x-vind-de-fout>

<x-callout type="tip">

**Vuistregel.** Geef je een `int`, `bool` of andere value type mee aan een methode? Dan werkt de methode met een *kopie*. Geef je een object mee? Dan werkt de methode met *hetzelfde* object en zie je wijzigingen ook buiten de methode terug.

</x-callout>

<x-nav label="Klaar met de theorie?">
[Oefeningen](/pages/week1-oefeningen.html)
[Quiz](/pages/week1-meetmoment.html)
[Inleveropdracht](/pages/week1-inleveropdracht.html)
[Week 2](/pages/week2-theorie.html)
</x-nav>
