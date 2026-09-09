---
week: 12
title: API + EF Core — invoer valideren
goal: je kunt binnenkomende gegevens valideren met if-statements, met Data Annotations en met een [RegularExpression], en je kunt een eenvoudige regex lezen
accent: stone
summary: "Je API slaat nu klakkeloos op wat de client meestuurt. Deze week controleer je die invoer eerst: met simpele if-statements, met Data Annotations op je model (Validator.TryValidateObject) en met reguliere expressies voor patronen zoals een postcode of kenteken."
leeruitkomsten:
  - Ik kan invoer valideren met if-statements
  - Ik kan invoer valideren met Data Annotations en Validator.TryValidateObject
  - Ik ken de voor- en nadelen van beide manieren
  - Ik kan een [RegularExpression] schrijven en een eenvoudige regex lezen
---

## 12.1 Invoer valideren met if-statements

Om een degelijke applicatie te maken, moeten we de invoer van de gebruiker controleren. Dat noemen we **validatie** (Engels: *validation*). In week 11 sloeg je een gedeserialiseerd `Voertuig` meteen op — maar wat als het kenteken leeg is of de prijs negatief? Dan sla je rommel op.

De eenvoudigste manier is met **if-statements**. We demonstreren de manieren aan de hand van een klein venster met een naam-invoerveld (`nameTextBox`), een leeftijd-invoerveld (`ageTextBox`), een `Validate`-knop en een leeg tekstveld `validationResultsTextBlock` waarin in het rood een bericht getoond wordt.

![Een klein venster 'TestValidation' met invoervelden Name (Janiek) en Age (0), een Validate-knop en bovenaan in het rood 'The field Age must be between 1 and 120.'](./assets/testvalidation-app.png)

<x-callout type="note">

In dit voorbeeld is het een knop in een venster, maar dezelfde validatiecode werkt net zo goed in een console-app of in een API-endpoint — je maakt een object van de ingevoerde gegevens en controleert dat vóór je het opslaat.

</x-callout>

```csharp
private void validateButton_Click(object sender, RoutedEventArgs e)
{
    var user = new User
    {
        Name = nameTextBox.Text,
        Age = int.TryParse(ageTextBox.Text, out var age) ? age : 0
    };

    var errors = new List<string>();

    if (string.IsNullOrWhiteSpace(user.Name))
    {
        errors.Add("The Name field is required.");
    }
    else if (user.Name.Length > 50)
    {
        errors.Add("The field Name must be a string with a maximum length of 50.");
    }

    if (user.Age < 1 || user.Age > 120)
    {
        errors.Add("The field Age must be between 1 and 120.");
    }

    if (errors.Count > 0)
    {
        validationResultsTextBlock.Text = string.Join(Environment.NewLine, errors);
    }
    else
    {
        validationResultsTextBlock.Text = "Validation succeeded!";
    }
}
```

## 12.2 Valideren met Data Annotations

Met 'attributen' uit de ingebouwde package `System.ComponentModel.DataAnnotations` leg je de voorwaarden vast **bij het model** in plaats van in je methode. "Annotations" betekent annotaties — aanmerking, aantekening. Met C#-attributes plaats je extra informatie bij o.a. classes, methodes en eigenschappen.

```csharp
using System.ComponentModel.DataAnnotations;

public class User
{
    [Required]
    [MaxLength(50)]
    public string Name { get; set; }

    [Range(1, 120)]
    public int Age { get; set; }
}
```

Bij het klikken op de knop **instantiëren** we een `User` met de ingevoerde gegevens. Vervolgens maken we een `ValidationContext` en roepen we `Validator.TryValidateObject` aan, die aan de hand van de attributen validatie uitvoert:

```csharp
private void validateButton_Click(object sender, RoutedEventArgs e)
{
    var user = new User
    {
        Name = nameTextBox.Text,
        Age = int.TryParse(ageTextBox.Text, out var age) ? age : 0
    };

    var context = new ValidationContext(user);
    var results = new List<ValidationResult>();

    if (!Validator.TryValidateObject(user, context, results, true))
    {
        var errors = new List<string>();
        foreach (var validationResult in results)
        {
            errors.Add(validationResult.ErrorMessage);
        }
        validationResultsTextBlock.Text = string.Join(Environment.NewLine, errors);
    }
    else
    {
        validationResultsTextBlock.Text = "Validation succeeded!";
    }
}
```

In de documentatie van Microsoft is een lijst te vinden met alle attributen die je bij een eigenschap kunt plaatsen: <https://learn.microsoft.com/en-us/dotnet/api/system.componentmodel.dataannotations>

![Een tabel uit de Microsoft-documentatie met attributen zoals MaxLengthAttribute, MinLengthAttribute, PhoneAttribute, RangeAttribute, RegularExpressionAttribute en RequiredAttribute, elk met een korte omschrijving](./assets/dataannotations-lijst.png)

