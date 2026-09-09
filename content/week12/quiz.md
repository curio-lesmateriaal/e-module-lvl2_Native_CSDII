---
week: 12
title: Quiz Week 12 — invoer valideren
passScore: 70
questions:
  - id: w12q1
    question: Wat is validatie?
    options:
      - Het controleren of invoer aan de voorwaarden voldoet
      - Het versleutelen van gegevens
      - Het opslaan van gegevens
      - Het omzetten van JSON naar objecten
    correct: 0
    explanation: Validatie controleert of de door de gebruiker aangeleverde gegevens bruikbaar en correct zijn, vóór je ze opslaat.
  - id: w12q2
    question: Wat is een nadeel van valideren met if-statements?
    options:
      - Het werkt niet in een API
      - Het wordt al snel lang en repetitief, en de regels staan niet bij het model
      - Je kunt er geen foutmeldingen mee geven
      - Het is onveilig
    correct: 1
    explanation: If-statements geven volledige controle, maar bij veel velden wordt het lang; Data Annotations zetten de regels bij het model.
  - id: w12q3
    question: Welke package bevat de attributen [Required], [MaxLength] en [Range]?
    options:
      - "System.Text.Json"
      - "Microsoft.EntityFrameworkCore"
      - "System.ComponentModel.DataAnnotations"
      - "System.Net"
    correct: 2
    explanation: Data Annotations zitten in System.ComponentModel.DataAnnotations.
  - id: w12q4
    question: Welke methode voert de validatie op basis van Data Annotations uit?
    options:
      - "Validator.TryValidateObject"
      - "JsonSerializer.Deserialize"
      - "context.SaveChanges"
      - "Regex.IsMatch"
    correct: 0
    explanation: TryValidateObject vult een lijst met ValidationResults en geeft true/false terug.
  - id: w12q5
    question: "Je schrijft `[Required]` in plaats van `[RequiredAttribute]`. Klopt dat?"
    options:
      - Nee, de volledige naam is verplicht
      - Alleen bij [Range]
      - Alleen in een console-app
      - Ja, bij attribute-classes mag je de 'Attribute'-suffix weglaten
    correct: 3
    explanation: Beide schrijfwijzen zijn geldig voor C#-attributes.
  - id: w12q6
    question: Waar gebruik je het <code>[RegularExpression]</code>-attribuut voor?
    options:
      - Om te controleren of een string aan een bepaald patroon voldoet
      - Om een getal binnen een bereik te houden
      - Om een veld verplicht te maken
      - Om JSON te deserialiseren
    correct: 0
    explanation: Een regex beschrijft een tekstpatroon; het attribuut checkt of de waarde daaraan voldoet (bijv. een postcode).
  - id: w12q7
    question: "Wat matcht de regex `^[0-9]{4}[A-Z]{2}$`?"
    options:
      - "1234ab"
      - "1234AB"
      - "12 34AB"
      - "AB1234"
    correct: 1
    explanation: 4 cijfers, dan 2 hoofdletters, niets ervoor of erna — precies het postcodeformaat 1234AB.
  - id: w12q8
    question: "Wat betekent `\\s?` in de regex `^[0-9]{4}\\s?[A-Z]{2}$`?"
    options:
      - Precies één spatie is verplicht
      - Een witruimte-teken is op die plek optioneel
      - Er mogen alleen letters staan
      - Het is het einde van de string
    correct: 1
    explanation: "`\\s` is witruimte, `?` maakt het optioneel — zo mag de postcode mét of zónder spatie."
---