![Dezelfde documentatietabel met pijlen die MaxLengthAttribute, RangeAttribute en RequiredAttribute koppelen aan een codevoorbeeld met [Required], [MaxLength(50)] en [Range(1, 120)]](./assets/dataannotations-attributen.jpg)

<x-callout type="warning">

C#-attribute-classes zijn bijzonder: je mag bij het gebruiken van de klasse de 'Attribute'-suffix weglaten. Dus je mag zowel `[RequiredAttribute]` als `[Required]` schrijven, beide zijn valide.

</x-callout>

<x-compare>
<x-compare-item title="If-statements">

- Volledige controle, geen extra kennis nodig
- Wordt al snel lang en repetitief bij veel velden
- De regel en de melding staan in je methode, niet bij het model

</x-compare-item>
<x-compare-item title="Data Annotations">

- Kort: de regels staan als attributen bij het model
- Herbruikbaar: overal waar je het model valideert gelden dezelfde regels
- Je hebt `Validator.TryValidateObject` één keer nodig

</x-compare-item>
</x-compare>

## 12.3 Validatie met [RegularExpression]

Het `[RegularExpression]`-attribuut (meestal met data-annotaties) valideert of een string overeenkomt met een bepaald **patroon**. Dat patroon schrijf je in een **Regular Expression** (regex).

```csharp
[RegularExpression(@"^[0-9]{4}[A-Z]{2}$", ErrorMessage = "Postcode moet 4 cijfers gevolgd door 2 hoofdletters zijn.")]
public string Postcode { get; set; }
```

In dit voorbeeld valideert het attribuut of de postcode voldoet aan het formaat `1234AB`.

### Wat is Regular Expression?

Een regex is een **tekstpatroon** waarmee je kunt controleren of een string aan bepaalde eisen voldoet. Regex bestaat niet alleen in C#, maar ook in JavaScript, Python, Java, PHP, Ruby, Perl en zelfs in editors zoals VS Code en Notepad++.

### Voorbeelden met uitleg per teken

**Nederlandse postcode:** `^[0-9]{4}[A-Z]{2}$`

- `^` — begin van de string
- `[0-9]{4}` — precies 4 cijfers:
  - `[` — start set
  - `0-9` — de cijfers 0 t/m 9
  - `]` — eind set
  - `{` — start herhalingsinformatie
  - `4` — precies 4 keer
  - `}` — eind herhalingsinformatie
- `[A-Z]{2}` — precies 2 hoofdletters (`A-Z` = de letters A t/m Z)
- `$` — einde van de string

Voorbeeld geldig: `1234AB` — Ongeldig: `123AB`, `1234ab`, `12 34AB`

Sommige mensen schrijven hun postcode met een spatie. Dan pas je de regex aan: `^[0-9]{4}\s?[A-Z]{2}$`. Hier betekent `\s?` dat op die plek een witruimte-teken (`\s`) optioneel (`?`) is. Nu ook geldig: `1234 AB`

**Telefoonnummer (NL mobiel):** `^06\d{8}$`

- `^` — begin van de string
- `06` — moet beginnen met 06
- `\d{8}` — precies 8 cijfers, `\d` = cijfer
- `$` — einde van de string

Voorbeeld geldig: `0612345678` — Ongeldig: `0712345678`, `06-12345678`

Via <https://regex101.com/> kun je jouw regex testen en uitleg vinden over de overige tekens.

![Screenshot van regex101.com met de regex ^[0-9]{4}\s?[A-Z]{2}$, een lijst teststrings waarvan 4813 AB en 1212AB matchen (groen omcirkeld) en 222BA, test en 2112 aa niet (rood kruis). Links is de flavor '.NET 7.0 (C#)' geselecteerd.](./assets/regex101.png)

<x-invul>
prompt: Vul de regex aan die precies 4 cijfers, dan precies 2 hoofdletters vereist (postcode zonder spatie).
code: |-
  ^[0-9]___[A-Z]___$
blanks:
  - answer: "{4}"
  - answer: "{2}"
explanation: "{4} en {2} geven aan hoe vaak de set ervoor herhaald moet worden."
</x-invul>

<x-vind-de-fout>
code: |-
  public class Klant
  {
      [Required]
      public string Naam { get; set; }

      [Range(1, 120)]
      public string Leeftijd { get; set; }
  }
errorLine: 7
hint: Kijk naar het type van de property waar [Range] op staat.
explanation: "[Range(1, 120)] hoort op een getal (int), niet op een string. Maak van Leeftijd een int."
</x-vind-de-fout>

<x-nav label="Klaar met de theorie?">
[Oefeningen](/pages/week12-oefeningen.html)
[Quiz](/pages/week12-meetmoment.html)
[Checklist](/pages/checklist.html)
</x-nav>
